# Cloud Security Architecture

## Purpose

Cloud security architecture is the design of security controls, trust boundaries, identities, networks, workloads, data, and management processes within cloud environments. Cloud computing changes where infrastructure runs and who manages particular layers, but it does not remove the need for security architecture.

A secure cloud design must answer several questions:

- Who owns and manages each security responsibility?
- Which resources are publicly reachable?
- Which identities can access them?
- How are workloads isolated?
- Where is sensitive data stored and processed?
- How are encryption keys and secrets protected?
- How are configurations monitored?
- How are cloud activities logged and investigated?
- How will the organization recover from compromise or service disruption?

A useful Security+ model is:

**Identity → Network → Workload → Data → Management plane → Logging → Resilience**

Cloud security is therefore an architecture problem as much as a technology problem.

---

## 1. Cloud Computing Fundamentals

Cloud computing provides on-demand access to computing resources such as:

- Compute
- Storage
- Networking
- Databases
- Applications
- Security services
- Development platforms

Cloud resources can generally be provisioned and modified more rapidly than traditional physical infrastructure.

This creates security advantages such as automation and centralized policy enforcement, but it can also increase risk when users can rapidly create resources without appropriate governance.

Common cloud characteristics include:

- On-demand self-service
- Broad network access
- Resource pooling
- Rapid elasticity
- Measured or metered service

From a security perspective, rapid provisioning means that identity, configuration, logging, and policy controls must operate at cloud speed.

---

## 2. Cloud Service Models

Security+ commonly distinguishes three major cloud service models:

1. Infrastructure as a Service (IaaS)
2. Platform as a Service (PaaS)
3. Software as a Service (SaaS)

The major difference is **how much of the technology stack is managed by the cloud provider versus the customer**.

---

## 3. Infrastructure as a Service (IaaS)

**IaaS** provides virtualized infrastructure such as:

- Virtual machines
- Virtual networks
- Storage
- Load balancers
- Network interfaces

The customer generally manages more of the operating environment than in PaaS or SaaS.

A simplified model is:

```text
Application        → Customer
Guest OS           → Customer
Virtual resources  → Shared/provider infrastructure
Physical hardware  → Provider
```

Customer security responsibilities may include:

- Operating-system patching
- Application security
- Identity and access management
- Network configuration
- Security groups/firewall rules
- Data protection
- Secrets
- Workload monitoring

### Security+ scenario

If a cloud customer deploys a VM and fails to patch its operating system, the customer may still be responsible even though the physical server is owned by the cloud provider.

---

## 4. Platform as a Service (PaaS)

**PaaS** provides a managed platform on which customers deploy applications without managing as much underlying infrastructure.

The provider generally manages more of:

- Operating system infrastructure
- Runtime platform
- Underlying hardware
- Platform maintenance

The customer remains responsible for areas such as:

- Application code
- Application configuration
- Data
- Identities and permissions
- Application-level security

PaaS reduces infrastructure management overhead but does not eliminate customer security responsibilities.

---

## 5. Software as a Service (SaaS)

**SaaS** provides a complete application service managed primarily by the provider.

Examples include cloud-hosted:

- Email
- Collaboration platforms
- CRM systems
- Business applications
- Document management systems

The provider manages most underlying infrastructure and application platform components.

The customer still needs to secure:

- User identities
- Authentication
- MFA
- Authorization
- Data handling
- Configuration
- Sharing permissions
- Administrative accounts
- Usage policies

A common mistake is assuming that because a SaaS provider manages the application infrastructure, the customer no longer has security responsibilities.

---

## 6. Service Model Comparison

| Layer | IaaS | PaaS | SaaS |
|---|---|---|---|
| Physical hardware | Provider | Provider | Provider |
| Virtualization/infrastructure | Mostly provider | Provider | Provider |
| OS/platform | Customer manages more | Provider manages more | Provider |
| Application | Customer | Customer | Provider |
| Data | Customer | Customer | Customer/shared responsibility |
| Identity/configuration | Customer | Customer | Customer |

