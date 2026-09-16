# Resilience, Redundancy, and High Availability

## 1. Introduction

Security architecture is not only about preventing unauthorized access. An enterprise must also remain available when components fail, networks are disrupted, systems become overloaded, or a security incident affects production infrastructure. This is the purpose of **resilience, redundancy, high availability, fault tolerance, and recovery-oriented architecture**.

A resilient architecture assumes that failures can occur and designs the environment so that a failure does not automatically become a major business outage. The objective is not simply to add more hardware. The architecture must identify important services, understand their dependencies, eliminate unacceptable single points of failure, provide sufficient capacity, and define how the environment will continue operating or recover.

A useful Security+ relationship is:

**Business requirement → Availability requirement → Failure analysis → Architecture → Redundancy/HA controls → Monitoring and failover → Testing → Recovery**

---

## 2. Resilience

**Resilience** is the ability of a system, service, or organization to withstand disruption, continue providing an acceptable level of service, and recover or adapt when necessary.

Resilience is broader than simply having duplicate servers. It can include:

- Redundant infrastructure
- High-availability configurations
- Fault-tolerant components
- Backup systems
- Disaster recovery capabilities
- Alternate network paths
- Geographic redundancy
- Capacity planning
- Monitoring and alerting
- Automated failover
- Manual recovery procedures
- Tested recovery processes
- Security controls that prevent one incident from disabling the entire environment

A resilient architecture considers both **technical failure** and **operational disruption**. For example, a server may remain available after a disk failure because it uses redundant storage, while a business service may still become unavailable if its only authentication service fails. Resilience therefore has to be evaluated across dependencies rather than only at the individual component level.

### Resilience Is Not the Same as Recovery

Recovery generally focuses on restoring service after disruption. Resilience includes the ability to absorb or withstand disruption and continue operating where possible.

For example:

- A backup restored three hours after a server failure provides recovery capability.
- A redundant server that immediately takes over provides high availability.
- A fault-tolerant system that continues operating despite a component failure provides fault tolerance.
- An architecture combining these capabilities provides broader resilience.

---

## 3. Redundancy

**Redundancy** means providing additional components, paths, or resources so that the failure of one component does not necessarily cause service failure.

Examples include:

- Two network switches instead of one
- Multiple Internet connections
- Multiple power supplies
- Multiple storage devices
- Multiple application servers
- Multiple domain controllers
- Multiple DNS servers
- Multiple database nodes
- Redundant firewalls
- Multiple load balancers
- Multiple availability zones
- Multiple physical locations

Redundancy is useful only when the redundant component can actually take over the required workload.

### Example

Suppose an organization has a production application server capable of handling 1,000 concurrent users. A standby server can handle only 100 users.

Although a second server exists, it does not provide adequate capacity for a complete failure. The architecture therefore has redundancy, but the redundancy may not satisfy the organization's availability requirement.

This is an important Security+ scenario concept:

> **Redundancy must include sufficient capacity, not merely duplicate equipment.**

---

## 4. Single Point of Failure

A **single point of failure (SPOF)** is a component whose failure can cause a service or larger system to become unavailable because there is no adequate alternative path or component.

Common examples include:

- One firewall protecting the entire organization
- One Internet circuit
- One power source
- One DNS server
- One authentication server
- One database server
- One core switch
- One storage controller
- One application server
- One cooling system
- One physical data center

### SPOF Analysis

Architecture reviews should identify dependencies and ask:

1. What happens if this component fails?
2. Is there another component that can perform the same function?
3. Will traffic automatically fail over?
4. Does the alternate component have enough capacity?
5. Is the alternate component dependent on the failed component?
6. Has failover actually been tested?

A common mistake is to create apparent redundancy while leaving a hidden dependency.

### Example of Hidden SPOF

An organization deploys two redundant application servers, but both depend on one database server. If the database fails, both application servers may become unusable.

The application tier is redundant, but the overall application architecture still contains a database SPOF.

---

## 5. High Availability

**High availability (HA)** is an architecture designed to minimize service interruption by using redundant components, failover mechanisms, clustering, load balancing, monitoring, and other availability controls.

HA does not necessarily mean zero downtime. Instead, the objective is to reduce the probability, duration, and impact of service interruption to an acceptable level.

High availability commonly uses:

- Clustering
- Failover
- Load balancing
- Active-active systems
- Active-passive systems
- Redundant network paths
- Redundant power
- Multiple availability zones
- Health checks
- Automated service restart
- Replication
- Geographic redundancy

---

## 6. Active-Active Architecture

In an **active-active** architecture, multiple systems are actively processing production workloads at the same time.

For example:

```text
                 Users
                   |
             Load Balancer
              /         \
             /           \
        Server A       Server B
        ACTIVE         ACTIVE
```

Both servers contribute to the workload. If one fails, the remaining server can continue serving traffic, assuming it has sufficient capacity.

### Advantages

- Uses resources continuously
- Can provide strong availability
- Can distribute workload
- Can scale horizontally
- Failure of one node does not necessarily stop service

### Considerations

- Application state may need synchronization
- Shared data must remain consistent
- Load balancing must detect unhealthy nodes
- Remaining nodes must have enough capacity
- More complex configuration may be required

---

## 7. Active-Passive Architecture

In an **active-passive** architecture, one component normally handles production traffic while another remains available as a standby.

```text
              Production Traffic
                     |
                Primary A
                 ACTIVE
                     |
              Standby B
                PASSIVE
```

If the primary fails, the standby becomes active through an automated or manual failover process.

### Advantages

- Can simplify application state management
- Standby infrastructure is available for failover
- Useful for systems that do not support multiple active instances

### Limitations

- Passive resources may be underutilized
- Failover may introduce downtime
- Standby capacity must be sufficient
- Failover configuration itself can fail
- Data synchronization must be maintained

---

## 8. Failover

**Failover** is the process of transferring service from a failed or unavailable component to another component.

Failover can be:

### Automatic Failover

The environment detects a failure and switches to another resource automatically.

Examples:

- Load balancer removes an unhealthy server
- Cluster promotes a standby node
- Redundant firewall takes over
- Virtual machine automatically restarts on another host

Automatic failover can reduce recovery time, but it must be carefully designed and tested. Incorrect health checks can cause unnecessary failovers or fail to recognize real failures.

### Manual Failover

An administrator performs the transition.

Manual failover may be appropriate when:

- The environment is highly sensitive to incorrect automatic actions
- Human verification is required
- The failure condition is difficult to detect automatically
- The service requires controlled transition

The trade-off is that manual failover generally takes longer.

---

## 9. Failback

**Failback** is the process of returning service to the original or preferred component after it has been repaired or restored.

Example:

```text
Normal:
Server A → Active
Server B → Standby

Failure:
Server A → Failed
Server B → Active

After repair:
Server A → Restored
Server B → Active

Failback:
Server A → Active
Server B → Standby
```

Failback should be planned carefully. Immediately switching back without validation can cause another outage if the original component has not been fully repaired or synchronized.

---

## 10. Fault Tolerance

**Fault tolerance** is the ability of a system to continue operating despite the failure of certain components.

Fault tolerance generally aims for extremely low interruption or seamless continuation of service.

Examples can include:

- RAID protecting against disk failure
- Redundant power supplies
- Multiple network interfaces
- Redundant network paths
- Fault-tolerant servers
- Replicated processing components

Fault tolerance is stronger than simply having a spare component. The system is designed to continue functioning while the failure occurs.

### Fault Tolerance vs High Availability

High availability usually focuses on minimizing downtime through failover and redundancy. Fault tolerance aims to continue operation despite a defined component failure, potentially with little or no visible interruption.

Fault-tolerant architectures can be more expensive and complex because they may require duplicated processing, synchronized state, specialized hardware, or continuous replication.

---

## 11. Clustering

A **cluster** is a group of systems working together to provide a service.

Clusters can provide:

- High availability
- Load distribution
- Failover
- Scalability
- Maintenance flexibility

A cluster may use active-active or active-passive designs depending on the technology and business requirement.

### Cluster Failure Considerations

A cluster does not automatically guarantee availability. Consider:

- Shared storage dependencies
- Shared databases
- Cluster network dependencies
- Quorum requirements
- Authentication dependencies
- DNS dependencies
- Management-plane dependencies
- Licensing or software dependencies

The complete service architecture must be evaluated rather than assuming that multiple nodes eliminate every failure scenario.

---

## 12. Load Balancing

A **load balancer** distributes network or application traffic across multiple backend systems.

For example:

```text
                 Clients
                    |
              Load Balancer
             /      |      \
            /       |       \
        Web-1     Web-2     Web-3
```

