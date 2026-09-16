# Identity and Access Management Operations

Identity and Access Management (IAM) operations are the day-to-day processes used to make sure the **right identity gets the right access to the right resource at the right time for the right reason**.

IAM is not simply the process of creating usernames and passwords. In a real environment, IAM connects people, devices, applications, services, credentials, groups, roles, policies, authentication mechanisms, authorization decisions, logging, reviews, and account lifecycle processes.

A useful operational model is:

**Identity → Authentication → Authorization → Access → Monitoring → Review → Modification → Revocation**

Security+ questions frequently present an operational problem such as a terminated employee retaining access, a contractor receiving excessive permissions, an administrator sharing a privileged password, or a service account having unnecessary interactive logon rights. The correct answer usually comes from understanding the IAM lifecycle and applying least privilege, separation of duties, strong authentication, and timely access review.

---

## 1. Why IAM Is a Security Operation

Every protected resource needs some mechanism for deciding **who or what is allowed to access it**. That decision can involve a human user, workstation, server, application, cloud workload, API client, or device.

Consider an employee who joins an organization. The employee may need access to email, a corporate laptop, a file share, a ticketing system, and applications belonging to their department. Later, the employee transfers to another department. Some old permissions are no longer appropriate, while new permissions are required. Eventually, the employee leaves the organization and all organizational access must be revoked.

This makes IAM a continuous operational process rather than a one-time configuration task.

Poor IAM operations can result in:

- Unauthorized access.
- Privilege escalation.
- Account takeover.
- Data exposure.
- Persistence after employee termination.
- Orphaned accounts.
- Excessive administrative privileges.
- Credential theft and reuse.
- Insider misuse.
- Service disruption caused by unauthorized changes.

A strong IAM program therefore combines **identity lifecycle management, authentication, authorization, privilege management, monitoring, and periodic review**.

---

# 2. Identity, Authentication, Authorization, and Accounting

These terms are closely related but describe different stages of access control.

## 2.1 Identification

Identification is the process by which a subject claims an identity.

For example:

```text
Username: dheeraj
Employee ID: EMP1024
Email: dheeraj@example.com
```

The identity claim itself does not prove that the person is actually Dheeraj.

---

## 2.2 Authentication

Authentication answers:

> **“Are you really the identity you claim to be?”**

Examples include:

- Password.
- PIN.
- Hardware security key.
- Smart card.
- Fingerprint.
- Facial recognition.
- Certificate.
- One-time password.

Authentication establishes confidence in an identity.

---

## 2.3 Authorization

Authorization answers:

> **“Now that we know who you are, what are you allowed to do?”**

For example, two authenticated employees may access the same application but have different permissions:

```text
Employee A → Read customer records
Employee B → Read + modify customer records
Administrator → Read + modify + manage application configuration
```

Authentication does not automatically grant authorization.

---

## 2.4 Accounting

Accounting records what a subject did after obtaining access.

Examples include:

- Login time.
- Source IP address.
- Resource accessed.
- File modified.
- Administrative command executed.
- Failed authentication attempt.
- Permission change.
- Account creation or deletion.

Accounting supports auditing, detection, investigation, and compliance.

A useful distinction is:

**Authentication = Who are you?**

**Authorization = What can you do?**

**Accounting = What did you do?**

---

# 3. IAM Identity Lifecycle

IAM must follow an identity throughout its entire organizational lifecycle.

A simplified lifecycle is:

```text
Request
   ↓
Identity verification
   ↓
Provisioning
   ↓
Authentication
   ↓
Authorization
   ↓
Monitoring and review
   ↓
Role/permission changes
   ↓
Suspension or termination
   ↓
Deprovisioning
```

The most important operational principle is that access should change when the user's business relationship with the organization changes.

---

# 4. Joiner, Mover, Leaver (JML)

JML is one of the most important IAM operational concepts.

## 4.1 Joiner

A **joiner** is a newly authorized person entering the organization.

Example:

A new employee joins the Finance department.

The organization may provision:

- Corporate identity.
- Email account.
- Laptop account.
- VPN access.
- Finance application access.
- Appropriate file-share permissions.
- MFA enrollment.

The important security principle is that the employee should receive **only the access required for the assigned role**.

Do not solve onboarding by giving everyone broad access and expecting permissions to be removed later.

---

## 4.2 Mover

