# Cryptographic Architecture

## Purpose

Cryptography supports confidentiality, integrity, authentication, and non-repudiation. Architecture decisions should select algorithms, protocols, keys, and trust mechanisms appropriate to the data and environment.

## Symmetric Cryptography

The same secret key is used for encryption and decryption. It is efficient for protecting large amounts of data but requires secure key distribution.

## Asymmetric Cryptography

A key pair contains a public key and a private key. Asymmetric cryptography supports secure key establishment, digital signatures, and identity mechanisms but is generally more computationally expensive than symmetric encryption.

## Hashing

Cryptographic hashes provide fixed-length representations used for integrity verification, password storage designs, and other security functions. Hashing is not encryption and is not intended to be reversible.

## Digital Signatures

A digital signature provides integrity and authentication and can support non-repudiation. The private key signs and the corresponding public key verifies.

## PKI

Public Key Infrastructure manages certificates, certificate authorities, trust relationships, revocation, and lifecycle processes that support public-key authentication.

## Key Management

Security depends heavily on key protection. Keys should be generated securely, stored with appropriate protection, rotated according to policy, revoked when compromised, and destroyed when no longer required.

## Exam Focus

Symmetric encryption is efficient for bulk data; asymmetric cryptography supports key exchange and signatures; hashing supports integrity and password protection; PKI establishes certificate-based trust.