Load balancing can improve both availability and scalability.

### Health Checks

Load balancers can perform health checks to determine whether backend systems are available.

If Web-2 becomes unhealthy, the load balancer can stop sending new traffic to it while continuing to use healthy servers.

### Security Benefits

Depending on architecture, a load balancer can also:

- Reduce direct exposure of backend servers
- Centralize TLS termination
- Support traffic filtering
- Provide logging
- Integrate with WAF capabilities

Load balancing is not automatically a security control. Its primary purpose is traffic distribution and availability, although some implementations provide additional security functions.

---

## 13. Geographic Redundancy

Geographic redundancy places redundant systems in different physical locations.

This protects against events that affect an entire facility, such as:

- Natural disasters
- Major power failures
- Fires
- Flooding
- Regional network failures
- Facility-wide security incidents

Possible architectures include:

- Multiple data centers
- Multiple cloud regions
- Multiple availability zones
- Colocation facilities
- Disaster recovery sites

Geographic redundancy is particularly important when the failure domain is larger than a single server or rack.

### Failure Domain

A **failure domain** is a set of components that may fail because they share a common dependency or event.

For example, two servers in the same rack may be redundant against a server failure but not against a rack-level power failure.

Similarly, two cloud instances in the same availability zone may not protect against an availability-zone outage.

A strong architecture places redundancy across appropriate failure domains.

---

## 14. Power Redundancy

Power failure is an important availability concern.

Common controls include:

### UPS

An **uninterruptible power supply (UPS)** provides temporary power when the primary electrical supply fails. It can also help protect systems from certain power-quality problems.

UPS systems provide time for:

- Generators to start
- Systems to shut down safely
- Power service to be restored

### Generators

Generators can provide longer-duration backup power when utility power is unavailable.

### Dual Power Supplies

Servers may use multiple power supply units connected to separate power sources or circuits.

The goal is to avoid a single power component disabling the server.

### Important Architecture Point

Two power supplies connected to the same failed upstream power source do not necessarily provide true power-path redundancy. The complete power chain must be considered.

---

## 15. Network Redundancy

Network availability can be improved through:

- Multiple switches
- Multiple routers
- Multiple firewalls
- Multiple Internet service providers
- Redundant links
- Link aggregation
- Dynamic routing
- Alternate paths
- Redundant VPN tunnels
- Diverse physical paths

### Path Diversity

Two network links are more resilient when they do not share the same physical failure point.

For example, two fiber connections entering the building through the same conduit may both fail if the conduit is damaged.

True resilience therefore considers **physical path diversity**, not merely the number of cables.

---

## 16. Storage Redundancy

Storage redundancy protects against storage-component failures and can support availability.

Common technologies include RAID and replicated storage.

### RAID

RAID combines multiple drives to provide redundancy, performance, or both depending on the RAID level.

Examples:

- **RAID 0:** striping without redundancy
- **RAID 1:** mirroring
- **RAID 5:** striping with distributed parity and protection against a single drive failure
- **RAID 6:** distributed parity allowing protection against two drive failures
- **RAID 10:** combination of mirroring and striping

RAID improves storage availability in certain failure scenarios, but **RAID is not a backup**. It does not by itself protect against accidental deletion, ransomware, corruption, or site-wide destruction.

---

## 17. Database Resilience

Databases can become major availability dependencies. Common approaches include:

- Replication
- Database clustering
- Synchronous replication
- Asynchronous replication
- Read replicas
- Automatic failover
- Distributed database architectures

### Synchronous Replication

Data is replicated to another system as part of the write operation. This can reduce data loss during failure but may introduce latency and requires suitable connectivity and architecture.

### Asynchronous Replication

Data is replicated after the primary operation completes. This can provide greater performance or geographic flexibility, but the secondary system may temporarily lag behind the primary.

The choice depends on requirements such as performance, distance, consistency, and acceptable data loss.

---

## 18. Capacity Planning

Availability architecture must consider **capacity**, not just component count.

Suppose three web servers each operate at 40% utilization during normal conditions. If one fails, the remaining two may still have enough capacity to handle the workload.

Now suppose two servers normally operate at 80% utilization. Losing one may overload the remaining server even though the architecture technically contains redundancy.

Capacity planning should consider:

- Normal utilization
- Peak utilization
- Expected growth
- Failure scenarios
- Maintenance operations
- Traffic spikes
- Attack traffic
- Resource exhaustion

