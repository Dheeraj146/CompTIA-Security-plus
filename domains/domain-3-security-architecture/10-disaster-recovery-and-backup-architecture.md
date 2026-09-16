# Disaster Recovery and Backup Architecture

Disaster recovery (DR) and backup architecture are concerned with preserving the availability and recoverability of systems and data when normal operations are disrupted. A secure architecture does not assume that prevention will always succeed. It assumes that hardware can fail, software can become corrupted, ransomware can compromise systems, administrators can make mistakes, facilities can become unavailable, and natural or human-caused events can interrupt operations.

The objective is therefore not simply to "have backups." The objective is to design a recovery capability that can restore the right services, within the required time, with an acceptable amount of data loss, while preventing the recovery environment itself from becoming another attack path.

---

## 1. Disaster Recovery Fundamentals

Disaster recovery is the collection of policies, architectures, procedures, technologies, and resources used to restore technology services after a disruptive event.

A disaster can include:

- Hardware failure
- Storage failure
- Power failure
- Network outage
- Data-center outage
- Fire, flood, or other environmental event
- Malware or ransomware
- Accidental deletion
- Database corruption
- Software failure
- Misconfiguration
- Insider activity
- Cloud-service disruption
- Loss of a critical provider or dependency

DR is different from ordinary troubleshooting. Troubleshooting attempts to return an individual component or service to normal operation. Disaster recovery addresses a significant disruption in which normal production capabilities may be unavailable or unreliable.

### The basic DR question

A DR architecture must answer:

> **If the primary environment becomes unavailable, how will the organization continue or restore critical operations?**

That question requires more than selecting a backup technology. It requires understanding business priorities, dependencies, recovery objectives, alternate infrastructure, data protection, personnel, communications, and testing.

---

## 2. Business Requirements Drive Recovery Architecture

Recovery architecture should begin with business requirements rather than with a particular backup product.

For example, consider two systems:

- An internal development server can potentially tolerate several days of downtime.
- An online payment service may need to be restored within minutes.

Using exactly the same recovery architecture for both systems may be unnecessary or inadequate.

A business-driven recovery design considers:

- Critical business services
- Supporting applications
- Data sensitivity
- Data dependencies
- Acceptable downtime
- Acceptable data loss
- Regulatory requirements
- Financial impact of downtime
- Availability requirements
- Recovery staffing
- Geographic requirements
- Budget and operational complexity

This is why DR architecture should be connected to **business impact analysis (BIA)** and risk assessment.

---

## 3. Recovery Time Objective (RTO)

**Recovery Time Objective (RTO)** defines the maximum targeted amount of time within which a service or business function should be restored after a disruption.

Think of RTO as:

> **How quickly do we need the service back?**

For example:

- RTO = 4 hours → the organization targets restoration within four hours.
- RTO = 15 minutes → the architecture must support much faster recovery.
- RTO = 24 hours → slower recovery mechanisms may be acceptable.

### RTO and architecture

A low RTO generally requires more prepared recovery capabilities.

Possible technologies include:

- Hot sites
- Active-active infrastructure
- Real-time or near-real-time replication
- Automated failover
- Preconfigured standby systems
- Load-balanced redundant services
- Rapid infrastructure provisioning

A high RTO may permit:

- Manual restoration
- Cold sites
- Periodic backups
- Longer provisioning processes

### Important distinction

RTO measures **time**.

It does not measure how much data can be lost.

---

## 4. Recovery Point Objective (RPO)

**Recovery Point Objective (RPO)** defines the maximum acceptable amount of data loss measured in time.

Think of RPO as:

> **How much recent data can we afford to lose?**

Suppose an organization has an RPO of one hour. If the primary system fails at 4:00 PM, the recovery design should aim to restore data to a point no older than approximately 3:00 PM.

A smaller RPO requires more frequent data protection.

Examples include:

- Continuous replication
- Near-real-time replication
- Frequent snapshots
- Frequent incremental backups
- Transaction-log backups

### RPO versus RTO

| Metric | Main Question | Concern |
|---|---|---|
| RTO | How quickly must service return? | Downtime |
| RPO | How much recent data can be lost? | Data loss |

### Security+ exam trap

