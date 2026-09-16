# 05 — Credential and Password Attacks

## 1. Introduction

**Credential attacks** are attacks in which an adversary attempts to obtain, guess, steal, reuse, manipulate, or abuse authentication information in order to gain access to an account or system.

A credential can include more than a password. Depending on the authentication system, credentials may involve:

- Username and password
- Password hash
- Authentication token
- Kerberos ticket
- API key
- Certificate
- Session cookie
- MFA approval
- Other authentication artifacts

Credentials are valuable because compromised authentication can provide an attacker with access that appears legitimate. A malicious login may therefore be harder to distinguish from normal user activity than an obviously malicious executable.

A useful attack chain is:

**Credential discovery → Credential acquisition → Authentication attempt → Account access → Privilege/access expansion → Persistence or objective**

Security+ questions frequently test whether you can distinguish **how the attacker obtained or abused the credential**.

---

# 2. Password Attack Fundamentals

Passwords are commonly targeted because users often create predictable passwords, reuse passwords between services, or choose passwords that are vulnerable to guessing.

Password attacks can broadly be divided into:

### Online attacks

The attacker repeatedly interacts with the authentication service.

Examples:

- Brute force against a login page
- Password spraying
- Credential stuffing

Online attacks can often be detected through authentication logs, rate limits, account lockouts, and abnormal login patterns.

### Offline attacks

The attacker obtains password-related data such as hashes and attempts to recover passwords without repeatedly contacting the original authentication service.

Offline attacks are particularly important because normal online protections such as login throttling may not protect the password-cracking process itself.

---

# 3. Brute-Force Attack

A **brute-force attack** systematically attempts many possible passwords or combinations until a valid credential is discovered.

The attacker does not necessarily rely on knowing what type of password the user chose. The method attempts combinations according to a defined search space.

### Simplified example

If a password is known to contain four numeric characters, an attacker can systematically test possible combinations.

### Why password length matters

A larger password search space increases the number of possibilities an attacker must test.

For this reason, long, unique passwords or passphrases are generally more resistant to brute-force guessing than short passwords.

### Online brute force

An attacker repeatedly submits login attempts to the authentication service.

Defensive controls can include:

- Rate limiting
- Account lockout where appropriate
- Authentication monitoring
- MFA
- Risk-based authentication

### Offline brute force

If an attacker has obtained password hashes, the attacker can perform guesses against the hashes without repeatedly submitting login attempts to the original system.

### Exam clue

If the scenario emphasizes **systematically trying many possible combinations**, think **brute force**.

---

# 4. Dictionary Attack

A **dictionary attack** uses a prepared list of likely passwords rather than trying every possible combination.

The list may contain:

- Common words
- Common passwords
- Previously observed passwords
- Names
- Dates
- Common substitutions
- Organization-specific terms

### Why it works

Many users choose passwords based on words or patterns that are easier to remember.

For example, users may choose passwords based on names, sports teams, seasons, locations, or common phrases.

### Brute force vs dictionary

**Brute force:** systematically searches combinations.

**Dictionary:** prioritizes likely passwords from a prepared list.

A dictionary attack can be much more efficient when the victim's password is predictable.

---

# 5. Password Spraying

**Password spraying** tests a small number of commonly used passwords against many different accounts.

Instead of doing this:

**One account → many passwords**

The attacker does this:

**Many accounts → one or a few passwords**

### Why attackers use spraying

Many organizations implement account-lockout policies after repeated failed attempts against an account.

Password spraying attempts to reduce the chance of triggering those controls against any single account.

### Example

An attacker obtains a list of 500 usernames and tests one commonly used password against each account before moving to another password.

### Detection

Look for:

- Same password attempt across many accounts
- Authentication failures distributed across users
- Unusual authentication sources
- Repeated low-volume failures

### Exam clue

**One/few passwords against many accounts → password spraying.**

---

# 6. Credential Stuffing

**Credential stuffing** uses previously stolen username/password combinations against other services.

The attack depends on **password reuse**.

### Example

Suppose credentials from an unrelated website are leaked. An attacker tests the same username and password combination against corporate email, cloud services, or other accounts.

If the user reused the password, the attacker may gain access.

