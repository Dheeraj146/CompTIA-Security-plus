# Disaster Recovery and Incident Response Planning

## 1. Purpose of Disaster Recovery and Incident Response Planning

Organizations cannot assume that preventive security controls will stop every disruptive event. Even a well-designed environment can experience:

- Ransomware
- Major cyberattacks
- Data corruption
- Hardware failure
- Cloud outages
- Power failures
- Natural disasters
- Fire or flooding
- Critical supplier outages
- Insider incidents
- Loss of a facility
- Destructive administrative mistakes

Because of this, organizations need documented plans that explain **what happens when prevention fails**.

Two important planning disciplines are:

- **Disaster Recovery (DR):** restoring technology, systems, services, and data after a major disruption.
- **Incident Response (IR):** managing and responding to security incidents.

Both support business continuity, but they solve different problems.

A useful mental model is:

**Business Continuity → Keep critical business functions operating**

**Disaster Recovery → Restore technology and services**

**Incident Response → Manage the security incident**

These activities can occur at the same time.

---

## 2. Disaster Recovery Fundamentals

**Disaster recovery** is the process of restoring critical technology capabilities after a disruptive event.

A DR plan should answer questions such as:

- What systems must be recovered?
- In what order?
- Where will they be recovered?
- Which people are responsible?
- What dependencies must be restored first?
- Which backups or replicas will be used?
- What are the RTO and RPO?
- How will recovery be validated?
- How will the organization communicate during recovery?
- How will normal operations be restored after temporary recovery?

DR is therefore more than "restore the backup."

A complete recovery process considers the **entire service dependency chain**.

---

## 3. DR Planning and the BIA

Disaster recovery priorities should be derived from the **Business Impact Analysis (BIA)**.

The BIA identifies:

- Critical business processes
- Business impacts
- Dependencies
- Maximum tolerable disruption
- RTO
- RPO
- Recovery priorities

The DR plan translates those requirements into technical recovery procedures.

The relationship can be represented as:

**BIA → Recovery Requirements → DR Strategy → DR Procedures → Testing → Improvement**

For example:

The BIA determines that an order-processing system has an RTO of 2 hours and an RPO of 15 minutes.

The DR team must then design an architecture capable of meeting those requirements.

The BIA establishes **what the business requires**.

DR determines **how technology will support those requirements**.

---

## 4. Recovery Objectives

### Recovery Time Objective (RTO)

**RTO** defines the targeted maximum amount of time to restore a service or process.

Example:

> RTO = 4 hours

The recovery strategy should aim to restore the service within four hours.

### Recovery Point Objective (RPO)

**RPO** defines the maximum acceptable amount of data loss measured in time.

Example:

> RPO = 30 minutes

The recovery solution should allow the organization to recover to a point no more than approximately 30 minutes before the disruption.

### Maximum Tolerable Downtime (MTD)

**MTD/MTPD** is the maximum period the business can tolerate disruption before consequences become unacceptable.

A common relationship is:

**RTO < MTD**

RTO is the target; MTD is the outer business tolerance.

---

## 5. DR Strategies

Different recovery strategies provide different combinations of cost, recovery speed, complexity, and resilience.

### Backups

Backups provide recoverable copies of data or systems.

They are particularly important for:

- Data corruption
- Accidental deletion
- Ransomware recovery
- Hardware failure
- Disaster recovery

However, backup alone may not satisfy a very short RTO.

### Replication

Replication maintains copies of data or workloads in another location or system.

Replication can reduce recovery time, but it must be designed carefully.

If malicious or corrupted data is replicated immediately, the secondary copy may also contain the problem.

### Failover

Failover moves service operation from a failed primary component to a secondary component.

Examples:

- Database failover
- Server clustering
- Network failover
- Cloud service failover

Failover can provide rapid recovery, but it requires correctly configured and tested secondary infrastructure.

### Alternate Sites

Organizations can use:

- Hot sites
- Warm sites
- Cold sites

The appropriate option depends on recovery requirements and cost constraints.

---

## 6. Backup Strategy

A DR plan should define how backups are created, protected, retained, and restored.

Important considerations include:

- Backup frequency
- Backup type
- Retention period
- Storage location
- Encryption
- Access controls
- Integrity verification
- Restoration testing
- Offline or immutable copies
- Geographic separation

The backup strategy must match the required RPO.

For example:

If the organization requires an RPO of 15 minutes, taking one backup every 24 hours clearly does not satisfy that requirement.