A **mover** changes role, department, responsibilities, location, or employment status.

Example:

```text
Before:
Sales employee → CRM + Sales Share + Sales applications

After transfer to HR:
HR employee → HR application + HR Share
```

A common security failure occurs when new permissions are added without removing obsolete permissions.

The result may become:

```text
Old Sales permissions
        +
New HR permissions
        =
Unnecessary privilege
```

This is sometimes called **privilege accumulation** or **permission creep**.

Mover processes should therefore include both:

1. Granting newly required access.
2. Removing access that is no longer required.

---

## 4.3 Leaver

A **leaver** is a person whose relationship with the organization has ended.

Deprovisioning may include:

- Disabling the identity.
- Revoking active sessions.
- Revoking VPN access.
- Removing group memberships.
- Revoking application access.
- Invalidating authentication tokens.
- Revoking certificates where appropriate.
- Rotating shared or service credentials affected by the departure.
- Recovering devices and badges.
- Removing physical access.
- Preserving required evidence and records according to policy.

The goal is to prevent a former user from retaining a usable authentication path.

### Security+ Scenario

An employee is terminated at 10:00 AM. Their manager reports that the employee can still access corporate applications at 10:30 AM.

The immediate IAM concern is **failure of timely deprovisioning**. Investigators should also determine whether active sessions, tokens, VPN connections, API credentials, or delegated access remain valid.

---

# 5. Account Provisioning and Deprovisioning

## Provisioning

Provisioning is the process of creating an identity and granting the access required for that identity's role.

A controlled provisioning workflow might be:

```text
HR creates employee record
        ↓
Manager confirms role
        ↓
IAM system creates identity
        ↓
Role/group membership assigned
        ↓
MFA enrolled
        ↓
Required applications provisioned
        ↓
Access logged and auditable
```

Automated provisioning can reduce manual mistakes, particularly in large organizations.

---

## Deprovisioning

Deprovisioning removes or disables access when it is no longer authorized.

A secure process should consider more than simply deleting the user's directory account.

Potential access paths include:

- Active Directory account.
- Cloud identity.
- SaaS applications.
- VPN.
- SSH keys.
- API tokens.
- Personal access tokens.
- Certificates.
- Mobile device management.
- Physical access badges.
- Shared credentials.
- Service/application relationships.

Deleting one identity record does not necessarily invalidate every credential associated with that identity.

---

# 6. Least Privilege

**Least privilege** means giving a subject the minimum permissions necessary to perform its authorized function.

Suppose a help-desk employee needs to reset user passwords.

A poorly designed permission model might make the employee a domain administrator.

A least-privilege design would provide a narrowly defined capability such as password reset without granting unrelated administrative powers.

The difference is significant:

```text
Required task:
Reset password

Excessive privilege:
Domain Administrator

Least privilege:
Delegated password-reset permission
```

Least privilege limits the potential damage if an account is compromised or misused.

---

# 7. Need-to-Know

**Need-to-know** limits access to information based on whether the subject actually requires that information to perform an authorized task.

Least privilege is generally about **permissions and capabilities**.

Need-to-know is strongly concerned with **access to specific information**.

Example:

A security analyst may have access to the SIEM because the analyst needs to investigate alerts. That does not automatically mean the analyst needs access to every HR salary record.

A user can therefore have a legitimate organizational role while still being denied access to information unrelated to that role.

---

# 8. Role-Based Access Control (RBAC)

RBAC assigns permissions to roles and then assigns users to those roles.

Example:

```text
Role: SOC Analyst L1
    ↓
Permissions:
- Read SIEM alerts
- Search logs
- Create tickets
- Escalate incidents

User: Dheeraj
    ↓
Member of SOC Analyst L1
```

The user inherits permissions from the role.

RBAC is useful because access can be managed according to job responsibilities rather than individually configuring every user.

### Common advantage

If 100 employees perform the same job, the organization can manage a common role instead of maintaining 100 independent permission sets.

### Common risk

Poorly designed roles can become too broad. If the role contains unnecessary permissions, every member of the role receives those permissions.

---

# 9. Attribute-Based Access Control (ABAC)

ABAC evaluates attributes when making an authorization decision.

Possible attributes include:

- User department.
- Job role.
- Device security posture.
- Location.
- Time.
- Resource classification.
- Application.
- Network context.