The exact division varies by provider and service, so the organization must verify the provider's documented responsibility model rather than relying on assumptions.

---

## 7. Shared Responsibility Model

The **shared responsibility model** divides security and operational responsibilities between the cloud provider and the customer.

A useful conceptual model is:

```text
Cloud Provider
├── Physical facilities
├── Physical hardware
├── Core infrastructure
└── Provider-managed services

Customer
├── Identity and access
├── Data
├── Configuration
├── Workloads
└── Application security
```

The exact boundary changes depending on the service model.

### Important principle

**Cloud security is shared, not transferred completely to the provider.**

Customers must understand which controls are inherited from the provider and which they must implement themselves.

---

## 8. Cloud Deployment Models

Common deployment models include:

### Public Cloud

Infrastructure is operated by a cloud provider and made available to multiple customers.

### Private Cloud

Cloud infrastructure is dedicated to a single organization.

### Hybrid Cloud

Combines private/on-premises resources with public cloud resources.

### Community Cloud

Infrastructure is designed for organizations with shared requirements or interests.

The important security considerations are:

- Ownership
- Access
- Isolation
- Regulatory requirements
- Data location
- Operational responsibility

---

## 9. Cloud Identity and Access Management

Identity is one of the most important security boundaries in cloud environments.

Cloud resources are often accessed through APIs and management consoles rather than physical interfaces.

Therefore, a compromised cloud identity can potentially control significant infrastructure.

Important controls include:

- Strong authentication
- MFA
- Role-based access control
- Least privilege
- Privileged access management
- Conditional access
- Short-lived credentials where supported
- Access reviews
- Service identities
- Logging

The principle is:

**Authenticate the identity, evaluate context, authorize the specific action, and record the activity.**

---

## 10. Human and Workload Identities

Cloud environments commonly contain both human identities and workload identities.

### Human Identity

Examples:

- Administrator
- Developer
- Security analyst
- Help desk user

### Workload Identity

Examples:

- Application service
- VM workload
- Container
- Serverless function
- Automated deployment process

Workload identities should not automatically receive broad administrative permissions.

For example, an application that only needs to read objects from one storage location should receive a narrowly scoped role rather than full account administration.

---

## 11. Federation and Single Sign-On

Cloud environments often integrate with enterprise identity providers.

**Federation** allows authentication and identity relationships to operate across security domains.

**Single Sign-On (SSO)** allows users to authenticate through a central identity system and access multiple services without separately managing credentials for each service.

Security benefits include:

- Centralized authentication
- Centralized account lifecycle management
- Consistent MFA
- Reduced password reuse
- Centralized logging
- Faster account revocation

However, the central identity provider becomes a critical dependency and must be strongly protected.

---

## 12. MFA in Cloud Environments

Multi-factor authentication significantly reduces the risk associated with stolen passwords.

Factors commonly include:

- Something you know
- Something you have
- Something you are

MFA should receive particular attention for:

- Cloud administrators
- Privileged users
- Root/break-glass accounts
- Developers with production access
- Security administrators

A cloud account with administrative permissions and only a password presents a high-value target.

---

## 13. Privileged Cloud Accounts

Cloud root or highly privileged administrative accounts can control large portions of an environment.

Security architecture should minimize direct use of such accounts.

Controls include:

- MFA
- Separate administrative identities
- Least privilege
- Privileged access management
- Short-lived privileged access
- Logging
- Alerting
- Emergency-account procedures

Administrative accounts should not be used for ordinary daily activities when a lower-privileged identity is sufficient.

---

## 14. Cloud Network Architecture

Cloud providers typically provide software-defined networking capabilities.

Common components include:

- Virtual networks/VPCs
- Subnets
- Route tables
- Security groups
- Network ACLs
- Cloud firewalls
- Load balancers
- Private endpoints
- NAT gateways

