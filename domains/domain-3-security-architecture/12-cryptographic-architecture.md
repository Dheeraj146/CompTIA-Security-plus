# Cryptographic Architecture

Cryptographic architecture is the deliberate design and implementation of cryptographic mechanisms to protect information, communications, identities, applications, and systems. In a secure architecture, cryptography is not simply the act of encrypting a file. It includes selecting appropriate cryptographic algorithms, managing keys, establishing trust, validating identities, protecting certificates, handling cryptographic lifecycle events, and ensuring that security controls are used for the correct purpose.

For Security+, the most important principle is to understand **what security property a cryptographic mechanism provides, how the keys are used, where trust comes from, and what operational requirements surround the cryptography**.

---

## 1. What Cryptography Protects

Cryptography can support several security objectives.

### Confidentiality

Confidentiality prevents unauthorized parties from understanding protected information.

Encryption is the primary cryptographic mechanism used for confidentiality.

Examples:

- Encrypting a laptop disk
- Encrypting database backups
- Using HTTPS for web traffic
- Encrypting files before transmission

### Integrity

Integrity provides assurance that information has not been modified in an unauthorized or unexpected manner.

Cryptographic hashes and digital signatures can provide integrity protection.

### Authentication

Cryptographic mechanisms can help establish the identity of a user, device, service, or organization.

Examples include:

- Certificates
- Digital signatures
- Public/private key authentication
- Kerberos-related cryptographic mechanisms

### Non-repudiation

Non-repudiation is the ability to provide evidence supporting the origin and integrity of an action or message so that the signer cannot easily deny having performed it.

Digital signatures can support non-repudiation when the surrounding identity, key-management, and operational controls provide the required assurance.

---

## 2. Encryption vs Hashing

One of the most important Security+ distinctions is that **encryption and hashing are not the same thing**.

### Encryption

Encryption transforms plaintext into ciphertext using a cryptographic algorithm and key.

The intended recipient can use the appropriate key and process to recover the plaintext.

Conceptually:

**Plaintext → Encryption + Key → Ciphertext → Decryption + Key → Plaintext**

### Hashing

Hashing transforms input into a fixed-length digest.

Conceptually:

**Input → Hash function → Digest**

A secure cryptographic hash is designed to make it computationally impractical to reverse the digest into the original input.

### Exam distinction

If the requirement is:

> "Protect information so unauthorized users cannot read it."

Think **encryption**.

If the requirement is:

> "Detect whether data has changed."

Think **hashing or another integrity mechanism**.

---

## 3. Symmetric Cryptography

**Symmetric cryptography** uses the same secret key, or corresponding shared secret material, for encryption and decryption.

Conceptually:

**Sender + shared secret → encryption → ciphertext → decryption + same shared secret → recipient**

Both parties must possess the secret securely.

### Advantages

- Fast
- Efficient for large volumes of data
- Suitable for bulk encryption
- Generally less computationally expensive than asymmetric cryptography

### Disadvantage

The major challenge is **secure key distribution**.

If two parties need to communicate securely using a shared secret, they need a secure method to establish or distribute that secret.

---

## 4. Examples of Symmetric Algorithms

Common symmetric algorithms include:

- AES
- 3DES
- ChaCha20

### AES

**Advanced Encryption Standard (AES)** is a widely used symmetric encryption standard.

AES supports key sizes including:

- 128-bit
- 192-bit
- 256-bit

The key size and security of an implementation must be considered along with the mode of operation and key-management architecture.

### 3DES

Triple DES applies the DES cipher through a multiple-encryption construction. It is an older technology and has largely been replaced by modern algorithms such as AES.

For contemporary designs, legacy algorithms should not be selected merely because they are familiar.

### ChaCha20

ChaCha20 is a modern stream cipher commonly used with an authentication mechanism such as Poly1305 in the ChaCha20-Poly1305 authenticated-encryption construction.

---

## 5. Modes of Operation

Block ciphers such as AES require a mode of operation to define how blocks of data are processed.

Important concepts include:

- ECB
- CBC
- CTR
- GCM

### ECB

Electronic Codebook (ECB) encrypts identical plaintext blocks independently.

This can reveal patterns in structured data and is generally unsuitable for securely encrypting arbitrary structured information.

### CBC

Cipher Block Chaining (CBC) links blocks using chaining mechanisms. Secure implementations require appropriate initialization vectors and authentication considerations.

Encryption alone does not necessarily provide integrity.

### GCM

Galois/Counter Mode (GCM) provides authenticated encryption when used correctly.

It can provide:

- Confidentiality
- Integrity/authentication of ciphertext

This is an example of **authenticated encryption**.

---

## 6. Authenticated Encryption

Authenticated encryption combines confidentiality with integrity/authentication of the protected data.