### N+1 and N+2

**N** represents the number of components required to handle the workload.

- **N+1:** enough capacity for the required workload plus one additional component
- **N+2:** enough capacity for the required workload plus two additional components

For example, if four servers are required to handle the production workload, an N+1 architecture would provide five servers.

The correct level depends on business requirements and risk tolerance.

---

## 19. Maintenance and Resilience

Availability architecture should support maintenance without unnecessary service interruption.

Examples include:

- Rolling updates
- Redundant nodes
- Live migration
- Maintenance failover
- Clustered applications
- Blue/green deployment
- Canary deployment

A redundant architecture can allow administrators to take one node offline while other nodes continue serving users.

However, maintenance procedures must account for reduced redundancy during the maintenance window. If an environment normally has N+1 capacity and one redundant node is removed, another failure may create an outage.

---

## 20. Monitoring and Health Detection

HA systems require accurate monitoring to determine whether components are healthy.

Useful signals include:

- CPU utilization
- Memory utilization
- Disk health
- Network availability
- Application response time
- Service status
- Database connectivity
- Replication status
- Cluster status
- Power status
- Storage status

### Health Checks

A basic network health check may confirm that a host responds to a connection. A deeper application health check may verify that the actual service is functioning correctly.

For example, a web server can respond to ICMP while its application is returning errors. Therefore, a simple ping may not be sufficient as an HA health check.

Good health checks should detect meaningful service failure without causing unnecessary failover.

---

## 21. Redundancy and Security Architecture

Availability and security are closely related.

A security control can itself become a single point of failure. For example, an organization may deploy a highly secure firewall but use only one firewall appliance. If it fails, all external connectivity may be lost.

Security architecture should therefore consider redundant:

- Firewalls
- VPN gateways
- Authentication services
- DNS infrastructure
- Logging infrastructure where required
- Network paths
- Security monitoring components
- Identity services

The goal is not to duplicate every component automatically. Redundancy should be based on business criticality and failure impact.

---

## 22. Resilience and Defense in Depth

Defense in depth is primarily a security strategy, while resilience focuses strongly on continued operation and recovery. However, the two concepts can reinforce each other.

For example:

```text
Internet
   |
Firewall Cluster
   |
DMZ
   |
Load Balancer
   |
Web Cluster
   |
Application Cluster
   |
Database Replication
   |
Backup / Recovery
```

This architecture uses multiple layers so that the failure or compromise of one component does not automatically expose or disable the entire service.

However, adding layers also adds complexity. Every additional component introduces configuration, monitoring, maintenance, and dependency requirements.

---

## 23. Redundancy vs Backup

These concepts are often confused.

### Redundancy

Redundancy provides an alternate component or path so service can continue when a component fails.

Example:

> A second application server takes over when the first server fails.

### Backup

A backup is a separate copy of data used for restoration after data loss, corruption, deletion, or another recovery event.

Example:

> A database backup is restored after ransomware encrypts the production database.

A redundant system can replicate corruption or malicious changes, so redundancy does not replace backups.

---

## 24. Resilience vs Disaster Recovery

**Resilience** emphasizes the ability to withstand and continue through disruption.

**Disaster recovery (DR)** focuses on restoring IT services after a major disruption.

For example:

- A redundant firewall pair provides high availability.
- A secondary data center provides geographic resilience and can support DR.
- Backups support restoration after data loss.
- A documented DR plan defines how systems are restored following a major event.

These capabilities complement one another but are not interchangeable.

---

## 25. Cloud Availability Architecture

Cloud environments provide availability mechanisms such as:

- Multiple availability zones
- Multiple regions
- Load balancers
- Auto-scaling
- Managed database replication
- Object-storage redundancy
- Health checks
- Automated instance replacement

Cloud architecture does not automatically guarantee resilience. If an organization deploys all workloads into one availability zone, it may retain a significant failure dependency.

### Cloud Design Principle

Distribute critical workloads across appropriate failure domains while considering:

- Application architecture
- Data consistency
- Network latency
- Cost
- Data residency
- Recovery requirements
- Service dependencies

---

## 26. Auto-Scaling

**Auto-scaling** automatically adjusts computing resources based on workload or defined conditions.

It can improve availability during unexpected increases in demand.

For example:

```text
Normal demand → 3 application instances
High demand  → 6 application instances
Demand falls  → 3 application instances
```