A secure design should separate public-facing services from private workloads.

Example:

```text
Internet
   |
Public Load Balancer
   |
Web/Application Tier
   |
Private Database Tier
```

The database should not need to be directly reachable from the public internet.

---

## 15. Public and Private Subnets

A **public subnet** generally contains resources with a path to or from the public internet through the cloud architecture.

A **private subnet** is designed to reduce direct internet exposure.

A common architecture is:

```text
Internet
   |
Public Subnet
   |
Load Balancer
   |
Private Application Subnet
   |
Private Database Subnet
```

Private does not mean automatically secure. Routing, security groups, identities, application controls, and other policies must still be correctly configured.

---

## 16. Security Groups

A cloud **security group** is a virtual traffic-control mechanism associated with cloud resources or network interfaces, depending on the provider.

Rules may specify:

- Source
- Destination
- Protocol
- Port
- Direction

Security groups should follow least privilege.

Avoid broad rules such as:

```text
Source: 0.0.0.0/0
Port: Any
Action: Allow
```

unless the exposure is explicitly required and appropriately protected.

---

## 17. Network ACLs

Cloud network ACLs provide another layer of traffic control at the subnet or network level, depending on the platform.

They can complement security groups and cloud firewalls.

Defense in depth may therefore look like:

```text
Internet
   ↓
Cloud Firewall
   ↓
Network ACL
   ↓
Security Group
   ↓
Host/Application Control
```

The exact behavior and statefulness of these mechanisms varies by provider, so administrators must understand the specific implementation.

---

## 18. Private Endpoints

Private endpoints allow workloads to access supported cloud services through private network paths rather than requiring direct public internet exposure.

They can reduce exposure of sensitive service traffic and simplify network access controls.

Security teams should still apply:

- Identity controls
- Authorization
- Network policy
- Logging
- Encryption

A private network path does not eliminate the need for authentication and authorization.

---

## 19. Cloud API Security

Cloud infrastructure is heavily controlled through APIs.

An attacker with valid API credentials may be able to:

- Create resources
- Modify network rules
- Access storage
- Change IAM permissions
- Delete resources
- Disable security controls

API security therefore depends heavily on:

- Strong authentication
- Least privilege
- Credential protection
- MFA for administrative access where supported
- Rate limiting where appropriate
- Logging
- Monitoring
- Secure development practices

Cloud APIs should be treated as critical administrative interfaces.

---

## 20. Cloud Management Plane

The management plane controls cloud resources.

Examples include:

- Cloud consoles
- IAM systems
- Infrastructure APIs
- Deployment systems
- Resource-management services

Protecting the management plane is essential because compromise can allow an attacker to modify the environment itself.

Security architecture should separate administrative activities from ordinary application traffic and use strong identity controls.

---

## 21. Cloud Data Security

Cloud data can exist in multiple states:

- Data at rest
- Data in transit
- Data in use

Controls should be selected according to the data and threat model.

### Data at Rest

Protect stored data through access control and encryption where appropriate.

### Data in Transit

Use secure protocols and encryption to protect network communication.

### Data in Use

Data may be exposed while being processed by applications or workloads. Appropriate application, identity, host, and platform controls are required.

---

## 22. Cloud Encryption and Key Management

Encryption can protect data if unauthorized parties gain access to storage or communications.

Cloud environments may provide managed key-management services.

Security considerations include:

- Key ownership
- Key rotation
- Access control
- Key separation
- Audit logging
- Key lifecycle
- Backup/recovery of keys where appropriate

A key-management system is itself a sensitive security component and must be protected from unauthorized administrative access.

---

## 23. Secrets Management

Cloud applications commonly require credentials for:

- Databases
- APIs
- Storage
- Service accounts
- External services

Secrets should not be stored casually in:

- Source code
- Public repositories
- Container images
- Unprotected configuration files

Dedicated secrets-management services can provide controlled storage, access policies, rotation, and auditing.

---