If a question says:

> "The organization can tolerate losing no more than 15 minutes of transaction data."

The key requirement is **RPO**, not RTO.

If it says:

> "The service must be restored within 15 minutes."

The key requirement is **RTO**.

---

## 5. Recovery Time and Recovery Point Are Related but Independent

An organization can have a low RPO but a high RTO, or a low RTO but a relatively high RPO.

For example:

### Low RPO, high RTO

Data may be replicated continuously, so very little data is lost. However, the organization may still need several hours to provision and configure the application environment.

### Low RTO, high RPO

A standby environment may be available immediately, but its data may only be synchronized once every few hours.

Therefore:

**Fast recovery does not automatically mean little data loss.**

And:

**Little data loss does not automatically mean fast service restoration.**

---

## 6. Backup Fundamentals

A backup is a separate copy of data maintained so that the original data can be restored after deletion, corruption, failure, or compromise.

Backups protect against scenarios such as:

- Accidental deletion
- Hardware failure
- File corruption
- Database corruption
- Ransomware
- Malicious modification
- Application failure
- User error

However, backups are only useful if they are:

1. Available when needed
2. Protected from unauthorized modification
3. Complete enough to satisfy recovery requirements
4. Retained for the required period
5. Recoverable
6. Tested

A backup that cannot be restored is not a dependable recovery capability.

---

## 7. Full Backup

A **full backup** copies all selected data in the backup set.

For example, if a server has 500 GB of data selected for backup, a full backup captures that selected data set.

### Advantages

- Simple restoration process
- Self-contained backup set
- Easy to understand
- Useful as a baseline

### Disadvantages

- Requires more storage
- Takes longer to perform
- Can consume more network and system resources

Full backups are often used periodically as the baseline for incremental or differential backups.

---

## 8. Incremental Backup

An **incremental backup** stores data changed since the previous backup of any type.

Example:

- Sunday: Full backup
- Monday: Changes since Sunday
- Tuesday: Changes since Monday
- Wednesday: Changes since Tuesday

To restore Wednesday's state, the recovery process generally needs:

**Sunday full + Monday incremental + Tuesday incremental + Wednesday incremental**

### Advantages

- Small backup size after the full baseline
- Faster individual backup operations
- Lower storage consumption

### Disadvantages

- Restoration can require multiple backup sets
- A missing or corrupted incremental backup can affect the recovery chain

### Exam concept

Incremental means:

> **Changes since the last backup.**

---

## 9. Differential Backup

A **differential backup** stores data changed since the last full backup.

Example:

- Sunday: Full backup
- Monday: Changes since Sunday
- Tuesday: All changes since Sunday
- Wednesday: All changes since Sunday

To restore Wednesday's state, the process generally requires:

**Sunday full + Wednesday differential**

### Advantages

- Restoration is simpler than a long incremental chain
- Only the latest differential plus the full backup is normally needed

### Disadvantages

- Differential backups grow larger as time passes from the full backup
- Storage requirements can be greater than incremental backups

### Exam concept

Differential means:

> **Changes since the last full backup.**

---

## 10. Backup Comparison

| Backup Type | Captures Changes Since | Typical Backup Size | Restoration Complexity |
|---|---|---|---|
| Full | Entire selected data set | Largest | Simplest |
| Incremental | Previous backup | Usually smallest | Higher |
| Differential | Last full backup | Grows over time | Moderate |

The choice depends on the organization's recovery objectives, available storage, network capacity, backup windows, and restoration requirements.

---

## 11. Snapshot and Backup Are Not the Same

A snapshot captures the state of a system, volume, virtual machine, or storage resource at a particular point in time.

Snapshots can be useful for:

- Rapid rollback
- Short-term recovery
- Testing changes
- Virtual-machine recovery
- Protecting against configuration mistakes

However, a snapshot should not automatically be treated as a complete backup strategy.

If snapshots reside on the same storage infrastructure as production data, a failure affecting that storage could potentially affect both the production workload and the snapshots.

Similarly, an attacker who compromises the production environment may also be able to delete or encrypt accessible snapshots.

A robust architecture therefore considers independent and appropriately protected backup copies.

---