---

## 7. Backup Types

### Full Backup

A full backup copies the complete selected dataset.

Advantages:

- Simple restoration
- Self-contained recovery point

Disadvantages:

- Requires more storage
- Takes longer to create

### Incremental Backup

An incremental backup stores changes since the previous backup of any type.

Advantages:

- Faster backups
- Lower storage consumption

Disadvantage:

- Restoration may require the full backup and multiple incremental backups.

### Differential Backup

A differential backup stores changes since the last full backup.

Advantages:

- Restoration is generally simpler than a long incremental chain.

Disadvantage:

- Each differential grows as more changes occur.

The backup method should be selected according to recovery requirements, storage capacity, operational complexity, and RPO/RTO.

---

## 8. The 3-2-1 Backup Principle

A common backup resilience principle is:

**3 copies of data**

**2 different types of storage/media**

**1 copy stored off-site**

The purpose is to avoid depending on a single copy or failure domain.

Modern ransomware-resistant strategies often extend this concept with:

- Offline copies
- Immutable backups
- Air-gapped recovery copies
- Separate administrative credentials
- Independent backup infrastructure

The security objective is not simply to have multiple copies. The copies should remain recoverable if production systems or administrative credentials are compromised.

---

## 9. Immutable and Offline Backups

### Immutable Backup

An immutable backup is protected against modification or deletion for a defined period.

This can help protect recovery points from:

- Ransomware
- Malicious administrators
- Compromised backup accounts
- Accidental deletion

### Offline Backup

An offline backup is not continuously connected to the production environment.

This reduces the possibility that a compromise of the production environment automatically reaches the backup.

### Important distinction

A backup stored in another folder on the same compromised system is not equivalent to an independent recovery copy.

The organization must consider **failure domains and administrative dependencies**.

---

## 10. Backup Encryption and Key Management

Backups can contain highly sensitive information.

Therefore, organizations should consider:

- Encryption at rest
- Encryption during transfer
- Strong access controls
- Separate backup credentials
- Key management
- Key rotation where appropriate
- Recovery access procedures

Encryption creates an important dependency:

> If encrypted backups exist but the organization cannot access the required keys, recovery may fail.

Therefore, key-management continuity must be included in DR planning.

---

## 11. Recovery Sequence

A DR plan should define the order in which systems are recovered.

A generic sequence may look like:

1. Assess the incident/disaster
2. Declare or activate the appropriate recovery plan
3. Establish communications
4. Stabilize or secure the recovery environment
5. Restore foundational infrastructure
6. Restore identity and authentication dependencies
7. Restore networking and DNS
8. Restore storage and databases
9. Restore critical applications
10. Restore supporting applications
11. Validate data and application functionality
12. Validate security controls
13. Resume business operations
14. Monitor the recovered environment
15. Return to normal operations when appropriate

The exact order depends on the architecture.

For example, an application may require:

**Network → DNS → Identity → Database → Application**

Trying to restore the application first may not produce a usable service.

---

## 12. Recovery Dependencies

Recovery planning must identify upstream and downstream dependencies.

Examples:

**Application**
→ Database

**Database**
→ Storage

**Users**
→ Identity provider

**Applications**
→ DNS

**Remote users**
→ Internet/VPN

**Cloud workload**
→ Cloud identity and management plane

**Payment application**
→ Payment processor

This means DR should be designed around **business services**, not isolated servers.

---

## 13. Recovery Validation

Recovery is not complete merely because a server starts.

Validation should confirm:

### Availability

Can users access the service?

### Integrity

Is the recovered data correct and complete?

### Functionality

Does the application actually perform required business operations?

### Security

Are:

- Authentication controls working?
- Authorization controls working?
- Logging enabled?
- Monitoring functioning?
- Endpoint protection active?
- Network controls correctly configured?

### Data consistency

Are related systems synchronized correctly?

For example, restoring a database without validating application-to-database consistency can produce operational errors.

---

## 14. Failover and Failback

### Failover

**Failover** moves operations from the primary environment to a secondary environment.

Example:

**Primary data center fails → Secondary data center becomes active**

### Failback

**Failback** returns operations from the secondary environment to the primary environment after the primary environment has been repaired.

A complete DR plan should address both.

Failback must be carefully controlled because moving workloads back can introduce:

- Data synchronization problems
- Configuration differences
- New outages
- Unexpected dependencies