Examples include:

- AES-GCM
- ChaCha20-Poly1305

This is important because encrypting data alone does not automatically guarantee that an attacker cannot modify the ciphertext without detection.

A secure architecture should therefore consider both:

**Can unauthorized parties read the data?**

and:

**Can unauthorized parties modify the data without detection?**

---

## 7. Initialization Vectors and Nonces

Some cryptographic modes require an initialization vector (IV) or nonce.

These values help ensure that encryption operations do not produce undesirable repeated patterns.

The exact requirements depend on the algorithm and mode.

A particularly important rule is that some constructions require **nonce uniqueness**. Reusing a nonce incorrectly can seriously weaken security.

Developers should therefore use well-tested cryptographic libraries rather than inventing their own nonce-generation logic.

---

## 8. Asymmetric Cryptography

**Asymmetric cryptography**, also called public-key cryptography, uses a key pair:

- Public key
- Private key

The keys are mathematically related, but the private key is kept secret while the public key can be distributed.

Asymmetric cryptography supports:

- Digital signatures
- Public-key authentication
- Key establishment
- Certificate-based trust

### Key rule

**Public key → can be distributed.**

**Private key → must remain protected.**

Compromise of a private key can have serious consequences depending on what the key is used for.

---

## 9. Public-Key Encryption Concept

Suppose Alice wants to send confidential information to Bob using public-key encryption.

1. Bob has a public/private key pair.
2. Bob makes his public key available.
3. Alice obtains Bob's authentic public key.
4. Alice encrypts the appropriate information using Bob's public key.
5. Bob uses his private key to perform the corresponding private-key operation.

The important architectural problem is not merely generating keys. Alice needs confidence that the public key actually belongs to Bob.

This is where certificates and PKI become important.

---

## 10. Digital Signatures

A **digital signature** uses asymmetric cryptography to provide evidence of authenticity and integrity.

Conceptually:

**Message → Hash → Digest → Sign with private key → Signature**

The recipient can use the corresponding public key to verify the signature.

A simplified verification process is:

**Message → Hash → Compare with verified signature information**

If the message has changed, signature verification should fail.

### Key rule

**Private key signs.**

**Public key verifies.**

This is a critical Security+ exam distinction.

---

## 11. Digital Signature Properties

Digital signatures can provide:

- Integrity
- Authentication of the signing key holder
- Evidence of origin
- Support for non-repudiation

However, a signature is only meaningful if the public key can be reliably associated with the claimed identity.

That association is commonly supported by certificates and PKI.

---

## 12. Hash Functions

A cryptographic hash function produces a fixed-length digest from input data.

Important properties include:

- Deterministic output
- Fixed-length digest for a given algorithm
- Efficient computation
- Preimage resistance
- Collision resistance

A tiny change in input should produce a substantially different digest.

Example concept:

**File A → SHA-256 → Digest A**

**Modified File A → SHA-256 → Different Digest**

The difference can indicate that the file changed.

---

## 13. Common Hash Algorithms

Examples include:

- SHA-256
- SHA-384
- SHA-512
- SHA-3

Older algorithms such as MD5 and SHA-1 have known collision weaknesses and should not be selected for modern security-sensitive integrity requirements merely because they are widely recognized.

### Important distinction

Hashing is not encryption.

A hash digest is not intended to be decrypted back into the original input.

---

## 14. Password Hashing

Passwords should not normally be stored as plaintext.

They should be processed using password-specific hashing mechanisms designed to make large-scale guessing attacks more expensive.

Modern password-storage approaches commonly use algorithms such as:

- Argon2
- bcrypt
- scrypt

A unique **salt** should be used for each password.

### Salt

A salt is additional random data combined with a password before password hashing.

The salt helps prevent attackers from efficiently using precomputed tables against many password hashes.

### Important distinction

General-purpose fast hashes such as SHA-256 are not automatically appropriate as password-storage algorithms by themselves. Password hashing should use a deliberately slow, memory-hard or computationally expensive password-hashing design where appropriate.

---

## 15. Salting vs Encryption

A salt does not encrypt a password.

It is additional input used with a password-hashing process.

For example:

**Password + unique salt → password hashing function → stored password verifier**

During login, the stored salt and appropriate password-hashing parameters are used to calculate a new verifier for comparison.

---

## 16. Key Exchange and Key Establishment

Symmetric encryption is efficient, but two parties need a shared secret.

Asymmetric cryptography can help establish shared secrets without directly transmitting the final symmetric encryption key in plaintext.

A common example is **Diffie-Hellman (DH)** key exchange.

The basic concept allows two parties to derive shared secret material over a communication channel without simply sending the resulting secret directly across the network.

### Important limitation