## 12. The 3-2-1 Backup Concept

A commonly used backup strategy is the **3-2-1 approach**:

- Maintain at least **3 copies** of important data
- Store them on at least **2 different types of storage/media**
- Keep at least **1 copy off-site**

The exact implementation can vary, but the underlying principle is diversification.

The goal is to avoid a single event destroying every copy.

For example, if production data and every backup are located in the same building, a major physical disaster could affect all copies.

---

## 13. Offline and Immutable Backups

Modern ransomware makes backup protection particularly important.

### Offline backup

An offline backup is disconnected from the production environment when not being used.

Because it is not continuously accessible, compromise of production systems is less likely to directly modify or delete the offline copy.

### Immutable backup

An immutable backup is protected against modification or deletion for a defined retention period.

Immutability can be implemented through technologies and storage mechanisms that enforce retention and prevent ordinary administrative operations from altering protected backup data.

### Why this matters

If an attacker obtains administrative access and can delete all online backups, simply having "many backups" may not be sufficient.

Backup architecture should therefore consider:

- Separate administrative credentials
- MFA
- Privileged access controls
- Network isolation
- Immutable storage
- Offline copies
- Retention locks
- Backup monitoring
- Restore testing

---

## 14. Backup Security

Backup systems are high-value targets because they contain copies of valuable organizational data.

Security controls should include:

### Encryption

Backups should be encrypted where appropriate, particularly when they contain sensitive or regulated information.

Encryption should address:

- Data at rest
- Data in transit

### Access control

Only authorized personnel and services should be able to create, modify, delete, or restore backups.

### Separation of duties

The same administrator should not necessarily have unrestricted authority over both production systems and backup destruction.

### MFA

Strong authentication should protect privileged backup-management operations.

### Network isolation

Backup infrastructure can be placed in a separate security zone or network so compromise of ordinary production endpoints does not automatically provide access to backup management systems.

### Monitoring

Organizations should monitor unusual events such as:

- Mass backup deletion
- Unexpected retention changes
- Failed backup jobs
- Unusual restore operations
- New administrative accounts
- Large changes in backup volume

---

## 15. Backup Retention

Retention defines how long backup data is preserved.

Retention requirements can depend on:

- Business requirements
- Legal requirements
- Regulatory requirements
- Investigation requirements
- Contractual requirements
- Storage costs
- Recovery objectives

A backup may be technically available but still unusable if it has expired before the organization discovers the need for historical recovery.

Retention should therefore be deliberately designed rather than selected arbitrarily.

---

## 16. Backup Integrity and Restoration Testing

Creating a backup is only the first step.

The organization must verify that the backup can actually be used to recover the required system or data.

Testing should verify:

- Backup completeness
- Backup integrity
- Restore procedures
- Application dependencies
- Credentials and access
- Network connectivity
- DNS dependencies
- Database consistency
- Configuration requirements
- Personnel responsibilities
- Recovery timing

### Example

Suppose an organization successfully backs up a database every night. During an actual incident, administrators discover that the backup exists but the application requires a different database version and the required encryption key is unavailable.

The backup technically exists, but the recovery process fails.

This is why **restore testing** is critical.

---

## 17. Recovery Site Types

Recovery sites provide alternate facilities or infrastructure from which operations can be restored.

### Hot Site

A **hot site** is a highly prepared alternate environment with substantial infrastructure already available.

It may contain:

- Servers
- Networking
- Storage
- Power
- Applications or preconfigured systems
- Connectivity

A hot site is designed for rapid recovery.

### Advantages

- Fast recovery
- High readiness
- Suitable for low-RTO requirements

### Disadvantages

- Expensive
- Complex to maintain
- Requires synchronization and operational management

---

## 18. Warm Site

A **warm site** has some infrastructure prepared but generally requires additional configuration, data restoration, or system preparation before production operations can resume.

It represents a middle ground between hot and cold sites.

### Advantages

- Less expensive than a fully prepared hot site
- Faster recovery than a cold site

### Disadvantages

- Recovery requires additional work
- May not satisfy extremely low RTO requirements

---

## 19. Cold Site

A **cold site** provides basic facilities such as physical space, power, environmental controls, or network connectivity, but substantial technology deployment and configuration may still be required.

