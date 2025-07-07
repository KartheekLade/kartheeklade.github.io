---
layout: post
title: Digital Signatures Cryptography’s Proof of Trust
date: 2025-07-07 23:57:34
categories: [cryptography]
tags: [security, encryption, cryptography]
last_modified_at: 2025-07-07
---

#### What Are Digital Signatures?

A digital signature is a cryptographic technique used to verify that a digital message or document:
  1. Was created by the claimed sender (authenticity), and
  2. Has not been altered since it was signed (integrity).

It works using asymmetric cryptography the sender signs data using their private key, and anyone can verify the signature using the corresponding public key. If even one bit of the signed data changes, the signature becomes invalid. Think of it like a tamper evident seal on medicine, Only the manufacturer (private key holder) can apply it -> Anyone can verify its authenticity (public key) -> Any damage to the packaging (message alteration) breaks the seal except it's built on strong math and impossible to forge without the private key

Unlike passwords or handwritten signatures, digital signatures are not guessable or reusable. Even a small change in the data results in a completely different signature, making tampering easy to detect. Digital signatures are widely used in secure email (PGP), software distribution, e-contracts, and blockchain systems.


#### How do they work

Digital signatures follow a three step process:

1. *Hashing*
   The sender applies a cryptographic hash function (e.g., SHA-256) to the original message. This produces a fixed size digest that represents the content uniquely.

2. *Signing with Private Key*
   The sender cryptographically signs the hash using their private key creating a *digital signature*. It is sent along with the original message.

3. *Verification with Public Key*
   The receiver verifies the signature using the sender’s public key to retrieve the original hash. They also compute the hash of the received message.

   * If the two hashes match, the signature is valid—the message is authentic and untampered.
   * If they differ, either the message was altered, or the signature is not from the claimed sender.

This mechanism ensures both authenticity and integrity, without requiring the sender and receiver to share any secret keys. The process can be illustrated as follows:

<pre><div class="mermaid">
flowchart LR
    A["📄 Message"] --> H1["🔍 Hash (SHA-256)"]
    H1 --> S["✍ Sign with Private Key"]
    S --> SIG["📦 Digital Signature"]
    SIG -->|Sent with Message| R["📨 Receiver"]
    R --> H2["🔍 Recompute Hash"]
    R --> V["🔎 Verify with Public Key"]
    H2 --> COMP[" Validate Signature"]
    V --> COMP
    COMP -->|Valid| OK["✔️ Authentic & Untampered"]
    COMP -->|Invalid| BAD["⚠️ Tampered or Invalid"]
</div></pre>

Three Key Steps:

  1. Hashing: SHA-256 creates a unique message fingerprint
  2. Signing: Private key signs the hash → signature
  3. Verification: Public key decrypts signature; hashes must match

well, this ain't as simple as we mentioned above we would also need the full strength of trust, While this process verifies message integrity, it assumes one critical thing you already trust that the public key belongs to the sender. 

In reality, attackers could substitute their own key (a "man in the middle" attack). This is solved by PKI (Public Key Infrastructure) which verifies who owns that key by a system that binds identities to keys using digital certificates issued by trusted authorities. Here's how PKI integrates with digital signatures to establish trust:


<pre><div class="mermaid">

flowchart TD
    %% === Sender Side ===
    M["📄 Message"] --> H1["Hash (e.g., SHA-256)"]
    H1 --> SIGN["Sign with Private Key"]
    SIGN --> SIG["Digital Signature"]
    SIG -->|Bundled with| PKG["Message + Signature + Certificate"]

    %% === Receiver Flow ===
    PKG --> RCV["📥 Receiver"]
    RCV --> CERT_CHECK["🔍 Validate Certificate"]
    CERT_CHECK -->|Valid| PUB["🔑 Extract Public Key"]
    CERT_CHECK -->|Invalid| FAIL_CERT["❌ Untrusted Certificate"]

    RCV --> H2["🔁 Recompute Hash"]
    PUB --> VERIFY["🔎 Verify Signature"]
    H2 --> VERIFY
    VERIFY --> VALID["Cryptographic Validation"]
    VALID -->|Valid| OK["✔️ Authentic & Untampered"]
    VALID -->|Invalid| FAIL_SIG["⚠️ Tampered or Invalid"]

    %% === PKI Trust Chain ===
    CERT_CHECK --> LEAF["📜 End-Entity Cert"]
    LEAF --> INTER["🏢 Intermediate CA"]
    INTER --> ROOT["🏛️ Root CA (Trusted Anchor)"]
    ROOT --> TRUST["🔐 Pre-Trusted (OS/Browser)"]

    %% === Optional ===
    SIG --> TSA["⏲️ Timestamp (Optional)"]
    TSA --> PKG
</div></pre>

#### PKI Trust Verification

