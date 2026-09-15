# 1. Security Concepts and Principles

## 1.1 What Is Information Security?

Information security is the practice of protecting information and the systems that create, process, store, transmit, and dispose of that information. The objective is not simply to prevent hacking. A mature security program protects information against unauthorized disclosure, unauthorized modification, destruction, interruption, and misuse while allowing legitimate users and business processes to continue operating.

Security therefore has two dimensions: protection and enablement. A control that makes a system completely inaccessible may technically reduce some threats, but it can also make the system unusable. Security professionals must balance risk reduction with availability, usability, cost, and business requirements.

## 1.2 The CIA Triad

The CIA triad is the fundamental model used to describe three primary security objectives: confidentiality, integrity, and availability.

### Confidentiality

Confidentiality means information is accessible only to authorized subjects and systems. The goal is to prevent unauthorized disclosure.

Examples include:

- Encrypting sensitive files at rest.
- Using TLS to protect data in transit.
- Restricting payroll records to authorized personnel.
- Applying least privilege to administrative interfaces.
- Preventing users from reading another department's confidential data.

A confidentiality failure is commonly called a data disclosure or data breach. Stealing a password database, viewing another user's medical record without authorization, or intercepting unencrypted traffic can all violate confidentiality.

### Integrity

Integrity means information remains accurate, complete, trustworthy, and protected from unauthorized alteration. Integrity applies to both data and systems.

Examples include:

- Hashing a downloaded file and comparing the result with a trusted value.
- Using digital signatures to detect unauthorized modification.
- Restricting who can modify a database.
- Maintaining file permissions.
- Using checksums to detect accidental or malicious changes.

If an attacker changes a bank account number in a transaction record, confidentiality may not be affected, but integrity has been compromised.

### Availability

Availability means authorized users can access systems and information when required. Availability is particularly important for services such as authentication, DNS, healthcare systems, payment systems, and emergency communications.

Availability controls include redundancy, clustering, backups, load balancing, failover, disaster recovery, capacity planning, and protection against denial-of-service attacks.

### CIA trade-offs

The three objectives can conflict. For example, very strong encryption and access controls may increase confidentiality but introduce operational overhead. Aggressive security restrictions may reduce exposure but make legitimate access difficult. Security architecture therefore seeks an appropriate balance based on risk and business requirements.

## 1.3 Authentication, Authorization, and Accounting

These three concepts describe different stages of access control and are commonly abbreviated as AAA.

### Authentication

Authentication answers: **Who are you?**

A system authenticates a subject by validating one or more credentials or authentication factors. Common factors include:

- Something you know — password or PIN.
- Something you have — hardware token or smart card.
- Something you are — fingerprint or facial characteristic.
- Somewhere you are — location or network context.
- Something you do — behavioral characteristics such as typing patterns.

Multi-factor authentication (MFA) requires authentication factors from different categories. Entering a password and then approving a login through a separate authenticator application is an example of MFA.

### Authorization

Authorization answers: **What are you allowed to do?**

After authentication establishes identity, authorization determines the resources and operations available to that identity. A user might successfully authenticate but still be denied access to a payroll database because the user's role does not provide the required permissions.

### Accounting / Auditing

Accounting records what a subject did. Security systems can record logins, file access, administrative actions, configuration changes, and other activities. These records support accountability, incident investigation, compliance, and forensic analysis.

A useful sequence is:

`Authentication → Authorization → Accounting`

Identity is established first, permissions are evaluated second, and activity is recorded for accountability.

## 1.4 Non-Repudiation

Non-repudiation provides evidence that helps establish that a particular party performed an action or approved information, making it difficult for that party to credibly deny the action later.

Digital signatures are a common mechanism for non-repudiation because they can bind a signer to a specific message or document when the private signing key is properly controlled. Audit logs can also provide evidence of actions, although logs alone do not automatically provide strong non-repudiation because their trustworthiness depends on how they are protected and managed.