Example policy:

```text
Allow access if:
User.department = Finance
AND
Resource.classification = Internal
AND
Device.compliance = Compliant
```

ABAC can provide more contextual authorization than a simple role-only model.

---

# 10. Other Access Control Models

Security+ can distinguish several access control concepts.

## Discretionary Access Control (DAC)

The owner of a resource can generally determine who receives access.

Example:

A file owner grants another user read access to a document.

## Mandatory Access Control (MAC)

Access is determined by centrally enforced security labels and policy rather than ordinary users deciding permissions.

A classic example is a classified-information environment where subjects and objects have security classifications.

## Rule-Based Access Control

Access is determined by predefined rules.

Example:

```text
Allow administrative access only from the management network.
```

These models can overlap conceptually with broader authorization systems, so focus on **who or what makes the access decision and what information the decision uses**.

---

# 11. Authentication Factors

Authentication factors are commonly grouped into categories.

### Something you know

Examples:

- Password.
- PIN.
- Security answer.

### Something you have

Examples:

- Hardware security key.
- Smart card.
- OTP token.
- Registered authenticator device.

### Something you are

Examples:

- Fingerprint.
- Face.
- Iris.

### Somewhere you are

Examples:

- Trusted geographic context.
- Network location.

### Something you do

Examples can include behavioral characteristics such as typing patterns.

Security+ questions may test whether two authentication methods actually represent independent factors.

---

# 12. Multi-Factor Authentication (MFA)

MFA requires authentication using multiple **independent factor categories**.

For example:

```text
Password + hardware security key
```

combines:

```text
Something you know
+
Something you have
```

Using two passwords is not true MFA because both belong to the same factor category.

MFA reduces the impact of password compromise, although it does not eliminate all authentication attacks. Attackers may still target sessions, tokens, recovery mechanisms, phishing-resistant credentials, or users themselves.

---

# 13. Adaptive and Risk-Based Authentication

Adaptive authentication evaluates contextual information before determining how strongly a user should authenticate.

Possible signals include:

- Device posture.
- Geographic location.
- Login time.
- Previous behavior.
- IP reputation.
- Impossible travel indicators.
- Application sensitivity.
- Authentication history.

Example:

```text
Normal:
User + managed laptop + normal location
→ standard authentication

Risky:
User + unknown device + unusual location
→ MFA or stronger verification
```

This is often associated with conditional access and Zero Trust-style access decisions.

---

# 14. Single Sign-On (SSO)

SSO allows a user to authenticate through an identity provider and then access multiple trusted applications without separately authenticating to each application.

Conceptually:

```text
User
 ↓
Identity Provider
 ↓
Authentication
 ↓
Application A
Application B
Application C
```

SSO improves usability and can centralize authentication controls such as MFA and account lifecycle management.

However, the identity provider becomes highly important. Compromise of the identity provider or privileged identity infrastructure can affect many applications.

Therefore, SSO should be protected with strong authentication, privileged access controls, monitoring, and secure recovery procedures.

---

# 15. Federation

Federation allows identities managed by one trusted identity domain to be used to access resources in another domain.

Example:

```text
Organization Identity Provider
          ↓
       Trust
          ↓
External SaaS Application
```

The application does not necessarily maintain an independent password database for every organizational user.

Common federation technologies and concepts include:

- SAML.
- OAuth 2.0.
- OpenID Connect.
- Federation trust.
- Identity providers.
- Service providers/relying parties.

### Important distinction

**SSO** describes the user experience/capability of authenticating once and accessing multiple services.

**Federation** describes a trust relationship in which identity information is accepted across organizational or security domains.

They are related but not identical.

---

# 16. Directory Services

Directories store and organize identity-related information.

Common directory concepts include:

- Users.
- Groups.
- Computers.
- Organizational units.
- Attributes.
- Policies.
- Authentication information.

LDAP is a common protocol used to interact with directory services.

Microsoft Active Directory environments commonly use LDAP-related directory operations along with Kerberos and other Windows authentication mechanisms.

Security operations should monitor directory changes because attackers frequently target identity infrastructure for persistence and privilege escalation.

Important events include:

- New account creation.
- Group membership changes.
- Privileged group changes.
- Password resets.
- Account disablement.
- Service principal changes.
- Delegation changes.
- Authentication failures.

---

