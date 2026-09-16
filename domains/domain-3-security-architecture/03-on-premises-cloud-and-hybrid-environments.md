# 03 — On-Premises, Cloud, and Hybrid Environments

## 1. Introduction

Organizations can deploy technology in **on-premises environments, cloud environments, hybrid environments, or multiple cloud environments**. The deployment model changes who owns the infrastructure, who operates different security controls, where data resides, how systems communicate, and how security responsibilities are divided.

Security architecture must therefore consider more than the physical location of a server.

Important questions include:

- Who owns the infrastructure?
- Who manages the physical hardware?
- Who manages the operating system?
- Who configures the network?
- Who manages identities?
- Who protects the data?
- Where is the data stored?
- How do users connect to the service?
- How are logs collected?
- What happens if the provider becomes unavailable?
- What security responsibilities remain with the customer?

A useful model is:

**Deployment model → Ownership → Responsibility → Trust boundaries → Connectivity → Security controls → Monitoring → Resilience**

---

# 2. What Is an On-Premises Environment?

An **on-premises environment** generally means technology infrastructure operated within facilities controlled or managed by the organization.

This may include:

- Physical servers
- Storage systems
- Network switches
- Routers
- Firewalls
- Wireless infrastructure
- Virtualization platforms
- Databases
- Applications
- Physical data centers

The organization usually has direct control over much of the underlying infrastructure.

However, on-premises does not mean automatically secure. The organization must still protect physical infrastructure, operating systems, networks, identities, applications, data, and administrative interfaces.

---

# 3. On-Premises Security Responsibilities

An organization operating its own infrastructure commonly has responsibility for a broad set of controls.

These can include:

- Physical access control
- Environmental protection
- Power and cooling
- Network security
- Firewall configuration
- Operating-system security
- Application security
- Identity management
- Patch management
- Endpoint protection
- Logging and monitoring
- Backup and recovery
- Vulnerability management

The exact division of responsibilities can vary when external managed services or vendors are involved.

---

# 4. Advantages of On-Premises Architecture

On-premises infrastructure can provide substantial direct control.

Potential advantages include:

### Direct infrastructure control

The organization can control hardware, network architecture, physical access, and many configuration decisions.

### Predictable physical location

The organization can determine where equipment is physically located and implement physical security controls around it.

### Existing infrastructure integration

Organizations with established data centers and internal applications may integrate new systems directly into existing architecture.

### Specialized requirements

Some workloads may have technical or operational requirements that make dedicated infrastructure appropriate.

These advantages come with additional operational responsibilities.

---

# 5. Challenges of On-Premises Architecture

Operating infrastructure internally requires significant planning and resources.

Challenges can include:

- Hardware acquisition
- Capital expenditure
- Hardware maintenance
- Physical security
- Power management
- Cooling
- Capacity planning
- Hardware replacement
- Disaster recovery
- Patching
- Staffing
- Security monitoring

The organization cannot assume that physical ownership eliminates security risk.

---

# 6. What Is Cloud Computing?

**Cloud computing** provides on-demand access to computing resources through a service provider.

Depending on the provider and service model, resources can include:

- Virtual machines
- Storage
- Databases
- Networking
- Application platforms
- Software applications
- Identity services
- Security services

Cloud environments can provide rapid scalability and reduce the need for customers to operate physical infrastructure directly.

However, cloud adoption changes—not eliminates—the organization's security responsibilities.

---

# 7. Characteristics of Cloud Computing

Common cloud characteristics include:

- On-demand resource provisioning
- Resource pooling
- Elasticity
- Broad network access
- Measured usage
- Provider-managed infrastructure

Cloud resources can often be provisioned faster than traditional physical infrastructure.

This flexibility is valuable, but it can also create security risks if resources are deployed without appropriate governance and configuration controls.

---

# 8. Cloud Security Architecture

Cloud security requires understanding the boundary between:

**Cloud provider responsibilities**

and

**Customer responsibilities**.

This is commonly described through the **shared responsibility model**.

The provider secures the infrastructure and services that it is responsible for, while the customer remains responsible for security controls within the customer's portion of the service.

The exact boundary depends on the service being consumed.

---

# 9. Shared Responsibility Model

A useful way to understand cloud responsibility is to ask:

- Who owns the physical data center?
- Who secures the physical servers?
- Who manages the virtualization layer?
- Who manages the operating system?
- Who secures the application?
- Who configures identity and access?
- Who protects the data?
- Who configures network security?
- Who monitors the customer's environment?

The answers depend on the provider, contract, and service model.

The most important Security+ lesson is:

> **Moving a workload to the cloud does not automatically transfer every security responsibility to the cloud provider.**

---

# 10. Infrastructure as a Service (IaaS)

**Infrastructure as a Service (IaaS)** provides fundamental infrastructure resources such as:

- Virtual machines
- Storage
- Virtual networking
- Network interfaces
- Security controls around virtual infrastructure

The provider generally manages the physical infrastructure and virtualization layer.

The customer generally has significant responsibility for:

- Guest operating systems
- Applications
- Identities
- Data
- Operating-system configuration
- Host-based security
- Network configuration within the cloud environment

The exact responsibility boundary varies by provider and service.

---

# 11. IaaS Example

Suppose an organization deploys a Linux virtual machine in a cloud environment.

The provider may be responsible for:

- Physical server
- Data-center facilities
- Physical network
- Hypervisor infrastructure

The customer may be responsible for:

- Linux configuration
- Installed applications
- User accounts
- SSH configuration
- Firewall rules configured by the customer
- Application security
- Data
- Access policies

If the customer leaves SSH broadly exposed with weak authentication, the cloud provider does not automatically fix that customer configuration.

---

# 12. Platform as a Service (PaaS)

**Platform as a Service (PaaS)** provides a managed platform on which customers deploy applications.

The provider manages more of the underlying environment than in IaaS.

Depending on the service, the customer may primarily manage:

- Application code
- Application configuration
- Data
- Identity and access policies
- Application-level security

PaaS reduces some infrastructure-management responsibilities but does not eliminate application and data security responsibilities.

---

# 13. PaaS Example

Imagine a developer deploys an application to a managed application platform.

The provider may manage:

- Servers
- Operating system components
- Runtime platform
- Infrastructure scaling

The customer still needs to secure:

- Application code
- Authentication
- Authorization
- Secrets
- Data
- Application configuration

A vulnerable application remains vulnerable even when hosted on a managed PaaS platform.

---

# 14. Software as a Service (SaaS)

**Software as a Service (SaaS)** provides a complete application as a managed service.

Examples of SaaS categories include:

- Email
- Collaboration
- Customer relationship management
- Document management
- Enterprise applications

The provider manages most of the underlying infrastructure and application platform.

Customers still have important responsibilities, including:

- Identity management
- Authentication
- MFA
- User permissions
- Data-sharing policies
- Configuration
- Endpoint security
- Organizational processes

---

# 15. SaaS Example

An organization uses a cloud-hosted collaboration application.

The provider may manage:

- Physical servers
- Operating systems
- Application infrastructure
- Application availability

The customer still needs to control:

- Which employees have accounts
- Which users are administrators
- MFA configuration
- External sharing
- Data access
- Account lifecycle

A customer can therefore create a security problem through poor SaaS configuration even when the provider's infrastructure is secure.

---

# 16. IaaS vs PaaS vs SaaS

| Model | Provider Manages More | Customer Manages More |
|---|---|---|
| IaaS | Physical infrastructure and virtualization | OS, applications, identities, data, configurations |
| PaaS | Infrastructure and more platform components | Application, data, identity, configuration |
| SaaS | Infrastructure and application platform | Identity, access, data usage, configuration |

As the service becomes more managed, the customer generally manages fewer underlying infrastructure components.

However, the exact responsibility boundary must always be verified for the specific service.

---

# 17. Security Responsibility Is Not the Same as Ownership

An important concept is that **ownership, operation, and security responsibility are related but not always identical**.

For example, a provider may own and operate physical servers while the customer remains responsible for the security configuration of the virtual machine running on them.

Therefore, security architecture should explicitly document:

- Asset owner
- Service provider
- Administrator
- Security responsibility
- Data owner
- Incident-response responsibility

---

# 18. Cloud Misconfiguration

Cloud environments are frequently highly configurable.

A misconfiguration can create significant exposure even when the underlying cloud infrastructure is secure.

Examples include:

- Publicly accessible storage
- Excessive permissions
- Exposed management interfaces
- Insecure security-group rules
- Weak identity policies
- Disabled logging
- Unencrypted sensitive data
- Hard-coded secrets

Cloud security therefore requires continuous configuration management.

---

# 19. Infrastructure as Code

**Infrastructure as Code (IaC)** defines infrastructure through machine-readable configuration rather than relying exclusively on manual deployment.

IaC can improve:

- Repeatability
- Version control
- Change tracking
- Standardization
- Automation

Security benefits can include the ability to review infrastructure changes before deployment and enforce approved configurations.

However, insecure IaC templates can reproduce insecure configurations at scale.

