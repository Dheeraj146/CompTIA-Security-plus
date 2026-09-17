# Domain 4 — Module 14: Backup, Recovery, and Business Continuity Operations

Backup, recovery, and business continuity operations ensure that an organization can continue or restore critical services after failures, cyberattacks, disasters, human error, or infrastructure loss.

For Security+, the important concepts are not simply knowing that backups exist. You must understand **what is being protected, how much data can be lost, how quickly services must return, where recovery dependencies exist, how backups are protected from attackers, and how recovery is tested**.

A useful operational model is:

**Identify critical services → Define recovery objectives → Protect data → Create backups/replicas → Protect recovery infrastructure → Test restoration → Recover in priority order → Validate → Return to operation → Improve**

---

# 1. Backup vs Recovery vs Business Continuity

These concepts are closely related but solve different problems.

### Backup

A backup is a copy of data or system information maintained so that it can be restored after loss, corruption, deletion, or compromise.

### Recovery

Recovery is the process of restoring systems, applications, data, and services to an acceptable operational state.

### Business Continuity

Business continuity focuses on maintaining critical business functions during and after a disruptive event.

For example, if an organization's primary application is unavailable:

- A backup provides recoverable data.
- Recovery restores the application and supporting infrastructure.
- Business continuity may provide an alternate manual process or alternate service so the business can continue while recovery occurs.

---

# 2. Why Backups Are a Security Control

Backups are not only an IT administration function. They are an important security control against:

- Ransomware.
- Accidental deletion.
- Hardware failure.
- Software corruption.
- Insider activity.
- Configuration mistakes.
- Natural disasters.
- Data corruption.
- Failed deployments.

However, a backup is useful only if it is **available, protected, complete enough, and actually restorable**.

A backup that has silently failed for six months is not a meaningful recovery capability.

---

# 3. Recovery Objectives

Before designing recovery operations, the organization must determine business requirements.

Two critical concepts are:

## Recovery Time Objective — RTO

**RTO is the target maximum amount of time required to restore a service after a disruption.**

Example:

> A payment service has an RTO of 2 hours.

The organization must design recovery capabilities capable of restoring the service within that objective.

## Recovery Point Objective — RPO

**RPO defines the acceptable amount of data loss measured in time.**

Example:

> An application has an RPO of 15 minutes.

The organization should have a recovery mechanism capable of restoring data to a point no more than approximately 15 minutes before the disruption, subject to the organization's actual implementation and assumptions.

### Easy distinction

**RTO = How quickly can we recover?**

**RPO = How much recent data can we afford to lose?**

---

# 4. RTO Example

Suppose an online banking service has an RTO of 30 minutes.

A recovery design that takes 8 hours does not satisfy that requirement, even if the backups themselves are excellent.

The organization may therefore require:

- Standby infrastructure.
- Automated failover.
- Rapid provisioning.
- Replication.
- Preconfigured systems.
- Documented recovery procedures.

The recovery technology must be selected according to the business objective.

---

# 5. RPO Example

Suppose a database has an RPO of 5 minutes.

If the only backup is created once every 24 hours, the organization could potentially lose almost an entire day's transactions.

That backup strategy does not meet the stated RPO.

A lower RPO generally requires more frequent backups, continuous replication, transaction-log protection, or another mechanism capable of preserving more recent state.

---

# 6. Backup Types

Understanding backup types is important for both operations and Security+ questions.

## Full Backup

Copies all selected data.

### Advantages

- Simple restoration model.
- Complete backup set by itself.

### Disadvantages

- Requires more storage.
- Takes longer to create.

---

## Incremental Backup

Copies data changed since the most recent backup of any type.

Example:

```text
Sunday: Full
Monday: Incremental
Tuesday: Incremental
Wednesday: Incremental
```

To restore Wednesday, the organization generally needs the Sunday full backup and the subsequent incremental backups through Wednesday.

### Advantage

Efficient backup storage and backup time.

### Disadvantage

Restoration can require multiple backup sets.

---

## Differential Backup

Copies data changed since the most recent full backup.

Example:

```text
Sunday: Full
Monday: Differential
Tuesday: Differential
Wednesday: Differential
```

Wednesday's differential contains changes since Sunday's full backup.

### Advantage

Restoration generally requires the full backup plus the latest differential.

### Disadvantage

Differential backups grow larger as more changes accumulate after the full backup.

---

# 7. Incremental vs Differential

This is a common Security+ distinction.

| Type | Changes since | Restoration concept |
|---|---|---|
| Full | Everything selected | Full backup alone may be sufficient for the backed-up data |
| Incremental | Last backup of any type | Full + each required incremental |
| Differential | Last full backup | Full + latest differential |