# 17. Privileged Access Management (PAM)

Privileged accounts can make high-impact changes to systems, applications, networks, and identity infrastructure.

Examples include:

- Domain administrators.
- Cloud administrators.
- Database administrators.
- Network administrators.
- Security administrators.
- Root accounts.
- Highly privileged service identities.

PAM reduces the risk associated with these identities.

Typical PAM capabilities include:

- Privileged credential vaulting.
- Credential rotation.
- Just-in-time access.
- Approval workflows.
- Session recording.
- Command monitoring.
- Administrative activity logging.
- Temporary privilege elevation.
- Emergency access controls.

---

# 18. Just-in-Time Privileged Access

Instead of permanently giving an administrator powerful permissions, access can be granted only for the period required to perform a task.

Example:

```text
Administrator normally:
Standard privileges

Task:
Patch database server

Request:
Temporary DB administrator access

Approval:
Security/manager policy

Access:
30 minutes

Task complete:
Privilege automatically removed
```

This reduces the time during which privileged credentials can be abused.

---

# 19. Privileged Account Monitoring

Privileged activity should receive greater scrutiny because administrative accounts can make changes with significant security consequences.

Useful telemetry includes:

- Privileged logins.
- Source workstation.
- Source IP.
- Commands executed.
- Files accessed.
- Group membership changes.
- Policy changes.
- New administrator creation.
- Authentication anomalies.
- Unusual administrative time or location.

A SOC may create detections for events such as:

```text
Normal user
   ↓
Suddenly added to privileged group
   ↓
Privileged login
   ↓
Security policy modified
```

The combination may represent a high-value investigation path.

---

# 20. Service Accounts

A service account is an identity used by an application, service, scheduled task, or automated process rather than a normal human user.

Example:

```text
Web application
      ↓
Service account
      ↓
Database
```

Service accounts require careful management because they can have long-lived credentials and may be overlooked during normal user reviews.

Security principles include:

- Minimum required privileges.
- No unnecessary interactive logon.
- Credential rotation.
- Monitoring.
- Ownership assignment.
- Documented purpose.
- Regular review.
- Avoiding shared human use.

A service account should not automatically receive administrator privileges simply because an application is difficult to configure.

---

# 21. Machine and Workload Identities

Modern environments also contain non-human identities such as:

- Servers.
- Containers.
- Cloud workloads.
- Applications.
- APIs.
- Automation pipelines.
- IoT devices.

These identities require lifecycle management just like human identities.

For example:

```text
Container
 ↓
Workload identity
 ↓
Cloud API
 ↓
Storage bucket
```

The workload should receive only the permissions required for its function.

Long-lived static API keys should be avoided when a safer short-lived identity mechanism is available.

---

# 22. Password and Credential Operations

Password policies are one component of IAM operations.

Security teams may manage:

- Minimum password requirements.
- Password history.
- Password reset procedures.
- Account lockout policies.
- Failed-login thresholds.
- Temporary credentials.
- Credential recovery.
- MFA enrollment.

However, password complexity alone is not a complete identity security strategy.

Organizations should also consider:

- MFA.
- Password managers.
- Phishing-resistant authentication.
- Breached-password detection.
- Conditional access.
- Monitoring.
- Strong recovery procedures.

---

# 23. Account Lockout

Account lockout can reduce password-guessing attacks by temporarily preventing authentication after repeated failures.

Example:

```text
Failed login 1
Failed login 2
Failed login 3
        ↓
Account temporarily locked
```

But aggressive lockout policies can also be abused for denial-of-service against user accounts.

Therefore, Security+ scenarios may require balancing brute-force protection with operational availability.

Controls can include:

- Progressive delays.
- Risk-based authentication.
- MFA.
- Monitoring.
- Smart lockout mechanisms.

---

# 24. Access Reviews and Recertification

Access reviews verify that users still require the permissions they currently possess.

A review might ask:

```text
Does the employee still work here?
Does the employee still perform this role?
Does the employee still need this application?
Does the employee still need this privilege?
Is the account dormant?
Are there conflicting permissions?
```

Managers, resource owners, application owners, and security teams may have different responsibilities in the review process.

The important objective is to identify and remove unnecessary access.

---

# 25. Dormant, Orphaned, and Stale Accounts

These terms describe important IAM risks.

## Dormant account

An account that exists but has not been used for a defined period.