## 24. Cloud Storage Security

Cloud storage misconfiguration is a common source of exposure.

Security teams should evaluate:

- Public access settings
- Identity permissions
- Bucket/container policies
- Encryption
- Versioning
- Logging
- Data classification
- Retention
- Backup

A storage resource intended for internal use should not be publicly accessible merely because an application requires cloud access.

---

## 25. Cloud Misconfiguration

Misconfiguration can occur when cloud resources are deployed with insecure settings.

Examples include:

- Public storage
- Public management interfaces
- Overly permissive security groups
- Excessive IAM permissions
- Disabled logging
- Unencrypted sensitive data
- Exposed databases
- Unprotected APIs
- Default credentials

Cloud environments make configuration mistakes particularly significant because automation can replicate the same insecure configuration across many resources.

---

## 26. Infrastructure as Code and Cloud Security

**Infrastructure as Code (IaC)** allows cloud resources to be defined through configuration files.

Security benefits include:

- Repeatability
- Version control
- Peer review
- Automated testing
- Consistent deployment

Security risks include:

- Insecure templates
- Hard-coded secrets
- Overly permissive network rules
- Excessive IAM permissions
- Unreviewed changes

IaC should therefore be included in security review and automated scanning.

---

## 27. Configuration Drift

**Configuration drift** occurs when deployed resources gradually differ from their approved baseline.

For example:

```text
Approved Configuration
        ↓
Manual Change
        ↓
Actual Configuration
        ↓
Security Gap
```

Cloud configuration-management and posture-management tools can help identify drift.

Organizations should compare deployed resources against approved security baselines and investigate unexpected changes.

---

## 28. Cloud Security Posture Management

**Cloud Security Posture Management (CSPM)** focuses on identifying and helping remediate cloud configuration and security posture issues.

CSPM capabilities may include:

- Misconfiguration detection
- Compliance checks
- Security-policy validation
- Risk identification
- Configuration monitoring
- Remediation workflows

CSPM does not replace IAM, endpoint protection, application security, or monitoring. It is one part of the cloud security architecture.

---

## 29. Cloud Workload Protection

Cloud workloads can include:

- VMs
- Containers
- Kubernetes workloads
- Serverless functions
- Managed databases

Workload security can involve:

- Vulnerability management
- Endpoint/runtime protection
- Secure configuration
- Identity controls
- Network segmentation
- Logging
- Application security

The organization should protect workloads according to their technology and service model.

---

## 30. Containers and Cloud Security

Containers allow applications to run in lightweight isolated environments, often on cloud infrastructure.

Cloud container security should address:

- Image provenance
- Image vulnerabilities
- Registry security
- Runtime security
- Container privileges
- Secrets
- Network policies
- Orchestrator security
- Workload identity

A secure container image does not automatically mean that the orchestration platform or cloud account is secure.

---

## 31. Serverless Security

**Serverless computing** allows customers to run application code without directly managing the underlying server infrastructure.

Security responsibilities can include:

- Application code
- Function permissions
- Input validation
- Dependencies
- Secrets
- API configuration
- Logging
- Data access

The provider manages more of the underlying infrastructure, but insecure function permissions or application code can still create serious vulnerabilities.

---

## 32. Cloud Logging and Monitoring

Cloud platforms generate extensive telemetry.

Important sources include:

- Authentication events
- IAM changes
- API activity
- Network flow logs
- Storage access
- Resource creation/deletion
- Configuration changes
- Security-service alerts

Centralized logging helps identify suspicious activity such as:

```text
New Administrator Created
        ↓
Security Group Modified
        ↓
Storage Made Public
        ↓
Large Data Download
```

Cloud logs should be protected against unauthorized modification or deletion.

---

## 33. Cloud Threat Detection

Cloud monitoring should identify suspicious behaviors such as:

- Impossible or unusual login patterns
- Unexpected privileged actions
- New access keys
- Sudden resource creation
- Security-control changes
- Unusual API calls
- Large data transfers
- Public exposure of resources