The difference is the **reference point** used to determine what changed.

---

# 8. Snapshot

A snapshot captures the state of a system, volume, virtual machine, or storage resource at a particular point in time, depending on the platform.

Snapshots can be useful for:

- Rapid rollback.
- Short-term recovery.
- Testing changes.
- Virtual-machine recovery.

However, a snapshot is not automatically equivalent to an independent backup.

If the snapshot resides on the same underlying storage or is affected by the same failure, it may not provide adequate protection.

---

# 9. Replication

Replication maintains copies of data or systems on another system or location.

Replication can support availability and recovery, but it must be designed carefully.

### Synchronous replication

Changes are committed to the replica in coordination with the primary operation.

### Advantage

Very low potential data loss.

### Disadvantage

Requires suitable latency and connectivity and can introduce performance or availability dependencies.

### Asynchronous replication

Changes are replicated after the primary system commits them.

### Advantage

Can support greater geographic distance and reduce latency requirements.

### Disadvantage

The replica may lag behind, creating potential data loss when the primary fails.

---

# 10. Backup Frequency

Backup frequency should be driven by business requirements rather than an arbitrary schedule.

Factors include:

- RPO.
- Data change rate.
- Business criticality.
- Regulatory requirements.
- Storage cost.
- Network capacity.
- Recovery capability.

A critical transactional database may require far more frequent protection than a rarely changing archive.

---

# 11. The 3-2-1 Backup Principle

A common backup strategy is:

**3 copies of data → 2 different storage media/types → 1 copy off-site**

The principle reduces the chance that a single failure destroys every copy.

For example:

```text
Production Data
      ↓
Primary Storage
      ↓
Local Backup
      ↓
Off-Site Backup
```

Modern environments often extend this principle with additional isolation and immutability requirements.

---

# 12. Offline Backups

An offline backup is not continuously accessible to the production environment.

This can protect backups from attacks that compromise production credentials or systems.

For example, if ransomware compromises a server and can access the backup repository using the same credentials, the attacker may encrypt or delete the backups too.

An offline or otherwise isolated backup reduces that attack path.

---

# 13. Immutable Backups

An **immutable backup** is protected from modification or deletion for a defined period or under defined controls.

Immutability is valuable against:

- Ransomware.
- Malicious administrators.
- Compromised backup credentials.
- Accidental deletion.

The exact implementation varies by platform.

The key concept is:

> **Attackers should not be able to modify the protected recovery copy even after compromising production systems.**

---

# 14. Backup Encryption

Backups can contain highly sensitive information, so they should be protected appropriately.

Encryption may be used:

- At rest.
- During transfer.
- In backup storage.

Key management is equally important. If encryption keys are lost, the backup may become unrecoverable.

Therefore, backup security includes both:

**Data protection + key protection**

---

# 15. Backup Access Control

Backup infrastructure should not automatically use the same identities and permissions as production infrastructure.

Important controls may include:

- Least privilege.
- Separate administrative accounts.
- MFA.
- Role-based access.
- Restricted management networks.
- Privileged access management.
- Strong monitoring.
- Immutable storage.
- Separation of duties.

Compromising one production administrator should not automatically provide unrestricted ability to destroy every backup.

---

# 16. Backup Integrity

A backup should be periodically validated.

Validation can include:

- Backup-job success verification.
- Integrity checks.
- Hashes where appropriate.
- Catalog validation.
- Test restoration.
- Application-level validation.

A backup job reporting **“successful”** does not necessarily prove that the organization can successfully restore the business service.

---

# 17. Restore Testing

Restore testing is one of the most important operational activities.

A proper test can answer:

- Can the backup be located?
- Can it be read?
- Can it be decrypted?
- Can the system be restored?
- Are dependencies available?
- Is the recovered data complete?
- Does the application work?
- Can users authenticate?
- Is the restored system secure?
- Does the recovery process meet the RTO?

Testing converts an assumed recovery capability into a demonstrated capability.

---

# 18. Recovery Dependencies

Recovery is rarely as simple as restoring one server.

A business application may depend on:

```text
Application
    ↓
Database
    ↓
Identity / Active Directory
    ↓
DNS
    ↓
Network
    ↓
Storage
    ↓
Third-party services
```

If DNS or identity is unavailable, the application may remain unusable even when its server has been restored.

Therefore, recovery planning must identify dependencies and recovery order.

---

# 19. Recovery Order

Critical services should be recovered according to business priorities and technical dependencies.

For example:

```text
1. Network infrastructure
2. Identity services
3. DNS/DHCP/core infrastructure
4. Storage/database services
5. Application services
6. User-facing systems
```

The exact sequence varies by environment.

The important concept is that **recovery order should be dependency-aware and business-driven**.

---

# 20. Business Continuity

Business continuity asks:

> How can the organization continue performing critical functions while normal systems are unavailable?

Possible continuity mechanisms include:

- Alternate work locations.
- Remote-work capability.
- Manual procedures.
- Alternate suppliers.
- Alternate communication methods.
- Redundant systems.
- Alternate processing facilities.
- Emergency staffing arrangements.

Business continuity is broader than IT recovery because it includes people, processes, facilities, suppliers, technology, and communications.

---

# 21. Business Impact Analysis — BIA

A **Business Impact Analysis** identifies critical business processes and evaluates the consequences of their disruption.

A BIA may determine:

- Which processes are most critical.
- Maximum tolerable downtime.
- Recovery priorities.
- Financial impact.
- Operational impact.
- Legal/regulatory impact.
- Customer impact.
- Dependencies.
- Recovery objectives.

The BIA helps establish requirements for continuity and recovery architecture.

---

# 22. Disaster Recovery Sites

Organizations may use different levels of alternate recovery facilities.

## Cold site

Provides basic facilities but requires significant setup before operations can resume.

### Characteristics

- Lower ongoing cost.
- Longer recovery time.
- More configuration required.

## Warm site

Provides partially prepared infrastructure.

### Characteristics

- Moderate cost.
- Moderate recovery time.
- Some systems/configuration already available.

## Hot site

Provides highly prepared or active infrastructure capable of rapid transition.

### Characteristics

- Higher cost.
- Faster recovery.
- More infrastructure and maintenance required.

The appropriate option depends on business recovery requirements.

---

# 23. High Availability vs Disaster Recovery

These are often confused.

### High Availability

Designed to minimize service interruption during component failures.

Examples:

- Redundant servers.
- Clustered systems.
- Load balancing.
- Failover systems.

### Disaster Recovery

Designed to restore services after significant disruption.

Examples:

- Backup restoration.
- Alternate-region recovery.
- Disaster-recovery site.
- Rebuilding infrastructure.

High availability reduces downtime from failures; disaster recovery provides a recovery capability when disruption exceeds normal HA mechanisms.

---

# 24. Failover and Failback

### Failover

Moving service operation from a failed or unavailable primary system to an alternate system.

### Failback

Returning operations to the original or designated primary environment after the underlying issue is resolved.

Failback should be controlled and validated rather than performed immediately without checking the environment.

---

# 25. Backup and Ransomware

Ransomware changes how organizations must think about backup security.

A traditional backup repository may be vulnerable if attackers obtain backup-administrator credentials.

A ransomware-resistant strategy can include:

- Offline copies.
- Immutable copies.
- Separate administrative identities.
- MFA.
- Restricted management access.
- Backup-network segmentation.
- Multiple recovery copies.
- Monitoring for backup deletion attempts.
- Regular restore testing.

The goal is not merely to **have backups**, but to ensure attackers cannot easily destroy the organization's ability to recover.

---

# 26. Cloud Backup and Recovery

Cloud environments provide additional recovery options such as:

- Object-storage backups.
- Cross-region replication.
- Automated snapshots.
- Infrastructure as Code.
- Managed database backups.
- Alternate-region deployments.
- Versioned storage.
- Immutable/object-lock capabilities where supported.

However, cloud recovery introduces dependencies such as:

- Cloud identity.
- Network connectivity.
- Provider availability.
- API access.
- Encryption keys.
- DNS.
- Quotas.
- Service dependencies.
- Infrastructure definitions.

A cloud backup is not automatically independent from a compromised cloud account.

---

# 27. Infrastructure as Code and Recovery

Infrastructure as Code can accelerate recovery by defining infrastructure in reproducible form.

For example:

```text
IaC Definition
      ↓
Network
      ↓
Compute
      ↓
Security Controls
      ↓
Application
      ↓
Monitoring
```

Instead of manually rebuilding every component, the organization can provision a known configuration.

However, IaC files themselves must be protected. A compromised or incorrect configuration can reproduce insecure infrastructure.

---

# 28. Recovery Validation

After restoration, validate:

- System integrity.
- Data integrity.
- Application functionality.
- Authentication.
- Authorization.
- Network connectivity.
- Security configuration.
- Endpoint protection.
- Logging and monitoring.
- Backup operation.
- Required integrations.

A recovered server that is online but missing EDR, logging, or required security configuration should not automatically be considered fully recovered.