---

## 15. Disaster Recovery Sites

### Hot Site

A hot site is already equipped and relatively ready for operational use.

**Strength:** Fast recovery.

**Trade-off:** Higher cost and operational complexity.

### Warm Site

A warm site has significant infrastructure but requires additional preparation.

**Strength:** Balance between cost and recovery speed.

**Trade-off:** Requires activation and configuration work.

### Cold Site

A cold site provides facilities but requires substantial setup.

**Strength:** Lower cost.

**Trade-off:** Slow recovery.

Security+ questions often test the relationship between **recovery speed and cost**.

---

## 16. Cloud Disaster Recovery

Cloud platforms can support DR through:

- Cross-region replication
- Availability zones
- Infrastructure as Code
- Automated deployment
- Snapshots
- Object-storage backups
- Managed databases
- Replication
- Automated failover

However, cloud DR has dependencies.

Organizations should consider:

- Cloud account access
- Identity provider availability
- DNS
- Network connectivity
- Encryption keys
- Secrets
- API access
- Provider availability
- Region failures
- Configuration recovery

A cloud backup is not automatically a complete DR strategy.

---

## 17. Infrastructure as Code for Recovery

**Infrastructure as Code (IaC)** can help organizations rebuild infrastructure consistently.

Instead of manually creating every server and network component, the organization can maintain declarative definitions for:

- Networks
- Security groups
- Servers
- Databases
- IAM configurations
- Load balancers
- Monitoring

During recovery, infrastructure can potentially be recreated from controlled definitions.

However, IaC must itself be protected.

If the IaC repository is compromised, recovery infrastructure could be deployed with malicious configuration.

Therefore, protect:

- Source repositories
- CI/CD pipelines
- Deployment credentials
- Secrets
- Infrastructure definitions

---

## 18. Incident Response Planning

**Incident Response (IR)** is the structured process used to prepare for, detect, analyze, contain, eradicate, and recover from security incidents.

An IR plan defines:

- Roles
- Responsibilities
- Authority
- Escalation
- Communication
- Investigation
- Evidence handling
- Containment
- Eradication
- Recovery
- Documentation
- Post-incident improvement

The objective is to avoid improvising critical decisions during a security incident.

---

## 19. Incident Response Lifecycle

A common lifecycle can be represented as:

**Preparation**
↓
**Detection and Analysis**
↓
**Containment**
↓
**Eradication**
↓
**Recovery**
↓
**Post-Incident Activity**

Different frameworks may use different terminology or combine phases, but the underlying objectives remain similar.

---

## 20. Preparation

Preparation occurs before an incident.

It includes:

- Creating IR policies
- Defining roles
- Creating playbooks
- Establishing communication channels
- Deploying logging and monitoring
- Maintaining contact lists
- Training responders
- Establishing forensic capabilities
- Preparing backup and recovery mechanisms
- Testing response procedures
- Establishing legal and regulatory escalation procedures

Preparation determines how quickly the organization can act when an incident occurs.

---

## 21. Incident Response Roles

An incident-response team may include:

- SOC analysts
- Incident responders
- Security engineers
- System administrators
- Network engineers
- Digital forensics specialists
- Malware analysts
- IT leadership
- Legal counsel
- Privacy personnel
- Human resources
- Public relations
- Executive management
- Vendor representatives

The exact structure depends on organizational size.

A critical principle is **role clarity**.

People should know:

- Who declares an incident
- Who can isolate systems
- Who approves major containment actions
- Who communicates externally
- Who contacts regulators
- Who preserves evidence
- Who authorizes recovery

---

## 22. Detection and Analysis

An incident may begin as:

**Event → Alert → Investigation → Incident**

Not every security event is an incident.

For example:

A failed login is an event.

A SIEM rule detecting hundreds of failed logins may generate an alert.

Investigation may determine that the activity is a password attack against a real account.

If confirmed as a security incident, the organization enters the appropriate incident-response process.

---

## 23. Incident Triage

Triage determines:

- Is this a real incident?
- What happened?
- Which systems are affected?
- Which accounts are affected?
- Is the attacker still active?
- What is the severity?
- What is the potential business impact?
- What evidence must be preserved?
- Who must be notified?

A SOC analyst should avoid immediately taking destructive actions before understanding the situation when evidence preservation or containment requirements matter.

---

## 24. Incident Severity

Organizations commonly classify incidents according to factors such as:

- Number of affected systems
- Criticality of affected assets
- Data sensitivity
- Privilege level of compromised accounts
- Attacker persistence
- Business impact
- Regulatory implications
- Safety impact
- Public exposure

For example:

A compromise of a noncritical test workstation may require a different escalation path than compromise of a domain administrator account.

Severity should be based on **impact and risk**, not merely the number of alerts.

---

## 25. Containment

Containment limits the damage and prevents an incident from spreading.

Examples:

- Isolating an endpoint
- Blocking malicious IP addresses
- Disabling a compromised account
- Revoking credentials
- Blocking malicious domains
- Segmenting affected systems
- Removing network access
- Quarantining a host

### Short-Term Containment

Designed to quickly limit immediate damage.

Example:

> Isolate a ransomware-infected endpoint from the network.

### Long-Term Containment

Provides more controlled stabilization while investigation continues.

Example:

> Move an affected application into a restricted network segment while responders investigate the root cause.

Containment decisions must balance security with business availability and evidence preservation.

---

## 26. Eradication

**Eradication** removes the cause or persistence mechanism of the incident.

Examples:

- Remove malware
- Remove malicious persistence
- Patch the exploited vulnerability
- Disable compromised accounts
- Remove unauthorized scheduled tasks
- Delete malicious services
- Rotate compromised credentials
- Remove attacker-created access paths

Eradication should address the **root cause**, not merely the visible symptom.

For example:

If malware entered through an unpatched vulnerability, deleting the malware without patching the vulnerability leaves the attack path open.

---

## 27. Reimaging vs Cleaning

For heavily compromised endpoints, organizations may choose to **reimage** the system rather than attempting to manually clean every artifact.

Reimaging can provide greater confidence that malicious software and persistence have been removed, assuming the recovery image and process are trusted.

However, evidence may need to be preserved before rebuilding.

This creates an important relationship:

**Preserve evidence → Contain → Eradicate/reimage → Recover**

The exact sequence depends on the incident and organizational procedures.

---

## 28. Recovery

Recovery returns affected systems to trusted operational status.

Activities can include:

- Restoring from trusted backups
- Rebuilding systems
- Restoring applications
- Resetting credentials
- Reconnecting systems
- Validating configurations
- Monitoring for reinfection
- Confirming business functionality

Recovery should not simply mean "turn the system back on."

The organization should verify that the original attack path has been addressed.

---

## 29. Post-Incident Activity

After the incident, the organization should conduct a lessons-learned review.

Questions include:

- What happened?
- When did it begin?
- How was it detected?
- What controls worked?
- What controls failed?
- Why was it possible?
- How long did containment take?
- Was evidence preserved correctly?
- Were communications effective?
- Were recovery objectives achieved?
- What should change?

The goal is not merely to document the incident.

The goal is to **reduce the probability or impact of recurrence**.

---

## 30. Root Cause Analysis

Root cause analysis attempts to identify why the incident was possible.

Example:

Observed problem:

> Employee workstation infected with ransomware.

Possible deeper causes:

- Phishing email reached the user
- Malicious attachment executed
- Macro/script controls were insufficient
- Endpoint detection did not alert
- User had excessive privileges
- Network segmentation was weak
- Backup protection was inadequate

The visible malware infection is not necessarily the root cause.

A good investigation looks through the entire attack chain.

---

## 31. Incident Communications

Incident communication must be planned before an incident.

Potential audiences include:

- Technical responders
- Management
- Executives
- Legal
- Privacy teams
- Employees
- Customers
- Suppliers
- Regulators
- Law enforcement
- Media/public

Different audiences require different information.

### Need-to-Know

Sensitive incident information should be provided according to:

- Authorization
- Role
- Business need
- Legal requirements

Responders should avoid uncontrolled disclosure of sensitive technical or personal information.

---

## 32. Out-of-Band Communication

If the organization's normal communication infrastructure may be compromised, unavailable, or monitored by an attacker, responders may need an **out-of-band communication channel**.

Examples can include:

- Separate emergency communications
- Alternate telephone systems
- Independent collaboration mechanisms
- Pre-established emergency contact procedures

The key idea is that the backup communication mechanism should not depend entirely on the compromised infrastructure.

---

## 33. Legal and Regulatory Coordination

Certain incidents may trigger:

- Breach notification requirements
- Contractual notification requirements
- Regulatory reporting
- Law-enforcement involvement
- Legal preservation requirements

