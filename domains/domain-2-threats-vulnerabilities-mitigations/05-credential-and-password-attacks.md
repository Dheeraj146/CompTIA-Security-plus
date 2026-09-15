# Credential and Password Attacks

## 1. Overview

Credential attacks attempt to obtain, guess, reuse, or abuse authentication information. Passwords are frequently targeted because a compromised credential can provide legitimate-looking access and may bypass controls designed only to detect malicious software.

## 2. Major Attack Types

### Brute Force
The attacker systematically tries possible passwords until a valid password is found. Strong, long, unique passwords and rate limiting reduce effectiveness.

### Dictionary Attack
The attacker tries words and commonly used password patterns from a prepared list. It is more efficient than trying every possible combination when users select predictable passwords.

### Password Spraying
A small number of commonly used passwords are tested against many accounts. This avoids repeatedly failing against one account and may evade account-lockout thresholds.

### Credential Stuffing
Previously stolen username/password pairs are tested against other services. It succeeds because users reuse passwords across systems.

### Offline Password Cracking
A stolen password database or password hash is attacked without repeatedly communicating with the authentication service. This makes online lockout controls ineffective against the cracking process itself.

### Rainbow Tables
Precomputed data can be used to reverse certain unsalted password hashes more efficiently. Unique salts substantially reduce the usefulness of precomputation because identical passwords no longer produce identical stored hashes.

### Default Credentials
Devices, applications, and appliances may be deployed with vendor-supplied usernames and passwords. Leaving these unchanged creates an easily avoidable weakness.

### Pass-the-Hash
An attacker uses a captured password hash as an authentication artifact rather than first recovering the plaintext password. This is particularly relevant in Windows environments.

### Pass-the-Ticket
An attacker abuses a captured Kerberos ticket to authenticate as another identity without necessarily knowing the account password.

### Kerberoasting
An attacker with appropriate domain access requests Kerberos service tickets and attempts to crack material associated with service accounts offline. Strong service-account passwords and managed service identities reduce risk.

### AS-REP Roasting
Accounts configured so Kerberos preauthentication is not required can expose material that an attacker may attempt to crack offline.

### MFA Fatigue
An attacker repeatedly sends authentication prompts hoping that the victim eventually approves one out of confusion, annoyance, or social pressure. Number matching, phishing-resistant MFA, and user training help mitigate this risk.

## 3. Password Storage and Hashing

Passwords should not be stored as plaintext. Password-based authentication systems should use appropriate password-hashing mechanisms with unique salts and suitable work factors. Encryption and hashing are different: encryption is designed to be reversible with a key, while a cryptographic hash is designed as a one-way transformation.

## 4. Defensive Controls

Use long unique passwords, password managers, MFA, phishing-resistant authentication, account lockout or throttling where appropriate, breached-password detection, privileged-account controls, unique service-account credentials, secure password hashing, monitoring for authentication anomalies, and rapid credential revocation after compromise.

## 5. Exam Comparisons

- **Brute force:** tries many combinations.
- **Dictionary:** tries likely words/patterns.
- **Password spraying:** one/few passwords against many accounts.
- **Credential stuffing:** reuses credentials stolen elsewhere.
- **Pass-the-hash:** abuses a password hash.
- **Pass-the-ticket:** abuses a Kerberos ticket.
- **MFA fatigue:** manipulates the user into approving authentication.

## 6. Key Takeaways

Credential attacks can look like legitimate authentication. Detection therefore requires context such as impossible travel, unusual devices, abnormal login times, repeated failures, unfamiliar locations, and unexpected privilege use.