Auto-scaling can help protect against resource exhaustion, but it does not solve every availability problem. If a shared database, DNS service, authentication service, or network dependency fails, adding more application instances may not restore the service.

---

## 27. Security and Availability Trade-Offs

Security architecture often involves trade-offs.

Examples:

- Strict traffic inspection may introduce latency.
- Multiple security appliances increase availability but also increase complexity.
- Geographic redundancy improves resilience but increases cost.
- Synchronous replication may improve consistency but increase latency.
- Automatic failover reduces recovery time but may create incorrect transitions if health checks are poorly designed.
- Highly restrictive security controls may affect availability if legitimate dependencies are blocked.

Security+ questions often test whether the proposed architecture satisfies the **actual business requirement**, rather than whether the technology sounds more advanced.

---

## 28. Testing High Availability

A redundant architecture is only trustworthy when failover has been tested.

Testing can include:

- Controlled server failure
- Network-link failure
- Firewall failover
- Storage failure
- Power-path failure
- Database failover
- Availability-zone failure simulation where appropriate
- Restoration testing
- Application health validation

Testing should verify:

1. Failure is detected.
2. The correct component takes over.
3. Required capacity remains available.
4. Data remains consistent within defined requirements.
5. Users can access the service.
6. Monitoring records the event.
7. Alerts are generated appropriately.
8. Failback works correctly when required.

Untested failover should not be assumed to work merely because the architecture diagram contains redundant components.

---

## 29. Common Availability Failure Patterns

### 29.1 Redundant Servers, Shared Database SPOF

Multiple application servers exist, but all depend on one database server.

**Problem:** database failure disables the service.

**Lesson:** analyze dependencies across the complete service chain.

### 29.2 Two Links, One Provider

Two Internet connections are installed, but both use the same physical provider infrastructure.

**Problem:** a provider-side failure can affect both links.

**Lesson:** redundancy should consider provider and physical-path diversity.

### 29.3 Backup Server Without Enough Capacity

A standby server exists but cannot handle the production workload.

**Problem:** failover causes resource exhaustion.

**Lesson:** redundancy must include capacity planning.

### 29.4 RAID Treated as Backup

An organization assumes RAID protects against ransomware and accidental deletion.

**Problem:** RAID protects against certain disk failures, not all data-loss scenarios.

**Lesson:** maintain independent backups.

### 29.5 HA Without Monitoring

Two servers exist, but the load balancer cannot correctly identify an unhealthy application.

**Problem:** traffic continues to be sent to the failed service.

**Lesson:** HA requires reliable health detection.

### 29.6 Automatic Failover Without Testing

Failover is configured but has never been tested.

**Problem:** configuration errors may remain undiscovered until a real outage.

**Lesson:** test failover and recovery regularly.

---

## 30. Important Distinctions for Security+

| Concept | Primary Purpose |
|---|---|
| Resilience | Withstand disruption and recover/adapt effectively |
| Redundancy | Provide alternate components or paths |
| High availability | Minimize service interruption |
| Fault tolerance | Continue operating despite defined component failures |
| Failover | Move service to an alternate component |
| Failback | Return service to the preferred/original component |
| Clustering | Combine systems to provide a service, often for HA or scalability |
| Load balancing | Distribute traffic across systems |
| Geographic redundancy | Protect against site or regional failures |
| Backup | Restore lost, corrupted, or deleted data |
| Disaster recovery | Restore services after major disruption |
| Auto-scaling | Dynamically adjust capacity based on demand |
| SPOF | Component whose failure can cause service disruption |

---

## 31. Security+ Scenario Reasoning

When a question describes a service that **must remain available if one server fails**, think about redundancy, clustering, load balancing, or failover.

When it says **multiple systems actively process traffic**, think **active-active**.

When it says **one primary system runs while another waits for failure**, think **active-passive**.

When it says the system **continues operating despite a component failure**, think **fault tolerance**.

When it asks how to **distribute requests across multiple servers**, think **load balancing**.

When it describes a failure affecting an entire building or region, think about **geographic redundancy and separate failure domains**.

When it describes recovering data after deletion or ransomware, think **backup and recovery**, not merely redundancy.

When the question emphasizes **avoiding downtime during maintenance**, consider HA, clustering, rolling maintenance, and redundant capacity.