## Orphaned account

An account that no longer has an appropriate owner or responsible identity.

Example:

```text
Employee leaves
   ↓
Application account remains
   ↓
No owner
   ↓
Orphaned account
```

## Stale permissions

Permissions that remain even though the user's business requirement has changed.

All can increase attack surface.

---

# 26. Separation of Duties

**Separation of duties (SoD)** prevents one person from controlling an entire sensitive process when independent checks are appropriate.

Example:

```text
Person A → Creates payment
Person B → Approves payment
```

If one compromised identity can both create and approve the transaction, the attacker may bypass an important control.

SoD is especially relevant to:

- Financial systems.
- Privileged administration.
- Security operations.
- Software deployment.
- Change management.
- Procurement.

---

# 27. Break-Glass or Emergency Accounts

A break-glass account is an emergency identity used when normal administrative access is unavailable.

Example:

```text
Identity provider outage
        ↓
Normal administrators cannot authenticate
        ↓
Emergency account used
```

Because these accounts bypass or provide an alternative to normal access workflows, they require strong protection.

Good operational practices include:

- Strong credentials.
- Restricted use.
- Secure storage.
- Monitoring.
- Alerting whenever used.
- Regular testing.
- Clear ownership.
- Immediate investigation after use.

A break-glass account should not become an ordinary daily administrator account.

---

# 28. Conditional Access and Device Posture

Access decisions can consider whether the device itself is trustworthy enough to access a resource.

Possible device conditions include:

- Managed by the organization.
- Encrypted.
- Patched.
- Running endpoint protection.
- Compliant with security policy.
- Known to the organization.

Example:

```text
User identity valid
        ↓
Device not managed / high risk
        ↓
Access denied or stronger verification required
```

This connects IAM with endpoint security and Zero Trust principles.

---

# 29. Certificate-Based Identity

Certificates can be used to authenticate users, devices, or services.

For example:

```text
Device
 ↓
Client certificate
 ↓
Authentication system
 ↓
Device identity verified
```

Certificate-based authentication is useful for machine identity and can reduce reliance on reusable passwords.

Operational challenges include:

- Certificate issuance.
- Renewal.
- Revocation.
- Private-key protection.
- Expiration monitoring.
- Certificate inventory.

An expired certificate can cause legitimate services to fail, while a compromised certificate may require rapid revocation or replacement.

---

# 30. API Keys, Tokens, and Secrets

Applications commonly use credentials that are not traditional passwords.

Examples:

- API keys.
- OAuth tokens.
- Access tokens.
- Refresh tokens.
- SSH keys.
- Client certificates.
- Cloud access keys.

These are still identities or authentication material and must be managed securely.

A common failure is storing secrets directly in source code:

```text
Git repository
   ↓
Hard-coded API key
   ↓
Repository exposure
   ↓
Attacker obtains credential
```

Secrets should instead be managed through appropriate secret-management mechanisms and rotated when exposure is suspected.

---

# 31. Third-Party and Guest Identities

External users may require access to organizational resources.

Examples include:

- Contractors.
- Vendors.
- Consultants.
- Partners.
- Temporary workers.

These identities should have:

- Named ownership.
- Defined purpose.
- Expiration where appropriate.
- Limited scope.
- Strong authentication.
- Monitoring.
- Periodic review.

A major risk is granting permanent access to a contractor for a project that lasts only three months.

---

# 32. Cloud IAM Operations

Cloud platforms rely heavily on IAM.

Cloud IAM can include:

- Users.
- Groups.
- Roles.
- Policies.
- Service identities.
- Workload identities.
- Federation.
- MFA.
- Conditional access.
- API credentials.

Cloud IAM is especially sensitive because a single identity may have permissions across many resources.

Example:

```text
Compromised cloud administrator
        ↓
Storage access
Database access
VM management
IAM modification
Logging modification
        ↓
Potentially large blast radius
```

Therefore, privileged cloud identities require strong controls, logging, and separation of duties.

---

# 33. IAM Logging and Monitoring

IAM events are valuable security telemetry.

Monitor for:

- Successful logins.
- Failed logins.
- MFA failures.
- MFA enrollment changes.
- Password resets.
- New accounts.
- Disabled accounts.
- Privileged group changes.
- Role changes.
- Permission changes.
- Token issuance.
- API-key creation.
- Certificate changes.
- Unusual authentication locations.
- Impossible travel patterns.
- Break-glass account use.