Detection can combine identity, network, endpoint, and cloud-control-plane telemetry.

---

## 34. Cloud Backup Architecture

Cloud data should be protected with appropriate backup and recovery mechanisms.

Consider:

- Backup frequency
- Retention
- Geographic redundancy
- Encryption
- Access control
- Immutability where appropriate
- Recovery testing
- Separate administrative access

Backups should be protected from the same compromise that affects production systems.

For example, if an attacker can use the same administrative account to delete both production data and backups, the backup architecture provides weaker resilience.

---

## 35. Cloud Availability Zones and Regions

Cloud providers commonly divide infrastructure into geographic regions and availability zones or equivalent fault domains.

### Availability Zone

A distinct infrastructure location within a cloud region designed to provide failure isolation from other zones.

### Region

A larger geographic area containing one or more availability zones.

Using multiple zones can improve availability.

Using multiple regions can provide stronger geographic resilience but introduces additional:

- Cost
- Latency
- Data-transfer requirements
- Data-residency considerations
- Operational complexity

Architecture should match the required recovery and availability objectives.

---

## 36. High Availability in Cloud Architecture

A cloud workload can be designed to avoid dependence on a single instance or infrastructure component.

For example:

```text
Load Balancer
   |
   +---- Instance A
   +---- Instance B
   +---- Instance C
```

If one instance fails, other instances may continue serving traffic.

High availability should also consider:

- Identity dependencies
- Databases
- DNS
- Networking
- Storage
- Monitoring
- Management services

Creating multiple application servers does not help if every server depends on one unavailable database or network component.

---

## 37. Disaster Recovery in the Cloud

Cloud environments can support several recovery architectures.

Examples include:

- Backup and restore
- Pilot light
- Warm standby
- Hot standby
- Multi-region deployment

The choice depends on:

- Recovery Time Objective (RTO)
- Recovery Point Objective (RPO)
- Cost
- Business criticality
- Data requirements

Security architecture must ensure that recovery environments are protected to an appropriate level and do not become forgotten insecure copies of production.

---

## 38. Cloud Data Residency and Sovereignty

Organizations may have legal, contractual, or business requirements governing where data is stored or processed.

Security architecture should therefore consider:

- Geographic location
- Regulatory requirements
- Customer contracts
- Data classification
- Cross-border transfers
- Provider region selection

Moving data to a different cloud region can have implications beyond performance and cost.

---

## 39. Multi-Cloud Architecture

**Multi-cloud** means using services from multiple cloud providers.

Potential benefits include:

- Avoiding dependence on one provider
- Access to specialized capabilities
- Business continuity options
- Geographic flexibility

Challenges include:

- Different IAM models
- Different network architectures
- Different logging formats
- Different security controls
- Skills requirements
- Increased configuration complexity

Security governance should provide consistent principles even when implementation differs between providers.

---

## 40. Vendor Lock-In

**Vendor lock-in** occurs when an organization becomes highly dependent on a provider's proprietary technologies or services, making migration difficult or expensive.

Security implications include:

- Difficulty changing providers during an incident
- Dependency on provider-specific security controls
- Migration complexity
- Data portability concerns
- Different security architectures during migration

Organizations should understand exit requirements and portability before becoming heavily dependent on specialized services.

---

## 41. Managed Service Providers and MSSPs

Organizations may use:

- Managed Service Providers (MSPs)
- Managed Security Service Providers (MSSPs)

These third parties may operate infrastructure or security services on behalf of the organization.

Security considerations include:

- Third-party access
- Privileged accounts
- Contractual security requirements
- Logging
- Incident notification
- Data handling
- Access termination
- Audit rights

Outsourcing operational work does not automatically eliminate organizational accountability for protecting its assets and data.

---

## 42. Third-Party Cloud Access

Vendor and contractor access should follow least privilege.

Controls may include:

- Dedicated accounts
- MFA
- Time-limited access
- Role-based permissions
- Restricted network paths
- Approval workflows
- Session logging
- Access reviews
- Immediate revocation after contract termination

Avoid sharing permanent administrator credentials with third parties.

---

## 43. Cloud Shadow IT

**Shadow IT** occurs when employees or departments use technology services without appropriate organizational approval or visibility.

Examples include:

- Unapproved cloud storage
- Personal SaaS accounts
- Unapproved cloud workloads
- External collaboration tools

Security risks include:

- Data leakage
- Unknown identities
- Weak authentication
- Missing logging
- Compliance problems
- Unmanaged backups

Organizations can reduce shadow IT through governance, approved service catalogs, identity integration, monitoring, and user awareness.

---

## 44. Cloud Resource Sprawl

Cloud resource sprawl occurs when organizations accumulate resources that are no longer required.

Examples include:

- Unused VMs
- Old storage volumes
- Abandoned snapshots
- Unused access keys
- Forgotten test environments
- Unused databases

Sprawl increases:

- Attack surface
- Cost
- Configuration-management burden
- Exposure to forgotten vulnerabilities

Lifecycle management should include resource ownership, inventory, review, and secure decommissioning.

---

## 45. Cloud Decommissioning

When cloud resources are retired, security teams should ensure that:

- Access credentials are revoked
- Data is handled according to retention requirements
- Snapshots are reviewed
- Logs are retained as required
- Secrets are removed or rotated
- DNS records are cleaned up
- Public access is removed
- Resource ownership is updated

Simply deleting an application does not guarantee that every associated security dependency has been removed.

---

## 46. Cloud Security Architecture Trade-Offs

Cloud architecture involves trade-offs.

### Security vs. Convenience

Restrictive controls can increase security but may make rapid development more difficult.

### Security vs. Cost

Multi-zone or multi-region resilience can increase cost.

### Centralization vs. Resilience

Centralized security services simplify management but can become critical dependencies.

### Flexibility vs. Governance

Highly flexible provisioning can increase the risk of shadow resources and configuration errors.

### Managed Services vs. Portability

Managed services reduce operational burden but may increase dependency on provider-specific technology.

---

## 47. Cloud Security Architecture Review

A cloud architecture review should consider:

### Identity

- Who can access the environment?
- Is MFA enabled for privileged users?
- Are permissions least privileged?
- Are service identities controlled?

### Network

- Which resources are public?
- Are private workloads appropriately isolated?
- Are security groups restrictive?
- Are management interfaces protected?

### Data

- Where is sensitive data stored?
- Is encryption required?
- Who controls the keys?
- Are backups protected?

### Workloads

- Are images and dependencies trusted?
- Are systems patched?
- Are runtime controls implemented?

### Monitoring

- Are API and authentication logs collected?
- Are configuration changes detected?
- Are security alerts centralized?

### Resilience

- Are critical workloads redundant?
- Are backups tested?
- Are recovery environments protected?

---

## 48. Common Cloud Security Failures

### Public Storage

Sensitive data is unintentionally exposed through an overly permissive storage policy.

### Excessive IAM Permissions

Users or workloads receive administrative access when they only require limited permissions.

### Exposed Management Interface

Administrative services are accessible from untrusted networks.

### Hard-Coded Secrets

Credentials are stored in source code, images, or configuration files.

### Disabled Logging

The organization cannot investigate cloud activity because important telemetry was never enabled or retained.

### Unmanaged Resources

Old test systems, snapshots, or access keys remain active after their intended use.

### Insecure IaC

An insecure template repeatedly deploys the same weak configuration.

### Missing Backup Isolation

Attackers who compromise production can also delete recovery data.

---

## 49. Security+ Scenario Examples

### Scenario 1 — Cloud VM Not Patched

An organization deploys a virtual machine through IaaS and assumes the provider patches the operating system.

**Issue:** the customer generally retains responsibility for the guest OS in an IaaS model.

