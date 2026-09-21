# Security Documentation and Records

## 1. Why Security Documentation Matters

Security documentation converts organizational requirements, decisions, processes, and technical knowledge into information that people can consistently use.

A security program cannot depend entirely on individual memory.

Consider an incident-response team where only one administrator knows:

- Which systems are critical
- Where firewall rules are documented
- Which accounts are privileged
- Who must be contacted during an incident
- Where backups are located
- How to isolate a compromised server

If that administrator is unavailable, the organization may lose important operational knowledge.

Documentation reduces this dependency by creating an authoritative record.

Security documentation supports:

- Governance
- Operations
- Incident response
- Disaster recovery
- Business continuity
- Change management
- Troubleshooting
- Training
- Auditing
- Compliance
- Risk management
- Accountability
- Knowledge transfer

A useful mental model is:

**Requirement → Decision → Procedure → Evidence → Review → Update**

---

## 2. Documentation vs Records

These concepts are related but not identical.

### Documentation

Documentation describes how something should work, how something is configured, or what requirements apply.

Examples:

- Security policy
- Incident response procedure
- Network diagram
- Configuration standard
- Disaster recovery plan

### Record

A record provides evidence that an activity, event, decision, or transaction occurred.

Examples:

- Completed access review
- Approved change request
- Audit result
- Incident ticket
- Training completion record
- System log
- Vendor assessment
- Meeting approval

A procedure says:

> "Privileged access must be reviewed quarterly."

A completed quarterly access review is a **record** demonstrating that the activity occurred.

This distinction is important for Security+ questions.

---

## 3. Documentation Hierarchy

Organizations commonly use several documentation levels.

A simplified hierarchy is:

**Policy → Standard → Procedure → Guideline**

These documents serve different purposes.

### Policy

A policy states management's requirements and direction.

It answers:

> **What is required and why?**

Example:

> All organizational systems must use approved authentication mechanisms.

Policies should generally avoid excessive technical implementation details.

### Standard

A standard establishes mandatory specifications or requirements for implementing a policy.

It answers:

> **What specific requirement must be followed?**

Example:

> Administrative accounts must use MFA and comply with the organization's approved authentication standard.

### Procedure

A procedure provides step-by-step instructions.

It answers:

> **How is the requirement performed?**

Example:

> Step 1: Open the identity-management console.  
> Step 2: Select the administrator account.  
> Step 3: Verify MFA enrollment.  
> Step 4: Record the review result.

### Guideline

A guideline provides recommended practices rather than mandatory instructions.

It answers:

> **What is recommended?**

Example:

> Administrators should avoid using privileged accounts for routine web browsing.

Organizations may use different terminology, but the key distinction is the level of authority and detail.

---

## 4. Policy vs Procedure — Important Exam Distinction

A common Security+ scenario asks what document should contain a particular type of information.

If the question describes:

> "Management requires all employees to report suspected security incidents."

That is a **policy-level requirement**.

If it asks:

> "What steps should an employee follow to report an incident?"

That is a **procedure**.

Remember:

**Policy = what/why**

**Procedure = how**

---

## 5. Standards

A standard converts broad policy requirements into measurable or enforceable technical or operational requirements.

For example:

### Policy

Sensitive information must be protected.

### Standard

Sensitive information must be encrypted using organization-approved cryptographic mechanisms when stored on portable devices.

### Procedure

The endpoint administrator performs the following configuration steps to enable approved encryption.

This progression connects management requirements to operational implementation.

---

## 6. Guidelines

Guidelines provide recommendations rather than mandatory requirements.

For example:

> Users should avoid connecting corporate devices to unknown public USB charging stations.

Guidelines provide useful direction while allowing judgment where strict procedures may not be necessary.

A question describing a **recommended practice** rather than a mandatory requirement is often pointing toward a guideline.

---

## 7. Security Documentation Categories

A security program may maintain many different documents.

Important examples include:

- Security policies
- Standards
- Procedures
- Guidelines
- System security plans
- Network diagrams
- Data-flow diagrams
- Asset inventories
- Configuration baselines
- Risk registers
- Risk treatment plans
- Incident response plans
- Incident playbooks
- Business continuity plans
- Disaster recovery plans
- Disaster recovery runbooks
- Access-control documentation
- Change records
- Vulnerability reports
- Penetration-testing reports
- Vendor assessments
- Audit evidence
- Training records
- Exception records
- Risk acceptance records
- Security architecture documentation