Security teams should not independently make legal determinations.

Organizations should define escalation paths involving:

- Legal counsel
- Privacy personnel
- Compliance
- Management

This is especially important when personal, financial, healthcare, or regulated information is involved.

---

## 34. Evidence Preservation

Incident response and digital forensics often overlap.

If an incident may require investigation, organizations should consider:

- Preserving relevant logs
- Capturing volatile evidence when appropriate
- Protecting original evidence
- Recording collection details
- Maintaining chain of custody
- Hashing acquired evidence where appropriate

A responder should avoid unnecessarily destroying evidence through careless actions.

For example, immediately wiping a compromised system may remove valuable forensic information.

The correct action depends on the incident, business impact, evidence requirements, and organizational procedures.

---

## 35. Incident Response Playbooks

A **playbook** provides predefined steps for a specific type of incident.

Examples:

- Phishing playbook
- Ransomware playbook
- Malware infection playbook
- Account compromise playbook
- Data exfiltration playbook
- DDoS playbook
- Cloud compromise playbook

A good playbook defines:

- Trigger conditions
- Investigation steps
- Required evidence
- Decision points
- Containment actions
- Escalation requirements
- Communication requirements
- Recovery actions
- Closure criteria

Playbooks reduce uncertainty and improve consistency.

---

## 36. SOAR and Incident Response

Security Orchestration, Automation, and Response (**SOAR**) can automate repetitive incident-response activities.

For example:

**SIEM alert**
→ SOAR enriches IP reputation
→ Queries EDR
→ Checks affected account
→ Creates incident ticket
→ Requests analyst approval
→ Isolates endpoint

Automation can reduce response time.

However, high-impact actions should have appropriate safeguards.

For example, automatically disabling every account that generates a suspicious alert could create a significant business outage.

Therefore, automation should use:

- Confidence thresholds
- Approval gates
- Least privilege
- Logging
- Rollback procedures
- Exception handling

---

## 37. Incident Response Testing

An IR plan should be exercised.

Testing can include:

### Tabletop Exercise

Teams discuss a simulated incident.

Useful for testing:

- Roles
- Escalation
- Decision-making
- Communications
- Policy understanding

### Simulation

Participants respond to a more realistic scenario.

### Technical Exercise

Teams perform actual technical response actions.

Examples:

- Isolating an endpoint
- Blocking an indicator
- Restoring a system
- Rotating credentials

Testing identifies gaps before a real incident exposes them.

---

## 38. DR Testing

DR testing should verify whether systems can actually be recovered.

Possible activities include:

- Backup restoration
- Failover testing
- Alternate-site activation
- Database recovery
- Application recovery
- Network recovery
- Identity recovery
- Full recovery exercises

Important measurements include:

- Actual recovery time
- Actual data recovery point
- Recovery failures
- Dependency failures
- Personnel readiness

The organization should compare actual results with required RTO/RPO.

---

## 39. Incident Response vs Disaster Recovery

Consider a ransomware incident.

### Incident Response

The IR team:

1. Detects ransomware
2. Investigates affected systems
3. Determines scope
4. Contains infected endpoints
5. Identifies the initial access path
6. Removes persistence
7. Preserves evidence

### Disaster Recovery

The DR team:

1. Identifies trusted recovery points
2. Restores infrastructure
3. Restores databases
4. Restores applications
5. Validates systems
6. Returns services to operation

### Business Continuity

The business:

1. Activates alternate processes
2. Maintains critical customer services
3. Uses unaffected systems
4. Communicates with customers and suppliers

These activities are related but have different objectives.

---

## 40. Incident Response vs Business Continuity

**Incident Response asks:**

> How do we handle the security incident?

**Business Continuity asks:**

> How do we keep critical business functions operating?

For example, during a DDoS attack:

IR may investigate the attack and identify indicators.

BC may activate alternate customer-service procedures.

Network operations may reroute traffic.

DR may become involved if systems require restoration.

---

## 41. Incident Response vs Disaster Recovery vs Backup

These are frequently confused.

| Concept | Primary Purpose |
|---|---|
| Incident Response | Manage and respond to security incidents |
| Disaster Recovery | Restore technology and services |
| Backup | Provide recoverable copies of data |
| Business Continuity | Maintain critical business functions |

A backup is a **recovery resource**, not the entire DR program.

DR is a **recovery capability**, not the entire business continuity program.

IR is the **incident-management process**, not simply system restoration.