When a proposed solution has duplicate components but both depend on the same underlying service, look for the **hidden SPOF**.

---

## 32. Architecture Decision Checklist

When designing or evaluating resilience and availability, ask:

### Business Requirements

- Which services are critical?
- What level of downtime is acceptable?
- What recovery requirements exist?
- What performance level must be maintained during failure?

### Failure Analysis

- What can fail?
- What is the failure domain?
- Are there single points of failure?
- Could one incident affect multiple redundant components?

### Architecture

- Is active-active or active-passive appropriate?
- Is fault tolerance required?
- Is geographic redundancy required?
- Is load balancing required?
- Are network and power paths redundant?

### Capacity

- Can the surviving systems handle the workload?
- Is N+1 or greater capacity necessary?
- What happens during peak demand?

### Dependencies

- Is authentication redundant?
- Is DNS redundant?
- Is storage redundant?
- Is the database redundant?
- Are external providers redundant where necessary?

### Operations

- Is failover monitored?
- Is failover tested?
- Is failback documented?
- Are administrators alerted?
- Are maintenance procedures safe when redundancy is temporarily reduced?

---

## 33. Common Security+ Exam Traps

### Trap 1: Redundancy = High Availability

Redundancy is a mechanism that can support availability. High availability is the broader architecture and objective of minimizing interruption.

### Trap 2: RAID = Backup

RAID provides protection against certain storage failures. It is not a replacement for independent backups.

### Trap 3: Two Components Automatically Eliminate an SPOF

The two components may share a common dependency such as power, network connectivity, storage, DNS, or authentication.

### Trap 4: Active-Passive Means No Downtime

Failover may take time, and the standby must be correctly configured and synchronized.

### Trap 5: More Redundancy Is Always Better

Additional redundancy increases cost and architectural complexity. The design should match business requirements and risk.

### Trap 6: Cloud Means Automatically Highly Available

Cloud platforms provide availability capabilities, but the customer must architect workloads appropriately across failure domains.

### Trap 7: Load Balancing Is Only About Performance

Load balancing can distribute workloads and also improve availability by removing unhealthy systems from service.

### Trap 8: A Backup Can Replace HA

A backup supports restoration but normally does not provide the immediate service continuity expected from an HA architecture.

---

## 34. Practical Example: Highly Available Web Application

Consider an e-commerce application that must remain available if one application server fails.

A possible architecture is:

```text
                         Internet
                            |
                    Redundant Firewall Pair
                            |
                     Load Balancer Pair
                       /           \
                      /             \
              Web Server A       Web Server B
                  ACTIVE              ACTIVE
                      \             /
                       \           /
                    Application Tier
                           |
                  Database Cluster
                     /          \
                    /            \
             Database A      Database B
                    |
             Replicated Storage
                    |
              Independent Backups
```

The architecture addresses several different failure scenarios:

- Firewall failure → redundant firewall can take over.
- Web-server failure → load balancer removes unhealthy server.
- Application-node failure → another node continues processing.
- Database-node failure → database failover can occur.
- Storage failure → storage redundancy may preserve availability.
- Data corruption/ransomware → independent backups support recovery.

The important lesson is that **different availability problems require different controls**.

---

## 35. Key Takeaways

1. **Resilience** is the broader ability to withstand disruption and recover or adapt effectively.
2. **Redundancy** provides alternate components or paths so individual failures do not automatically cause outages.
3. **High availability** minimizes service interruption through architectures such as clustering, failover, load balancing, and redundant infrastructure.
4. **Fault tolerance** aims to continue operation despite defined component failures.
5. **Active-active** systems actively process workloads simultaneously.
6. **Active-passive** systems use a primary component and a standby component.
7. **Failover** transfers service to an alternate component; **failback** returns service when appropriate.
8. Always identify **single points of failure** and hidden shared dependencies.
9. Redundancy must include **sufficient capacity** to handle failure conditions.
10. Geographic and physical-path diversity are important when the failure domain extends beyond one device.
11. **RAID is not a backup**.
12. Cloud environments require deliberate architecture across appropriate failure domains; cloud adoption alone does not guarantee HA.
13. Monitoring and health checks are essential for effective automated failover.
14. Failover and recovery must be **tested**, not merely documented or assumed to work.
15. Security architecture should itself avoid becoming a single point of failure.
16. Security+ scenario questions usually require matching the **business availability requirement and failure condition** to the appropriate architecture.