The appropriate document depends on the question being answered.

---

## 8. System Security Plan

A **System Security Plan (SSP)** documents how a system is protected and how applicable security requirements are implemented.

It may describe:

- System purpose
- System boundaries
- Architecture
- Data processed
- Security controls
- Roles
- Authentication
- Access control
- Network protections
- Monitoring
- Incident response
- Backup
- Configuration management

The exact format depends on the organization and applicable framework.

An SSP is particularly useful for demonstrating how security requirements apply to a particular system.

---

## 9. Network Diagrams

Network diagrams document the architecture and connectivity of systems.

They may show:

- Routers
- Switches
- Firewalls
- Servers
- Endpoints
- DMZs
- VPN connections
- Cloud environments
- Network segments
- Internet connections
- Security controls

A useful network diagram can support:

- Troubleshooting
- Incident response
- Architecture review
- Change management
- Disaster recovery
- Risk analysis

### Security concern

Network diagrams can also reveal sensitive information.

If an attacker obtains a detailed diagram, it may reveal:

- Critical servers
- Security devices
- Trust boundaries
- Management networks
- External connections

Therefore, diagrams should be appropriately classified and protected.

---

## 10. Data-Flow Diagrams

A **data-flow diagram (DFD)** focuses on how information moves between:

- Users
- Applications
- Databases
- APIs
- External systems
- Third parties

It is especially useful for understanding:

- Trust boundaries
- Data processing
- Sensitive data movement
- Third-party integrations
- Encryption requirements
- Privacy requirements

A network diagram answers:

> How are systems connected?

A data-flow diagram answers:

> How does information move through the system?

These can complement each other.

---

## 11. Asset Inventories

An asset inventory documents organizational assets.

It may contain:

- Asset identifier
- Hostname
- IP address
- Owner
- Location
- System type
- Software
- Business function
- Classification
- Criticality
- Lifecycle state

An accurate inventory supports:

- Vulnerability management
- Patch management
- Incident response
- Risk assessment
- Compliance
- Decommissioning

You cannot reliably protect assets you do not know exist.

---

## 12. Configuration Documentation

Configuration documentation records how systems are configured.

Examples:

- Firewall rules
- Server settings
- Cloud configurations
- IAM configuration
- Security-tool settings
- Network settings
- Application settings

Configuration documentation helps administrators determine:

> What should this system look like?

This is particularly useful when combined with a **secure baseline**.

---

## 13. Baselines

A **security baseline** defines an approved configuration state.

Examples:

- Required Windows security settings
- Approved Linux configuration
- Firewall baseline
- Browser configuration
- Cloud security baseline

Documentation should identify the expected state.

If a system deviates from the baseline, the organization can investigate whether the change is:

- Authorized
- Unintentional
- Malicious
- Temporary
- Required for a business purpose

---

## 14. Risk Registers

A **risk register** records identified risks and their management status.

Typical fields include:

- Risk ID
- Risk description
- Asset
- Threat
- Vulnerability
- Likelihood
- Impact
- Risk level
- Risk owner
- Treatment
- Due date
- Status
- Residual risk

The risk register provides organizational visibility into outstanding risk.

It should be maintained as risks change.

---

## 15. Risk Acceptance Records

When an organization chooses to accept a risk, the decision should be documented appropriately.

A risk acceptance record may identify:

- Risk
- Business impact
- Existing controls
- Residual risk
- Rationale
- Risk owner
- Approval
- Acceptance period
- Review date

This provides accountability.

A security analyst should not silently decide:

> "The risk is acceptable."

Risk acceptance is generally a management decision made by an appropriately authorized party.

---

## 16. Exception Records

Security policies and standards may occasionally require exceptions.

Examples:

- Legacy application cannot support MFA
- Operational technology cannot support a required patch
- Business system requires a temporary firewall rule
- Vendor integration requires a temporary configuration deviation

An exception record should document:

- Requirement being excepted
- Reason
- Scope
- Duration
- Risk
- Compensating controls
- Approver
- Expiration/review date