These events can be forwarded to a SIEM for correlation.

Example detection path:

```text
New privileged account
      +
Login from unusual source
      +
Security policy change
      ↓
High-priority investigation
```

A single login event may be benign. A sequence of related IAM events can provide much stronger evidence.

---

# 34. IAM and Incident Response

IAM controls are frequently involved in incident response.

If an account is compromised, responders may need to:

1. Disable or restrict the account.
2. Revoke active sessions.
3. Revoke tokens.
4. Reset credentials.
5. Rotate affected API keys.
6. Revoke or replace certificates where necessary.
7. Remove unauthorized group membership.
8. Identify persistence mechanisms.
9. Review historical authentication activity.
10. Determine what resources the identity accessed.

Do not assume that changing a password automatically removes attacker access. Existing sessions, tokens, application credentials, or alternate authentication paths may remain valid depending on the platform.

---

# 35. IAM and Zero Trust

Zero Trust does not mean simply “use MFA.”

A Zero Trust approach continuously evaluates whether access should be allowed based on identity, device, resource, context, and policy.

A conceptual model is:

```text
User identity
     +
Device posture
     +
Application/resource
     +
Context/risk
     +
Policy
     ↓
Access decision
```

The principle is often summarized as **never implicitly trust; continuously evaluate access**.

IAM provides a major part of the identity and policy foundation required for this model.

---

# 36. Common IAM Operational Failures

## Failure 1: Terminated account remains active

**Problem:** Former employee retains access.

**Risk:** Unauthorized access and potential data theft.

**Correct operational response:** Prompt deprovisioning, session/token revocation where appropriate, and investigation of activity after termination.

---

## Failure 2: Mover receives new access but keeps old access

**Problem:** Permission creep.

**Risk:** Excessive privilege.

**Correct response:** Reassess the complete access set during role transition.

---

## Failure 3: Everyone receives administrator rights

**Problem:** Excessive privilege.

**Risk:** Large blast radius after account compromise.

**Correct principle:** Least privilege.

---

## Failure 4: Shared administrator account

**Problem:** Multiple people use one identity.

**Risk:** Poor accountability and difficult attribution.

**Better approach:** Named privileged identities with PAM and individual authentication.

---

## Failure 5: Service account has interactive administrator access

**Problem:** Automation identity has unnecessary privileges.

**Risk:** Compromise of the application may become compromise of the infrastructure.

**Better approach:** Dedicated identity, minimal privileges, credential rotation, and restricted usage.

---

## Failure 6: Dormant accounts are never reviewed

**Problem:** Unused identities remain available to attackers.

**Risk:** Attack surface increases without corresponding business value.

**Better approach:** Periodic access review and lifecycle enforcement.

---

## Failure 7: MFA recovery is weak

**Problem:** Strong MFA exists, but an attacker can bypass it through a weak recovery process.

**Risk:** Account takeover through the recovery channel.

**Lesson:** Secure the entire authentication lifecycle, not just the primary login mechanism.

---

# 37. Practical IAM Scenario

Consider this environment:

```text
Company
│
├── HR
├── Finance
├── Sales
└── SOC
```

An employee moves from Sales to Finance.

Before the move:

```text
Sales employee
├── Sales application
├── Sales file share
└── CRM
```

After the move, the employee needs:

```text
Finance employee
├── Finance application
└── Finance file share
```

A weak IAM process adds Finance permissions but leaves all Sales permissions intact.

The employee now has access to both departments.

The correct IAM process is:

```text
Role change detected
        ↓
Review old permissions
        ↓
Remove obsolete Sales access
        ↓
Grant required Finance access
        ↓
Verify resulting permissions
        ↓
Log the change
```

This is a classic **mover + least privilege + access review** scenario.

---

# 38. IAM Decision Framework for Security+ Questions

When you see an IAM scenario, ask these questions in order:

### Step 1 — Who is the subject?

Is it:

- Human user?
- Administrator?
- Contractor?
- Service account?
- Device?
- Application?
- Cloud workload?

### Step 2 — Is the identity lifecycle correct?

Ask:

- Is this a joiner?
- Mover?
- Leaver?
- Dormant account?
- Orphaned identity?

### Step 3 — How is identity verified?