Basic DH by itself does not authenticate the identities of the participants.

An attacker could potentially perform a man-in-the-middle attack if authentication is not provided through another mechanism.

This is why real secure protocols combine key establishment with authentication and other security mechanisms.

---

## 17. Diffie-Hellman Variants

Common concepts include:

- DH
- ECDH
- Ephemeral key exchange

**Elliptic Curve Diffie-Hellman (ECDH)** uses elliptic-curve cryptography for key agreement.

Ephemeral key exchange can provide **forward secrecy** when implemented as part of an appropriate protocol design.

---

## 18. Forward Secrecy

**Forward secrecy** means that compromise of a long-term private key should not allow an attacker to decrypt previously captured session traffic, assuming ephemeral session keys were properly established and then discarded.

For example:

1. An attacker records encrypted traffic today.
2. The attacker later obtains a server's long-term private key.
3. With forward secrecy, the attacker should not automatically be able to decrypt the previously captured sessions.

Ephemeral Diffie-Hellman mechanisms are commonly used to support this property in modern protocols.

---

## 19. Public Key Infrastructure (PKI)

**Public Key Infrastructure (PKI)** is the collection of technologies, roles, policies, procedures, and trust relationships used to manage public-key certificates and associated cryptographic identities.

PKI commonly involves:

- Certificate authorities
- Digital certificates
- Registration processes
- Certificate validation
- Certificate revocation
- Certificate lifecycle management
- Trust stores

PKI solves an important problem:

> **How can a system determine that a public key belongs to the identity it claims to represent?**

---

## 20. Digital Certificates

A digital certificate binds an identity or identifier to a public key through a digitally signed certificate structure.

A certificate can contain information such as:

- Subject identity
- Public key
- Issuer
- Validity period
- Serial number
- Key usage information
- Extended key usage
- Subject Alternative Name (SAN)
- Digital signature from the issuing CA

The certificate allows relying parties to evaluate whether a public key should be trusted for a particular identity and purpose.

---

## 21. Certificate Authority (CA)

A **Certificate Authority (CA)** issues and signs certificates.

A CA is trusted by systems that trust the CA's certificate or trust anchor.

A simplified hierarchy is:

**Root CA → Intermediate CA → End-entity certificate**

The exact hierarchy can be more complex, but the principle is that trust can be delegated through a certificate chain.

---

## 22. Root CA

A **root CA** is a trust anchor at the top of a certificate hierarchy.

Root CA private keys require strong protection because compromise can undermine trust in certificates issued through that authority.

For this reason, organizations may use highly restricted systems and procedures for root CA operations.

---

## 23. Intermediate CA

An **intermediate CA** receives authority from a higher-level CA and can issue certificates to lower-level entities.

Using intermediates can help protect the root CA by keeping routine certificate issuance away from the root signing key.

Conceptually:

**Root CA trusts Intermediate CA → Intermediate CA issues server certificate**

---

## 24. Certificate Validation

A certificate should not be trusted simply because it exists.

Validation can include checking:

- Signature chain
- Trusted issuer
- Validity period
- Subject/SAN identity
- Key usage
- Extended key usage
- Revocation status where applicable
- Appropriate algorithm/security requirements

For example, when connecting to a secure website, the client checks whether the certificate is valid for the hostname being accessed.

---

## 25. Certificate Revocation

Certificates may need to be revoked before their natural expiration.

Reasons can include:

- Private-key compromise
- Incorrect certificate issuance
- Identity changes
- CA policy violations
- Loss of control of the associated system

Two important certificate-revocation mechanisms are:

- CRL
- OCSP

---

## 26. Certificate Revocation List (CRL)

A **Certificate Revocation List (CRL)** is a published list of certificates that have been revoked by a certificate authority.

A client can obtain the relevant CRL and check whether a certificate's serial number appears on it.

### Limitation

CRLs can become large and may not provide the most immediate possible status information.

---

## 27. Online Certificate Status Protocol (OCSP)

**OCSP** allows a client to query certificate status information from an OCSP responder.

The response can indicate whether the certificate is:

- Good
- Revoked
- Unknown

OCSP can provide more targeted status checking than downloading a complete CRL.

---

## 28. OCSP Stapling

**OCSP stapling** allows a server to obtain a signed OCSP response and provide it to clients during the TLS interaction.

This can reduce the need for every client to contact the CA's OCSP responder directly.

It can improve privacy and reduce latency/dependency on external OCSP infrastructure.

---

## 29. PKI Trust Models

Trust can be organized in different ways.

### Hierarchical trust

A root CA delegates trust to intermediate authorities.

### Web of trust

A decentralized model in which participants establish trust relationships with keys or identities.

PGP/OpenPGP commonly uses a web-of-trust concept rather than relying exclusively on a conventional hierarchical public CA model.