Exceptions should be controlled rather than becoming permanent undocumented deviations.

---

## 17. Compensating Controls

When the preferred control cannot be implemented, a **compensating control** may reduce the associated risk.

Example:

A legacy system cannot support modern authentication.

Possible compensating controls could include:

- Network isolation
- Restricted administrative access
- Additional monitoring
- Jump-host access
- Application allowlisting

The exception and compensating controls should be documented.

A compensating control does not mean:

> "We ignored the requirement."

It means:

> "The original control cannot be implemented as intended, so another control is being used to address the risk."

---

## 18. Change Records

Security-relevant changes should be documented.

A change record may include:

- Requestor
- System
- Requested change
- Business reason
- Risk assessment
- Testing
- Approval
- Implementation window
- Rollback plan
- Implementation result
- Validation

This creates traceability.

If a firewall rule suddenly allows inbound traffic, the organization should be able to determine:

- Who requested it
- Why it was needed
- Who approved it
- When it was implemented

---

## 19. Change Documentation and Incident Investigation

Change records are valuable during investigations.

Suppose a server begins generating unusual outbound traffic.

Investigators discover that a firewall rule was modified two hours earlier.

The change record may help determine whether the rule was:

- Authorized
- Misconfigured
- Related to the incident
- A malicious change

This demonstrates why documentation is part of operational security, not merely administrative paperwork.

---

## 20. Incident Response Documentation

Incident-response documentation can include:

- Incident response plan
- Incident response policy
- Playbooks
- Contact lists
- Escalation procedures
- Severity definitions
- Communication procedures
- Evidence-handling procedures
- Incident tickets
- Investigation timelines
- Lessons learned

### Plan vs Playbook

A plan establishes the overall response framework.

A playbook provides focused response instructions for a specific scenario.

Examples:

- Phishing playbook
- Ransomware playbook
- Malware playbook
- Account compromise playbook
- Data breach playbook

---

## 21. Incident Records

An incident record should preserve the important facts about an event.

It may contain:

- Detection time
- Reporter
- Affected assets
- Indicators
- Initial assessment
- Severity
- Actions taken
- Evidence
- Communications
- Containment
- Eradication
- Recovery
- Lessons learned

Accurate incident records support:

- Investigation
- Management reporting
- Compliance
- Legal review
- Lessons learned
- Future prevention

---

## 22. Chain of Custody Documentation

When evidence may be used for disciplinary, legal, or investigative purposes, chain of custody can be important.

Documentation may record:

- Evidence identifier
- Description
- Collection time
- Collection location
- Collector
- Hash value where applicable
- Transfer history
- Storage location
- Persons handling evidence
- Dates and times
- Reason for transfer

The objective is to demonstrate that evidence remained controlled and its integrity was maintained.

---

## 23. Audit Evidence

Audits require evidence that controls exist and operate.

Evidence may include:

- Policies
- Configuration screenshots
- System reports
- Access reviews
- Logs
- Tickets
- Change approvals
- Training records
- Vulnerability reports
- Incident records
- Vendor assessments

Strong evidence should be:

- Relevant
- Reliable
- Traceable
- Current
- Sufficient for the control being tested

A policy alone does not necessarily prove that a control is operating.

---

## 24. Policy vs Evidence

Consider this requirement:

> Privileged access must be reviewed quarterly.

A policy stating this requirement is evidence that the requirement exists.

But an auditor may also need:

- Quarterly review records
- Reviewer identity
- Review date
- Accounts reviewed
- Findings
- Remediation evidence

This demonstrates operation of the control.

Therefore:

**Policy = requirement**

**Record = evidence of activity**

---

## 25. Documentation as an Audit Trail

An audit trail provides traceability between actions and responsible parties.

For example:

**Request → Approval → Change → Validation → Record**

This allows an organization to reconstruct what happened.

Auditability is important for:

- Accountability
- Compliance
- Investigations
- Change management
- Fraud detection
- Security monitoring

---

## 26. Documentation Version Control

Security documents change over time.

Version control should identify:

- Document name
- Version
- Owner
- Approval status
- Effective date
- Review date
- Change history
- Previous version
- Next review

Example:

**Incident Response Plan v3.2**