---

## 42. Detailed Security+ Scenario — Ransomware

A company discovers ransomware spreading across workstations.

The SOC confirms malicious activity.

### Immediate priority

Contain the spread.

Possible action:

> Isolate affected systems from the network.

After containment:

- Determine scope
- Preserve evidence
- Identify initial access
- Identify persistence
- Eradicate malware
- Patch the exploited weakness
- Restore from trusted recovery points
- Validate systems
- Monitor for reinfection

The key lesson is that **recovery should not begin blindly before containment and appropriate investigation**.

---

## 43. Detailed Security+ Scenario — Compromised Administrator

A privileged administrator account is suspected of compromise.

Potential response:

1. Validate the alert
2. Determine whether malicious activity is active
3. Preserve relevant evidence
4. Disable or restrict the compromised account
5. Revoke active sessions/tokens
6. Reset credentials securely
7. Investigate activity performed by the account
8. Determine whether other accounts or systems were compromised
9. Eradicate persistence
10. Monitor and validate recovery

Because the account is privileged, severity and potential scope may be high.

---

## 44. Detailed Security+ Scenario — Failed Recovery

A company successfully restores its application server but users cannot access the application.

Investigation reveals that the identity service was not restored.

The failure demonstrates:

**Incomplete dependency analysis.**

The lesson is:

> Recover the service dependency chain, not merely the application server.

---

## 45. Detailed Security+ Scenario — Ransomware Backups

A ransomware attack encrypts production systems and attempts to delete backups.

The organization has:

- Immutable backups
- Separate backup credentials
- Offline recovery copies
- Tested restoration procedures

These controls improve recovery resilience because compromise of production does not automatically provide unrestricted control over every recovery copy.

---

## 46. Detailed Security+ Scenario — Evidence vs Recovery

A compromised server contains potentially important forensic evidence, but the business wants it immediately wiped and rebuilt.

The security team should consider:

- Evidence-preservation requirements
- Business impact
- Containment
- Legal requirements
- Forensic needs
- Availability requirements

The key principle is that destructive recovery actions can eliminate evidence.

Where evidence matters, preserve appropriate evidence **before destructive remediation**, unless immediate safety or containment requirements dictate otherwise.

---

## 47. Detailed Security+ Scenario — Communication Failure

During a major security incident, corporate email is unavailable.

The IR team cannot depend on the same email infrastructure to coordinate the response.

The appropriate planning concept is:

**Out-of-band communication.**

Organizations should establish alternate communication mechanisms before emergencies occur.

---

## 48. Detailed Security+ Scenario — Tabletop vs Technical Test

Management wants to verify whether incident responders understand their roles and escalation procedures without changing production systems.

A:

**Tabletop exercise**

is appropriate.

If the organization wants to verify that a backup can actually restore a database, it needs a:

**Technical recovery test.**

---

## 49. Common Disaster Recovery Failures

### Failure 1: "We have backups, so we have DR."

Backups are only one component.

**Better approach:** design complete recovery procedures.

### Failure 2: Recovery order ignores dependencies.

The application is restored before identity or database services.

**Better approach:** map dependencies and recovery sequence.

### Failure 3: Backups are never tested.

The organization discovers during the disaster that restoration fails.

**Better approach:** perform regular restoration tests.

### Failure 4: Backups share the same administrative credentials.

A compromised administrator can delete production and backups.

**Better approach:** separate privileges and protect recovery infrastructure.

### Failure 5: Recovery copies are continuously exposed.

Ransomware reaches connected backups.

**Better approach:** use appropriate offline or immutable recovery mechanisms.

### Failure 6: RTO/RPO are unrealistic.

The organization promises recovery faster than its architecture can provide.

**Better approach:** test actual recovery performance against business requirements.

### Failure 7: DR plan is outdated.

Systems, vendors, contacts, and architecture have changed.

**Better approach:** update the plan after significant changes.

---

## 50. Common Incident Response Failures

### Failure 1: No defined authority

Responders do not know who can isolate systems or disable accounts.

**Better approach:** define decision authority in advance.

### Failure 2: Acting before validating

An analyst immediately disables a critical account based on a false positive.

**Better approach:** validate and assess severity before high-impact actions when circumstances permit.

### Failure 3: Destroying evidence

A compromised system is wiped before relevant evidence is preserved.

**Better approach:** coordinate containment, evidence preservation, and remediation.

