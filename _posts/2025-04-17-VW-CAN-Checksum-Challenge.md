---
layout: post
title: Solving the Volkswagen CAN Checksum Challenge
date: 2025-04-17 00:05:36
categories: [CTF]
tags: [CTF]
last_modified_at: 2025-04-17
---


# 🛠️ Solving the Volkswagen CAN Checksum Challenge (CRC8 AUTOSAR Style)

This challenge explores the calculation of a CRC8 checksum used in Volkswagen CAN messages. Specifically, it uses the **AUTOSAR CRC8 with polynomial 0x2F**—a common checksum mechanism in automotive software stacks.

---

## 🎯 Challenge Statement

> Compute the correct one-byte checksum `XX` for the CAN message with payload `XX0f0300`.  
> The flag format is `CTF{XX}`.

You’re provided with 15 CAN messages in the format:
```
<checksum><payload>
```
For example:
```
74000300
c1010300
31020300
...
```

The checksum is **calculated over a 4-byte payload**, where:
- The last byte is a **"secret" byte**
- The secret byte is derived from the **CAN arbitration ID**, which is not directly given

The checksum process includes:
1. Appending the secret byte to the actual payload (3 bytes)
2. Applying **CRC8-AUTOSAR** (Polynomial = `0x2F`, Init = `0xFF`, Non-reversed)
3. XORing the result with `0xFF`

---

## 🔍 Step-by-Step Solution

### Step 1: CRC Function Setup

```python
import crcmod

# Setup AUTOSAR CRC8 with polynomial 0x2F
crc = crcmod.mkCrcFun(poly=0x12F, initCrc=0xFF, rev=False)
```

---

### Step 2: Deduce the Secret Byte

We reverse-engineer the secret byte by iterating over all possible 0-255 values.

```python
# Known payload from one message, excluding checksum
payload = b'  '  # corresponds to '000300'

for secret in range(256):
    test_data = payload + secret.to_bytes(1, 'big')
    computed_checksum = crc(test_data) ^ 0xFF
    if computed_checksum == 0x74:  # from '74000300'
        print(f"Secret byte found: {hex(secret)}")
```

✅ This reveals the **secret byte is `0xC3`**

---

### Step 3: Solve the CTF Payload

With the secret byte found, apply it to the new payload.

```python
new_payload = b' ' + b'Ã'
checksum = crc(new_payload) ^ 0xFF
print(f"CTF flag: CTF{{{checksum:02X}}}")
```

✅ Output: `CTF{35}`

---

## ✅ Final Answer

```text
CTF{35}
```

---

## 🔁 Summary

| Step | Action |
|------|--------|
| 1️⃣  | Set up AUTOSAR CRC8 function |
| 2️⃣  | Brute force to find the secret byte using sample messages |
| 3️⃣  | Use found byte to calculate checksum for new payload |

---

## 📚 References

- [AUTOSAR CRC Specification](https://www.autosar.org/)
- [`crcmod` Python library](https://pypi.org/project/crcmod/)
- [CAN Protocol Overview](https://en.wikipedia.org/wiki/CAN_bus)

---

Stay secure and happy reversing! 🔐  
_Published by [Kartheek Lade](https://kartheeklade.github.io/)_