Review date:

**2026-09-01**

Approved by:

**Security Management**

Change:

**Updated ransomware containment procedure**

This makes the authoritative version identifiable.

---

## 27. Document Ownership

Every important document should have an accountable owner.

The owner may be responsible for:

- Accuracy
- Review
- Approval coordination
- Updates
- Distribution
- Retention
- Version control

Without ownership, documents often become stale.

A document saying:

> "Last reviewed five years ago"

may no longer reflect the actual environment.

---

## 28. Document Review

Documents should be reviewed according to organizational requirements and whenever significant changes occur.

Triggers may include:

- New technology
- Major architecture changes
- New regulations
- New business processes
- Security incidents
- Audit findings
- Organizational restructuring
- New vendors
- Cloud migration

A fixed review schedule is useful, but event-driven review is also important.

---

## 29. Document Approval

Important documents should have appropriate approval.

Approval establishes that the organization accepts the requirements.

Examples:

- Security policy → management approval
- Technical standard → appropriate security/technical authority
- Incident response plan → appropriate stakeholders
- Business continuity plan → business leadership

The exact approval authority depends on organizational governance.

---

## 30. Document Distribution

Having a document is not enough.

Authorized personnel must be able to find and use the current version.

Organizations should consider:

- Central repository
- Access controls
- Searchability
- Version identification
- Distribution
- Offline availability where necessary
- Removal of obsolete copies

For incident response, critical documentation may need to remain available even if normal corporate systems are unavailable.

---

## 31. Out-of-Band Documentation

During a major security incident, normal infrastructure may be unavailable or compromised.

For example:

- Corporate email may be unavailable
- Identity services may be compromised
- File shares may be encrypted
- Collaboration platforms may be inaccessible

Therefore, critical response documentation may need an independent or otherwise resilient access method.

Examples:

- Offline emergency contact list
- Protected alternate repository
- Printed critical procedures
- Independent communication channel

The objective is resilience.

---

## 32. Secure Documentation

Documentation itself can contain sensitive information.

Examples:

- Network diagrams
- IP addresses
- Administrative procedures
- Architecture diagrams
- Incident details
- Personal information
- Vendor credentials
- Recovery procedures
- Security-tool configuration

Therefore, documentation should be protected according to its classification.

Controls may include:

- Least privilege
- MFA
- Encryption
- Access logging
- Version control
- Secure storage
- Retention controls

---

## 33. Never Store Secrets Carelessly

Operational documents sometimes become dangerous repositories for secrets.

Examples include:

- Passwords
- API keys
- Private keys
- Recovery codes
- Service-account credentials

Sensitive secrets should generally be stored in appropriate secret-management systems rather than ordinary documentation.

If a procedure says:

> "Use this password to access the server."

the password should not simply be embedded in a widely accessible document.

Instead, the procedure should reference the approved credential-management mechanism.

---

## 34. Records Retention

Records should be retained according to applicable:

- Legal requirements
- Regulatory requirements
- Contractual requirements
- Business requirements
- Organizational policies

Retention should not automatically mean:

> Keep everything forever.

Indefinite retention can create:

- Privacy risk
- Storage cost
- Legal discovery burden
- Increased breach impact
- Data-management complexity

Retention should be intentional.

---

## 35. Legal Hold

A **legal hold** may require an organization to preserve information that would otherwise be deleted under normal retention rules.

For example:

> A litigation process begins involving a particular transaction.

Relevant emails, records, and documents may need to be preserved.

Normal automated deletion may need to be suspended for affected information.

This is why retention and legal processes must be coordinated.

---

## 36. Secure Records Disposal

When retention requirements expire and no preservation requirement applies, records may need secure disposal.

Depending on the medium, this may involve:

- Secure deletion
- Media sanitization
- Cryptographic erasure
- Physical destruction

Disposal should be documented where required.

A disposal record may include:

- Data/system
- Date
- Method
- Responsible person
- Authorization
- Verification

---

## 37. Records Integrity

Important records should be protected against unauthorized alteration.

Controls may include:

- Access restrictions
- Immutable storage
- Digital signatures
- Hashing
- Write-once storage
- Audit logs
- Version control

This is particularly important for:

- Audit evidence
- Incident records
- Security logs
- Compliance records
- Legal evidence

If records can be silently modified, their evidentiary value decreases.

---

## 38. Documentation and Confidentiality

Some documents may reveal information that should not be broadly distributed.

For example, a penetration-test report may identify:

- Vulnerable systems
- Exploitable weaknesses
- Internal addresses
- Administrative interfaces
- Security-control gaps

Therefore, security documentation should not automatically be classified as public.

Access should be based on legitimate need.

---

## 39. Documentation and Integrity

Documentation must remain accurate.

A stale network diagram can be worse than having no diagram because responders may trust incorrect information.

For example:

Documentation says:

> Firewall A protects the database network.

The actual environment changed six months ago and the database is now behind Firewall B.

During an incident, responders may make incorrect decisions based on obsolete documentation.

Therefore:

**Accuracy + currency = operational value**

---

## 40. Documentation and Availability

Security documentation must also be available when needed.

This creates a three-part security requirement:

**Confidentiality + Integrity + Availability**

Examples:

- Confidentiality → restrict access to sensitive architecture documents.
- Integrity → prevent unauthorized modifications.
- Availability → ensure responders can access critical procedures during incidents.

This is especially important for:

- Incident response
- Disaster recovery
- Business continuity
- Emergency contacts
- Recovery procedures

---

## 41. Documentation Dependencies

Some documents depend on others.

For example:

**Asset inventory**
→ supports vulnerability management

**Network diagram**
→ supports incident investigation

**Data-flow diagram**
→ supports privacy analysis

**Risk register**
→ supports risk reporting

**Configuration baseline**
→ supports configuration monitoring

**Incident response plan**
→ supports incident handling

**DR plan**
→ supports recovery

Documentation should therefore be treated as an interconnected system.

---

## 42. Documentation During System Changes

Major technology changes should trigger documentation updates.

Examples:

- New cloud environment
- New firewall
- New application
- New data store
- Network redesign
- New vendor
- Identity-platform migration
- New backup architecture

A common failure is:

> Infrastructure changes but documentation does not.

This creates **configuration/documentation drift**.

---

## 43. Documentation Drift

Documentation drift occurs when documentation no longer matches reality.

Examples:

- Old IP addresses
- Removed servers still listed
- Missing cloud resources
- Incorrect firewall topology
- Former employees listed as administrators
- Outdated vendor contacts

Drift can create:

- Incident-response delays
- Audit findings
- Configuration errors
- Security gaps
- Incorrect risk assessments

Documentation should therefore be maintained as part of change management.

---

## 44. Runbooks

A **runbook** provides operational instructions for recurring technical tasks.

Examples:

- Restarting a failed service
- Rotating certificates
- Recovering a server
- Isolating an endpoint
- Restoring a database
- Performing a failover

Runbooks should be:

- Clear
- Tested
- Version-controlled
- Owned
- Updated

A runbook is especially valuable when a task must be performed correctly under pressure.

---

## 45. Playbook vs Runbook

These terms can overlap in real organizations, but a useful distinction is:

### Playbook

Focuses on responding to a scenario.

Example:

**Ransomware Response Playbook**

### Runbook

Focuses on executing a technical operational task.

Example:

**Database Failover Runbook**

A Security+ scenario may use these terms differently depending on organizational context, so focus on the described purpose.

---

## 46. Standard Operating Procedures

A **Standard Operating Procedure (SOP)** documents a repeatable process.

Examples:

- Employee onboarding
- Employee offboarding
- Access review
- Vulnerability scanning
- Patch deployment
- Security incident escalation

An SOP reduces variation between personnel and shifts.

---

## 47. Knowledge Transfer

Documentation is particularly important when:

- Employees leave
- Teams change
- Systems are transferred
- Vendors change
- On-call rotations change

Good documentation prevents organizational knowledge from disappearing when an individual leaves.

This is one reason documentation is an operational resilience control.

---

## 48. Security Documentation and Third Parties

Vendor relationships create additional documentation requirements.

Records may include:

- Security questionnaires
- Contracts
- Security clauses
- SLAs
- SOC reports
- Assessment results
- Vendor contacts
- Incident notification procedures
- Data-processing agreements
- Offboarding records