### Credential stuffing vs password spraying

| Attack | Pattern |
|---|---|
| Password spraying | One/few common passwords against many accounts |
| Credential stuffing | Previously stolen username/password pairs reused against another service |

### Defensive controls

- Unique passwords
- Password managers
- MFA
- Breached-password detection
- Monitoring for unusual authentication
- Risk-based access controls

---

# 7. Default Credentials

**Default credentials** are vendor-provided usernames and passwords supplied with devices, applications, appliances, or other systems.

Examples can include credentials used for:

- Network devices
- Printers
- Cameras
- IoT devices
- Security appliances
- Applications

If the default password remains unchanged after deployment, an attacker who knows the vendor defaults may gain immediate access.

### Defensive control

Change default credentials during deployment and disable or remove unnecessary default accounts where possible.

This is a basic but important security-hardening practice.

---

# 8. Offline Password Cracking

In an **offline password attack**, the attacker obtains password-related data, such as password hashes, and performs guessing without repeatedly interacting with the authentication service.

### Why this is dangerous

Online controls such as:

- Account lockout
- Login throttling
- CAPTCHA
- IP-based rate limiting

may not stop the offline cracking process because the attacker is no longer repeatedly authenticating against the original service.

### Defensive priorities

The security of the stored password representation becomes critical.

Organizations should use appropriate password-hashing algorithms, unique salts, and suitable work factors rather than plaintext or weak storage methods.

---

# 9. Password Hashing

A **cryptographic hash** transforms input data into a fixed-length output according to a hashing algorithm.

Password storage should use password-specific hashing mechanisms designed to make large-scale guessing expensive.

The goal is not simply to produce a hash. The password-storage mechanism should also make password guessing computationally costly.

### Hashing vs encryption

**Hashing:** designed as a one-way transformation and normally does not provide a decryption operation.

**Encryption:** designed to be reversible when the appropriate key is available.

A system should therefore not treat encrypted passwords and hashed passwords as equivalent security mechanisms.

---

# 10. Salting

A **salt** is additional random data combined with a password before password hashing.

A properly implemented password-storage system uses a **unique salt for each password**.

### Why salts matter

Without unique salts, identical passwords can produce identical hashes when the same hashing process is used. This can make precomputed attacks more useful and can reveal that different users have the same password.

With unique salts, the same password produces different stored password hashes.

### Important distinction

A salt is not a secret key. It is generally stored alongside the password hash.

Its purpose is to make precomputation and large-scale comparison of password hashes less effective.

---

# 11. Rainbow Tables

A **rainbow table** is a form of precomputed data designed to help recover passwords from certain password hashes more efficiently than calculating every candidate from scratch for every target.

Rainbow tables are primarily associated with **unsalted or poorly protected password hashes**.

Unique salts substantially reduce the usefulness of precomputed tables because the attacker would need to account for each unique salt.

### Exam clue

If the question describes **precomputed hashes/tables used to recover passwords**, think **rainbow table**.

---

# 12. Pass-the-Hash

**Pass-the-hash (PtH)** is an attack in which an attacker uses a captured password hash or related authentication material to authenticate, rather than first recovering the plaintext password.

This is particularly relevant in Windows environments where certain authentication mechanisms can accept password-derived material.

### Why it matters

The attacker may not need to know the actual password.

Therefore, simply changing a password is not always enough to understand or remediate the broader compromise. Incident responders must consider where the authentication material was obtained and whether other systems or accounts were affected.

### Defensive considerations

- Credential protection
- Least privilege
- Restricting administrative access
- Network segmentation
- Monitoring lateral movement
- Protecting privileged accounts
- Reducing unnecessary credential exposure

### Exam clue

**Attacker authenticates using a stolen password hash without recovering the plaintext password → pass-the-hash.**

---

# 13. Pass-the-Ticket

**Pass-the-ticket (PtT)** involves abusing a captured Kerberos authentication ticket to authenticate as another identity.

The attacker is using an existing authentication artifact rather than necessarily knowing the account password.

### Why it matters

Kerberos tickets can provide access within a domain environment. If a valuable ticket is compromised, an attacker may be able to access resources associated with that identity.

### Pass-the-hash vs pass-the-ticket