### Enterprise PKI

An organization can operate its own internal CA infrastructure for:

- Employee certificates
- Device certificates
- Internal TLS
- Wi-Fi authentication
- VPN authentication
- Smart cards
- Application identities

---

## 30. Key Management Lifecycle

Cryptographic security depends heavily on key management.

A key lifecycle can include:

**Generation → Distribution → Storage → Use → Rotation → Revocation → Archival/Recovery → Destruction**

Each stage must be controlled.

Weak key management can defeat strong cryptographic algorithms.

---

## 31. Secure Key Generation

Keys should be generated using cryptographically secure random mechanisms appropriate to the algorithm.

Poor randomness can make keys predictable.

Keys should not be generated using ordinary pseudo-random functions that are not designed for cryptographic use.

---

## 32. Key Storage

Private and secret keys require strong protection.

Possible protection mechanisms include:

- Hardware Security Modules (HSMs)
- Trusted Platform Modules (TPMs)
- Secure key-management systems
- Access-controlled encrypted storage
- Hardware-backed keystores

The correct mechanism depends on the sensitivity and use of the key.

---

## 33. Hardware Security Module (HSM)

An **HSM** is specialized hardware designed to securely generate, store, and use cryptographic keys and perform cryptographic operations.

HSMs can help protect high-value keys such as:

- CA private keys
- Code-signing keys
- Payment-related keys
- Database encryption keys

An HSM can be designed so that sensitive private-key material is difficult to extract even if an application interacts with the device to perform cryptographic operations.

---

## 34. Trusted Platform Module (TPM)

A **TPM** is a hardware security component designed to provide protected cryptographic operations and storage for certain keys and measurements.

It can support functions such as:

- Device identity
- Key protection
- Secure boot-related measurements
- Platform integrity mechanisms

A TPM is generally associated with an endpoint or computing platform, whereas an HSM is typically designed as a specialized cryptographic security system.

---

## 35. Key Rotation

**Key rotation** replaces a cryptographic key with a new key according to policy or operational requirements.

Reasons include:

- Limiting cryptographic exposure
- Meeting policy requirements
- Responding to risk
- Reducing impact of long-term key use
- Supporting algorithm migration

Key rotation must be designed so applications can transition without losing access to legitimately protected data.

---

## 36. Key Revocation

A key may need to be revoked or invalidated when:

- It is compromised
- Its owner is no longer authorized
- A device is retired
- A certificate is revoked
- A cryptographic algorithm becomes unacceptable

Revocation is different from routine rotation.

**Rotation** is planned replacement.

**Revocation** is withdrawal of trust or authorization before normal lifecycle completion.

---

## 37. Key Destruction

Keys should be securely destroyed when they are no longer required, subject to legal, business, and recovery requirements.

Destroying the key associated with encrypted data can make the data effectively inaccessible, which is sometimes intentionally used as part of secure data destruction.

However, key destruction must be carefully controlled so that required records are not accidentally rendered unrecoverable.

---

## 38. Key Escrow and Recovery

**Key escrow** involves storing cryptographic keys or key-recovery material with a trusted mechanism so that authorized recovery can occur under defined conditions.

Possible use cases include:

- Business continuity
- Legal recovery requirements
- Enterprise encrypted-data recovery
- Recovery after administrator loss

Key escrow introduces significant security and governance considerations because an escrow system becomes a high-value target.

---

## 39. Key Agreement vs Key Transport

### Key agreement

Both parties contribute information to establish shared secret material.

Diffie-Hellman is an example.

### Key transport

One party generates a secret and securely transports or protects it for the other party using an asymmetric mechanism.

Understanding the distinction helps explain why protocols use different cryptographic operations during session establishment.

---

## 40. Hybrid Cryptography

Modern secure protocols commonly combine symmetric and asymmetric cryptography.

Why?

- Asymmetric cryptography is useful for authentication and key establishment.
- Symmetric cryptography is efficient for bulk data encryption.

A simplified secure-session process is:

1. Establish or authenticate identities.
2. Perform asymmetric key agreement or key establishment.
3. Derive symmetric session keys.
4. Encrypt bulk traffic using efficient symmetric cryptography.
5. Authenticate/integrity-protect the traffic.

This is why secure protocols do not generally encrypt every byte of a long session directly with an expensive public-key operation.

---

## 41. TLS and Cryptographic Architecture

**Transport Layer Security (TLS)** protects application-layer communications over an untrusted network.

HTTPS is HTTP carried over TLS.

TLS can provide:

- Confidentiality
- Integrity
- Server authentication
- Optional client authentication

A simplified architecture is:

**Client → TLS handshake → Certificate/authentication + key establishment → Symmetric session → Protected application data**