---

# 29. Recovery Testing Types

Organizations can test recovery through different levels of exercises.

### Tabletop exercise

Participants discuss a scenario and decisions without actually restoring systems.

Useful for:

- Roles.
- Communication.
- Decision-making.
- Procedure validation.

### Simulation

The organization simulates technical or operational conditions more realistically.

### Technical recovery test

Actual systems or recovery infrastructure are used to validate restoration capabilities.

### Full interruption test

A highly realistic test that may involve actual service transition or interruption, subject to organizational risk and planning.

The exact terminology varies between organizations.

---

# 30. Backup Retention

Retention defines how long backup copies are maintained.

Retention requirements can be influenced by:

- Business needs.
- Legal requirements.
- Regulatory requirements.
- Contractual obligations.
- Storage cost.
- Data sensitivity.
- Recovery requirements.

Keeping every backup forever is not automatically better. Excessive retention can increase cost, storage requirements, privacy exposure, and the amount of sensitive data an attacker could potentially access.

---

# 31. Recovery and Security Baselines

Recovered systems should return to a known secure configuration.

The recovery process should include:

- Secure baseline.
- Required patches.
- Correct access permissions.
- Endpoint protection.
- Firewall configuration.
- Logging.
- Monitoring.
- Credential rotation where required.

Restoring an old vulnerable system image without applying current security requirements can recreate the original security problem.

---

# 32. Recovery After a Cyber Incident

Cyber recovery differs from simple hardware failure recovery.

If a system was compromised, the organization must determine whether the backup itself is trustworthy.

For example, restoring a backup created after an attacker obtained persistence may restore the compromise.

Therefore, cyber recovery should consider:

- When compromise began.
- Whether backups were exposed.
- Whether backup credentials were compromised.
- Whether malicious files existed in backups.
- Whether restoration points predate the compromise.
- Whether systems require rebuilding instead of restoration.

A **known-good recovery point** is more important than simply choosing the newest backup.

---

# 33. Recovery Scenario — Ransomware

Suppose a company discovers that ransomware encrypted production servers.

A disciplined approach could be:

### Step 1 — Contain

Prevent further spread and protect backup infrastructure.

### Step 2 — Determine scope

Identify affected systems and accounts.

### Step 3 — Identify a trusted recovery point

Determine which backup or replica predates compromise and remains trustworthy.

### Step 4 — Validate dependencies

Confirm identity, DNS, networking, storage, and application dependencies.

### Step 5 — Restore or rebuild

Recover systems according to business priority and dependency order.

### Step 6 — Secure the recovered environment

Apply patches, secure configurations, credential resets, and monitoring.

### Step 7 — Validate

Test application functionality and security controls.

### Step 8 — Resume operations

Return services to production in a controlled manner.

### Step 9 — Lessons learned

Address the initial access vector and recovery weaknesses.

---

# 34. Recovery Scenario — Database Failure

Suppose a critical database server fails at 10:00.

The organization has:

- A full backup from Sunday.
- Incremental backups each day.
- Transaction-log protection.

The recovery team must determine the appropriate recovery point based on the database's RPO and available recovery mechanisms.

It must also consider application dependencies, authentication, network access, and data integrity.

Restoring the database alone may not restore the complete business service.

---

# 35. Common Backup and Recovery Failures

## Failure 1 — Never testing restores

A successful backup job does not prove successful recovery.

**Better approach:** perform periodic restore testing.

## Failure 2 — Keeping backups on the same system

A storage failure or ransomware event can destroy both production and backup copies.

**Better approach:** use independent and appropriately separated copies.

## Failure 3 — Using the same administrator credentials

Compromised production credentials may provide access to backups.

**Better approach:** separate backup administration and apply least privilege/MFA.

## Failure 4 — Ignoring RPO/RTO

A technically functional backup strategy may still fail business requirements.

**Better approach:** design recovery around defined objectives.

## Failure 5 — Restoring the newest backup automatically

The newest backup may contain attacker activity or corruption.

**Better approach:** identify a trustworthy recovery point.

## Failure 6 — Ignoring dependencies

Restoring an application server without identity, DNS, database, or network services may not restore the business function.

**Better approach:** map dependencies and recovery order.

## Failure 7 — Recovering insecure systems

An old image may contain known vulnerabilities.

**Better approach:** apply current security requirements during recovery.

## Failure 8 — Treating snapshots as complete backups

A snapshot may depend on the same underlying infrastructure.

**Better approach:** maintain independent recovery copies where required.

---

# 36. Security+ Exam Distinctions