- **Pass-the-hash:** abuses password-hash-derived authentication material.
- **Pass-the-ticket:** abuses a Kerberos ticket.

These are easy to confuse in exam questions, so identify the authentication artifact described in the scenario.

---

# 14. Kerberoasting

**Kerberoasting** is an attack against Kerberos service accounts in which an attacker with appropriate domain access requests service tickets for accounts associated with services and attempts to crack the encrypted material offline to recover the service account password.

### Why service accounts are important

Service accounts can have:

- Long-lived credentials
- Elevated permissions
- Access to important applications
- Passwords that are changed infrequently

If a service account has a weak password, offline cracking may eventually recover it.

### Defensive controls

- Strong service-account passwords
- Managed service accounts where appropriate
- Least privilege
- Monitoring unusual service-ticket requests
- Reducing unnecessary service-account privileges

### Exam clue

If the scenario involves **Kerberos service tickets and service accounts**, consider **Kerberoasting**.

---

# 15. AS-REP Roasting

**AS-REP roasting** targets accounts for which Kerberos preauthentication is not required.

When preauthentication is disabled for an account, an attacker with the appropriate access may be able to request authentication information that can be attacked offline.

### Key distinction

**Kerberoasting → service accounts/service tickets**

**AS-REP roasting → accounts without required Kerberos preauthentication**

### Defensive control

Require Kerberos preauthentication where operationally appropriate and maintain strong account credentials.

---

# 16. MFA Fatigue

**MFA fatigue** is a social engineering technique in which an attacker repeatedly sends authentication requests to a victim hoping that the victim eventually approves one because of confusion, annoyance, habit, or pressure.

The attacker may already possess the victim's username and password. The remaining obstacle is MFA approval.

### Example

A user receives repeated authentication prompts late at night. After receiving many prompts, the user accidentally approves one simply to make the notifications stop.

### Defensive controls

- Number matching
- Phishing-resistant MFA
- User awareness
- Authentication monitoring
- Conditional access
- Alerting on repeated authentication prompts

MFA improves security, but the design and implementation of the MFA method matter.

---

# 17. Credential Attacks Against Cloud Services

Cloud applications introduce additional authentication attack surfaces.

Attackers may target:

- Cloud email
- SaaS applications
- VPN accounts
- Identity providers
- Administrator accounts
- API credentials
- OAuth tokens
- Session cookies

A compromised cloud identity can provide broad access without requiring malware on the endpoint.

### Defensive controls

- MFA
- Conditional access
- Risk-based authentication
- Strong password policies
- Privileged access management
- Token/session monitoring
- Identity logging
- Rapid credential revocation

---

# 18. Credential Theft vs Credential Attack

These terms are related but not identical.

**Credential theft** means obtaining authentication information without authorization.

Examples include:

- Stealing passwords through phishing
- Capturing credentials with malware
- Obtaining credentials from a breach
- Stealing authentication tokens

**Credential attack** is broader and includes guessing, reuse, cracking, or abusing authentication material.

For example, credential stuffing uses credentials that may have already been stolen elsewhere.

---

# 19. Credential Attack Detection

Credential attacks can be difficult to identify because successful authentication may appear legitimate.

Security teams should analyze authentication context.

### Useful indicators

- Repeated failed logins
- Authentication from unusual locations
- Impossible-travel patterns
- New or unfamiliar devices
- Unusual login times
- Multiple accounts targeted from one source
- Successful login after many failures
- Sudden privilege use
- Authentication from unusual infrastructure
- Unexpected password-reset activity
- Repeated MFA prompts

### Important principle

An unusual login is an **indicator**, not automatically proof of compromise.

Analysts should correlate authentication logs with endpoint, network, identity, and user context.

---

# 20. Credential Attack Mitigation

A layered strategy should address both the credential and the authentication system.

## 20.1 Strong and Unique Passwords

Long, unique passwords make guessing and credential reuse attacks more difficult.

Password managers can help users maintain unique credentials across services.

## 20.2 MFA

MFA adds another authentication factor so a password alone is not sufficient.

Where possible, organizations should prefer authentication methods resistant to phishing and MFA-prompt abuse.

## 20.3 Rate Limiting and Throttling