##### Certificate Chain: Sender's Cert → Intermediate CA → Root CA  
  Imagine a ID card (sender's certificate) issued by a local DMV (Intermediate CA), which was authorized by the central government (Root CA). To trust the ID, you verify all these links in the chain

    - End Entity Certificate: The sender's "ID card" (contains their public key + identity)
    - Intermediate CA Cert: A middleman CA that signed the sender's cert (like a DMV)
    - Root CA Cert: The ultimate trust anchor (like a government). Pre installed in your OS/browser

  Firstly, receiver checks if the sender's cert was signed by an Intermediate CA --> Checks if the Intermediate CA was authorized by a Root CA --> Verifies all signatures cryptographically. It Matters as it prevents impersonation by ensuring every cert in the chain is properly authorized.  



##### Trust Anchor: Root CA Must Be Pre Trusted
  You only trust IDs issued by governments your country recognizes. Similarly, your device only trusts Root CAs pre-installed in its "trust store."

    - Trust Store: A list of Root CA certificates hardcoded in your OS/browser (e.g., Apple, Microsoft, Google manage these).  
    - Example: If "GoDaddy Root CA" is in your trust store, you trust all certs signed by GoDaddy or its intermediates.  
 
  So, Root CA's public key is pre installed in your device --> Any cert chain ending at this Root CA is automatically trusted. No need to manually verify every sender just trust the Root CA. 

##### Revocation Checks (CRL/OCSP) *(Critical)*  

  Like checking if a driver's license was revoked before accepting it as ID

    - CRL (Certificate Revocation List): A "blacklist" of revoked certs (updated periodically)
    - OCSP (Online Certificate Status Protocol): A real time API to check if a cert is revoked
    
  The process is as followed 
    
    1. Receiver asks: *"Is this certificate still valid?"*  
      - CRL: Downloads a list of revoked serial number
      - OCSP: Queries a server for the cert's status
    2. If revoked, verification fails—even if the chain is valid
    it stops attackers who stole a private key but haven’t expired yet.  


#### Visual Analogy  
| PKI Concept          | Real-World Equivalent          | What Could Go Wrong?               |
|----------------------|--------------------------------|------------------------------------|
| End-Entity Cert  | Your driver's license          | Fake ID                            |
| Intermediate CA  | Local DMV office               | Rogue DMV employee                 |
| Root CA          | Federal government             | Corrupt government (rare)          |
| Revocation Check | Checking for stolen licenses   | Forgetting to check the blacklist  |




#### Real World Uses  
Digital signatures silently power security in systems you use daily:

##### Code Signing  
  Developers sign software with their private key. Your OS verifies the signature using the publisher's public key before installation. When Windows Update installs a driver, it checks Microsoft's signature. If tampered, you'll see *Windows can't verify the publisher of this driver* it prevents supply chain attacks (like SolarWinds)

##### Blockchain Transactions  
  Bitcoin uses ECDSA signatures. Your wallet signs transactions with a private key, miners verify with your public address. which enables trustless value transfer.
  
```python
# Bitcoin Transaction Signing (Simplified)
from ecdsa import SigningKey # Uses SECP256k1 curve

private_key = SigningKey.generate() # Wallet's secret
tx_data = "Send 0.1 BTC to Alice" 
signature = private_key.sign(tx_data.encode())

# Network verifies using sender's public address
```


##### Legal e-Signatures  
  Platforms like DocuSign use digital signatures + audit trails. Each action is hashed and signed with tamper proof timestamps. it complies with eIDAS (EU) and ESIGN Act (US) when using QES (Qualified Electronic Signatures)

Even robust systems have vulnerabilities. Here's how attackers strike—and how we defend:

| Attack Vector         | Example                      | Mitigation                          | Technical Implementation          |
|-----------------------|------------------------------|-------------------------------------|-----------------------------------|
| Stolen Private Keys | CodeSign hack (2023)         | Hardware Security Modules (HSMs) | Keys never leave FIPS 140-2 Level 3 devices |
| Weak Algorithms     | SHA-1 collision (2017)       | SHA-3 or BLAKE3 hashing     | `openssl dgst -sha3-256 document.pdf` |
| Certificate Spoofing | Fake HTTPS certs             | Certificate Transparency logs   | Chrome requires CT for EV certs |


Here's Algorithm Upgrade Path timeline, to give relavancey on what we use today;

<pre><div class="mermaid">
timeline
    2001 : SHA-1
    2011 : "Deprecation starts"
    2017 : "SHAttered collision attack"
    2023 : SHA-3 adoption
    2030 : Post-quantum standards
</div></pre>

#### TL;DR
1. Certificate Chain: Ensures the sender’s cert is properly authorized
2. Trust Anchor: Root CAs are the ultimate source of trust (pre installed) 
3. Revocation: Prevents use of compromised certificates
4. Defense in Depth: HSMs + algorithm upgrades + transparency logs

In short, this system is what enables the HTTPS padlock you see in your browser ensuring that you're really communicating with a trusted website like *kartheeklade.com*, without having to manually verify its identity.

I hope this blog post gave you a good overview of Digital Signatures & PKI. If you are reading up to this point, you might be interested in cyber security. Going forward, i will try to add more intresting blogs like this one so, keep an eye on this blog page. I hope you enjoyed reading this as much as I enjoyed writing it :) made with <3 Kartheek Lade