## 1.5 Least Privilege

Least privilege means granting a subject only the permissions necessary to perform its authorized task and no more.

For example, an analyst who only needs to investigate alerts should not automatically receive domain administrator privileges. A web application service account that only needs to read a specific database should not have permission to modify every database on the server.

Least privilege reduces the potential impact of compromised accounts, malicious insiders, accidental changes, and exploited applications.

## 1.6 Separation of Duties

Separation of duties divides sensitive responsibilities among multiple people or roles so that one person cannot independently complete an entire high-risk process.

For example, one employee may request a payment while another approves it. In an infrastructure environment, one administrator might create a privileged account while another reviews or approves the change.

The purpose is to reduce fraud, abuse, and single-person control over critical operations.

## 1.7 Job Rotation and Mandatory Vacations

Job rotation periodically moves personnel between responsibilities. This can reduce dependence on one individual and can expose fraudulent processes that depend on a person continuously controlling a task.

Mandatory vacations require personnel in sensitive positions to be absent for a defined period. During the absence, another person performs the responsibilities. This can reveal unauthorized procedures, hidden transactions, or activities that were being concealed by the employee.

These are administrative security controls rather than technical security mechanisms.

## 1.8 Defense in Depth

Defense in depth uses multiple independent or partially independent security layers instead of relying on one control.

A layered architecture might include:

`User awareness → MFA → Endpoint protection → Network segmentation → Firewall → IDS/IPS → SIEM monitoring → Incident response`

If one control fails, other controls can still reduce the likelihood or impact of compromise. Defense in depth is particularly valuable because real environments contain configuration errors, software vulnerabilities, human mistakes, and previously unknown attack techniques.

## 1.9 Security Through Obscurity

Security through obscurity relies primarily on hiding implementation details rather than using strong security controls. Examples include assuming an unusual port number makes a service secure or assuming attackers cannot discover a hidden administrative URL.

Changing a default port can reduce automated noise, but it should not be treated as a primary security control. A robust design assumes that an attacker may discover architecture details and still cannot bypass properly implemented authentication, authorization, encryption, and monitoring.

## 1.10 Risk-Based Security

Security decisions should be based on risk rather than on the assumption that every asset requires identical protection.

A simplified risk relationship is:

`Risk ≈ Likelihood × Impact`

Likelihood represents how probable a harmful event is, while impact represents the consequences if it occurs. Risk management uses this relationship to prioritize limited security resources.

For example, an internet-facing authentication server containing sensitive data generally deserves stronger protection and monitoring than a low-value isolated test system.

## 1.11 Security Objectives in Practice

Security professionals should translate abstract principles into concrete controls. If confidentiality is the primary concern, access control and encryption may receive greater emphasis. If availability is critical, redundancy and recovery capabilities become central. If integrity is critical, access restrictions, hashing, digital signatures, change control, and monitoring become particularly important.

A good security architecture does not select technologies first and ask what problem they solve later. It starts with assets, threats, business requirements, and security objectives, then selects controls appropriate to the risk.

## Security+ Exam Focus

- Know the CIA triad and recognize real-world examples of confidentiality, integrity, and availability failures.
- Distinguish authentication from authorization and accounting.
- Understand least privilege and separation of duties.
- Understand why defense in depth uses multiple security layers.
- Recognize non-repudiation as evidence supporting accountability for an action.
- Understand that changing a port or hiding information is not a substitute for strong security controls.

## Key Takeaways

1. Confidentiality prevents unauthorized disclosure.
2. Integrity protects information from unauthorized or improper modification.
3. Availability ensures authorized access when needed.
4. Authentication establishes identity; authorization determines permissions; accounting records activity.
5. Least privilege limits the permissions available to a subject.
6. Separation of duties reduces the risk of abuse by distributing sensitive responsibilities.
7. Defense in depth reduces reliance on any single security control.
8. Security decisions should be driven by risk, business requirements, and security objectives.