Authentication systems can limit the number or speed of repeated attempts.

This is particularly useful against online guessing attacks.

However, throttling alone does not stop offline password cracking.

## 20.4 Account Lockout

Account lockout can reduce repeated guessing but must be designed carefully because aggressive lockout can also be abused for denial of service by intentionally causing accounts to lock.

## 20.5 Password Breach Detection

Organizations can prevent known compromised passwords from being used and can monitor for evidence that credentials have appeared in known breach datasets, subject to appropriate security and privacy practices.

## 20.6 Privileged Access Management

Administrative credentials should receive stronger protection because compromise of a privileged account can significantly increase attacker capability.

## 20.7 Least Privilege

Users and service accounts should receive only the permissions required for their roles.

If a credential is compromised, least privilege can reduce the attacker's reachable resources.

## 20.8 Credential Revocation

When credentials are suspected of compromise, organizations should rapidly invalidate or rotate them and investigate where the credentials were exposed.

---

# 21. Attack Comparison Table

| Attack | What the attacker does | Defining clue |
|---|---|---|
| Brute force | Tries many possible combinations | Systematic guessing |
| Dictionary attack | Tries likely words/passwords from a list | Prepared word list |
| Password spraying | Tries one/few passwords against many accounts | Many accounts, few passwords |
| Credential stuffing | Reuses stolen username/password pairs | Credentials stolen elsewhere |
| Offline cracking | Cracks stolen password hashes without online authentication | Password data obtained first |
| Rainbow table | Uses precomputed data against certain hashes | Precomputed hash data |
| Default credentials | Uses vendor-provided credentials left unchanged | Factory/default account/password |
| Pass-the-hash | Uses captured password-hash material | Hash used instead of plaintext password |
| Pass-the-ticket | Uses a captured Kerberos ticket | Kerberos ticket |
| Kerberoasting | Targets service-account Kerberos ticket material | Service accounts/service tickets |
| AS-REP roasting | Targets accounts without required Kerberos preauthentication | AS-REP/preauthentication condition |
| MFA fatigue | Repeatedly prompts victim to approve authentication | Repeated MFA requests |

---

# 22. Important Security+ Distinctions

### Brute Force vs Dictionary

**Brute force:** systematically explores possible combinations.

**Dictionary:** prioritizes likely passwords from a prepared list.

### Password Spraying vs Credential Stuffing

**Password spraying:** attacker chooses a small number of passwords and tests them against many accounts.

**Credential stuffing:** attacker uses previously stolen username/password pairs against another service.

### Pass-the-Hash vs Pass-the-Ticket

**Pass-the-hash:** password-hash-derived authentication material.

**Pass-the-ticket:** Kerberos ticket.

### Kerberoasting vs AS-REP Roasting

**Kerberoasting:** targets service accounts through Kerberos service-ticket material.

**AS-REP roasting:** targets accounts where Kerberos preauthentication is not required.

### Online vs Offline Cracking

**Online:** authentication service is actively contacted.

**Offline:** attacker works against obtained password-related data without repeatedly contacting the authentication service.

---

# 23. Detailed Security+ Scenario

### Scenario

A security analyst reviews authentication logs and finds that an external IP attempted the same password against 80 employee accounts. Most attempts failed, and no individual account received enough attempts to trigger the organization's normal lockout threshold.

### Analysis

The important clue is:

**One password → many accounts**

This is characteristic of **password spraying**.

The attacker is not repeatedly attacking one account with hundreds of passwords. The pattern is distributed across many accounts.

### Appropriate defensive actions

The organization could investigate:

- The source infrastructure
- Authentication logs
- Targeted accounts
- Successful authentications
- MFA events
- Endpoint activity associated with successful accounts

It may also consider controls such as authentication throttling, stronger authentication, MFA, conditional access, and detection rules.

---

# 24. Detailed Credential Stuffing Scenario

### Scenario

A company discovers that an employee's username and password were exposed in a breach of an unrelated website. Shortly afterward, the same credentials are used to attempt access to the employee's corporate account.

### Analysis

The defining clue is **reuse of previously compromised credentials from another service**.

This is credential stuffing.

### Root cause

The underlying weakness is password reuse.

