# Domain 5 — Module 1: Governance and Security Policies

Security governance is the management and oversight structure through which an organization directs, controls, and evaluates its information-security program. Governance connects **business objectives, risk, legal and regulatory requirements, security strategy, accountability, and operational execution**.

A useful mental model is:

**Business Objectives → Governance → Policies → Standards → Procedures → Technical/Administrative Controls → Measurement → Review and Improvement**

Governance is not the same thing as day-to-day security operations. Operations implement and monitor controls; governance establishes direction, accountability, authority, requirements, and oversight.

---

# 1. What Is Security Governance?

Security governance establishes how an organization makes and oversees security decisions.

It answers questions such as:

- Who has authority to make security decisions?
- Who is accountable for protecting information and systems?
- What level of risk is acceptable?
- Which laws, regulations, contracts, and standards apply?
- What security objectives must the organization achieve?
- Which controls are required?
- How is security performance measured?
- Who can approve exceptions?
- How are security failures escalated?
- How does management verify that security requirements remain effective?

Governance therefore establishes the **direction and accountability** of the security program.

---

# 2. Governance vs Security Operations

These concepts are closely related but serve different purposes.

### Governance

Focuses on:

- Direction.
- Accountability.
- Risk oversight.
- Policies.
- Compliance.
- Security strategy.
- Management decisions.
- Organizational requirements.

### Security Operations

Focuses on:

- Monitoring.
- Detection.
- Incident response.
- Vulnerability management.
- Configuration management.
- Security-tool operation.
- Investigation.
- Recovery.

Example:

> Management establishes that privileged access must use MFA.

That is a **governance/policy requirement**.

> Administrators configure MFA for privileged accounts and monitor authentication events.

That is **security operations**.

---

# 3. Governance Aligns Security With Business Objectives

Security should support the organization's mission rather than operate independently from it.

Consider a hospital, bank, university, and manufacturing company. Their most important assets, regulatory obligations, availability requirements, and threat environments differ.

Governance helps determine:

```text
Business Objective
       ↓
Critical Assets
       ↓
Risks
       ↓
Security Requirements
       ↓
Controls
       ↓
Measurement
```

For example, if a business depends heavily on an online payment platform, governance may establish requirements for protecting payment information, controlling privileged access, maintaining availability, and meeting applicable compliance obligations.

The exact controls are then implemented by technical and operational teams.

---

# 4. Security Strategy

A security strategy describes the organization's broader approach to managing security risk.

It may establish priorities such as:

- Identity-centric security.
- Zero Trust principles.
- Cloud-security requirements.
- Data protection.
- Security monitoring.
- Resilience.
- Third-party risk management.
- Regulatory compliance.
- Security awareness.

Strategy is broader than a single policy.

For example:

> "Reduce unauthorized access to sensitive information."

is a strategic objective.

A policy can translate that objective into mandatory organizational requirements.

---

# 5. Policy

A **policy** is a high-level, mandatory statement of management intent.

A policy answers:

> **What must the organization do?**

Examples:

- Information Security Policy.
- Acceptable Use Policy.
- Access Control Policy.
- Password and Authentication Policy.
- Data Classification Policy.
- Incident Response Policy.
- Remote Access Policy.
- Encryption Policy.
- Backup Policy.
- Change Management Policy.
- Third-Party Security Policy.

A policy normally does not provide every technical implementation detail.

---

# 6. Standards

A **standard** provides specific, mandatory requirements that support a policy.

A standard answers:

> **What specific requirement must be followed?**

For example:

**Policy:**

> Sensitive systems must use strong authentication.

**Standard:**

> Privileged accounts must use MFA and approved authentication mechanisms.

The standard is more specific than the policy.

---

# 7. Procedures

A **procedure** provides step-by-step instructions for performing a task consistently.

A procedure answers:

> **How is the required task performed?**

For example, an MFA-enrollment procedure might describe:

1. Verify the employee's identity.
2. Create or activate the account.
3. Enroll the approved authentication method.
4. Verify successful authentication.
5. Record completion.
6. Escalate enrollment failures.

Procedures are operational documents.

---

# 8. Guidelines