Third-party documentation should identify responsibilities and evidence.

---

## 49. Documentation and Compliance

Compliance programs often require evidence.

For example, an organization may need to demonstrate:

- Policy approval
- Access reviews
- Security training
- Vulnerability remediation
- Change approval
- Incident handling
- Vendor assessments

The organization therefore needs records that demonstrate that required activities actually occurred.

A key principle is:

> **If a control is required, the organization should be able to demonstrate how it is implemented and provide appropriate evidence that it operates.**

---

## 50. Documentation and Metrics

Security metrics depend on reliable records.

For example:

> "Critical vulnerabilities are remediated within 15 days."

To measure this, the organization needs reliable records of:

- Vulnerability discovery date
- Severity
- Asset
- Remediation date
- Exceptions
- Validation

Poor documentation produces unreliable metrics.

---

## 51. Documentation and Automation

Automation can improve documentation consistency.

Examples:

- Automatically generating asset inventories
- Recording change events
- Generating compliance reports
- Recording access-review results
- Automatically creating incident tickets
- Capturing configuration snapshots

However, automation should not be assumed to make records correct automatically.

Automated data can still be:

- Incomplete
- Misconfigured
- Incorrect
- Stale

Organizations should validate important records.

---

## 52. Documentation Quality

Good security documentation should be:

### Accurate

It reflects the actual environment.

### Current

It is updated after relevant changes.

### Complete

It contains enough information for its intended purpose.

### Clear

Authorized users can understand it.

### Controlled

Changes are managed.

### Traceable

The source, owner, version, and history can be identified.

### Accessible

Authorized personnel can retrieve it when needed.

### Protected

Sensitive information is appropriately secured.

---

## 53. Common Documentation Failures

### Failure 1: No Owner

Nobody is accountable for keeping the document current.

### Failure 2: No Review Date

Documents become obsolete without anyone noticing.

### Failure 3: Multiple Uncontrolled Copies

Personnel use different versions.

### Failure 4: Excessive Detail in Policies

Policies become difficult to maintain because they contain implementation-specific instructions.

### Failure 5: Insufficient Procedure Detail

A procedure is so vague that two administrators perform the task differently.

### Failure 6: Sensitive Information in Public Documentation

Architecture or credentials are exposed unnecessarily.

### Failure 7: Documentation Updated After the Fact

Important changes are made but never recorded.

### Failure 8: No Evidence

The organization has a policy but cannot demonstrate that it is implemented.

### Failure 9: Indefinite Retention

Records are retained without considering legal, privacy, or business requirements.

### Failure 10: No Emergency Access

Critical documentation is stored only on infrastructure that may be unavailable during a major incident.

---

## 54. Detailed Security+ Scenario 1 — Policy or Procedure?

Management states:

> All employees must report suspected phishing attempts.

Question:

What document establishes the mandatory organizational requirement?

**Policy.**

If the question instead asks:

> What exact steps should an employee follow to report the email?

That points toward a **procedure**.

---

## 55. Detailed Security+ Scenario 2 — Standard or Guideline?

The organization states:

> Administrative accounts must use MFA.

This is a mandatory requirement and is appropriate for a standard when expressed as a technical specification.

If the statement says:

> Administrators should avoid using privileged accounts for routine activities.

That is more consistent with a **guideline**.

The key distinction is mandatory vs recommended.

---

## 56. Detailed Security+ Scenario 3 — Documentation Drift

A firewall was replaced six months ago.

The network diagram still shows the old firewall.

During an incident, responders use the old diagram and investigate the wrong device.

The problem is:

**Documentation drift.**

The solution involves integrating documentation updates with change management and validating the current architecture.

---

## 57. Detailed Security+ Scenario 4 — Audit Evidence

An organization has a policy requiring quarterly access reviews.

An auditor asks:

> Show evidence that quarterly reviews actually occurred.

The organization should provide appropriate records such as:

- Completed reviews
- Dates
- Reviewers
- Accounts reviewed
- Findings
- Remediation

The policy alone does not prove operation.

---

## 58. Detailed Security+ Scenario 5 — Sensitive Documentation

A penetration-testing report contains exploitable vulnerabilities and internal addresses.

Should it be posted publicly for transparency?

No.