### RTO vs RPO

- **RTO:** maximum targeted recovery time.
- **RPO:** acceptable data-loss window measured in time.

### Full vs Incremental vs Differential

- **Full:** all selected data.
- **Incremental:** changes since the last backup.
- **Differential:** changes since the last full backup.

### Backup vs Snapshot

- **Backup:** independent recovery copy designed for restoration.
- **Snapshot:** point-in-time state that may support rollback but is not automatically an independent backup.

### Backup vs Replication

- **Backup:** recovery copy retained for restoration.
- **Replication:** maintains a copy synchronized or semi-synchronized with another system.

Replication alone may reproduce corruption or malicious changes, so it should not automatically be treated as a substitute for historical backups.

### High Availability vs Disaster Recovery

- **HA:** minimize service interruption.
- **DR:** restore services after significant disruption.

### Business Continuity vs Disaster Recovery

- **BC:** keep critical business functions operating.
- **DR:** restore technology/services.

### Failover vs Failback

- **Failover:** move to alternate operation.
- **Failback:** return to the primary/designated environment.

### Cold vs Warm vs Hot Site

- **Cold:** least prepared, slower recovery.
- **Warm:** partially prepared.
- **Hot:** highly prepared, faster recovery, higher cost.

---

# 37. Security+ Decision Framework

When analyzing a backup or recovery question, ask:

### 1. What is the business requirement?

Identify critical services and required recovery objectives.

### 2. What is the RTO?

Determine how quickly the service must return.

### 3. What is the RPO?

Determine how much recent data can be lost.

### 4. Are the backups independent and protected?

Consider offline, immutable, geographically separated, encrypted, and access-controlled copies.

### 5. Can the backups actually be restored?

Look for evidence of restore testing.

### 6. Is the recovery point trustworthy?

For cyber incidents, the newest copy may not be the safest copy.

### 7. What dependencies must be recovered first?

Consider identity, DNS, network, storage, databases, applications, and third parties.

### 8. Does the recovery process restore security as well as availability?

Validate patches, baselines, access controls, logging, monitoring, and credentials.

### 9. Does the recovery capability satisfy the business objectives?

A backup can exist and still fail the organization's RTO/RPO requirements.

---

# 38. Practical Backup and Recovery Workflow

```text
Identify Critical Services
          ↓
Perform Business Impact Analysis
          ↓
Define RTO / RPO
          ↓
Identify Data and Dependencies
          ↓
Design Backup / Replication Strategy
          ↓
Protect Backup Infrastructure
          ↓
Monitor Backup Jobs
          ↓
Test Restoration
          ↓
Validate Recovery Capability
          ↓
Incident / Failure Occurs
          ↓
Contain and Assess
          ↓
Select Trusted Recovery Point
          ↓
Recover in Priority / Dependency Order
          ↓
Validate Security and Functionality
          ↓
Return to Service
          ↓
Lessons Learned and Improve
```

---

# 39. Key Takeaways

- Backups provide recoverable copies; recovery restores services; business continuity keeps critical business functions operating.
- RTO answers **how quickly** a service must be restored.
- RPO answers **how much recent data** can be lost.
- Full, incremental, and differential backups use different reference points.
- Incremental backups generally require the full backup and each required incremental set for restoration.
- Differential restoration generally requires the full backup and the latest differential.
- Snapshots can support rollback but are not automatically independent backups.
- Replication can improve availability and recovery but may reproduce corruption or malicious changes.
- The 3-2-1 principle provides a foundation for backup resilience.
- Offline and immutable copies can significantly reduce ransomware-related backup destruction risk.
- Backup encryption requires secure key management.
- Backup administrators should use appropriate least privilege, MFA, and separation from production administration.
- A successful backup job does not prove successful recovery.
- Restore testing is essential.
- Recovery must account for dependencies such as identity, DNS, networking, databases, storage, and third-party services.
- Business continuity includes people, processes, facilities, suppliers, communications, and technology—not only backups.
- High availability reduces interruption; disaster recovery restores service after significant disruption.
- Cyber recovery requires selecting a trustworthy recovery point, not automatically the newest backup.
- Recovered systems must be validated for both security and functionality.

## Core Security+ Mental Model

**Business Requirement → BIA → RTO/RPO → Backup Design → Protection → Testing → Trusted Recovery Point → Dependency-Aware Recovery → Security Validation → Service Restoration → Continuous Improvement**

The central principle is: **a recovery capability is only useful when it is protected from the same failure that destroyed production, can actually be restored, meets business RTO/RPO requirements, and returns the environment to a secure and trustworthy state.**