A **guideline** provides recommended practices rather than the same mandatory authority as a policy or standard.

A guideline answers:

> **What is recommended?**

Examples include recommendations for:

- Secure password handling.
- Secure remote-work practices.
- Safe use of public networks.
- Handling sensitive information while traveling.

Guidelines are generally more flexible than mandatory requirements.

---

# 9. Policy Hierarchy

A useful Security+ distinction is:

```text
Policy
  ↓
Standard
  ↓
Procedure
  ↓
Guideline
```

Think of it as:

| Document | Primary Question | Typical Authority |
|---|---|---|
| Policy | What must be done? | Mandatory |
| Standard | What specific requirement must be met? | Mandatory |
| Procedure | How is the task performed? | Operational instruction |
| Guideline | What is recommended? | Flexible recommendation |

Do not confuse a procedure with a policy. A procedure tells someone how to perform a task; a policy establishes the requirement.

---

# 10. Example — Access Control

Suppose an organization wants stronger protection for privileged accounts.

### Policy

> Privileged access must be strongly authenticated and appropriately controlled.

### Standard

> Privileged accounts must use MFA and must not be shared.

### Procedure

> Follow these steps to provision, enroll, verify, and deactivate privileged accounts.

### Guideline

> Administrators should use dedicated administrative workstations when performing privileged tasks.

This example demonstrates how a broad governance requirement becomes progressively more actionable.

---

# 11. Security Policy vs Technical Control

A policy is not itself the same as a technical control.

For example:

> "All employees must use MFA."

is a policy requirement.

An identity provider configured to require MFA is a **technical control** that helps enforce the requirement.

Similarly:

> "Sensitive data must be encrypted at rest."

is a requirement, while disk encryption, database encryption, or cloud-storage encryption are controls used to implement it.

---

# 12. Roles and Responsibilities

Security governance requires clear accountability.

Potential participants include:

- Board of directors.
- Executive management.
- Chief Information Security Officer (CISO).
- Security leadership.
- IT leadership.
- System owners.
- Data owners.
- Data custodians.
- Security administrators.
- Privacy teams.
- Legal teams.
- Human resources.
- Internal audit.
- Risk/compliance teams.
- Third-party managers.
- End users.

The exact organizational structure varies, but responsibilities should be clearly defined.

---

# 13. Data Owner vs Data Custodian

This is an important distinction.

### Data Owner

The data owner is accountable for decisions concerning the data, such as classification, access requirements, and appropriate use.

### Data Custodian

The custodian is responsible for implementing and maintaining controls that protect the data.

Example:

A business department may own customer information, while the IT team operates the database and implements backups, access controls, and technical protections.

The custodian implements controls; the owner retains organizational accountability for the data.

---

# 14. System Owner

A system owner is responsible for a particular system or application and its associated security requirements.

The system owner may coordinate:

- Risk decisions.
- Access requirements.
- Security controls.
- Configuration requirements.
- Vulnerability remediation.
- Business continuity.
- System lifecycle.

Security teams provide expertise and controls, but ownership must remain clear.

---

# 15. Separation of Duties

**Separation of duties (SoD)** divides sensitive responsibilities among different people or roles to reduce the risk of fraud, abuse, or unauthorized actions.

Example:

```text
Person A
Creates payment

Person B
Approves payment
```

The same individual should not necessarily be able to create and approve a sensitive transaction.

In security administration, SoD might separate:

- Policy approval.
- Security administration.
- Audit.
- Exception approval.

This reduces the risk of a single individual having excessive control.

---

# 16. Least Privilege in Governance

Least privilege means granting only the access necessary to perform an authorized task.

Governance should establish expectations for least privilege, while technical teams implement those requirements through IAM, PAM, RBAC, ABAC, network controls, and application permissions.

Least privilege is therefore both a security principle and a governance requirement.

---

# 17. Accountability and Responsibility

These terms are related but should not be treated as interchangeable.

**Responsibility** generally refers to performing an assigned task.

**Accountability** refers to being answerable for the outcome or decision.

For example, an administrator may be responsible for implementing a security configuration, while the system owner may remain accountable for the system's security requirements.

Organizations should define these relationships clearly.

---