---

# 20. Configuration Drift

**Configuration drift** occurs when systems gradually deviate from their intended baseline.

For example:

```text
Approved configuration
        ↓
Initial deployment
        ↓
Manual changes
        ↓
Temporary exceptions
        ↓
Configuration drift
```

Drift can result in:

- Unexpected exposure
- Inconsistent security controls
- Compliance problems
- Difficult troubleshooting

Automated configuration management and continuous assessment can reduce drift.

---

# 21. Cloud Identity Architecture

Identity is particularly important in cloud environments because management interfaces are commonly accessible over networks rather than only through a physical internal network.

Important controls include:

- Strong authentication
- MFA
- Least privilege
- Role-based access
- Privileged access management
- Conditional access
- Service identities
- Short-lived credentials where appropriate

A compromised cloud administrator account can have significant impact even if the provider's physical infrastructure remains secure.

---

# 22. Federated Identity

**Identity federation** allows identities managed by one organization or identity provider to be used to access another service through established trust relationships.

A common example is:

```text
Employee
   |
Corporate Identity Provider
   |
Federated Authentication
   |
Cloud SaaS Application
```

Federation can simplify account management, but the identity provider becomes a critical security component.

---

# 23. Single Sign-On

**Single Sign-On (SSO)** allows users to authenticate through an identity system and access multiple authorized services without independently authenticating to each service in the traditional manner.

SSO can improve usability and centralized identity management.

However, compromise of the central identity system can affect many applications.

Therefore SSO should be protected with strong authentication, monitoring, and appropriate administrative controls.

---

# 24. Multi-Factor Authentication in Cloud Environments

Cloud administrative accounts should receive strong authentication protection.

MFA adds an additional authentication factor beyond a password.

This is especially important for:

- Cloud administrators
- Security administrators
- Privileged developers
- Billing administrators
- Identity administrators

MFA reduces the risk associated with stolen passwords, although it does not eliminate all identity threats.

---

# 25. Cloud Network Architecture

Cloud networks commonly provide constructs such as:

- Virtual networks
- Subnets
- Routing tables
- Security groups
- Network ACLs
- Load balancers
- Private endpoints
- Internet gateways

A secure cloud architecture should use these mechanisms to limit unnecessary connectivity.

Example:

```text
Internet
   |
Public Load Balancer
   |
Web Tier
   |
Private Application Tier
   |
Private Database Tier
```

The database does not need to be publicly exposed merely because the application is public.

---

# 26. Cloud Security Groups

Cloud platforms commonly provide **security groups** or similar workload-level network policies.

These controls can restrict traffic based on factors such as:

- Source
- Destination
- Protocol
- Port

They are useful for enforcing least-privilege network communication.

Security groups should be reviewed regularly because overly broad rules can expose workloads.

---

# 27. Private Endpoints

A **private endpoint** or equivalent private connectivity mechanism can allow a workload to access a service through private network paths rather than requiring direct public exposure.

This can reduce attack surface and keep sensitive service communication within controlled network boundaries.

The exact implementation varies by cloud platform.

---

# 28. Cloud Logging and Monitoring

Cloud environments require appropriate telemetry.

Important sources may include:

- Identity and authentication logs
- API activity logs
- Network flow information
- Resource configuration changes
- Application logs
- Storage access logs
- Administrative actions

Centralized monitoring helps detect events such as:

- New privileged accounts
- Public exposure changes
- Suspicious API activity
- Unusual geographic access
- Security-policy changes

---

# 29. Cloud API Security

Cloud infrastructure is heavily controlled through APIs.

Therefore, API credentials and permissions become important security assets.

Controls can include:

- Least privilege
- MFA for administrative access
- Strong credential management
- Short-lived credentials
- API logging
- Rate limiting where appropriate
- Monitoring administrative API activity

A compromised cloud API credential can be used to modify infrastructure without requiring physical access.

---

# 30. Secrets Management

Applications often require credentials, API keys, tokens, or certificates.

These should not be casually embedded in:

- Source code
- Public repositories
- Container images
- Configuration files
- Scripts

Dedicated secrets-management mechanisms can provide controlled storage, access, rotation, and auditing.

---

# 31. Hybrid Environments

A **hybrid environment** combines on-premises infrastructure with cloud resources.

Example:

```text
On-Premises Data Center
        |
 Secure Connectivity
        |
      Cloud
```

Organizations may choose hybrid architecture because of:

- Legacy applications
- Migration strategies
- Data residency requirements
- Regulatory constraints
- Performance requirements
- Existing investments
- Business continuity