**Concept:** shared responsibility.

---

### Scenario 2 — Public Database

A database is accessible directly from the internet even though it only needs to communicate with an application tier.

**Architecture improvement:** place the database in a private network segment and restrict access to the required application workloads.

---

### Scenario 3 — Developer Has Administrator Access

A developer only needs to deploy one application but receives broad cloud administrator permissions.

**Security principle:** least privilege.

Use a role that provides only the permissions necessary for the developer's responsibilities.

---

### Scenario 4 — Public Storage Exposure

A storage bucket containing sensitive files is accidentally made publicly accessible.

**Issue:** cloud misconfiguration.

**Controls:** restrictive storage policies, access reviews, configuration monitoring, encryption, and posture management.

---

### Scenario 5 — Cloud Credential Theft

An attacker obtains an administrator's cloud credentials.

**Priority controls:** MFA, strong identity security, least privilege, credential protection, monitoring, and rapid credential revocation.

---

### Scenario 6 — Automated Insecure Deployment

Every newly created cloud environment exposes a management port to the entire internet.

**Likely root cause:** insecure Infrastructure as Code or deployment template.

The template must be corrected and existing resources should be assessed for the same exposure.

---

### Scenario 7 — Protecting Backups From Ransomware

An attacker has administrative access to production and attempts to delete backups.

**Architecture goal:** separate backup administration and access paths, use appropriate immutable or protected copies, and test recovery.

---

### Scenario 8 — Multi-Region Resilience

A critical application cannot tolerate the loss of one geographic region.

**Architecture consideration:** multi-region deployment or an equivalent geographically resilient recovery design.

The decision must account for RTO, RPO, cost, data residency, and operational complexity.

---

## 50. Common Security+ Exam Traps

### Trap 1 — Cloud Provider Handles Everything

The provider manages its part of the infrastructure, but customers retain responsibilities based on the service model.

### Trap 2 — SaaS Means Customer Has No Security Responsibilities

Customers still manage identities, authentication, permissions, data handling, and configuration according to the service.

### Trap 3 — Private Subnet Means Secure

Private networking reduces direct exposure but does not replace authentication, authorization, patching, monitoring, or application security.

### Trap 4 — Encryption Solves Access Control

Encryption protects data under particular threat conditions; it does not replace identity and authorization controls.

### Trap 5 — IAM Permissions Are Only for Users

Workloads, applications, service accounts, and automation pipelines also require carefully scoped permissions.

### Trap 6 — Multi-Region Means Automatically Secure

Multiple regions can improve availability but add complexity and do not automatically secure applications or data.

### Trap 7 — CSPM Replaces Cloud Security

CSPM helps identify posture and configuration issues but does not replace identity security, application security, monitoring, or incident response.

### Trap 8 — Private Endpoint Means No Authentication

A private network path reduces exposure but does not eliminate the need for identity and authorization.

### Trap 9 — More Managed Means No Responsibility

Moving from IaaS toward PaaS or SaaS transfers more infrastructure responsibility to the provider, but customer responsibilities remain.

---

## 51. Important Cloud Security Distinctions

| Concept | Key idea |
|---|---|
| IaaS | Customer manages more of the OS/workload environment |
| PaaS | Provider manages more of the platform |
| SaaS | Provider manages most underlying application infrastructure |
| Shared responsibility | Provider and customer divide security responsibilities |
| Public cloud | Provider-operated shared cloud infrastructure |
| Private cloud | Cloud infrastructure dedicated to one organization |
| Hybrid cloud | Combination of private/on-premises and public cloud |
| Multi-cloud | Use of multiple cloud providers |
| IAM | Controls identities and permissions |
| MFA | Uses multiple authentication factors |
| Security group | Virtual traffic-control mechanism for cloud resources |
| Network ACL | Network/subnet-level traffic control, depending on provider |
| CSPM | Identifies cloud posture and configuration problems |
| IaC | Defines infrastructure through machine-readable configuration |
| Configuration drift | Actual configuration diverges from approved state |
| Private endpoint | Private connectivity to supported cloud services |
| Cloud region | Geographic cloud infrastructure area |
| Availability zone | Fault-isolated infrastructure location within a region |
| Shadow IT | Unapproved technology or cloud service use |
| Resource sprawl | Accumulation of unnecessary cloud resources |