# 18. Policy Lifecycle

Security policies should be managed throughout their lifecycle.

A typical lifecycle is:

```text
Identify Requirement
        ↓
Draft Policy
        ↓
Review
        ↓
Approve
        ↓
Publish
        ↓
Communicate
        ↓
Implement / Enforce
        ↓
Monitor Compliance
        ↓
Review and Update
        ↓
Retire or Replace
```

A policy that exists only in a document repository but is unknown to employees and not enforced provides limited practical value.

---

# 19. Policy Development

Policy development should begin with a clear business or security requirement.

Consider:

- Business objectives.
- Legal requirements.
- Regulatory requirements.
- Contractual obligations.
- Risk assessments.
- Industry requirements.
- Security incidents.
- Audit findings.
- Technology changes.

A policy should be understandable, enforceable, appropriately scoped, and consistent with higher-level organizational requirements.

---

# 20. Policy Approval

Policies generally require appropriate management authority before becoming organizational requirements.

Approval establishes that the organization formally accepts the requirement and its associated responsibilities.

The appropriate approver depends on organizational structure and policy significance.

Security personnel may draft or recommend a policy without being the final authority that approves it.

---

# 21. Policy Communication

A policy cannot be effective if the affected population does not know that it exists.

Communication may involve:

- Security-awareness training.
- Employee handbooks.
- Intranet publication.
- Onboarding processes.
- Manager communication.
- Technical enforcement notices.

For example, an acceptable-use policy should be communicated to employees before they are expected to comply with it.

---

# 22. Policy Enforcement

Policies establish requirements; controls enforce them.

Example:

```text
Password Policy
      ↓
Authentication Standard
      ↓
Identity-System Configuration
      ↓
Technical Enforcement
      ↓
Monitoring / Audit
```

Enforcement may involve:

- IAM controls.
- Endpoint configuration.
- Firewalls.
- DLP.
- Network access controls.
- Logging.
- Administrative processes.
- Disciplinary procedures where applicable.

---

# 23. Policy Review and Maintenance

Policies should be periodically reviewed and also reconsidered after significant changes.

Triggers may include:

- New regulations.
- New technology.
- Organizational restructuring.
- Major incidents.
- Audit findings.
- New business processes.
- Cloud adoption.
- Changes in threat environment.
- Changes in contractual obligations.

A policy can become outdated even if it was originally well designed.

---

# 24. Version Control and Document Control

Security policies should have controlled versions so employees and auditors can determine which version is currently authoritative.

Useful metadata includes:

- Policy title.
- Version number.
- Effective date.
- Owner.
- Approver.
- Review date.
- Classification.
- Revision history.
- Next review date.

Document control reduces ambiguity about which requirements are currently applicable.

---

# 25. Policy Exceptions

Organizations may encounter situations where a requirement cannot be met immediately.

For example, a legacy application may not support the organization's current authentication standard.

The correct response is not necessarily to ignore the policy.

Use a formal exception process.

An exception should identify:

- Requirement being waived.
- Reason for the exception.
- Affected systems or processes.
- Associated risk.
- Compensating controls.
- Risk owner.
- Approval authority.
- Start date.
- Expiration or review date.
- Conditions for removal.

---

# 26. Compensating Controls

A compensating control is an alternative measure used to reduce risk when the preferred control cannot be implemented as required.

Example:

A legacy server cannot support MFA.

Possible compensating controls could include:

- Network isolation.
- Restricted administrative access.
- Jump-host access.
- Strong monitoring.
- Additional authentication controls around the management path.
- Reduced exposure.

A compensating control should not be treated as a reason to permanently ignore the original requirement. The residual risk should remain visible and managed.

---

# 27. Risk Acceptance

Sometimes an organization knowingly accepts a residual risk.

Risk acceptance should be an informed organizational decision by an appropriate risk owner, not an informal statement by a technician who does not have authority to accept the risk.

Example:

```text
Requirement cannot currently be met
             ↓
Risk assessed
             ↓
Compensating controls applied
             ↓
Residual risk documented
             ↓
Authorized owner accepts risk
             ↓
Review date established
```

Risk acceptance should not be confused with risk elimination.

