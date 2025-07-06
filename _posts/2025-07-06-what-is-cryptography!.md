---
layout: post
title: What is Cryptography!
date: 2025-07-06 00:00:00
categories: [cryptography]
tags: [security, encryption, cryptography]
last_modified_at: 2025-07-06
---

#### Introduction to Cryptography

Cryptography is the art and science of securing information by transforming it into an unreadable format, ensuring that only authorized parties can access it. It plays a crucial role in protecting sensitive data, enabling secure communication, and safeguarding digital transactions. From ancient ciphers to modern encryption algorithms, cryptography has evolved to address the challenges of privacy and security in the digital age.

At its core, cryptography relies on mathematical techniques to encode and decode information. Common applications include:

  🔒 Securing passwords (e.g., hashing in databases)

  ✉️ Encrypting emails (PGP, S/MIME)

  💳 Protecting online banking (SSL/TLS)

With the rise of cyber threats, cryptography remains a cornerstone of cybersecurity, ensuring confidentiality, integrity, and authenticity in the digital world.

> Cryptography is not just about hiding information; it's about enabling trust in a connected world.

#### A Brief History of Cryptography

Cryptography has always been about one thing: protecting secrets. But how we’ve done that has evolved dramatically across time.

#### 🏛 The Evolution of Cryptography: Key Milestones

**🏛 Caesar Cipher (c. 50 BCE)**  
One of the earliest known encryption methods, famously used by Julius Caesar.  
➡️ **How it works:** Shift each letter in the message by a fixed number of places in the alphabet.  

Example:  
Plaintext: "HELLO"  
Shift: +3  
Ciphertext: "KHOOR"  

While simple by today’s standards, it was effective enough to confuse enemies in ancient times.


**⚙️ Enigma Machine (WWII, 1930s–1940s)**  
An electromechanical device used by Nazi Germany to encrypt military communications.  
➡️ **How it works:** Letters were scrambled using a series of rotating rotors and plugboards, with daily key settings changing the encryption pattern.  

Example:  
Plaintext: "A"  
Ciphertext: "T" (today) → "G" (tomorrow, with a new key setting)  

The Enigma Machine was eventually cracked by Allied cryptographers, including Alan Turing, marking a pivotal moment in both the war and cryptographic history.



**💡 From War Rooms to Web Browsers**  
Cryptography transitioned from a military tool to a cornerstone of modern digital security. Key milestones include:  

- **1976:** Diffie–Hellman key exchange introduced — the first method to securely share keys in public.  
- **1977:** RSA algorithm invented by Rivest, Shamir, and Adleman — a breakthrough in public-key cryptography.  
- **1991:** Phil Zimmermann released PGP (Pretty Good Privacy), empowering ordinary users with strong encryption for emails and files.  
- **2000s–Now:** AES (Advanced Encryption Standard) became the global standard for symmetric encryption, securing everything from Wi-Fi networks to mobile apps.


> From ancient ciphers to cutting-edge algorithms, cryptography has evolved to meet the ever-growing demands of privacy and security in a connected world.

Why It Matters Today. without cryptography, there would be no:

  - Secure messaging (WhatsApp’s end-to-end encryption).
  - Blockchain (Bitcoin’s SHA-256 hashing).
  - E-commerce (credit card encryption).

#### Core Concepts of Cryptography

Plaintext vs Ciphertext: Plaintext is readable data; ciphertext is the encrypted version. as in Plaintext: "Hello" → Ciphertext (encrypted): "Khoor" (Caesar shift +3)


Keys: Keys are used to encrypt and decrypt messages. Symmetric cryptography uses the same key for both, while asymmetric cryptography uses a pair of keys in  Symmetric Single key is used for both encryption and decryption (e.g., AES) fast but risky if key is stolen 
via any atacks or leaked.

Symmetric-Key Cryptography: Fast and efficient; uses the same key for encryption and decryption (e.g., AES).


<pre> <div class="mermaid">

flowchart LR
    P1["`📄 **Plaintext**<br>'I love pizza'`"] -->|🔒 Encrypt| C["`🔐 **Ciphertext**<br>'Xb92@kLm!1'`"]
    C -->|🔓 Decrypt| P2["`📄 **Plaintext**<br>'I love pizza'`"]
    
    P1 --> E["⚙️Encryption<br>Key + AES"]
    E -.->|🔑 Secure Channel| D["`⚙️**Decryption**<br>AES-256 + Key`"] 
    D -.-> C
    
    P2 --> S[✅ Success!]
    
    linkStyle 0,1 stroke:#333,stroke-width:2px
    linkStyle 2,3 stroke:#666,stroke-dasharray:3

</div> </pre>


    


Asymmetric-Key Cryptography Uses a public-private key pair; ideal for secure key exchange (e.g., RSA).