The report should be protected according to its sensitivity and shared only with authorized personnel.

The security principle is:

**Protect documentation itself as an information asset.**

---

## 59. Detailed Security+ Scenario 6 — Incident Documentation

During a ransomware incident, the normal file server is encrypted.

The incident response team cannot access the response plan stored on that file server.

This demonstrates a documentation availability failure.

Critical incident documentation should have a resilient access mechanism that remains available during major incidents.

---

## 60. Detailed Security+ Scenario 7 — Risk Acceptance

A legacy system cannot support a required security control.

Management decides to accept the residual risk temporarily.

The organization should document:

- Risk
- Reason
- Residual exposure
- Approver
- Expiration/review date
- Compensating controls where applicable

This creates accountability.

---

## 61. Detailed Security+ Scenario 8 — Legal Hold

An organization normally deletes email after a defined retention period.

A legal matter requires preservation of relevant email.

The normal deletion process should not destroy information subject to the applicable legal hold.

The organization must coordinate retention processes with legal requirements.

---

## 62. Detailed Security+ Scenario 9 — Secrets in Documentation

An administrator stores a production database password in a shared troubleshooting document.

This creates unnecessary credential exposure.

The password should be stored and retrieved through an approved secrets-management mechanism.

The documentation should explain the process without unnecessarily exposing the secret.

---

## 63. Detailed Security+ Scenario 10 — Change Record

A server suddenly stops receiving traffic.

An investigation shows that a firewall rule was changed.

The change-management record can help determine:

- Who requested the change
- Who approved it
- Why it was made
- When it occurred
- Whether testing was performed
- Whether rollback was planned

This demonstrates the security value of change records.

---

## 64. Security+ Exam Distinctions and Traps

### Policy vs Standard

**Policy:** management-level requirement and direction.

**Standard:** mandatory specific requirement used to implement policy.

### Standard vs Guideline

**Standard:** mandatory.

**Guideline:** recommended.

### Procedure vs Policy

**Procedure:** how to perform an activity.

**Policy:** what is required and why.

### Documentation vs Record

**Documentation:** describes requirements, systems, or processes.

**Record:** evidence that an event, activity, or decision occurred.

### Network Diagram vs Data-Flow Diagram

**Network diagram:** system/network connectivity.

**DFD:** movement and processing of information.

### Runbook vs Playbook

**Runbook:** operational execution of a task.

**Playbook:** response approach for a particular scenario.

### Policy vs Evidence

A policy demonstrates that a requirement exists.

A record demonstrates that an activity occurred.

### Retention vs Legal Hold

**Retention:** normal lifecycle requirement.

**Legal hold:** preservation requirement that can override normal deletion for affected information.

### Risk Acceptance vs Risk Mitigation

**Risk acceptance:** authorized decision to tolerate residual risk.

**Risk mitigation:** action to reduce risk.

---

## 65. Security+ Decision Framework

When a scenario involves security documentation, ask:

### Step 1 — What information is being requested?

Is it:

- Requirement?
- Technical specification?
- Procedure?
- Recommendation?
- Evidence?
- Architecture?
- Risk?
- Incident information?

### Step 2 — Who needs it?

Determine the authorized audience.

### Step 3 — What sensitivity does it have?

Apply appropriate classification.

### Step 4 — Is it authoritative?

Determine the current approved version.

### Step 5 — Is it current?

Check review date and recent changes.

### Step 6 — Does it need evidence?

If the question asks whether a control operated, look for records rather than only policies.

### Step 7 — Is there a legal or retention requirement?

Check retention and legal-hold requirements.

### Step 8 — Does the document contain secrets?

Credentials and keys should not be casually embedded in ordinary documentation.

### Step 9 — Is the documentation available during failure?

Critical operational documents should remain accessible during incidents and outages.

### Step 10 — Is the documentation connected to change management?

Major system changes should trigger appropriate documentation updates.

---

## 66. Complete Documentation Lifecycle

A mature documentation process can be represented as:

**Identify requirement**
↓
**Create document**
↓
**Assign owner**
↓
**Classify**
↓
**Review**
↓
**Approve**
↓
**Publish**
↓
**Control access**
↓
**Use**
↓
**Capture records/evidence**
↓
**Review/update**
↓
**Archive**
↓
**Retain**
↓
**Securely dispose**