---

# 32. Hybrid Security Boundaries

Hybrid architecture creates additional trust boundaries.

For example:

```text
Corporate Network
      |
VPN / Dedicated Connection
      |
Cloud Network
      |
Cloud Workloads
```

Security architecture must define:

- Which systems communicate
- Which protocols are allowed
- How identities are trusted
- How traffic is protected
- How logging works
- Who manages each side

---

# 33. Hybrid Connectivity

Common connectivity approaches can include:

- Site-to-site VPN
- Dedicated private connectivity
- Secure gateways
- Application-level connections

The choice depends on requirements such as:

- Bandwidth
- Latency
- Availability
- Security
- Cost
- Regulatory requirements

Connectivity should not create unrestricted trust between environments.

---

# 34. Hybrid Identity

Organizations may integrate on-premises identity systems with cloud identity services.

A simplified architecture is:

```text
On-Premises Directory
        |
 Identity Synchronization
        |
Cloud Identity Provider
        |
Cloud Applications
```

Security concerns include:

- Credential synchronization
- Privileged accounts
- MFA
- Federation
- Identity lifecycle
- Conditional access
- Logging

The identity integration layer becomes a critical trust relationship.

---

# 35. Hybrid Data Architecture

Organizations may keep certain data on-premises while processing applications in the cloud.

Example:

```text
Cloud Application
       |
Secure Connection
       |
On-Premises Database
```

Security architecture should consider:

- Encryption in transit
- Authentication
- Authorization
- Data classification
- Data residency
- Availability
- Network restrictions
- Monitoring

---

# 36. Data Residency

**Data residency** concerns the geographic location where data is stored or processed.

Organizations may have requirements that certain information remain within specific jurisdictions or regions.

Architecture decisions may therefore depend on:

- Regulatory obligations
- Contractual requirements
- Customer requirements
- Organizational policies

Data residency should be distinguished from broader concepts such as data sovereignty and localization requirements.

---

# 37. Multi-Cloud Architecture

**Multi-cloud** means using services from multiple cloud providers.

Example:

```text
Provider A
   |
   +---- Application

Provider B
   |
   +---- Analytics

Provider C
   |
   +---- Storage
```

Organizations may use multi-cloud architecture for:

- Specialized services
- Business requirements
- Provider diversification
- Existing acquisitions
- Regional requirements

However, multi-cloud increases operational and security complexity.

---

# 38. Multi-Cloud Security Challenges

Security teams may need to maintain consistent controls across different platforms.

Challenges include:

- Different IAM models
- Different logging systems
- Different network constructs
- Different security policies
- Different configuration tools
- Different APIs
- Different compliance mechanisms

A security architecture should define common organizational requirements while accounting for platform-specific implementation.

---

# 39. Cloud Vendor Lock-In

**Vendor lock-in** occurs when an organization becomes highly dependent on a particular provider's services, technologies, or architecture.

Potential concerns include:

- Migration complexity
- Cost changes
- Proprietary services
- Operational dependency
- Data portability

This is primarily an architectural and business consideration, but it can also affect security and resilience.

---

# 40. Managed Service Providers

A **Managed Service Provider (MSP)** operates technology or services on behalf of a customer.

Examples can include:

- Network management
- Cloud operations
- Security monitoring
- Infrastructure administration

Using an MSP can provide specialized expertise but introduces a third-party trust relationship.

---

# 41. Managed Security Service Provider

A **Managed Security Service Provider (MSSP)** provides managed security functions.

Services can include:

- Security monitoring
- SIEM operations
- Managed detection and response
- Vulnerability management
- Security-device management

The organization must still understand what responsibilities remain internal.

---

# 42. Third-Party Access Architecture

Third parties should receive only the access necessary for their approved function.

A poor design might be:

```text
Vendor
  |
Entire Corporate Network
```

A more controlled architecture may be:

```text
Vendor
  |
Secure Gateway
  |
Restricted Access
  |
Required Application
```

Controls can include:

- MFA
- Least privilege
- Network restrictions
- Time-limited access
- Logging
- Contractual requirements
- Access reviews

---

# 43. Cloud and On-Premises Security Comparison

| Area | On-Premises | Cloud |
|---|---|---|
| Physical infrastructure | Organization generally controls it | Provider generally controls it |
| Hardware maintenance | Customer | Provider for provider-owned infrastructure |
| Virtual infrastructure | Customer in self-managed environments | Often provider-managed depending on service |
| Identity | Customer | Shared/customer-managed depending on service |
| Application | Customer/provider depending on service | Responsibility varies by service |
| Data | Customer | Customer generally retains important responsibilities |
| Network configuration | Customer | Customer configures permitted cloud controls |
| Physical security | Customer | Provider for provider facilities |
| Scalability | Requires planning/procurement | Often rapidly scalable |
| Responsibility model | More directly customer-controlled | Shared responsibility |