---

## 52. Cloud Security Decision Framework

When solving a Security+ cloud architecture scenario, ask:

### Step 1 — Identify the Service Model

Is it IaaS, PaaS, or SaaS?

This determines the general responsibility boundary.

### Step 2 — Identify the Asset

Is the scenario about:

- VM?
- Application?
- Database?
- Storage?
- Identity?
- API?
- Network?
- Backup?

### Step 3 — Identify the Exposure

Is the resource:

- Publicly exposed?
- Privately accessible?
- Over-permissioned?
- Unmonitored?
- Misconfigured?

### Step 4 — Identify the Security Principle

Common answers involve:

- Least privilege
- MFA
- Defense in depth
- Segmentation
- Encryption
- Secure configuration
- Shared responsibility
- Resilience

### Step 5 — Protect the Management Plane

Ask who can create, modify, or delete cloud resources.

### Step 6 — Protect the Data

Consider confidentiality, integrity, availability, encryption, access control, retention, and recovery.

### Step 7 — Consider Monitoring

Determine how the organization would detect unauthorized activity or configuration changes.

### Step 8 — Consider Recovery

For critical workloads, evaluate backups, redundancy, RTO, RPO, and recovery testing.

---

## 53. Key Takeaways

- Cloud security is an architecture discipline involving identity, network, workload, data, management, monitoring, and resilience.
- IaaS, PaaS, and SaaS differ primarily in how responsibilities are divided between provider and customer.
- The shared responsibility model must always be considered when evaluating a cloud security scenario.
- Cloud providers secure the infrastructure they operate, while customers retain responsibilities according to the service and deployment model.
- Identity is a critical cloud security boundary because cloud resources are heavily controlled through APIs and management systems.
- MFA and least privilege are especially important for privileged cloud accounts.
- Human and workload identities should both receive appropriately scoped permissions.
- Public-facing services should be separated from private workloads where appropriate.
- Security groups, network ACLs, cloud firewalls, private endpoints, and segmentation can reduce unnecessary network exposure.
- Private networking does not eliminate the need for authentication and authorization.
- Cloud APIs and management planes are high-value security targets.
- Encryption protects data in appropriate threat scenarios, but encryption does not replace access control.
- Secrets should be stored using appropriate secrets-management mechanisms rather than embedded in code or images.
- Cloud storage must be carefully configured because accidental public exposure can result from simple policy mistakes.
- IaC improves consistency but can also reproduce insecure configurations if the templates are not reviewed and scanned.
- Configuration drift can create security gaps after deployment.
- CSPM helps identify cloud configuration and posture problems but does not replace other security controls.
- Containers and serverless workloads have their own security considerations within cloud environments.
- Cloud logging should capture authentication, API, network, storage, resource, and configuration activity as appropriate.
- Backups should be protected from the same administrative compromise that could affect production systems.
- Multiple availability zones or regions can improve resilience but introduce additional cost and complexity.
- Data residency and sovereignty requirements can affect region and architecture decisions.
- Multi-cloud can reduce certain dependencies but increases architectural and operational complexity.
- Shadow IT and resource sprawl increase attack surface and should be addressed through governance and lifecycle management.
- Third-party and MSP/MSSP access should be restricted, authenticated, logged, reviewed, and revoked when no longer required.

The central Security+ concept is:

**Moving infrastructure to the cloud changes the security responsibility boundary; it does not remove security responsibility. Identify what the provider manages, secure what the customer controls, protect identities and data, restrict network exposure, monitor the management plane, and design for recovery.**