This lifecycle prevents documentation from becoming a static file that nobody maintains.

---

## 67. Practical Example — Firewall Documentation

Consider an enterprise firewall.

### Before deployment

Document:

- Architecture
- Zones
- Interfaces
- Traffic requirements
- Security objectives
- Approved rules

### During deployment

Record:

- Change request
- Approval
- Configuration
- Testing
- Validation

### During operation

Maintain:

- Configuration baseline
- Rule reviews
- Logs
- Exceptions
- Change records

### During an incident

Use:

- Current network diagram
- Firewall configuration
- Logs
- Change records
- Incident procedures

### During retirement

Document:

- Decommissioning approval
- Data handling
- Configuration removal
- Asset status
- Final records

This demonstrates documentation throughout the operational lifecycle.

---

## 68. Practical Example — Incident Response Documentation

Suppose an endpoint is suspected of malware infection.

The response process may rely on:

**Incident response plan**
→ defines overall response responsibilities.

**Malware playbook**
→ defines the scenario-specific response.

**Endpoint isolation procedure**
→ explains technical steps.

**Network diagram**
→ identifies relevant infrastructure.

**Asset inventory**
→ identifies system owner and criticality.

**Incident ticket**
→ records actions and findings.

**Evidence record**
→ documents collected evidence.

**Lessons-learned report**
→ identifies improvements.

No single document contains the entire operational picture.

---

## 69. Final Mental Model

Remember the hierarchy:

**Policy**
→ What management requires.

**Standard**
→ What mandatory specification must be followed.

**Procedure**
→ How the activity is performed.

**Guideline**
→ What is recommended.

Then remember the evidence side:

**Record**
→ What actually happened.

And the architecture side:

**Diagram**
→ What exists and how it connects.

Then the governance side:

**Owner**
→ Who is accountable.

**Version**
→ Which document is authoritative.

**Retention**
→ How long it must be kept.

**Access control**
→ Who may view or modify it.

**Integrity**
→ How unauthorized changes are prevented or detected.

**Availability**
→ Whether it can be retrieved when needed.

The central Security+ principle is:

> **Security documentation is an operational security control: it establishes requirements, preserves institutional knowledge, provides evidence, supports investigations and recovery, and creates accountability.**

## Key Takeaways

- Documentation converts security requirements and operational knowledge into repeatable practices.
- **Policy = what/why.**
- **Standard = mandatory specification.**
- **Procedure = how.**
- **Guideline = recommended practice.**
- Documentation and records are related but not identical.
- A policy establishes a requirement; a record can demonstrate that an activity occurred.
- Network diagrams document connectivity; data-flow diagrams document information movement.
- Asset inventories support vulnerability management, incident response, risk management, and compliance.
- Configuration baselines establish approved states against which deviations can be identified.
- Risk registers provide visibility into identified risks and treatment.
- Risk acceptance should be authorized and documented.
- Exceptions should identify scope, reason, duration, risk, approval, and compensating controls where applicable.
- Change records provide traceability and are valuable during investigations.
- Incident plans, playbooks, procedures, tickets, and evidence records serve different purposes.
- Chain-of-custody records help demonstrate control and integrity of evidence.
- Audit evidence should demonstrate both the existence and, where required, operation of controls.
- Documents should have owners, versions, approval status, review dates, and change history.
- Documentation must be protected because it may contain sensitive architecture, personal information, or security details.
- Credentials, API keys, and private keys should not be casually stored in ordinary documentation.
- Critical documentation must remain available during incidents and outages.
- Records should be retained according to legal, regulatory, contractual, and organizational requirements.
- Legal holds can override normal deletion for relevant information.
- Documentation drift creates operational and security risk.
- Change management should trigger appropriate documentation updates.
- Good documentation is **accurate, current, complete, clear, controlled, traceable, accessible, and protected**.
- The overall lifecycle is:
  **Create → Own → Classify → Approve → Publish → Use → Record → Review → Update → Retain → Dispose**
- The goal is not to create documentation for its own sake; the goal is to ensure that security requirements, operational decisions, evidence, and institutional knowledge remain usable, trustworthy, and accountable.