This is a conceptual comparison. Actual responsibilities depend on the architecture and service contract.

---

# 44. Cloud Security Posture Management

**Cloud Security Posture Management (CSPM)** tools can assess cloud configurations against security policies and identify potential misconfigurations.

They may identify issues such as:

- Publicly exposed resources
- Excessive permissions
- Missing encryption
- Weak network rules
- Configuration deviations

CSPM can support continuous cloud-security assessment, but it does not replace proper architecture and governance.

---

# 45. Cloud Workload Protection

Cloud workloads may require controls such as:

- Endpoint protection
- Host-based firewalls
- Vulnerability management
- Container security
- Runtime monitoring
- Application security

The specific controls depend on the workload and service model.

A cloud virtual machine remains an operating system and application environment that requires appropriate security controls.

---

# 46. Cloud Storage Security

Cloud storage should be protected according to data sensitivity.

Important controls include:

- Access control
- Encryption
- Versioning where appropriate
- Logging
- Data lifecycle management
- Backup
- Public-access restrictions

A frequent architectural problem is accidentally exposing storage to the public internet.

---

# 47. Backup Architecture Across Environments

Hybrid and cloud environments should consider where backups are stored and how they are protected.

Important questions include:

- Are backups isolated from production?
- Are backups encrypted?
- Who can delete backups?
- Can ransomware reach backup systems?
- How quickly can data be restored?
- Are backups tested?

Cloud storage should not automatically be assumed to be a complete backup strategy.

---

# 48. Disaster Recovery in Hybrid Environments

Hybrid architecture can support disaster recovery by placing recovery resources in a separate environment.

For example:

```text
Primary On-Premises Environment
          |
      Replication
          |
      Cloud DR
```

However, the recovery architecture must also protect:

- Replication channels
- Recovery credentials
- Backup data
- Recovery configurations
- DNS changes
- Network connectivity

---

# 49. Security Architecture and Availability

Cloud environments can provide elastic capacity and managed availability features, but architecture must still account for:

- Provider outages
- Regional failures
- Network failures
- Identity-service failures
- Application failures
- Misconfiguration
- Account compromise

High availability may require distributing workloads across availability zones or regions where appropriate.

---

# 50. Region and Availability-Zone Concepts

Cloud providers commonly divide infrastructure into geographic regions and isolated availability zones or equivalent constructs.

A workload placed across multiple independent failure domains may have greater resilience than a workload dependent on one location.

However, geographic distribution introduces additional considerations such as:

- Cost
- Data residency
- Replication
- Latency
- Complexity

Architecture should balance these factors against business requirements.

---

# 51. Edge and Content Delivery Architecture

Cloud architectures may use edge services or content delivery networks to serve content closer to users.

Security architecture may place controls such as:

- DDoS protection
- Web application firewalls
- TLS termination
- Rate limiting
- Access controls

closer to the edge of the application architecture.

The purpose is to reduce unnecessary exposure and improve resilience and performance.

---

# 52. Containerized Cloud Workloads

Containers provide application isolation and packaging, but containerized environments introduce their own security boundaries.

Architecture should consider:

- Container images
- Registries
- Orchestration platforms
- Secrets
- Network policies
- Runtime security
- Image vulnerabilities

A container should not automatically be treated as a strong security boundary equivalent to a dedicated physical system.

Container architecture is covered more deeply in the virtualization and container module.

---

# 53. Serverless Architecture

**Serverless computing** allows organizations to execute application functions or use managed services without directly managing traditional servers.

The provider manages more of the infrastructure.

Customers still need to secure:

- Function code
- Permissions
- APIs
- Secrets
- Data
- Event sources
- Application logic

Serverless therefore changes the customer's security responsibilities but does not eliminate them.

---

# 54. Shadow IT in Cloud Environments

Cloud services can often be provisioned quickly without central IT involvement.

This can create **shadow IT**, where employees use technology without appropriate organizational approval or security review.

Risks include:

- Unknown data locations
- Unapproved applications
- Weak access control
- Data leakage
- Missing logging
- Compliance problems

Organizations can reduce this risk through governance, identity controls, asset discovery, approved-service catalogs, and monitoring.

---

# 55. Cloud Resource Sprawl

Cloud environments can accumulate unused resources.