Modern TLS versions are preferred over obsolete protocols and configurations.

---

## 42. TLS Certificates

When a browser connects to a secure website, the server presents a certificate.

The client can validate:

- Certificate chain
- Certificate validity
- Hostname/SAN
- Signature
- Key usage
- Trust anchor

After authentication and key establishment, symmetric session keys are used for efficient data protection.

This is a practical example of hybrid cryptography.

---

## 43. HTTPS

**HTTPS** is HTTP protected using TLS.

It helps protect web communications from:

- Eavesdropping
- Unauthorized modification
- Certain forms of session interception

However, HTTPS does not automatically make an application secure.

Application-layer vulnerabilities such as:

- SQL injection
- Broken authorization
- Insecure business logic
- Malicious file upload

can still exist over HTTPS.

Encryption protects the communication channel; it does not replace application security.

---

## 44. IPsec Cryptographic Architecture

**IPsec** is a suite of protocols used to protect IP communications.

Important components include:

- AH
- ESP
- IKE

### AH

Authentication Header can provide integrity, authentication of the source, and anti-replay protection for supported IP packet components.

AH does **not** provide confidentiality.

### ESP

Encapsulating Security Payload can provide confidentiality, integrity/authentication, and anti-replay protection depending on configuration.

ESP is commonly used for modern IPsec VPN implementations.

---

## 45. IPsec Transport vs Tunnel Mode

### Transport mode

Protects the payload of an IP packet while retaining the original IP header.

It is commonly associated with host-to-host communication.

### Tunnel mode

Encapsulates and protects the original IP packet inside a new IP packet.

It is commonly used for VPNs connecting networks or gateways.

### Exam distinction

**Transport mode → host-oriented protection.**

**Tunnel mode → encapsulated IP packet, commonly VPN gateway use.**

---

## 46. IKE

**Internet Key Exchange (IKE)** is used with IPsec to negotiate security associations and establish cryptographic parameters and keying material.

It supports tasks such as:

- Peer authentication
- Cryptographic algorithm negotiation
- Key establishment
- Security Association establishment

Modern IPsec deployments commonly use IKEv2.

---

## 47. Digital Certificates for Device Authentication

Certificates can authenticate devices without relying solely on passwords.

For example:

**Device → presents certificate → authentication system validates certificate → network access granted according to policy**

This approach is commonly used in:

- Enterprise Wi-Fi
- VPNs
- Device authentication
- Mutual TLS
- Machine-to-machine communication

---

## 48. Mutual TLS

In ordinary TLS, the server commonly authenticates to the client using a certificate.

With **mutual TLS (mTLS)**, both sides authenticate using certificates.

Conceptually:

**Client certificate ↔ Server certificate**

mTLS can be useful for:

- Service-to-service communication
- APIs
- Microservices
- Device authentication
- High-assurance internal services

---

## 49. Cryptographic Agility

**Cryptographic agility** is the ability to change cryptographic algorithms, keys, protocols, or parameters without redesigning the entire environment.

This is important because cryptographic algorithms and implementation requirements can change over time.

A cryptographically agile architecture should make it practical to:

- Replace algorithms
- Rotate keys
- Replace certificates
- Upgrade protocol versions
- Disable deprecated cryptography

Hard-coding one cryptographic method everywhere can make future security migration difficult.

---

## 50. Algorithm Selection

Cryptographic architecture should consider:

- Security strength
- Industry standards
- Protocol support
- Performance
- Hardware support
- Data sensitivity
- Compliance requirements
- Key-management requirements
- Lifecycle expectations

The strongest algorithm is not automatically the correct architectural choice if the implementation, protocol, or key-management process is insecure.

---

## 51. Cryptographic Deprecation

Older algorithms or protocols may become unsuitable because of:

- Cryptanalytic advances
- Increased computing capability
- Design weaknesses
- Protocol vulnerabilities
- Operational limitations

Organizations should maintain inventories of cryptographic dependencies so obsolete algorithms can be identified and replaced.

Examples of legacy technologies that should not be selected for modern security-sensitive designs merely because they are familiar include:

- DES
- 3DES for new deployments
- MD5 for security-sensitive integrity
- SHA-1 for modern collision-resistant signatures
- SSLv2/SSLv3
- Weak TLS configurations

---

## 52. Crypto Shredding

**Crypto shredding** is a data-destruction technique in which encryption keys protecting data are securely destroyed, making the encrypted data computationally inaccessible.

It can be useful in environments where:

- Data is encrypted by default
- Secure deletion is required
- Large distributed datasets must be retired

It depends on strong encryption and effective key management.

---

## 53. Data at Rest, in Transit, and in Use

Cryptographic architecture should consider the state of data.

### Data at rest

