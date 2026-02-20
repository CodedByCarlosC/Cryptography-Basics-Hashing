🔐 Cryptography Foundations – Public Key & Hashing Lab

📘 Overview

This repository documents my hands-on learning of **Public Key Cryptography and Hashing fundamentals** through a TryHackMe lab environment.

The focus of this project was to understand how modern systems establish trust, protect identities, secure communications, and safely store sensitive data — from both a **defensive** and **offensive** security perspective.

These cryptographic principles power:

- SSH authentication  
- HTTPS/TLS certificates  
- Secure key exchange  
- Password storage systems  
- Integrity verification  
- Hash cracking and forensic analysis  

Understanding these foundations is critical for cybersecurity, SOC analysis, and incident response roles.

---

# 🔑 Public Key Cryptography

## 🔹 Core Security Concepts

Public key cryptography helps enforce:

- **Authentication** – verifying identity  
- **Authenticity** – verifying message source  
- **Integrity** – ensuring data is not altered  
- **Confidentiality** – preventing unauthorized access  

---

## 🔹 RSA (Rivest–Shamir–Adleman)

- Based on difficulty of factoring large prime numbers  
- Public Key: (n, e)  
- Private Key: (n, d)  
- Variables explored:
  - p, q (prime numbers)
  - n = p × q
  - φ(n)
  - e (public exponent)
  - d (private exponent)
  - m (plaintext)
  - c (ciphertext)

Learned how RSA performs encryption and decryption using modular arithmetic and why large primes are essential for security.

---

## 🔹 Diffie-Hellman Key Exchange

- Establishes a shared secret over an insecure channel  
- No pre-shared key required  
- Used heavily in TLS handshakes  

Both parties independently compute the same shared key without transmitting it directly.

---

## 🔹 SSH Key Authentication

- Generated ED25519 key pairs  
- Examined:
  - Public vs private key structure  
  - Fingerprint verification  
  - authorized_keys behavior  
  - Proper file permissions (600)  

Understood how SSH prevents man-in-the-middle attacks and why private keys must be protected like passwords.

---

## 🔹 Digital Signatures

- Created using a private key  
- Verified using a public key  
- Protect integrity and authenticity  

Explored how hashing is incorporated before signing to ensure document integrity.

---

## 🔹 Certificates & TLS

- HTTPS relies on certificate chains of trust  
- Chain structure:
  - Website Certificate  
  - Intermediate CA  
  - Root CA  

Learned how browsers validate certificates and how Certificate Authorities establish trust.

---

## 🔹 PGP / GPG

- Generated GPG key pairs  
- Explored:
  - Signing vs encrypting  
  - Key expiration  
  - Import/export  
- Practiced decrypting encrypted files  

Reinforced understanding of public/private key cryptography in secure communication workflows.

---

# 🧩 Hashing Fundamentals

Hashing is:

- One-way  
- Keyless  
- Fixed-length output  
- Designed to resist reversal  

Any small change in input results in a drastically different output (avalanche effect).

---

## 🔹 Hash Functions Explored

- MD5 (deprecated)
- SHA1 (deprecated)
- SHA256
- SHA512

Observed how even a one-bit difference produces completely different hash outputs.

---

## 🔹 Hash Collisions

- Learned about the pigeonhole principle  
- Understood why collisions are mathematically inevitable  
- Studied why MD5 and SHA1 are considered insecure  

---

# 🔐 Secure Password Storage (Defensive)

## ❌ Insecure Practices

- Storing passwords in plaintext  
- Using outdated encryption  
- Using unsalted MD5/SHA1  

---

## ✅ Secure Practices

1. Use modern hashing algorithms:
   - Argon2  
   - Bcrypt  
   - Scrypt  
   - PBKDF2  

2. Add a **unique salt per user**  
3. Store:
   - Salt  
   - Hash  

Encryption is not ideal for password verification systems because compromise of the encryption key exposes all passwords.

---

## 🌈 Rainbow Tables & Salting

- Rainbow tables allow fast lookup of unsalted hashes  
- Salting prevents:
  - Duplicate hashes  
  - Precomputed lookup attacks  

Unique salts ensure that identical passwords produce different hashes.

---

# ⚔️ Hash Cracking (Offensive Perspective)

Hashes cannot be decrypted — they must be cracked.

Process:
1. Hash candidate passwords  
2. Compare against target hash  
3. Repeat until match is found  

---

## 🔹 Tools Used

### Hashcat (GPU-Accelerated)
hashcat -m <hash_type> -a <attack_mode> hashfile wordlist


- `-m` = hash mode number  
- `-a 0` = straight attack  
- Used `rockyou.txt` for practical cracking  

Explored cracking:
- Bcrypt  
- SHA256  
- SHA512  
- yescrypt  
- HMAC variants  

---

### John the Ripper

- CPU-based cracking tool  
- Works well in virtual machines  
- Supports many hash formats  

---

## 🔹 Linux Hash Recognition

Examined `/etc/shadow` format:



Basic syntax:
$prefix$options$salt$hash


Common prefixes:

| Prefix | Algorithm |
|--------|-----------|
| $y$ | yescrypt |
| $7$ | scrypt |
| $2b$ | bcrypt |
| $6$ | sha512crypt |
| $1$ | md5crypt |

---

## 🔹 Windows Hashes

- NTLM (variant of MD4)  
- Stored in SAM database  
- Context is critical when identifying hash types  

---

# 🔍 Integrity Verification

Hashing ensures files have not been modified.

- Used SHA256 to verify ISO images  
- Compared local hash with official signed checksum file  
- Learned how PGP-signed checksum files provide additional trust  

Also explored duplicate file detection via hash comparison.

---

# 🔐 HMAC (Keyed Hashing)

HMAC combines:

- A secret key (authenticity)  
- A hash function (integrity)  

Formula: HMAC(K, M) = H((K ⊕ opad) || H((K ⊕ ipad) || M))

HMAC ensures both integrity and authenticity of messages.

---

# 🔄 Hashing vs Encoding vs Encryption

## Hashing
- One-way  
- Cannot be reversed  

## Encoding
- Reversible  
- Used for compatibility (UTF-8, Base64)  
- Does NOT provide security  

## Encryption
- Reversible with a key  
- Protects confidentiality  

Practiced Base64 encoding and decoding to reinforce the distinction.

---

# 🛡️ Security Takeaways

- Public key cryptography establishes identity and trust  
- Hashing protects passwords and file integrity  
- Salting prevents rainbow table attacks  
- Modern hashing algorithms are intentionally slow  
- GPU acceleration significantly increases cracking speed  
- Encoding is not encryption  

---

# 🚀 Why This Matters

These concepts directly support:

- SOC investigations  
- Incident response  
- Password breach analysis  
- Secure system design  
- TLS/SSH troubleshooting  
- Hash identification in forensic analysis  

This lab strengthened both my defensive understanding and offensive awareness of cryptographic systems.