Examples include:

- Old virtual machines
- Unused storage
- Forgotten accounts
- Temporary security exceptions
- Unused API keys
- Test environments

Resource sprawl increases attack surface and cost.

Regular inventory and lifecycle management are therefore important.

---

# 56. Cloud Decommissioning

When cloud resources are no longer required, security architecture should include secure decommissioning.

Consider:

- Removing access permissions
- Revoking credentials
- Deleting unused resources
- Handling stored data
- Removing DNS records
- Removing firewall rules
- Reviewing backups
- Updating documentation

Simply stopping a workload may not remove all associated resources or access paths.

---

# 57. Contractual Security Requirements

When using cloud providers or MSPs, security requirements should be documented contractually where appropriate.

Important areas can include:

- Security responsibilities
- Incident notification
- Data protection
- Data location
- Audit rights
- Availability requirements
- Backup responsibilities
- Access controls
- Data deletion
- Service termination

Contracts help establish organizational expectations, but technical controls are still required.

---

# 58. Exit Strategy

A cloud architecture should consider how the organization would leave a provider if necessary.

An exit strategy may address:

- Data export
- Data deletion
- Credential revocation
- Application migration
- DNS changes
- Backup recovery
- Contract termination

This supports resilience and reduces operational dependency.

---

# 59. Security Architecture for Hybrid Identity

A hybrid identity environment can become a high-value target because compromise of identity synchronization or federation infrastructure can affect multiple environments.

Security architecture should therefore consider:

- Strong MFA
- Privileged account separation
- Conditional access
- Monitoring
- Secure synchronization
- Administrative isolation
- Recovery procedures

Identity integration should be treated as a critical trust relationship.

---

# 60. Security+ Scenario — IaaS

### Scenario

An organization deploys a virtual machine in IaaS. The provider manages the physical server, but the customer must configure the operating system and installed application.

The VM is deployed with an unnecessary service exposed to the internet.

### Analysis

The provider's responsibility for physical infrastructure does not make the customer's VM configuration secure.

### Lesson

**IaaS customers retain significant responsibility for guest operating systems, applications, identities, and configuration.**

---

# 61. Security+ Scenario — SaaS

### Scenario

A company uses a SaaS application. The provider manages the application infrastructure, but the organization allows external sharing of sensitive documents without restriction.

### Analysis

The customer's data-sharing configuration is still a customer security responsibility.

### Lesson

**SaaS reduces infrastructure-management responsibilities but does not eliminate customer responsibility for identity, access, and data governance.**

---

# 62. Security+ Scenario — Hybrid Architecture

### Scenario

An organization moves its application tier to the cloud but keeps a sensitive database on-premises.

### Analysis

The application and database now cross an additional trust boundary.

### Required considerations

- Secure connectivity
- Authentication
- Authorization
- Encryption
- Network restrictions
- Monitoring
- Availability

### Lesson

**Hybrid architecture requires deliberate integration between environments.**

---

# 63. Security+ Scenario — Multi-Cloud

### Scenario

A company uses one provider for analytics and another for application hosting.

Each platform has different IAM and logging mechanisms.

### Analysis

The organization must maintain consistent security requirements across different implementations.

### Lesson

**Multi-cloud can increase flexibility but also increases security and governance complexity.**

---

# 64. Security+ Scenario — Cloud Misconfiguration

### Scenario

A storage resource containing sensitive information becomes publicly accessible because of an incorrect access policy.

### Analysis

The underlying provider infrastructure may be operating correctly. The exposure is caused by customer configuration.

### Lesson

**Cloud security depends heavily on correct customer-side configuration and access control.**

---

# 65. Security+ Scenario — Third-Party Access

### Scenario

An MSP needs to administer a small set of servers.

The organization considers giving the MSP unrestricted access to the entire environment.

### Analysis

The requested access is broader than the business requirement.

### Architectural approach

Use restricted administrative access, MFA, logging, appropriate segmentation, and least privilege.

### Lesson

**Third-party access should be limited to required systems and functions.**

---

# 66. Security+ Scenario — Cloud Identity

### Scenario

An attacker obtains credentials for a cloud administrator account.

The account has permission to modify networking, storage, identities, and virtual machines.

### Analysis

The account represents a highly privileged identity boundary.

### Architectural controls

- MFA
- Least privilege
- Privileged access management
- Administrative logging
- Conditional access
- Separate administrative identities

### Lesson

**Cloud identity security is a critical part of cloud architecture.**

---

# 67. Security+ Scenario — Legacy Application

### Scenario