Data stored on:

- Disk
- SSD
- Database
- Backup
- Object storage

can be protected using encryption at rest.

### Data in transit

Data moving across networks can be protected using:

- TLS
- IPsec
- Secure VPNs
- Other secure protocols

### Data in use

Data currently being processed by a system may be exposed in memory or through computation.

Specialized technologies such as trusted execution environments and confidential-computing mechanisms can provide additional protections in certain environments, but they do not eliminate the need for conventional application and system security.

---

## 54. Database and Storage Encryption

Encryption at rest can be implemented at different layers.

Examples include:

- Full-disk encryption
- Volume encryption
- File-level encryption
- Database encryption
- Application-level encryption
- Object-storage encryption

The correct layer depends on the threat model.

For example, full-disk encryption can protect data if a physical drive is stolen, but it may not protect against an attacker who already has authorized access to a running system and can read decrypted data through the operating system.

---

## 55. Envelope Encryption

Envelope encryption uses one key to encrypt data and another key to protect the data-encryption key.

Conceptually:

**Data → Data Encryption Key (DEK) → Encrypted Data**

Then:

**DEK → Key Encryption Key (KEK) → Protected DEK**

This architecture allows data keys to be managed efficiently while higher-level key-management systems protect the keys used to protect them.

It is widely useful in cloud and enterprise encryption architectures.

---

## 56. Key Encryption Key vs Data Encryption Key

### Data Encryption Key (DEK)

Used to encrypt the actual data.

### Key Encryption Key (KEK)

Used to protect or encrypt another key, such as a DEK.

This separation supports scalable key management.

If a data set is very large, the system does not necessarily need to use a highly protected master key directly to encrypt every block of application data.

---

## 57. Cryptographic Erasure and Backup Considerations

Encryption and key destruction can affect backup architecture.

If encrypted data is backed up but its encryption key is destroyed, the backup may become unrecoverable.

Therefore key-management architecture must be integrated with:

- Backup
- Disaster recovery
- Retention
- Legal requirements
- Data destruction

Destroying encryption keys should be treated as a deliberate security operation.

---

## 58. Certificate Lifecycle Management

Certificates have a lifecycle:

**Request → Validation → Issuance → Deployment → Monitoring → Renewal/Replacement → Revocation/Expiration**

Poor certificate management can cause:

- Service outages
- Authentication failures
- TLS errors
- Expired certificates
- Loss of trust

Organizations should monitor certificate expiration and automate renewal where appropriate.

---

## 59. Private Key Protection

The private key is often the most sensitive component of a public-key system.

Examples:

- TLS server private key
- CA private key
- Code-signing private key
- User authentication private key

Private keys should be:

- Access-controlled
- Encrypted/protected at rest
- Restricted to authorized processes
- Rotated or replaced according to lifecycle policy
- Revoked when compromise is suspected

A certificate can be perfectly valid while the security of the corresponding private key is poor.

---

## 60. Code Signing

Code signing uses digital signatures to provide evidence about the origin and integrity of software.

A developer or organization signs an artifact with a private signing key.

A recipient can verify the signature using the corresponding public key and trust infrastructure.

Code signing can help detect:

- Unauthorized modification
- Artifact substitution
- Unsigned software

However, code signing does not prove that the software is free of vulnerabilities or malicious behavior. It primarily establishes information about the signer and integrity of the signed artifact.

---

## 61. Cryptography and Secure Email

Secure email can use cryptographic mechanisms such as:

- S/MIME
- OpenPGP
- TLS for mail transport

### TLS for email transport

TLS can protect communications between mail systems or clients and mail servers while the connection is active.

### S/MIME

S/MIME uses certificates and public-key cryptography to support email signing and encryption.

### OpenPGP

OpenPGP supports encryption and digital signatures using public-key cryptography and can use a web-of-trust model.

---

## 62. Encryption Does Not Equal Authentication

A common architectural mistake is assuming that encrypted data is automatically authenticated.

For example, encryption can prevent an observer from reading data, but depending on the construction, it may not prevent an attacker from modifying ciphertext.

Secure protocols should use authenticated encryption or separate integrity/authentication mechanisms where appropriate.

---

## 63. Cryptographic Protocol vs Cryptographic Algorithm

A **cryptographic algorithm** is the mathematical mechanism used for encryption, hashing, signing, or key agreement.

A **cryptographic protocol** defines how cryptographic mechanisms are combined during communication.

For example:

- AES → symmetric encryption algorithm
- SHA-256 → hash algorithm
- RSA/ECDSA → asymmetric cryptographic mechanisms
- TLS → protocol that combines cryptographic mechanisms for secure communications
- IPsec → protocol suite for protecting IP traffic

A secure algorithm used in an insecure protocol design can still produce a vulnerable system.