### Advantages

- Lower cost
- Useful for less critical workloads

### Disadvantages

- Slow recovery
- Requires significant preparation during the incident
- Usually unsuitable for very low RTO requirements

### Recovery site comparison

| Site | Readiness | Recovery Speed | Typical Cost |
|---|---|---|---|
| Hot | High | Fast | High |
| Warm | Medium | Moderate | Medium |
| Cold | Low | Slow | Lower |

---

## 20. Reciprocal and Alternate Recovery Arrangements

Organizations may use different recovery arrangements depending on size and requirements.

Possible approaches include:

- Dedicated alternate data center
- Cloud-based recovery environment
- Colocation facility
- Managed DR provider
- Reciprocal arrangements
- Portable infrastructure

A reciprocal arrangement involves organizations agreeing to support one another's recovery requirements, although practical capacity, compatibility, security, and contractual issues must be considered.

---

## 21. Geographic Redundancy

A recovery location should be geographically separated when the threat can affect an entire physical area.

For example, if the primary data center and backup data center are located in the same flood zone, geographic separation may be inadequate.

Relevant considerations include:

- Natural disasters
- Regional power failures
- Network-provider outages
- Political or civil disruption
- Fire zones
- Flood zones
- Earthquake zones
- Regional cloud failures

Geographic diversity reduces the likelihood that one event will simultaneously affect both primary and recovery infrastructure.

---

## 22. Data Replication

Replication maintains copies of data in another location or system.

### Synchronous replication

Data is written to multiple systems in coordination before the write is considered complete.

Advantages:

- Very small data-loss window
- Strong consistency between replicas when correctly implemented

Disadvantages:

- Requires low-latency connectivity
- Can introduce performance and availability dependencies
- More complex and expensive over large geographic distances

### Asynchronous replication

Data is replicated after the primary write rather than requiring all replicas to acknowledge the write immediately.

Advantages:

- Can work over greater distances
- Lower latency impact on primary operations

Disadvantages:

- Some recent data may be lost if the primary fails before replication completes

This distinction directly affects RPO.

---

## 23. Failover and Failback

### Failover

**Failover** is the process of moving service operation from a failed or unavailable primary system to an alternate system.

Failover can be:

- Automatic
- Manual
- Semi-automated

### Failback

**Failback** is the process of returning operations to the original or preferred production environment after the underlying problem has been resolved.

A complete recovery architecture should consider both.

For example:

**Primary failure → failover → recovery operations → primary restoration → failback**

Failback itself must be carefully controlled to avoid data inconsistency or another outage.

---

## 24. Disaster Recovery in Cloud Environments

Cloud environments provide several recovery capabilities, but moving workloads to the cloud does not automatically create a DR strategy.

Possible cloud DR mechanisms include:

- Cross-region replication
- Multi-zone deployment
- Automated infrastructure provisioning
- Infrastructure as Code
- Object-storage replication
- Managed database replication
- Cloud snapshots
- Backup vaults
- Automated failover
- Recovery environments that can be scaled when required

Organizations must still understand:

- Which data is replicated
- Where it is stored
- Who controls it
- How credentials are recovered
- What dependencies exist
- What recovery objectives are supported
- What happens if the cloud provider or region is unavailable

---

## 25. Infrastructure as Code and Recovery

Infrastructure as Code (IaC) can help rebuild infrastructure consistently.

Instead of manually configuring every server after a disaster, an organization can maintain machine-readable definitions for infrastructure resources.

Benefits include:

- Repeatability
- Faster provisioning
- Consistent configuration
- Reduced manual error
- Easier testing

However, IaC does not replace data backups.

IaC can help recreate infrastructure, while backups or replication preserve data and state.

---

## 26. Application Dependencies

A common DR failure occurs when an organization protects an application but forgets its dependencies.

An application may depend on:

- DNS
- Active Directory or another identity service
- Database servers
- APIs
- Certificate authorities
- Key-management systems
- Storage
- Network services
- Firewalls
- Load balancers
- External providers
- Authentication services

Recovering only the application server may therefore not restore the application.

### Dependency mapping

DR architecture should identify:

**Business service → Application → Database → Identity → Network → DNS → External dependencies**

Recovery order should reflect these dependencies.

---

## 27. Recovery Order and Prioritization

Not every system should necessarily be recovered simultaneously.

Critical systems should be prioritized based on business requirements.

A typical recovery sequence might involve:

1. Facilities and power
2. Network connectivity
3. Identity and authentication services
4. DNS and core infrastructure
5. Storage and databases
6. Critical application services
7. Supporting applications
8. Lower-priority systems
9. Validation and business-service restoration

The exact order depends on the architecture.

The important principle is:

> **Recover dependencies before dependent services.**

---

## 28. Disaster Recovery Testing

A DR plan that has never been tested is an assumption, not demonstrated capability.

Testing should validate both technology and organizational readiness.

### Tabletop exercise

A tabletop exercise is a discussion-based exercise in which participants walk through a hypothetical incident.

It validates:

- Roles
- Responsibilities
- Communication
- Decision-making
- Escalation procedures

It generally does not require actual system failure.

### Walkthrough

Participants review recovery procedures step by step to identify missing information, dependencies, or unclear responsibilities.

### Simulation

A simulated incident exercises procedures under realistic conditions without necessarily causing an actual production outage.

### Technical recovery test

Actual systems, backups, failover mechanisms, or recovery infrastructure are exercised.

This provides stronger evidence that the technical recovery capability works as intended.

---

## 29. Testing Progression

A mature recovery program may progress from low-risk activities to more realistic technical tests:

**Tabletop → Walkthrough → Simulation → Technical recovery/failover test**

Testing should be controlled so that the exercise itself does not create an unnecessary production outage.

---

## 30. Recovery Documentation

DR documentation should be sufficiently detailed that designated personnel can execute recovery procedures under stressful conditions.

Useful documentation includes:

- Recovery procedures
- System dependencies
- Network diagrams
- Application inventories
- Contact information
- Vendor information
- Escalation paths
- Credentials or secure credential-recovery procedures
- Backup locations
- Restoration sequences
- RTO/RPO requirements
- Failover procedures
- Failback procedures
- Validation procedures

Sensitive information should not be stored insecurely merely because it is needed during recovery.

---

## 31. Communication During Recovery

A major incident requires communication between technical teams, management, vendors, and potentially customers or regulators.

Recovery architecture should identify:

- Who declares the incident
- Who authorizes failover
- Who contacts vendors
- Who communicates with business units
- Who provides status updates
- Who handles regulatory notification when required
- Who approves return to normal operations

Technical recovery without coordinated communication can still result in operational failure.

---

## 32. Recovery of Identity and Security Services

Security services themselves must be recoverable.

Consider what happens if the recovery environment requires authentication through an identity service that exists only in the failed primary environment.

Recovery planning should therefore account for:

- Directory services
- Authentication
- MFA dependencies
- Privileged accounts
- Certificate authorities
- DNS
- Key management
- Secrets management
- Logging
- Security monitoring

Security controls should not become hidden dependencies that prevent legitimate recovery.

---

## 33. Backup and Ransomware Recovery

Ransomware can affect both production systems and connected backup infrastructure.

A resilient architecture should therefore separate backup management from ordinary production administration where practical.

Important controls include:

- Immutable backups
- Offline backups
- Separate backup credentials
- MFA
- Privileged access management
- Network segmentation
- Backup monitoring
- Restore testing
- Malware scanning during recovery
- Clean recovery environments

Recovery should also consider whether restoring a compromised backup would simply reintroduce malware into the environment.

---

## 34. Clean Recovery and Validation

Recovery is not complete merely because systems boot.

After restoration, the organization should validate:

- System integrity
- Application functionality
- Data consistency
- Identity services
- Network connectivity
- DNS resolution
- Security controls
- Logging
- Monitoring
- Endpoint protection
- Certificates
- External integrations

For a security incident, recovery should also establish confidence that the restored environment is not still compromised.

---

## 35. Single Points of Failure in DR Architecture

A recovery environment can contain its own SPOFs.

Examples:

- One recovery network link
- One DNS server
- One authentication server
- One backup repository
- One administrator account
- One cloud region
- One replication path
- One encryption key
- One vendor

