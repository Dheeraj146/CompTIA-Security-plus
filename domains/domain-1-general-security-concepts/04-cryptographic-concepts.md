# 4. Cryptographic Concepts

Cryptography is the discipline of protecting information through mathematical techniques. Security+ expects an understanding of what common cryptographic mechanisms accomplish, how they differ, and when they are appropriate.

## 4.1 Plaintext and Ciphertext

Plaintext is information in its readable or original form. Ciphertext is the transformed output produced by an encryption process.

Encryption converts plaintext into ciphertext using an algorithm and key. Decryption uses the appropriate key to recover the plaintext.

A simplified model is:

`Plaintext + Encryption Algorithm + Key → Ciphertext`

and:

`Ciphertext + Decryption Algorithm + Key → Plaintext`

Modern cryptography depends primarily on the secrecy and management of keys rather than keeping the algorithm secret.

## 4.2 Encryption vs Encoding vs Hashing

These concepts are frequently confused.

### Encryption

Encryption is designed to provide confidentiality. Encrypted information can be decrypted when the appropriate key is available.

### Encoding

Encoding changes data into another representation for compatibility, transmission, or storage. Encoding is not a security control because the transformation is normally reversible without a secret key.

For example, Base64 is encoding, not encryption.

### Hashing

Hashing produces a fixed-length digest from input data. A cryptographic hash is designed to be computationally infeasible to reverse and is primarily used for integrity verification and related security functions.

A hash is not intended to be decrypted.

## 4.3 Symmetric Cryptography

Symmetric cryptography uses the same secret key, or closely related secret material, for encryption and decryption.

Advantages:

- Fast.
- Efficient for large amounts of data.
- Suitable for high-throughput encryption.

Challenges:

- The secret key must be securely shared or established between parties.
- Large environments can face significant key-management complexity.

Common symmetric algorithms include AES and ChaCha20.

## 4.4 Asymmetric Cryptography

Asymmetric cryptography uses a key pair consisting of a public key and a private key.

The public key can generally be distributed. The private key must remain secret and under the control of its owner.

Asymmetric cryptography supports operations such as secure key establishment and digital signatures.

It is generally more computationally expensive than symmetric cryptography, so real-world protocols often combine asymmetric and symmetric techniques.

## 4.5 Hybrid Cryptography

Modern secure protocols commonly use a hybrid approach.

A simplified TLS-style process is:

1. The parties establish or authenticate public-key-based parameters.
2. They securely establish shared session key material.
3. Symmetric cryptography protects the bulk application data.
4. Integrity and authentication mechanisms protect the session.

This combines the key-management advantages of asymmetric cryptography with the performance of symmetric encryption.

## 4.6 Hashing

A cryptographic hash function accepts input of arbitrary practical length and produces a fixed-length digest.

Security properties commonly expected from a strong cryptographic hash include:

- Preimage resistance.
- Second-preimage resistance.
- Collision resistance.
- Efficient computation.

A small change in input should produce a substantially different digest. This property helps identify modified data.

Examples of modern cryptographic hash functions include SHA-256 and SHA-3. MD5 and SHA-1 have known weaknesses and should not be selected for new security-sensitive integrity applications.

## 4.7 Password Hashing and Salting

Passwords should not normally be stored as plaintext. Instead, password-verification systems should use password-specific hashing approaches designed to make large-scale guessing expensive.

A salt is a unique random value combined with a password before password hashing. Salts prevent identical passwords from producing identical stored values and make precomputed rainbow-table attacks less effective.

Password hashing should use algorithms designed for password storage, such as Argon2, bcrypt, scrypt, or PBKDF2, with parameters appropriate for the environment.

## 4.8 Digital Signatures

A digital signature provides evidence that a message was signed by the holder of a private signing key and that the signed data has not been modified since signing, assuming the cryptographic and key-management assumptions remain valid.

A simplified process is:

1. A hash is calculated from the message.
2. The signer uses the private key with the signature algorithm to create a signature over the appropriate data.
3. The recipient uses the signer's public key to verify the signature.
4. The recipient also verifies the signed data's integrity according to the signature scheme.

Digital signatures provide integrity and authentication of the signer and can support non-repudiation. They do not, by themselves, provide confidentiality.

## 4.9 Digital Certificates

A digital certificate binds an identity or subject to a public key through a trusted certificate authority hierarchy.

A certificate commonly contains information such as:

- Subject identity.
- Public key.
- Issuer.
- Validity period.
- Serial number.
- Signature algorithm information.
- Digital signature from the issuer.
- Extensions defining permitted uses and constraints.

A certificate does not contain the subject's private key. The private key must be protected separately.

## 4.10 Public Key Infrastructure

PKI is the collection of technologies, policies, procedures, roles, and systems used to issue, manage, validate, renew, revoke, and use digital certificates and public keys.

A simplified PKI trust process is:

`Certificate Authority → Issues Certificate → Client Validates Certificate → Public Key Used for Secure Operation`

Certificate validation can involve checking the issuing chain, validity dates, subject names, key usage, and revocation status.

## 4.11 Certificate Authorities

A Certificate Authority (CA) is a trusted entity that issues and signs certificates. A root CA is typically a trust anchor. Intermediate CAs can issue certificates on behalf of a root CA, reducing the need to use the root private key directly for routine issuance.

A certificate chain allows a relying party to establish a path from the presented certificate to a trusted root.

## 4.12 Certificate Revocation

A certificate may need to be revoked before its scheduled expiration if the private key is compromised, the certificate was issued incorrectly, or the subject should no longer be trusted.

Common revocation mechanisms include:

- Certificate Revocation Lists (CRLs).
- Online Certificate Status Protocol (OCSP).

The specific behavior depends on the protocol, client, and PKI implementation.

## 4.13 Key Management

Cryptographic algorithms are only as strong as their implementation and key management practices. Key management includes generation, distribution, storage, use, rotation, backup, recovery, archival, and destruction.

A compromised private key can undermine the security provided by an otherwise strong algorithm. Therefore, private keys should be protected using appropriate access controls, hardware security mechanisms where justified, and secure lifecycle procedures.

## 4.14 Data States

Security professionals commonly classify data into three states:

### Data at Rest

Data stored on persistent media such as disks, databases, backups, or removable drives.

Common protections include full-disk encryption, database encryption, file-level encryption, and access controls.

### Data in Transit

Data moving across a network or communication channel.

Common protections include TLS, IPsec, VPN technologies, and secure application protocols.

### Data in Use

Data actively being processed by a system or application. Protecting data in use can require strong process isolation, memory protections, access controls, confidential-computing technologies, and careful application architecture.

## Security+ Exam Focus

- Symmetric cryptography uses shared secret key material and is generally fast.
- Asymmetric cryptography uses public/private key pairs and supports secure key establishment and digital signatures.
- Hashing is not encryption and does not use a decryption process.
- Encoding is not encryption.
- Digital signatures provide integrity and signer authentication; they do not provide confidentiality by themselves.
- Certificates bind identities to public keys through a PKI trust model.
- Private keys must remain protected.
- Understand data at rest, in transit, and in use.

## Key Takeaways

1. Encryption protects confidentiality.
2. Hashing supports integrity and related security functions.
3. Encoding provides representation, not confidentiality.
4. Symmetric cryptography is efficient for bulk data.
5. Asymmetric cryptography uses public/private key pairs.
6. Hybrid protocols combine both approaches.
7. Digital signatures support integrity and authentication of the signer.
8. Certificates associate identities with public keys.
9. PKI manages trust and certificate lifecycle processes.
10. Strong cryptography requires strong key management.