---

## 64. Common Cryptographic Architecture Failures

### Failure 1 — Private key stored in source code

**Problem:** Anyone who gains repository access may obtain the key.

**Lesson:** Use secure key-management mechanisms.

### Failure 2 — Encryption without integrity protection

**Problem:** Confidentiality exists but unauthorized modification may not be detected.

**Lesson:** Use authenticated encryption or an appropriate integrity mechanism.

### Failure 3 — Expired certificates

**Problem:** Valid services can suddenly fail authentication or TLS validation.

**Lesson:** Implement certificate inventory and lifecycle monitoring.

### Failure 4 — Weak legacy algorithms

**Problem:** Old algorithms may no longer meet current security requirements.

**Lesson:** Maintain cryptographic agility and deprecation processes.

### Failure 5 — Unprotected backup encryption keys

**Problem:** Compromise of the key can expose protected backups.

**Lesson:** Protect keys independently from the data they protect.

### Failure 6 — No certificate revocation process

**Problem:** A compromised certificate may remain trusted.

**Lesson:** Implement certificate lifecycle and revocation procedures.

---

## 65. Security+ Scenario Reasoning

### Scenario 1 — Protect bulk data efficiently

An organization needs to encrypt several terabytes of stored data.

**Cryptographic direction:** Symmetric encryption.

Why? Symmetric algorithms are efficient for bulk data protection.

---

### Scenario 2 — Verify who signed a document

A recipient needs to verify that a document was signed by the holder of a particular private key and was not modified afterward.

**Cryptographic mechanism:** Digital signature.

Why? The private key signs and the corresponding public key verifies.

---

### Scenario 3 — Detect file modification

An analyst needs to determine whether a suspicious executable has changed since a known-good copy was created.

**Mechanism:** Cryptographic hash comparison.

Why? A change in the file should produce a different digest with a secure hash function.

---

### Scenario 4 — Establish certificate-based identity

An organization wants clients to determine whether a server's public key belongs to the claimed hostname.

**Architecture:** PKI and digital certificates.

Why? The certificate binds identity information to a public key through a trusted certificate authority hierarchy or another defined trust model.

---

### Scenario 5 — Protect against compromise of historical TLS sessions

An organization wants captured sessions to remain protected even if a long-term private key is compromised later.

**Requirement:** Forward secrecy.

**Architecture direction:** Appropriate ephemeral key exchange, such as ephemeral Diffie-Hellman mechanisms.

---

### Scenario 6 — Encrypt traffic between two networks

Two corporate networks communicate across the Internet and require protected IP communications.

**Technology:** IPsec VPN, commonly using ESP in tunnel mode.

Why? Tunnel mode encapsulates the original IP packet and is commonly used for network-to-network VPNs.

---

### Scenario 7 — Revoke a compromised certificate

A certificate's private key has been compromised and the certificate must no longer be trusted.

**Requirement:** Certificate revocation.

Possible mechanisms include CRL or OCSP depending on the environment.

---

### Scenario 8 — Protect encryption keys separately from data

A cloud application encrypts large amounts of data and wants to manage the data-encryption keys using a centralized key-management system.

**Architecture:** Envelope encryption using DEKs and KEKs.

---

## 66. Common Security+ Exam Traps

### Encryption vs hashing

- Encryption → reversible protection using keys
- Hashing → one-way digest used for integrity and other functions

### Symmetric vs asymmetric

- Symmetric → shared secret, efficient for bulk data
- Asymmetric → public/private key pair, useful for signatures and key establishment

### Public vs private key

- Public key → distributed
- Private key → protected

### Signing vs verification

- Private key → signs
- Public key → verifies

### Confidentiality vs integrity

- Confidentiality → prevents unauthorized reading
- Integrity → detects/prevents unauthorized modification through appropriate mechanisms

### AH vs ESP

- AH → integrity/authentication, not confidentiality
- ESP → can provide confidentiality plus integrity/authentication

### Transport vs tunnel mode

- Transport → protects payload while retaining original IP header
- Tunnel → encapsulates original packet, commonly for VPN gateways

### CRL vs OCSP

- CRL → published revocation list
- OCSP → status query

### Rotation vs revocation

- Rotation → planned key replacement
- Revocation → invalidating trust before normal expiration/lifecycle completion

### HSM vs TPM

- HSM → specialized cryptographic key-management hardware
- TPM → hardware security component integrated into a computing platform

### Certificate vs key

A certificate contains identity information and a public key plus issuer and validation information. It is not the private key itself.

---

## 67. Cryptographic Architecture Decision Framework

When solving a Security+ cryptography scenario, use this sequence:

### Step 1 — Identify the security objective

Is the requirement:

- Confidentiality?
- Integrity?
- Authentication?
- Non-repudiation?
- Key establishment?

### Step 2 — Identify the data state

Is the data:

- At rest?
- In transit?
- In use?

### Step 3 — Identify the cryptographic function

Choose among:

- Encryption
- Hashing
- Digital signature
- Key agreement
- Certificate-based authentication

### Step 4 — Select the cryptographic architecture

Determine whether the environment needs:

- Symmetric cryptography
- Asymmetric cryptography
- Hybrid cryptography
- PKI
- HSM
- TPM
- Secure key-management service

### Step 5 — Evaluate key lifecycle

Ask:

- How are keys generated?
- Where are they stored?
- Who can use them?
- How are they rotated?
- How are they revoked?
- How are they recovered?
- How are they destroyed?

### Step 6 — Validate operational requirements

Consider:

- Performance
- Availability
- Certificate expiration
- Backup and recovery
- Cryptographic agility
- Compliance
- Legacy compatibility

---

## 68. Practical PKI Example

Consider an employee accessing an internal application over TLS.

The simplified process is:

1. The server has a private/public key pair.
2. The server has a certificate containing its public key and identity information.
3. The certificate is signed by a trusted CA.
4. The employee's system validates the certificate chain.
5. The client confirms that the certificate is valid for the requested hostname.
6. TLS performs authenticated key establishment.
7. The session uses efficient symmetric cryptography for application traffic.
8. The private key remains protected on the server.

This demonstrates how multiple cryptographic mechanisms work together rather than operating as isolated technologies.

---

## 69. Cryptography and Zero Trust

Cryptography can support Zero Trust architectures by strengthening identity and communication security.

Examples include:

- Certificate-based device identity
- mTLS between services
- TLS for application communication
- Strong key management
- Signed software and configuration
- Encrypted sensitive data

However, cryptography does not itself implement Zero Trust. Zero Trust also requires identity, authorization, policy enforcement, monitoring, and continuous evaluation.

---

## 70. Key Takeaways

1. **Cryptographic architecture combines algorithms, keys, certificates, protocols, trust, and lifecycle management.**
2. **Encryption primarily provides confidentiality.**
3. **Hashing provides fixed-length digests and supports integrity verification and other security functions.**
4. **Hashing is not encryption and is not intended to be reversed.**
5. **Symmetric cryptography uses shared secret key material and is efficient for bulk encryption.**
6. **Asymmetric cryptography uses public/private key pairs and supports signatures, authentication, and key establishment.**
7. **The private key must remain protected; the public key can be distributed.**
8. **Digital signatures use the private key for signing and the corresponding public key for verification.**
9. **Authenticated encryption can provide both confidentiality and integrity/authentication.**
10. **AES is a widely used modern symmetric encryption algorithm.**
11. **Modern password storage should use dedicated password-hashing mechanisms with unique salts rather than storing plaintext passwords.**
12. **Diffie-Hellman provides key agreement but requires authentication mechanisms to prevent man-in-the-middle attacks.**
13. **Forward secrecy helps protect historical sessions against later compromise of long-term keys.**
14. **PKI establishes certificate-based trust between identities and public keys.**
15. **A certificate is not the same thing as a private key.**
16. **Certificate validation includes trust, identity, validity, usage, and revocation considerations.**
17. **CRLs provide published revocation information; OCSP provides certificate-status queries.**
18. **Key management is as important as the cryptographic algorithm itself.**
19. **HSMs provide specialized hardware protection for high-value cryptographic operations and keys.**
20. **TPMs provide hardware-backed security capabilities on computing platforms.**
21. **Key rotation is planned replacement; revocation withdraws trust or authorization.**
22. **TLS commonly uses asymmetric cryptography during establishment and symmetric cryptography for efficient session data protection.**
23. **IPsec uses mechanisms such as ESP, AH, and IKE; ESP is commonly used for confidentiality in VPNs.**
24. **IPsec transport mode protects packet payloads; tunnel mode encapsulates the original IP packet and is commonly used for VPNs.**
25. **Cryptographic agility makes future algorithm, certificate, and key migration easier.**
26. **Encryption does not automatically guarantee integrity.**
27. **Strong cryptography can still fail if keys, certificates, trust relationships, or implementations are poorly managed.**
28. **Cryptographic architecture must account for data at rest, in transit, and in use.**
29. **Envelope encryption separates data-encryption keys from higher-level key-encryption keys.**
30. **Secure application architecture should use established cryptographic libraries and protocols rather than custom cryptography.**
31. **Code signing verifies artifact integrity and signer information but does not prove that software is vulnerability-free.**
32. **Cryptographic security is a lifecycle discipline: generate, protect, use, rotate, revoke, recover when required, and securely destroy keys.**