Look for:

- Password.
- MFA.
- Certificate.
- Hardware key.
- Biometrics.
- Adaptive authentication.

### Step 4 — What is the authorization model?

Look for:

- RBAC.
- ABAC.
- Least privilege.
- Need-to-know.
- MAC/DAC/rule-based controls.

### Step 5 — Is the privilege excessive?

Ask:

> Does the subject have more access than the task requires?

If yes, least privilege is likely relevant.

### Step 6 — Is privileged access involved?

If yes, consider:

- PAM.
- Just-in-time access.
- Approval.
- Session monitoring.
- Credential vaulting.

### Step 7 — Is access being reviewed?

Look for:

- Access recertification.
- Dormant accounts.
- Orphaned accounts.
- Permission creep.

### Step 8 — Is the activity being monitored?

Look for:

- Authentication logs.
- Authorization events.
- Privileged activity.
- Directory changes.
- SIEM correlation.

---

# 39. Important Security+ Distinctions

| Concept | Meaning |
|---|---|
| Identification | Claims an identity |
| Authentication | Verifies identity |
| Authorization | Determines allowed actions |
| Accounting | Records activity |
| Least privilege | Minimum required permissions |
| Need-to-know | Access only to required information |
| RBAC | Permissions assigned through roles |
| ABAC | Access based on attributes/context |
| PAM | Controls and monitors privileged access |
| SSO | One authentication experience across multiple services |
| Federation | Trust relationship across identity domains |
| Provisioning | Creating/granting access |
| Deprovisioning | Removing/revoking access |
| JML | Joiner, mover, leaver lifecycle |
| Access review | Verifies continued need for permissions |
| Dormant account | Existing account with little/no recent use |
| Orphaned account | Account without appropriate ownership |
| Separation of duties | Divides sensitive responsibilities |
| Break-glass account | Emergency access identity |

---

# 40. Security+ Exam Traps

### Trap 1: Authentication vs authorization

If the question asks **who the user is**, think authentication.

If it asks **what the user can access**, think authorization.

---

### Trap 2: Password + password is not MFA

Two credentials from the same factor category do not become multiple independent factors simply because there are two credentials.

---

### Trap 3: SSO does not mean one password everywhere

SSO centralizes authentication and access to multiple services. It does not mean applications should all share the same password database.

---

### Trap 4: Least privilege is not the same as need-to-know

Least privilege focuses on minimum permissions/capabilities. Need-to-know focuses on limiting information access to what is necessary.

---

### Trap 5: Deleting a user does not necessarily revoke every credential

Investigate sessions, tokens, certificates, API keys, SSH keys, and application-specific identities where relevant.

---

### Trap 6: RBAC is not always the most contextual model

If the question emphasizes user, device, location, time, resource, and other contextual attributes, ABAC may be more appropriate.

---

### Trap 7: Privileged accounts need stronger controls

If a scenario involves domain administrators, cloud administrators, root, or other highly privileged identities, consider PAM, JIT access, monitoring, and separation of duties.

---

# 41. Key Takeaways

IAM operations protect the organization by controlling the complete lifecycle of identities and access.

The most important operational ideas are:

1. **Identification claims an identity; authentication verifies it.**
2. **Authorization determines what an authenticated subject can do.**
3. **Accounting records activity for auditing and investigation.**
4. **Joiner, mover, and leaver processes must change access as the business relationship changes.**
5. **Least privilege minimizes unnecessary permissions.**
6. **Need-to-know limits access to required information.**
7. **MFA uses independent authentication factors.**
8. **RBAC assigns permissions through roles; ABAC evaluates attributes and context.**
9. **PAM protects highly privileged identities through controls such as vaulting, JIT access, monitoring, and auditing.**
10. **Service accounts and workload identities require lifecycle management too.**
11. **Dormant and orphaned accounts increase attack surface.**
12. **Access reviews identify excessive, obsolete, and conflicting permissions.**
13. **Break-glass accounts should be restricted, monitored, and used only when necessary.**
14. **IAM events are valuable SIEM telemetry.**
15. **Strong IAM must cover authentication, authorization, credentials, sessions, tokens, certificates, and recovery mechanisms—not just passwords.**

The operational goal is not simply to make access possible. It is to ensure that access is **authorized, appropriate, limited, observable, reviewable, and removed when no longer required**.