<pre> <div class="mermaid">

flowchart LR
    S["👤 Sender"] -->|🔓 Encrypts with<br>Receiver's Public Key| ENC["📦 Encrypted Message"]
    ENC -->|📡 Sent over network| RCV["👤 Receiver"]
    RCV -->|🔑 Decrypts with <br> it's own Private Key| P["📄 Plaintext"]

    S --> PK["🔑 Public Key of Receiver"]
    RCV --> SK["🗝️ Private Key of Receiver"]

    linkStyle 0,1,2 stroke:#444,stroke-width:2px
    linkStyle 3,4 stroke:#999,stroke-dasharray:4

</div> </pre>




In simple lingo;          
🔓 Public Key: Shared openly. Anyone can use it to encrypt a message for you
🔐 Private Key: Kept secret. Only you can decrypt messages sent to you
📬 Ideal for: Secure email, key exchange, digital signatures (hold your horses we will talk about signatures in future blogs)

Hash Functions: One-way functions that produce a fixed-size output (e.g., SHA-256). Useful for password storage and data integrity (and Secure Boot too...)

<pre> <div class="mermaid">
flowchart TD

    %% Sender Side (Top Row)
    MSG["📤 Original Message<br><code>'hello123'</code>"] --> H1["🧮 SHA-256 Hash"]
    H1 --> DIGEST["🔐 Digest<br><code>2cf24dba5fb0a...</code>"]
    DIGEST -.->|📬 Sent with message| RCV["📥 Receiver"]

    %% Receiver Side (Bottom Row)
    RCV --> MRCV["📄 Received Message<br><code>'hello123'</code>"]
    MRCV --> H2["🧮 Recalculate SHA-256"]
    H2 --> COMP["🔁 Compare Hashes"]
    COMP -->|✅ Match| VALID["✅ Message Untouched"]
    COMP -->|❌ Mismatch| INVALID["⚠️ Message Tampered"]

    %% Positioning using invisible links to enforce 2 levels
    MSG -.-> MRCV

    %% Optional Styling
    linkStyle 0,1,2 stroke:#222,stroke-width:2px
    linkStyle 3,4,5,6 stroke:#666,stroke-dasharray:3

</div> </pre>


### 🚀 Modern Cryptography in Action

Cryptography isn’t just for spies and hackers it’s quietly working behind the scenes every time you use your phone, shop online, or check your bank account, Here are real-world examples where cryptography is making your digital life secure:

WhatsApp uses end-to-end encryption to ensure that only the sender and receiver can read messages not even WhatsApp can see them

<pre> <div class="mermaid">
flowchart LR
    
        YOU["👤 You<br><code>'I love 🍕'</code>"] --> WAPP["🟢 WhatsApp<br><code>'kD93*#Xz!&@9'</code>"] --> FRIEND["👤 Your Friend<br><code>'I love 🍕'</code>"]

    WAPP --> NOTE["💬 WhatsApp:<br><i>We <b>totally</b> can't read this 👀...<br>But hey, meta-data is tasty 😇</i>"]

</div> </pre>




HTTPS (SSL/TLS) secures your connection when visiting websites, protecting sensitive data like passwords and credit card numbers from eavesdroppers. Blockchain technologies like Bitcoin rely on cryptographic hash functions (e.g., SHA-256) and digital signatures to secure transactions and ensure immutability.

### 🧩 How Different Fields Use Cryptography

Cryptography isn’t just for banks and the military — it’s woven into nearly every modern digital system. Here’s how different sectors put it to work:

🏦 Banking
Banks use strong symmetric encryption (like AES-256) to protect transactions, PINs, and customer records. It ensures financial data remains confidential even over insecure networks.

⛓️ Blockchain & Cryptocurrency
Technologies like Bitcoin and Ethereum use hash functions (e.g., SHA-256) for data integrity and digital signatures for transaction verification — making sure no one can tamper with the blockchain.

🪖 Military & Defense
Defense communications are secured using classified, government-approved cryptographic protocols, including Suite B and post-quantum algorithms (in progress), ensuring confidentiality even in hostile environments.

🏥 Healthcare
Patient data is protected under regulations like HIPAA, using encryption to secure electronic health records (EHRs), prescriptions, and lab reports — especially during cloud transfers or remote diagnosis.

🌐 Internet of Things (IoT)
Devices like smart cameras, thermostats, and pacemakers rely on lightweight encryption algorithms (like ECC or ChaCha20) to keep communication secure — even on resource-limited hardware.


#### 🚨 Attacks on Cryptographic Systems

Cryptography is powerful, but it's not bulletproof. Many real-world attacks don’t break the math—they exploit how cryptography is **used** or **implemented**. Even the strongest systems can be undermined by poor implementation or weak keys:

🔑 **Brute Force Attacks**  
Brute force attacks involve systematically guessing every possible combination of keys until the correct one is found. This method exploits weak or short keys, as they reduce the number of combinations an attacker needs to try. For example, a 4-digit PIN like "1234" has only 10,000 possible combinations, making it relatively easy to crack compared to a 256-bit encryption key, which has an astronomically larger number of possibilities. Weak passwords such as "password" or "123456" are prime targets for brute force attacks, as they are commonly used and easy to guess.

🕵️‍♂️ **Man-in-the-Middle (MITM) Attacks**  
MITM attacks occur when an attacker secretly intercepts and manipulates communication between two parties without their knowledge. Imagine using public Wi-Fi at a coffee shop to log into your email. An attacker on the same network could intercept your login credentials if the connection is not encrypted. This is why secure protocols like HTTPS and end-to-end encryption are critical—they prevent attackers from eavesdropping or tampering with sensitive data during transmission.

⚡ **Side-Channel Attacks**  
Side-channel attacks exploit indirect information leaked by a system during its operation rather than directly attacking the cryptographic algorithm. These leaks can include physical clues such as power consumption, electromagnetic emissions, timing variations, or even sounds produced by the device. A famous example is the TEMPEST program, a U.S. government initiative that analyzed electromagnetic emissions from electronic devices to reconstruct sensitive information like screen content or keystrokes. Mitigating side-channel attacks often involves designing hardware and software to minimize such leaks and implementing countermeasures like randomization or shielding.

Cryptography is only as strong as its implementation. Understanding these attack vectors is essential for designing secure systems that can withstand real-world threats.

> Even unbreakable math can't save you from poor design or careless coding.

#### Cryptography vs Steganography

When it comes to securing information, cryptography and steganography are two distinct yet complementary techniques. Cryptography focuses on transforming a message into an unreadable format, ensuring that only those with the correct key can decipher it. For example, if you encrypt the phrase "Top Secret" using a key, the output might look like "kD93*df@!". Without the key, the message remains unintelligible. Steganography, on the other hand, takes a different approach. Instead of scrambling the message, it hides the existence of the message itself. Imagine embedding "Top Secret" within an innocent-looking image or audio file. To an observer, the file appears normal, but the hidden message can be extracted using specialized tools.

While cryptography secures the content of a message, steganography conceals its presence. Combining these techniques can create layers of security, making it harder for attackers to detect or access sensitive information.

<Pre>
<div class="mermaid">
flowchart LR
    subgraph CRYPTO["🔐 Cryptography"]
        C1["📌 Purpose: Hide the **content**"]
        C2["🔢 Output: Random looking ciphertext"]
        C3["🧠 Detection: Easy to notice"]
        C4["🔑 Needs a Key: ✅ Yes"]
        C5["💡 Bonus: Used in HTTPS, messaging apps"]
    end

    subgraph STEGO["🖼️ Steganography"]
        S1["📌 Purpose: Hide the **existence**"]
        S2["🎨 Output: Normal looking media"]
        S3["🕵️ Detection: Hard to detect"]
        S4["🔑 Needs a Key: ❌ Not always"]
        S5["💡 Bonus: Used for watermarking, covert messaging"]
    end

	CRYPTO ---- STEGO


    %% Vertical alignment
    C1 --> C2 --> C3 --> C4 --> C5
    S1 --> S2 --> S3 --> S4 --> S5
</div></pre>






#### The Future of Cryptography
As technology evolves, so do the challenges and opportunities in cryptography. Here are some key trends shaping its future:

Post-Quantum Cryptography: Quantum computers, with their immense processing power, pose a threat to current cryptographic algorithms. Post-quantum cryptography aims to develop algorithms that remain secure even against quantum attacks. These advancements are crucial for safeguarding data in a quantum-powered world.

AI & Cryptanalysis: Artificial intelligence is revolutionizing cryptography. On one hand, machine learning can enhance cryptographic systems by identifying vulnerabilities and optimizing algorithms. On the other hand, AI-powered cryptanalysis can be used to break weaker systems, pushing the need for stronger defenses. The future demands cryptographic solutions that are not only robust but also adaptive to emerging technologies and threats


#### ✅ Conclusion – Cryptography Isn’t Optional. It’s Inevitable.

Let’s get real.

  📌 Your chats? Encrypted  
  📌 Your bank transfers? Secured with cryptographic keys  
  📌 Your passwords? Stored as hashes (hopefully)  
  📌 Your browser? Running HTTPS with TLS in the background  



#### 🧠 TL;DR

* 🛡 **Cryptography ≠ just hiding secrets** it’s about creating **trust** in an untrusted world.
* 🎯 It's the backbone of modern digital life: from your WhatsApp messages to billion-dollar blockchain transactions.
* 🔐 *"In crypto we trust, the rest is just plaintext"*