---

# 28. Policy Violation vs Security Incident

A policy violation does not automatically mean a security incident, although it can become one depending on circumstances.

Example:

An employee uses an unauthorized cloud-storage service. This may initially be a policy violation.

If investigation shows sensitive corporate data was uploaded without authorization, the situation may require incident response.

The distinction depends on organizational definitions, evidence, and impact.

---

# 29. Acceptable Use Policy

An Acceptable Use Policy (AUP) defines how organizational technology and information resources may be used.

It may address:

- Corporate devices.
- Internet access.
- Email.
- Software installation.
- Personal use.
- Removable media.
- Cloud services.
- Monitoring.
- Prohibited activities.

The AUP establishes expected behavior rather than providing technical implementation instructions.

---

# 30. Access Control Policy

An access control policy establishes organizational requirements for granting, reviewing, modifying, and removing access.

It may address:

- Least privilege.
- Need-to-know.
- MFA.
- Privileged access.
- Account lifecycle.
- Access reviews.
- Third-party access.
- Remote access.
- Separation of duties.

Technical teams implement these requirements through IAM and related controls.

---

# 31. Data Classification Policy

A data classification policy establishes categories for information based on sensitivity, business value, legal requirements, or potential impact.

Common organizational categories may include:

- Public.
- Internal.
- Confidential.
- Restricted.

The exact classification scheme varies by organization.

Classification influences controls such as:

- Access restrictions.
- Encryption.
- Retention.
- Transmission requirements.
- Monitoring.
- Disposal.

---

# 32. Incident Response Policy

An incident response policy establishes management expectations for handling security incidents.

It may define:

- What constitutes an incident.
- Roles and responsibilities.
- Escalation requirements.
- Communication expectations.
- Evidence handling requirements.
- Reporting obligations.
- Authority to contain affected systems.

Detailed operational steps normally belong in incident-response procedures or playbooks.

---

# 33. Remote Access Policy

A remote-access policy establishes requirements for connecting to organizational resources from outside controlled environments.

It may address:

- VPN.
- MFA.
- Approved devices.
- Device posture.
- Encryption.
- Split tunneling.
- Privileged remote administration.
- Logging.
- BYOD.

Again, the policy defines requirements; technical configurations implement them.

---

# 34. Third-Party Security Policy

Organizations often depend on vendors, contractors, cloud providers, and managed services.

A third-party security policy can establish requirements for:

- Vendor security assessments.
- Contractual security requirements.
- Data protection.
- Access control.
- Incident notification.
- Audit rights.
- Data return or destruction.
- Offboarding.

This connects governance with third-party risk management.

---

# 35. Governance Committees

Organizations may establish security or risk committees to coordinate governance decisions.

A committee may include representatives from:

- Security.
- IT.
- Legal.
- Privacy.
- Compliance.
- Finance.
- Business units.
- Executive leadership.

The purpose is to bring appropriate stakeholders into decisions involving organizational risk and security requirements.

---

# 36. Board and Executive Oversight

Security governance may include executive and board-level oversight, particularly for significant organizational risks.

Management may review:

- Major security risks.
- Significant incidents.
- Compliance status.
- Security metrics.
- Risk acceptance.
- Security investment.
- Business resilience.

Technical teams provide evidence and operational information; leadership makes decisions within its organizational authority.

---

# 37. Compliance and Governance

Compliance requirements can originate from:

- Laws.
- Regulations.
- Contracts.
- Industry requirements.
- Internal policies.

Governance determines how applicable requirements are incorporated into the organization's security program.

Compliance is not identical to security. An organization can satisfy a particular compliance requirement while still having security weaknesses outside that requirement's scope.

---

# 38. Internal vs External Requirements

Security requirements can come from both internal and external sources.

### Internal

- Corporate policies.
- Risk decisions.
- Business requirements.
- Security standards.
- Internal audit findings.

### External

- Laws.
- Regulations.
- Customer contracts.
- Industry frameworks.
- Partner requirements.

Governance should maintain traceability between applicable requirements and implemented controls.

---

# 39. Control Objectives

A control objective describes what a security control is intended to achieve.

Example:

> Prevent unauthorized access to sensitive customer information.