A legacy application cannot be migrated immediately because it depends on specialized on-premises infrastructure, while newer services operate in the cloud.

### Architectural approach

Use a hybrid architecture with controlled connectivity, segmentation, restricted access, monitoring, and clearly defined responsibilities.

### Lesson

**Hybrid architecture can bridge legacy and modern environments while preserving controlled trust boundaries.**

---

# 68. Common Exam Traps

### Trap 1: Cloud provider secures everything

Incorrect.

Cloud security follows a shared responsibility model. Customer responsibilities remain, especially around identities, configurations, applications, and data.

### Trap 2: IaaS means the provider manages the operating system

Generally incorrect for standard IaaS virtual machines.

The customer commonly manages the guest operating system and applications.

### Trap 3: SaaS means the customer has no security responsibility

Incorrect.

Identity, access, configuration, data handling, and organizational security remain important.

### Trap 4: Hybrid means multi-cloud

Not necessarily.

Hybrid commonly combines on-premises and cloud environments. Multi-cloud specifically involves multiple cloud providers.

### Trap 5: Cloud automatically provides high availability

Incorrect.

Availability depends on the architecture, service, region, redundancy, configuration, and business requirements.

### Trap 6: Public cloud means data must be public

Incorrect.

Cloud resources can be private, restricted, or publicly accessible depending on configuration and architecture.

### Trap 7: VPN creates complete trust

Incorrect.

A VPN protects connectivity but does not eliminate the need for authentication, authorization, segmentation, and endpoint security.

### Trap 8: Provider infrastructure security protects against customer misconfiguration

Incorrect.

A customer can expose data through incorrect configuration even when the provider's infrastructure is secure.

### Trap 9: More cloud providers automatically means more security

Not necessarily.

Multi-cloud may provide flexibility or diversification but also increases operational and security complexity.

### Trap 10: Stopping a cloud resource removes every security concern

Not necessarily.

Credentials, storage, backups, DNS records, permissions, and other associated resources may remain.

---

# 69. Important Security+ Distinctions

| Concept | Meaning |
|---|---|
| On-premises | Infrastructure operated within organization-controlled facilities or environment |
| Cloud | Provider-delivered computing resources and services |
| IaaS | Managed infrastructure resources such as VMs, storage, and networking |
| PaaS | Managed application platform |
| SaaS | Managed application delivered as a service |
| Shared responsibility | Provider and customer divide security responsibilities |
| Hybrid | Combination of on-premises and cloud environments |
| Multi-cloud | Use of multiple cloud providers |
| MSP | Managed service provider |
| MSSP | Managed security service provider |
| Federation | Trust relationship allowing identities to work across organizations/services |
| SSO | Centralized authentication experience across multiple services |
| Data residency | Geographic location where data is stored or processed |
| Configuration drift | Deviation from an approved configuration baseline |
| Vendor lock-in | Dependence on a provider's services or technology |
| CSPM | Technology for assessing and managing cloud security posture |
| IaC | Infrastructure defined and managed through code/configuration |

---

# 70. Cloud Responsibility Reasoning Framework

When a Security+ question asks who is responsible for a security control, use this process.

### Step 1 — Identify the service model

Is it:

- IaaS?
- PaaS?
- SaaS?

### Step 2 — Identify the asset

Is the question about:

- Physical hardware?
- Virtual machine?
- Operating system?
- Application?
- Identity?
- Data?

### Step 3 — Determine who controls it

Ask:

> **Who can configure this component?**

The party controlling a component generally has responsibility for securing its configuration, subject to the provider's specific service model.

### Step 4 — Identify the trust boundary

Determine where responsibility changes between:

- Customer
- Cloud provider
- Third party
- Internal environment

### Step 5 — Identify the security requirement

Is the issue:

- Confidentiality?
- Integrity?
- Availability?
- Access control?
- Configuration?
- Monitoring?

### Step 6 — Check the architecture

Determine whether the design requires:

- Segmentation
- MFA
- Encryption
- Logging
- Least privilege
- Secure connectivity
- Redundancy

---

# 71. On-Premises vs Cloud Decision Framework

When comparing deployment models, consider:

### Control

How much direct control is required?

### Cost

Does the organization prefer capital expenditure, operational expenditure, or a combination?

### Scalability

How quickly does capacity need to change?

### Security responsibility

How much infrastructure does the organization want to operate itself?

### Compliance

Are there requirements concerning data location or specific controls?

### Availability

What level of redundancy is required?

### Legacy dependencies

Can existing applications operate in the target environment?

### Skills

Does the organization have the expertise required to operate the environment securely?