### Failure 4: Treating every alert as an incident

This creates unnecessary escalation and response fatigue.

**Better approach:** distinguish events, alerts, investigations, and confirmed incidents.

### Failure 5: Containing without addressing root cause

The infected endpoint is isolated but the exploited vulnerability remains open.

**Better approach:** eradicate the cause and close the attack path.

### Failure 6: No lessons learned

The organization returns to normal without improving controls.

**Better approach:** document findings and implement corrective actions.

---

## 51. Plan Maintenance

DR and IR plans must change with the environment.

Review and update plans after:

- Major architecture changes
- Cloud migration
- New critical applications
- New suppliers
- Organizational restructuring
- New facilities
- New regulatory requirements
- Major security incidents
- Significant technology changes
- Changes in personnel
- Changes in RTO/RPO
- Lessons learned from exercises

A plan that describes a retired system is not a useful recovery plan.

---

## 52. Documentation and Version Control

Plans should have:

- Document owners
- Version numbers
- Approval information
- Review dates
- Change history
- Distribution controls
- Contact information
- Escalation procedures

Sensitive recovery and incident-response documentation should also be protected from unauthorized access.

However, authorized responders must be able to access it during an emergency.

This creates a practical requirement:

**Secure access + emergency availability**

---

## 53. Metrics and Performance

Organizations can measure DR and IR effectiveness.

### DR Metrics

- Actual recovery time
- RTO achievement rate
- Actual recovery point
- RPO achievement rate
- Backup restoration success
- Failover success rate
- Number of unresolved recovery dependencies

### IR Metrics

- Mean Time to Detect (MTTD)
- Mean Time to Respond (MTTR)
- Time to containment
- Time to eradication
- Number of incidents
- Recurrence rate
- Playbook effectiveness
- Lessons-learned actions completed

Metrics should identify weaknesses and drive improvement rather than simply generate reports.

---

## 54. Security+ Exam Distinctions and Traps

### Trap 1 — RTO vs RPO

**RTO = time to restore**

**RPO = acceptable data loss**

### Trap 2 — MTD vs RTO

**MTD = maximum business tolerance**

**RTO = targeted recovery time**

### Trap 3 — BC vs DR

**BC = continue critical business functions**

**DR = restore technology/services**

### Trap 4 — IR vs DR

**IR = manage the security incident**

**DR = restore systems and services**

### Trap 5 — Backup vs DR

**Backup = recoverable data copy**

**DR = complete recovery capability**

### Trap 6 — Tabletop vs Technical Test

**Tabletop = discussion and decision exercise**

**Technical test = demonstrate actual recovery capability**

### Trap 7 — Containment vs Eradication

**Containment = stop or limit spread**

**Eradication = remove the threat and attack mechanism**

### Trap 8 — Recovery vs Lessons Learned

Recovery returns systems to service.

Lessons learned improve the organization after the event.

---

## 55. Security+ Decision Framework

When a question presents a disaster or security incident, use this sequence.

### Step 1 — Identify the Event

What happened?

- Cyberattack?
- Hardware failure?
- Natural disaster?
- Cloud outage?
- Data corruption?

### Step 2 — Identify the Business Impact

Which business functions are affected?

### Step 3 — Determine the Objective

Is the question about:

- Continuing business? → **BC**
- Restoring technology? → **DR**
- Handling a security incident? → **IR**

### Step 4 — Determine the Recovery Requirement

- Restore time → **RTO**
- Data loss → **RPO**
- Maximum tolerable disruption → **MTD/MTPD**

### Step 5 — Identify Dependencies

What must be restored first?

### Step 6 — Select the Appropriate Action

Examples:

- Isolate endpoint → containment
- Remove persistence → eradication
- Restore trusted backup → recovery
- Activate alternate site → continuity/DR strategy
- Discuss response responsibilities → tabletop

### Step 7 — Preserve Evidence When Required

Before destructive actions, determine whether forensic or legal preservation requirements apply.

### Step 8 — Validate Recovery

Confirm:

- Functionality
- Data integrity
- Security controls
- Monitoring
- Business operation

### Step 9 — Learn and Improve

Document:

- Root cause
- Control failures
- Response gaps
- Recovery gaps
- Corrective actions

---

## 56. Complete DR and IR Workflow

### Disaster Recovery