The organization should analyze the recovery architecture itself for dependencies and failure points.

---

## 36. DR and High Availability Are Not Identical

High availability and disaster recovery both improve availability, but they address different problems.

### High availability

HA is primarily concerned with maintaining service availability through redundancy and rapid failover during component or system failures.

Example:

Two application servers operate behind a load balancer. If one fails, traffic is sent to the other.

### Disaster recovery

DR addresses restoration after a larger disruption, potentially involving an entire facility, environment, or major service dependency.

Example:

A data center becomes unavailable, and workloads are restored in another geographic region.

### Key distinction

**HA reduces interruption during failures.**

**DR provides a strategy for recovering from major disruptions.**

An organization may require both.

---

## 37. DR and Business Continuity

Business continuity is broader than disaster recovery.

Business continuity focuses on maintaining critical business operations during disruption.

Disaster recovery focuses more specifically on restoring technology and services.

For example:

- Business continuity asks how the organization will continue processing customer orders.
- Disaster recovery asks how the systems supporting those orders will be restored.

They are closely related but not interchangeable.

---

## 38. Security Considerations in Recovery Architecture

Recovery systems must receive the same security attention as production systems.

Security requirements include:

- Least privilege
- Strong authentication
- Encryption
- Network segmentation
- Logging
- Monitoring
- Secure configuration
- Vulnerability management
- Malware protection
- Access reviews
- Physical security

A poorly secured DR environment can become an attacker's alternate entry point.

---

## 39. Common DR Architecture Failures

### Failure 1 — Backups exist but restores are never tested

**Problem:** The organization assumes the backup works.

**Lesson:** Perform restoration testing.

### Failure 2 — All backups are online

**Problem:** Ransomware can potentially access and destroy them.

**Lesson:** Use offline or immutable copies where appropriate.

### Failure 3 — Primary and backup are in the same disaster zone

**Problem:** One event can affect both.

**Lesson:** Consider geographic separation.

### Failure 4 — Only the application server is backed up

**Problem:** Dependencies such as databases, DNS, identity, or certificates are missing.

**Lesson:** Map the complete service dependency chain.

### Failure 5 — RPO is confused with RTO

**Problem:** Recovery requirements are misunderstood.

**Lesson:** RTO = time; RPO = data loss.

### Failure 6 — Recovery environment lacks capacity

**Problem:** A standby system exists but cannot handle production workload.

**Lesson:** Capacity planning is part of DR architecture.

### Failure 7 — Recovery credentials are unavailable

**Problem:** Administrators cannot authenticate to the recovery environment.

**Lesson:** Include identity and privileged-access recovery in DR planning.

---

## 40. Security+ Scenario Reasoning

### Scenario 1 — Maximum acceptable downtime

A company states that its payment service must be restored within 30 minutes after an outage.

**Requirement:** RTO

Why? The requirement specifies the maximum recovery time.

---

### Scenario 2 — Maximum acceptable data loss

A company states that it cannot lose more than five minutes of transaction data.

**Requirement:** RPO

Why? The requirement describes the amount of data that can be lost, measured in time.

---

### Scenario 3 — Ransomware deletes backups

An attacker compromises production and deletes accessible backup copies.

**Architecture improvement:** Offline or immutable backups with separate administrative controls.

Why? The recovery copies need protection from compromise of the production environment.

---

### Scenario 4 — Rapid recovery required

A critical service must be restored almost immediately, and the organization has sufficient budget for highly prepared infrastructure.

**Architecture direction:** Hot-site, active-active, or other highly prepared failover architecture depending on the specific requirements.

Why? Low RTO requires recovery resources that are already available or can fail over quickly.

---

### Scenario 5 — Lowest-cost recovery

A noncritical application can tolerate several days of downtime.

**Architecture direction:** A cold site or slower restoration strategy may satisfy the requirement.

Why? The business requirement does not justify the same investment as a near-zero-downtime service.

---

### Scenario 6 — Backup exists but restoration fails

An organization discovers during an outage that its backup files are corrupt.

**Problem:** Lack of backup integrity validation and restore testing.

The correct architectural lesson is not merely "perform backups." It is:

**Back up → protect → validate → test restoration.**

---

### Scenario 7 — Primary and DR facilities share the same region

A regional disaster affects both facilities.

**Problem:** Insufficient geographic diversity.

**Architecture consideration:** Use an appropriately separated recovery location or region based on the threat model and business requirements.

---

## 41. Common Security+ Exam Traps

### RTO vs RPO

- **RTO:** maximum targeted downtime
- **RPO:** maximum targeted data loss

### Incremental vs differential

- **Incremental:** changes since previous backup
- **Differential:** changes since last full backup

### Hot vs warm vs cold

- **Hot:** highly prepared and fastest recovery
- **Warm:** partially prepared
- **Cold:** least prepared and slower recovery

### HA vs DR

- **HA:** keeps services available through redundancy/failover
- **DR:** restores services after major disruption

### Backup vs replication

- **Backup:** retained copy used for recovery
- **Replication:** maintains another copy, often with a much smaller recovery-point gap

Replication does not automatically replace a backup strategy. Replication can copy corruption or malicious changes as well as legitimate data.

### Snapshot vs backup

A snapshot can provide rapid rollback but should not automatically be considered an independent, resilient backup.

---

## 42. Recovery Architecture Decision Framework

When solving a Security+ recovery scenario, use this sequence:

### Step 1 — Identify the business service

What must be protected?

### Step 2 — Determine the RTO

How quickly must it return?

### Step 3 — Determine the RPO

How much data loss is acceptable?

### Step 4 — Identify dependencies

What other systems must be available first?

### Step 5 — Identify failure scope

Is the problem a server, network, facility, region, provider, or entire environment?

### Step 6 — Select the architecture

Consider:

- Redundancy
- Replication
- Backup
- Hot/warm/cold site
- Cloud recovery
- Geographic separation
- Automated failover

### Step 7 — Protect the recovery environment

Apply:

- IAM
- MFA
- Segmentation
- Encryption
- Monitoring
- Immutable/offline backup controls

### Step 8 — Test

Verify that the architecture actually satisfies the required recovery objectives.

---

## 43. Practical Recovery Architecture Example

Consider an e-commerce organization with:

- Web servers
- Application servers
- Database servers
- Identity services
- DNS
- Payment integrations
- Customer data

The organization requires:

- RTO: 30 minutes
- RPO: 5 minutes

A possible architecture could include:

1. Multiple application instances for HA
2. Load balancing
3. Database replication
4. Frequent or near-real-time data protection
5. A geographically separated recovery environment
6. Automated infrastructure provisioning
7. Immutable backup copies
8. Separate backup administration
9. Continuous monitoring
10. Regular technical recovery testing

The exact technology is less important than whether the complete architecture satisfies the business requirements.

---

## 44. Key Takeaways

1. **Disaster recovery restores technology services after significant disruption.**
2. **RTO measures the required recovery time.**
3. **RPO measures acceptable data loss over time.**
4. **Full backups capture the selected data set.**
5. **Incremental backups capture changes since the previous backup.**
6. **Differential backups capture changes since the last full backup.**
7. **Backups should be protected against compromise of production systems.**
8. **Offline and immutable copies can improve resilience against ransomware.**
9. **Hot sites provide high readiness and rapid recovery.**
10. **Warm sites provide intermediate readiness.**
11. **Cold sites require substantial preparation before recovery.**
12. **Replication can reduce recovery-point gaps but does not automatically replace backups.**
13. **Snapshots are not automatically equivalent to independent backups.**
14. **Geographic separation helps protect against regional disasters.**
15. **Recovery dependencies must be mapped before recovery architecture is finalized.**
16. **Failover moves services to alternate infrastructure; failback returns them to the preferred environment.**
17. **Cloud environments can provide DR capabilities but still require deliberate architecture and testing.**
18. **IaC can accelerate infrastructure reconstruction but does not replace data protection.**
19. **DR testing validates whether the documented architecture actually works.**
20. **HA and DR are complementary: HA reduces service interruption, while DR addresses recovery from major disruption.**
21. **The strongest DR design is driven by business requirements, dependencies, security, recovery objectives, and testing—not by a backup product alone.**