### Mitigation

- Unique passwords
- Password manager
- MFA
- Breached-password screening
- Monitoring for suspicious authentication

---

# 25. Detailed Kerberos Scenario

### Scenario

An attacker with domain access requests service tickets associated with several service accounts. The attacker collects the ticket material and attempts to crack it offline.

### Analysis

The scenario points toward **Kerberoasting**.

The key clues are:

- Kerberos
- Service accounts
- Service tickets
- Offline password cracking

Do not confuse this with pass-the-ticket. In pass-the-ticket, the attacker abuses an existing captured Kerberos ticket for authentication. In Kerberoasting, the attacker targets service-account ticket material for offline password recovery.

---

# 26. Common Mistakes

### Mistake 1: Thinking every password attack is brute force

Different attack patterns have different names. Identify whether the attacker is guessing combinations, using a dictionary, spraying passwords, or reusing stolen credentials.

### Mistake 2: Confusing spraying with credential stuffing

Spraying uses one/few passwords across many accounts. Credential stuffing uses known username/password pairs obtained elsewhere.

### Mistake 3: Assuming MFA makes credential attacks impossible

MFA significantly changes the attack problem, but attackers may target MFA through phishing, fatigue, session theft, or other techniques.

### Mistake 4: Assuming account lockout stops offline cracking

Offline cracking does not require repeated authentication attempts against the original service.

### Mistake 5: Confusing a password hash with the password

A password hash is not simply an encrypted version of the password. Pass-the-hash demonstrates why stolen authentication material can be dangerous even when plaintext recovery has not occurred.

### Mistake 6: Confusing pass-the-hash and pass-the-ticket

Identify the artifact:

- Hash → pass-the-hash
- Kerberos ticket → pass-the-ticket

### Mistake 7: Treating every unusual login as proof of compromise

Authentication anomalies require investigation and correlation with other evidence.

---

# 27. Security+ Scenario Reasoning Framework

When you see a credential-attack question, work through the following process.

### Step 1: Identify the authentication artifact

Is the attacker using:

- Password?
- Password hash?
- Kerberos ticket?
- Username/password pair from another breach?
- MFA approval?

### Step 2: Determine the attack pattern

Ask:

- Many passwords against one account?
- One/few passwords against many accounts?
- Previously stolen credentials against another service?
- Offline cracking of stored hashes?

### Step 3: Identify the protocol or environment

If the scenario mentions Kerberos and service accounts, consider Kerberoasting.

If it mentions missing Kerberos preauthentication, consider AS-REP roasting.

### Step 4: Identify the control being tested

Possible controls include:

- MFA
- Password policy
- Rate limiting
- Account lockout
- Password managers
- Least privilege
- Privileged access management
- Credential monitoring
- Strong password hashing

### Step 5: Choose the control that addresses the actual weakness

For example:

**Password reuse → unique passwords and MFA**

**Online guessing → throttling/rate limiting**

**Stolen password hash → credential protection and privileged-access controls**

**MFA fatigue → stronger MFA methods and number matching**

---

# 28. Key Takeaways

1. Credential attacks target authentication information or authentication mechanisms.
2. Brute force systematically attempts possible combinations.
3. Dictionary attacks prioritize likely passwords from prepared lists.
4. Password spraying tests one or a few passwords against many accounts.
5. Credential stuffing reuses stolen credentials from another service.
6. Offline cracking operates against obtained password-related data rather than repeatedly contacting the authentication service.
7. Unique salts make precomputed rainbow-table attacks substantially less useful.
8. Default credentials should be changed during deployment.
9. Pass-the-hash abuses captured password-hash-derived authentication material.
10. Pass-the-ticket abuses captured Kerberos tickets.
11. Kerberoasting targets service-account ticket material for offline cracking.
12. AS-REP roasting targets accounts where Kerberos preauthentication is not required.
13. MFA fatigue attempts to manipulate users into approving authentication requests.
14. Long, unique passwords and MFA are important defenses, but no single control eliminates credential attacks.
15. Credential attacks can appear as legitimate authentication, so behavioral and contextual monitoring is essential.
16. Security+ questions are often solved by identifying the **credential artifact, attack pattern, protocol, and intended control**.
