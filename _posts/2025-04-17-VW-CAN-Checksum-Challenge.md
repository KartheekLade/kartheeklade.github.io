---
layout: post
title: Solving the Volkswagen CAN Checksum Challenge
date: 2025-04-17 00:05:36
categories: [CTF]
tags: [CTF]
last_modified_at: 2025-04-17
---

#### 🛠️ Solving the Volkswagen CAN Checksum Challenge (CRC8 AUTOSAR Style)

This challenge involves calculating a CRC8 checksum used in Volkswagen CAN messages, specifically the **AUTOSAR CRC8 with polynomial 0x2F**—a common checksum mechanism in automotive software stacks.

#### 🎯 Challenge Statement

Compute the correct one-byte checksum `XX` for the CAN message with payload `XX0f0300`.  
The flag format is `CTF{XX}`.

#### Provided Data

You’re given 15 CAN messages in the format `<checksum><payload>`. For example:
```
74000300
c1010300
31020300
...
```

#### Checksum Process

1. Append the secret byte to the 3-byte payload.
2. Apply **CRC8-AUTOSAR** (Polynomial = `0x2F`, Init = `0xFF`, Non-reversed).
3. XOR the result with `0xFF`.


#### 🔍 Solution Steps

##### Step 1: Set Up CRC Function

```python
import crcmod

# Setup AUTOSAR CRC8 with polynomial 0x2F
crc = crcmod.mkCrcFun(poly=0x12F, initCrc=0xFF, rev=False)
```

##### Step 2: Find the Secret Byte

Reverse-engineer the secret byte by iterating over all possible values (0-255).

```python
# Known payload from one message, excluding checksum
payload = b'\x00\x03\x00'  # corresponds to '000300'

for secret in range(256):
    test_data = payload + secret.to_bytes(1, 'big')
    computed_checksum = crc(test_data) ^ 0xFF
    if computed_checksum == 0x74:  # from '74000300'
        print(f"Secret byte found: {hex(secret)}")
```

✅ **Secret byte found: `0xC3`**


##### Step 3: Solve for New Payload

Use the secret byte to calculate the checksum for the new payload.

```python
new_payload = b'\x0F\x03\x00' + b'\xC3'
checksum = crc(new_payload) ^ 0xFF
print(f"CTF flag: CTF{{{checksum:02X}}}")
```

✅ **Output:** `CTF{35}`

#### ✅ Final Answer

```text
CTF{35}
```

#### 🔁 Summary

| Step | Action |
|------|--------|
| 1️⃣  | Set up AUTOSAR CRC8 function |
| 2️⃣  | Brute force to find the secret byte using sample messages |
| 3️⃣  | Use the secret byte to calculate checksum for the new payload |


#### 📚 References

- [AUTOSAR CRC Specification](https://www.autosar.org/)
- [`crcmod`](https://pypi.org/project/crcmod/)
- [CAN Protocol Overview](https://en.wikipedia.org/wiki/CAN_bus)


Stay secure and happy reversing! 🔐  
_Published by [Kartheek Lade](https://kartheeklade.github.io/)_