These factors should be evaluated together rather than choosing an environment based on one characteristic alone.

---

# 72. Secure Hybrid Architecture Checklist

A hybrid environment should address:

- Clear ownership
- Clear security responsibilities
- Secure connectivity
- Network segmentation
- Identity integration
- MFA
- Least privilege
- Encryption
- Logging
- Monitoring
- Data classification
- Data residency
- Backup and recovery
- Configuration management
- Incident response
- Third-party access
- Exit and migration planning

The objective is to avoid creating an uncontrolled bridge between two environments.

---

# 73. Security+ Architecture Reasoning Framework

For environment-deployment questions, use:

**Deployment model → Responsibility boundary → Asset → Trust relationship → Security control → Monitoring → Availability → Recovery**

Ask:

1. Where is the workload hosted?
2. Who controls the underlying layer?
3. Who controls the configuration?
4. What data is being protected?
5. What identities require access?
6. How do environments communicate?
7. Where are trust boundaries?
8. What happens if the provider or connection fails?
9. How is activity monitored?
10. How can the organization recover or migrate?

---

# 74. Key Takeaways

1. On-premises, cloud, and hybrid environments have different ownership and responsibility characteristics.
2. On-premises environments generally provide greater direct infrastructure control but also create greater operational responsibility.
3. Cloud computing provides on-demand resources but does not eliminate customer security responsibilities.
4. The shared responsibility model divides security responsibilities between provider and customer.
5. IaaS generally leaves customers responsible for guest operating systems, applications, identities, data, and configurations.
6. PaaS provides a more managed platform while customers remain responsible for applications, data, identities, and configuration within the service boundary.
7. SaaS provides a highly managed application, but customers still manage identity, access, data use, and configuration responsibilities.
8. The exact cloud responsibility boundary depends on the service and provider.
9. Cloud misconfiguration can expose resources even when provider infrastructure is securely operated.
10. IaC improves repeatability and change control but can also reproduce insecure configurations if templates are poorly designed.
11. Configuration drift can create security and compliance gaps.
12. Cloud identity is a critical security boundary because administrative actions can control large numbers of resources.
13. Federation and SSO centralize identity but make identity infrastructure highly important to protect.
14. MFA should protect sensitive cloud and administrative identities.
15. Cloud networks require segmentation and restricted communication just like on-premises networks.
16. Security groups, network ACLs, routing, and private connectivity can enforce cloud network policies.
17. Cloud logging should capture important identity, API, configuration, network, and resource activity.
18. Cloud APIs are high-value attack surfaces and require strong credential and authorization controls.
19. Secrets should be protected through appropriate secrets-management mechanisms rather than embedded casually in code.
20. Hybrid environments combine on-premises and cloud resources and therefore create additional trust boundaries.
21. Hybrid connectivity should be secure and limited to required communication.
22. Hybrid identity requires careful protection of synchronization and federation relationships.
23. Hybrid data architectures must consider encryption, authentication, authorization, monitoring, availability, and data residency.
24. Multi-cloud uses multiple cloud providers and can provide flexibility but increases security and governance complexity.
25. Vendor lock-in can affect migration, resilience, cost, and architectural flexibility.
26. MSPs and MSSPs introduce third-party trust relationships that require defined responsibilities and access controls.
27. Third-party access should follow least privilege and should be monitored.
28. Cloud storage requires access control, encryption, logging, and protection against unintended public exposure.
29. Cloud backups should be isolated appropriately from production and tested for recovery.
30. Cloud availability depends on architecture, redundancy, provider capabilities, configuration, and business requirements.
31. Geographic distribution can improve resilience but introduces cost, latency, replication, and data-residency considerations.
32. Serverless and containerized architectures change security responsibilities but do not eliminate application and identity security requirements.
33. Shadow IT and cloud resource sprawl increase attack surface and require governance and inventory.
34. Decommissioning cloud resources should include access revocation, data handling, DNS review, backup review, and documentation updates.
35. Contracts with providers should define important security, incident, availability, data, and termination responsibilities.
36. A cloud exit strategy can reduce operational dependency and improve resilience.
37. Security+ questions about cloud responsibility should be solved by identifying the service model and the layer being discussed.
38. Security+ questions about hybrid environments should focus on trust boundaries, secure connectivity, identity integration, and responsibility separation.
39. Security architecture should remain focused on business requirements, asset sensitivity, risk, controlled connectivity, and resilience regardless of where workloads are hosted.
40. The core reasoning chain is **deployment model → responsibility boundary → asset → trust relationship → control → monitoring → availability → recovery**.