Possible controls include:

- MFA.
- RBAC.
- Encryption.
- Logging.
- Access reviews.

The objective is broader than any one technology.

---

# 40. Policy-to-Control Mapping

Organizations can map requirements to controls and evidence.

```text
Policy Requirement
       ↓
Control Objective
       ↓
Security Control
       ↓
Implementation
       ↓
Evidence
       ↓
Measurement / Audit
```

Example:

```text
Policy:
Privileged access requires MFA
        ↓
Control:
MFA enforcement
        ↓
Implementation:
Identity provider policy
        ↓
Evidence:
Authentication logs / configuration
        ↓
Verification:
Periodic audit
```

This traceability is useful for governance, audits, and security assurance.

---

# 41. Governance Documentation

Governance documentation can include:

- Policies.
- Standards.
- Procedures.
- Guidelines.
- Risk registers.
- Exception records.
- Control documentation.
- Audit reports.
- Security metrics.
- Committee decisions.
- Meeting records.

Documentation provides evidence of decisions, accountability, and organizational requirements.

---

# 42. Common Governance Failures

## Failure 1 — Policy exists but nobody knows about it

A policy stored in a repository is not sufficient if affected personnel have not been informed.

**Better:** publish, communicate, train, and enforce.

## Failure 2 — Policy is too technical

A policy should establish management requirements rather than become an implementation manual.

**Better:** keep policy at the appropriate level and use standards/procedures for detail.

## Failure 3 — No policy owner

Without ownership, review and maintenance may be neglected.

**Better:** assign an owner and approval authority.

## Failure 4 — No review cycle

Threats, technology, business processes, and regulations change.

**Better:** establish periodic and event-driven review.

## Failure 5 — Informal exceptions

Employees or administrators bypass requirements without documented approval.

**Better:** use formal exception and risk-acceptance processes.

## Failure 6 — Permanent exceptions

A temporary exception remains indefinitely.

**Better:** establish expiration or review dates and conditions for removal.

## Failure 7 — Confusing compliance with security

Meeting one requirement does not guarantee complete security.

**Better:** treat compliance as one component of the broader risk-management program.

## Failure 8 — Unclear accountability

Multiple teams assume someone else owns a security decision.

**Better:** explicitly define roles, authority, responsibility, and accountability.

---

# 43. Security+ Scenario — Choosing the Correct Document

A question states:

> Management requires all privileged accounts to use MFA. The security team needs to define the exact technical requirement that all privileged accounts must meet.

The distinction is important:

- Management's high-level requirement belongs in a **policy**.
- The exact mandatory technical requirement belongs in a **standard**.
- The steps for enrolling an administrator belong in a **procedure**.
- Recommended administrative practices belong in a **guideline**.

Look for the wording that indicates the required level of detail.

---

# 44. Security+ Scenario — Legacy System Exception

A critical legacy application cannot satisfy a new security standard.

The appropriate governance process may be:

1. Identify the requirement that cannot be met.
2. Document the affected system.
3. Assess the associated risk.
4. Identify compensating controls.
5. Assign a risk owner.
6. Obtain appropriate approval.
7. Establish an expiration or review date.
8. Monitor the exception.
9. Remove the exception when the underlying limitation is resolved.

Simply ignoring the requirement is not effective governance.

---

# 45. Security+ Scenario — Policy vs Procedure

An organization states:

> Employees must report suspected security incidents immediately.

That is a policy-level requirement.

A document explaining exactly which portal to open, which fields to complete, which phone number to call, and what information to provide is a **procedure**.

The exam may present similar language to test whether you can distinguish the management requirement from the operational instructions.

---

# 46. Security+ Scenario — Accountability

A database administrator maintains the database security configuration, while the business department determines how customer data should be classified and who should have access.

This illustrates the distinction between operational custody and data ownership.

The administrator may be responsible for implementing controls, while the data owner remains accountable for decisions concerning the data.

---

# 47. Security+ Exam Distinctions and Traps

### Policy vs Standard

- **Policy:** high-level mandatory management requirement.
- **Standard:** specific mandatory requirement supporting the policy.

### Standard vs Procedure