**BIA**
↓
**Identify critical systems**
↓
**Determine RTO/RPO**
↓
**Map dependencies**
↓
**Design recovery architecture**
↓
**Implement backups/replication/failover**
↓
**Document procedures**
↓
**Test recovery**
↓
**Measure results**
↓
**Correct gaps**
↓
**Maintain plan**

### Incident Response

**Preparation**
↓
**Detection**
↓
**Validation and analysis**
↓
**Scoping and severity**
↓
**Containment**
↓
**Evidence preservation**
↓
**Eradication**
↓
**Recovery**
↓
**Monitoring and validation**
↓
**Lessons learned**
↓
**Corrective action**

---

## 57. Final Integrated Scenario

Consider an organization whose production environment is hit by ransomware.

### Phase 1 — Detection

EDR detects suspicious encryption behavior.

**IR begins.**

### Phase 2 — Analysis

SOC analysts determine:

- Multiple endpoints are affected
- A privileged account was abused
- File shares are being encrypted
- The attack is still active

### Phase 3 — Containment

Responders:

- Isolate affected systems
- Disable compromised accounts
- Restrict malicious network paths

The objective is to stop further damage.

### Phase 4 — Investigation

Responders determine:

- Initial access
- Persistence
- Lateral movement
- Systems affected
- Data potentially accessed

Evidence is preserved as required.

### Phase 5 — Eradication

The organization:

- Removes persistence
- Resets credentials
- Patches exploited vulnerabilities
- Rebuilds compromised systems where appropriate

### Phase 6 — Recovery

The DR team:

- Identifies trusted recovery points
- Restores infrastructure
- Restores databases
- Restores applications
- Validates data integrity
- Re-enables services

### Phase 7 — Business Continuity

Meanwhile, the business may:

- Activate manual processes
- Use alternate systems
- Redirect customer operations
- Maintain critical services

### Phase 8 — Lessons Learned

After recovery, the organization evaluates:

- Why initial access succeeded
- Why detection was delayed
- Why lateral movement was possible
- Whether backups survived
- Whether RTO/RPO were achieved
- Which controls need improvement

This scenario demonstrates why **IR, DR, and BC must work together without being treated as the same discipline.**

---

## 58. Key Takeaways

- **Disaster Recovery (DR)** focuses on restoring technology, services, and data after disruption.
- **Incident Response (IR)** focuses on managing security incidents.
- **Business Continuity (BC)** focuses on maintaining critical business functions.
- DR requirements should be derived from the **BIA**.
- **RTO** measures targeted restoration time.
- **RPO** measures acceptable data loss in time.
- **MTD/MTPD** represents the maximum tolerable disruption.
- Recovery order must consider **technical and business dependencies**.
- Backups are necessary but do not by themselves constitute a complete DR strategy.
- **3-2-1**, offline, and immutable approaches can improve backup resilience.
- Encryption and key management must be included in recovery planning.
- Recovery must be **tested and validated**, not assumed.
- **Failover** moves operations to a secondary environment; **failback** returns them to the primary environment.
- **Hot, warm, and cold sites** represent different recovery-speed and cost trade-offs.
- Cloud environments require consideration of regions, availability zones, identity, networking, DNS, keys, APIs, and provider dependencies.
- IaC can make recovery more consistent but must itself be protected.
- IR requires defined roles, authority, communication paths, playbooks, evidence procedures, and escalation.
- **Containment limits damage; eradication removes the threat and attack path; recovery restores trusted operations.**
- Incident communication should use authorization and need-to-know principles.
- Out-of-band communication is important when normal infrastructure may be unavailable or compromised.
- Tabletop exercises test decision-making and responsibilities; technical recovery tests demonstrate actual recovery capability.
- Lessons learned should result in measurable corrective actions.
- DR and IR plans must be maintained as the organization's technology, business processes, personnel, suppliers, and requirements change.

## Final Mental Model

Remember:

**BIA**
→ What must the business protect and how quickly must it recover?

**BC**
→ How do we continue critical business functions?

**DR**
→ How do we restore technology and services?

**IR**
→ How do we manage the security incident?

**RTO**
→ How quickly must it be restored?

**RPO**
→ How much data can be lost?

**MTD**
→ How long can the business tolerate disruption?

**Containment**
→ Stop the damage from spreading.

**Eradication**
→ Remove the threat and attack path.

**Recovery**
→ Restore trusted operations.

**Validation**
→ Prove the environment is functional and secure.

**Lessons Learned**
→ Improve the program so the next incident is handled better.