- **Standard:** what specific requirement must be met.
- **Procedure:** how to perform the task.

### Procedure vs Guideline

- **Procedure:** defined steps for performing a task.
- **Guideline:** recommended practice with greater flexibility.

### Governance vs Operations

- **Governance:** direction, accountability, oversight, requirements, and risk decisions.
- **Operations:** implementation, monitoring, investigation, response, and maintenance.

### Data Owner vs Data Custodian

- **Data owner:** accountable for data-related decisions and requirements.
- **Data custodian:** implements and maintains technical protections.

### Exception vs Risk Acceptance

- **Exception:** formally permits deviation from a requirement.
- **Risk acceptance:** authorized decision to accept residual risk.

### Policy vs Control

- **Policy:** establishes the requirement.
- **Control:** implements or enforces the requirement.

### Compliance vs Security

- **Compliance:** meeting specified external or internal requirements.
- **Security:** broader protection of systems, information, people, and business operations.

---

# 48. Security+ Governance Decision Framework

When a question describes a governance problem, ask:

### 1. What business or security objective is involved?

Identify what the organization is trying to protect or achieve.

### 2. Who has authority and accountability?

Determine the appropriate owner, management authority, or risk owner.

### 3. What requirement applies?

Identify policy, regulatory, contractual, business, or risk requirements.

### 4. What level of document is needed?

Determine whether the question is asking for a policy, standard, procedure, or guideline.

### 5. What control implements the requirement?

Identify the technical or administrative mechanism.

### 6. Is there a legitimate exception?

If the requirement cannot be met, use the formal exception process.

### 7. Who accepts residual risk?

Risk acceptance should be performed by an authorized risk owner.

### 8. What evidence demonstrates compliance?

Consider configurations, logs, training records, access reviews, audit records, or other evidence.

### 9. When should the requirement be reviewed?

Consider periodic reviews and event-driven triggers.

### 10. How does management verify effectiveness?

Use audits, metrics, assessments, incidents, and control testing.

---

# 49. Complete Governance Flow

```text
Business Objective
        ↓
Risk / Requirement
        ↓
Governance Direction
        ↓
Policy
        ↓
Standard
        ↓
Procedure
        ↓
Technical / Administrative Controls
        ↓
Implementation
        ↓
Monitoring / Evidence
        ↓
Audit / Measurement
        ↓
Management Review
        ↓
Update / Improve
```

This model shows how a management requirement becomes an operationally enforceable security practice.

---

# 50. Key Takeaways

- Security governance establishes direction, accountability, authority, and oversight.
- Governance connects security decisions with business objectives and risk.
- Governance is broader than day-to-day security operations.
- A policy is a high-level mandatory statement of management intent.
- A standard defines specific mandatory requirements.
- A procedure provides step-by-step instructions.
- A guideline provides recommended practices with greater flexibility.
- Policies should be approved, communicated, implemented, monitored, reviewed, updated, and eventually retired.
- Policies should have clear owners, approvers, version information, and review dates.
- Security requirements should be translated into controls and measurable evidence.
- Data owners make decisions concerning data; custodians implement and maintain technical protections.
- Separation of duties reduces the risk created by excessive concentration of authority.
- Least privilege should be established as an organizational requirement and implemented through appropriate controls.
- Exceptions should be formally documented and approved rather than handled informally.
- Compensating controls can reduce risk when a preferred control cannot be implemented.
- Risk acceptance is an authorized decision to accept residual risk; it does not eliminate that risk.
- Compliance requirements are important but do not automatically represent complete security.
- Governance documentation provides evidence of decisions, accountability, requirements, and oversight.
- Policies should be reviewed periodically and after significant changes, incidents, audit findings, or regulatory changes.
- Effective governance creates traceability from **requirement → control → evidence → measurement → improvement**.

## Core Security+ Mental Model

**Business Objective → Governance → Requirement → Policy → Standard → Procedure → Control → Evidence → Measurement → Review → Improvement**

The central principle is: **governance establishes who is accountable, what the organization requires, and how security decisions are overseen; policies express mandatory management intent, standards make requirements specific, procedures make them operational, and controls provide the mechanisms that enforce them.**