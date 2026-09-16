# 01 — Enterprise Security Architecture

## 1. Introduction

**Enterprise security architecture** is the structured design of an organization's technology environment so that security requirements are built into business systems, networks, applications, identities, data flows, cloud services, endpoints, and operational processes.

Security architecture is broader than selecting security products. A firewall, SIEM, EDR platform, or identity provider is only one component of a larger architecture. The architecture determines **where controls are placed, how systems communicate, where trust changes, how identities are evaluated, how data is protected, and how the organization continues operating when controls fail or systems are compromised**.

A useful architectural decision model is:

**Business requirements → Assets → Threats → Risk → Security requirements → Architecture → Controls → Validation → Continuous improvement**

The architecture should protect the organization while still allowing legitimate business operations.

---

# 2. Why Security Architecture Matters

A poorly designed environment can remain vulnerable even when many security products are installed.

For example, an organization might deploy:

- A firewall
- Endpoint protection
- Antivirus
- SIEM
- MFA
- IDS/IPS

but still have serious architectural weaknesses if:

- Critical servers share unrestricted network segments.
- Privileged accounts can administer everything from ordinary workstations.
- Sensitive databases are directly reachable by unnecessary systems.
- Cloud storage is publicly exposed.
- Administrative interfaces are exposed to the internet.
- Users receive excessive permissions.

Security architecture addresses these relationships.

The central question is not merely:

> **What security technology do we have?**

It is:

> **How should the environment be designed so that security controls work together and compromise is contained?**

---

# 3. Business Requirements and Security Architecture

Security architecture must support the organization's actual business requirements.

Before designing a security architecture, architects should understand:

- Business processes
- Critical services
- Regulatory requirements
- Data sensitivity
- Availability requirements
- User populations
- Technology dependencies
- Third-party dependencies
- Recovery requirements
- Threat environment

For example, a hospital cannot design availability controls in exactly the same way as a development laboratory because system downtime can have very different consequences.

Architecture therefore begins with understanding what the organization must protect and what it must continue operating.

---

# 4. Asset Identification

An architecture cannot protect assets that the organization does not know exist.

Assets can include:

- Servers
- Workstations
- Laptops
- Mobile devices
- Network infrastructure
- Applications
- Databases
- Cloud resources
- APIs
- Identities
- Credentials
- Cryptographic keys
- Intellectual property
- Customer information
- Operational technology

Asset identification supports decisions about where security controls should be applied.

A public web server, domain controller, employee laptop, and payment database may all require different controls because their functions, threats, and impact differ.

---

# 5. Security Objectives — CIA Triad

The **CIA triad** provides three fundamental security objectives:

1. Confidentiality
2. Integrity
3. Availability

These objectives influence architectural decisions throughout an enterprise.

---

# 6. Confidentiality

**Confidentiality** means preventing unauthorized disclosure of information.

Architecture can support confidentiality through:

- Access control
- Encryption
- Network segmentation
- Data classification
- Data-loss prevention
- Least privilege
- Secure authentication
- Physical security

### Example

A database containing sensitive customer information should not be directly accessible by every employee workstation.

A better architecture may allow only approved application servers to communicate with the database.

This reduces unnecessary access paths and supports confidentiality.

---

# 7. Integrity

**Integrity** means protecting information and systems against unauthorized or improper modification.

Architectural controls supporting integrity include:

- Access control
- Hashing
- Digital signatures
- Secure configuration
- Change management
- File integrity monitoring
- Version control
- Application security
- Logging and auditing

### Example

If a configuration file controls firewall behavior, unauthorized modification of that file could weaken the security architecture.

Strong access control, change management, and integrity monitoring can reduce this risk.

---

# 8. Availability

**Availability** means ensuring that authorized users can access systems and information when required.

Architectural availability controls can include:

- Redundant systems
- Clustering
- Load balancing
- Failover
- Backup systems
- Disaster recovery
- Multiple network paths
- DDoS protection
- Geographic redundancy
- Capacity planning

Availability must be designed according to business requirements.

A highly available architecture may require additional cost and complexity, but a system supporting a critical business process may justify those requirements.

---

# 9. Balancing CIA Requirements

Security architecture often requires trade-offs.

For example:

- Strong authentication may introduce additional user friction.
- Extensive logging may increase storage requirements.
- Aggressive filtering may block legitimate traffic.
- High redundancy increases infrastructure cost.
- Strict segmentation may complicate application communication.

The architect must select controls appropriate to the risk and business requirements rather than applying every possible control indiscriminately.

---

# 10. Defense in Depth

**Defense in depth** is the use of multiple security layers so that failure of one control does not automatically result in compromise.

Consider an internet-facing application.

A layered architecture might include:

1. Physical security
2. Network segmentation
3. Perimeter firewall
4. Web application firewall
5. Secure authentication
6. Application security controls
7. Endpoint protection
8. Logging and monitoring
9. Backup and recovery

If one layer fails, another layer can still reduce the likelihood or impact of compromise.

### Important point

Defense in depth is not simply buying many security products.

The controls should provide meaningful layers with different functions.

---

# 11. Defense in Depth Example

Imagine an attacker successfully exploits a public-facing application.

If the architecture has no additional controls, the compromised server may provide a direct path to internal databases and administrative systems.

With defense in depth:

**Internet → Firewall → DMZ/application segment → Application server → Restricted database segment**

Additional controls can include:

- MFA for administration
- EDR on servers
- Database access controls
- SIEM monitoring
- Network IDS/IPS

The compromise of one component therefore does not automatically compromise the entire environment.

---

# 12. Zero Trust Architecture

**Zero Trust** is an architectural approach that minimizes implicit trust and requires access decisions to be based on explicit security information rather than simply network location.

A user connected to the corporate network should not automatically receive broad access merely because the device is inside the traditional perimeter.

Important principles include:

- Verify explicitly.
- Apply least privilege.
- Assume breach.
- Minimize implicit trust.
- Continuously evaluate access.
- Use identity and device context.
- Segment resources.

Zero trust is therefore an architectural strategy rather than a single product.

---

# 13. Zero Trust and Network Location

Traditional perimeter thinking often assumes:

**Outside = untrusted**

**Inside = trusted**

Zero trust challenges this assumption.

An internal workstation may be:

- Compromised
- Misconfigured
- Used by a compromised account
- Running outdated software

Therefore, internal network location should not automatically grant broad access.

Access decisions can consider:

- User identity
- Device identity
- Device security posture
- Resource sensitivity
- Requested action
- Location/context
- Authentication strength
- Risk signals

---

# 14. Least Privilege

**Least privilege** means providing only the permissions necessary for an identity, application, service, or device to perform its authorized function.

Least privilege applies to:

- Human users
- Administrators
- Service accounts
- Applications
- APIs
- Cloud identities
- Devices

### Example

A reporting application may need read-only access to a database.

Giving it database administrator privileges creates unnecessary risk.

If the application is compromised, excessive privileges could allow an attacker to perform actions far beyond the application's legitimate requirements.

---

# 15. Privileged Access Architecture

Administrative access deserves additional protection because privileged identities can affect large portions of the environment.

Architectural controls may include:

- Separate administrative accounts
- MFA
- Privileged access management (PAM)
- Just-in-time access
- Just-enough administration
- Administrative jump hosts
- Session monitoring
- Strong authentication
- Restricted management networks

The objective is to reduce the opportunity for attackers to abuse administrative credentials.

---

# 16. Separation of Duties

**Separation of duties** means dividing sensitive responsibilities among different individuals or roles so that one person does not have unrestricted control over an important process.

Example:

One employee requests a financial change while another approves it.

In security architecture, separation of duties can reduce the risk of:

- Unauthorized changes
- Fraud
- Abuse of privilege
- Single-person control

It complements least privilege but is not identical to it.

---

# 17. Trust Boundaries

A **trust boundary** is a location where the level of trust, security control, or administrative authority changes.

Examples include:

- Internet → corporate network
- User network → server network
- Application server → database
- Corporate environment → cloud provider
- Standard user → privileged environment
- Guest network → internal network

Crossing a trust boundary should trigger appropriate controls.

These may include:

- Authentication
- Authorization
- Encryption
- Firewall filtering
- Inspection
- Logging
- Segmentation

---

# 18. Trust Boundary Example

Consider an online shopping application:

**Internet user → Web application → Application service → Database**

Each transition represents a security boundary.

The database should not automatically trust every request simply because it originated from an application server.

The architecture should enforce:

- Authentication where appropriate
- Authorization
- Network restrictions
- Input validation
- Encryption
- Logging

The purpose is to prevent one compromised component from automatically gaining unrestricted access to the next.

---

# 19. Attack Surface

The **attack surface** is the collection of exposed points through which an attacker could potentially interact with or affect an environment.

Examples include:

- Internet-facing services
- Open ports
- Applications
- APIs
- Remote-access services
- Wireless networks
- User accounts
- Cloud resources
- Mobile devices
- Physical interfaces

Security architecture should minimize unnecessary attack surface.

---

# 20. Attack Surface Reduction

Attack surface can be reduced through:

- Disabling unnecessary services
- Closing unnecessary ports
- Removing unused accounts
- Restricting administrative access
- Segmenting networks
- Removing obsolete systems
- Reducing cloud exposure
- Restricting APIs
- Applying least privilege
- Removing unnecessary software

The objective is not to eliminate every interface.

The objective is to ensure that necessary interfaces are deliberately exposed and appropriately protected.

---

# 21. Secure by Design

**Secure by design** means security requirements are considered during architecture and development rather than being added only after deployment.

A secure-by-design approach can include:

- Threat modeling
- Secure defaults
- Least privilege
- Strong authentication
- Encryption
- Input validation
- Secure error handling
- Logging
- Segmentation
- Minimal attack surface
- Secure update mechanisms

Security is therefore treated as a design requirement rather than a final-stage add-on.

---

# 22. Secure Defaults

A secure system should ideally begin in a reasonably secure state.

Examples include:

- Unnecessary services disabled
- Default credentials changed or prohibited
- Management interfaces restricted
- Encryption enabled where appropriate
- Least-privilege permissions applied
- Security logging enabled

Secure defaults reduce the number of unsafe decisions administrators or users must make after deployment.

---

# 23. Fail-Safe and Fail-Secure Concepts

Architectural decisions should consider how systems behave when something fails.

A **fail-secure** design generally prevents unauthorized access when a security mechanism fails.

For example, if an authorization service becomes unavailable, an application may deny access to a sensitive resource rather than granting access by default.

However, availability requirements may require carefully designed exceptions.

Security architects must understand the consequences of both failure modes.

---

# 24. Resilience in Security Architecture

Security architecture should account for the possibility that controls or systems will fail.

Resilience can include:

- Redundancy
- Failover
- Backups
- Alternate communication paths
- Geographic distribution
- Disaster recovery
- Incident-response capabilities

A resilient architecture can continue critical functions or recover them quickly after an outage or security event.

---

# 25. High Availability vs Redundancy

These concepts are related but not identical.

### Redundancy

Provides additional components or resources that can support operations if another component fails.

### High availability

Aims to keep a service operational with minimal interruption, often using redundancy, failover, clustering, load balancing, and monitoring.

Redundancy can contribute to high availability, but simply owning duplicate equipment does not guarantee effective high availability.

---

# 26. Segmentation as an Architectural Control

Segmentation divides an environment into security zones with controlled communication between them.

Example:

```text
Internet
   |
Firewall
   |
Public/DMZ Segment
   |
Application Segment
   |
Restricted Database Segment
```

If the public application is compromised, segmentation can limit direct access to the database and other internal systems.

Segmentation therefore supports:

- Attack-surface reduction
- Lateral-movement prevention
- Blast-radius reduction
- Access control
- Compliance requirements

---

# 27. DMZ Architecture

A **DMZ (demilitarized zone)** is a network segment designed to contain systems that must be accessible from less-trusted networks while limiting direct access to internal resources.

Common DMZ systems may include:

- Public web servers
- Reverse proxies
- Mail gateways
- Public DNS services

A DMZ should not be interpreted as automatically making a system secure.

Firewall policies and access controls must still restrict communication between the DMZ and internal networks.

---

# 28. Microsegmentation

**Microsegmentation** applies granular security boundaries to workloads, applications, or individual systems.

Instead of treating an entire server network as one trusted zone, policies can restrict communication between specific workloads.

This is especially useful in environments where:

- Applications have many dependencies.
- Workloads change dynamically.
- Cloud infrastructure is widely distributed.
- Lateral movement must be tightly constrained.

Microsegmentation is closely aligned with zero-trust principles.

---

# 29. Identity as a Security Boundary

Modern architectures increasingly treat identity as a major security boundary.

Instead of asking only:

**Where is this connection coming from?**

The architecture can also ask:

- Who is requesting access?
- What device are they using?
- What resource are they accessing?
- What action are they requesting?
- Is MFA satisfied?
- Is the device compliant?
- Is the request consistent with policy?

This supports identity-centric and zero-trust security models.

---

# 30. Authentication Architecture

Authentication establishes the identity of a user, device, or service.

Architectural authentication controls can include:

- Passwords
- MFA
- Certificates
- Smart cards
- Biometrics
- Federated identity
- Single sign-on
- Hardware security keys

Authentication should be appropriate to the sensitivity of the resource.

Privileged operations should generally receive stronger protection than low-risk activities.

---

# 31. Authorization Architecture

Authentication alone does not determine what an identity may do.

**Authorization** determines which resources and actions are permitted.

Architectural authorization models can include:

- Role-Based Access Control (RBAC)
- Attribute-Based Access Control (ABAC)
- Rule-based controls
- Policy-based access control

### Example

A user can successfully authenticate but still be denied access to a database table because the user's role does not authorize that action.

---

# 32. RBAC

**Role-Based Access Control (RBAC)** assigns permissions based on organizational roles.

Example:

```text
Sales Role
 ├── CRM access
 └── Sales reports

Security Analyst Role
 ├── SIEM access
 └── Security investigation tools
```

Users receive permissions through their assigned roles.

RBAC can simplify administration and support least privilege when roles are designed correctly.

---

# 33. ABAC

**Attribute-Based Access Control (ABAC)** makes access decisions using attributes.

Possible attributes include:

- User identity
- User role
- Device status
- Location
- Time
- Resource sensitivity
- Requested action

Example policy concept:

> Allow access to a sensitive application only when the user has the required role, the device is compliant, and strong authentication has been completed.

ABAC can support dynamic, context-aware access decisions.

---

# 34. Data-Centric Security Architecture

A data-centric architecture focuses security controls around the information itself.

Important activities include:

- Data classification
- Data ownership
- Access control
- Encryption
- Data retention
- Data-loss prevention
- Monitoring

For example, sensitive data may require stronger encryption and stricter access policies than publicly available information.

---

# 35. Data Classification

Data classification helps organizations determine the appropriate protection level for information.

Common organizational categories may include:

- Public
- Internal
- Confidential
- Restricted

The exact classification scheme varies by organization.

Classification influences:

- Access control
- Encryption
- Retention
- Monitoring
- Data-sharing requirements

---

# 36. Encryption in Architecture

Encryption can protect data:

### At rest

Data stored on disks, databases, backups, and other storage.

### In transit

Data moving across networks.

### In use

Data being processed by systems; protecting data in use may require specialized technologies and architectural approaches.

Encryption should be combined with proper key management because encryption without protected keys may not provide meaningful security.

---

# 37. Key Management Architecture

Cryptographic keys require their own lifecycle.

Important activities include:

- Key generation
- Secure storage
- Distribution
- Rotation
- Revocation
- Backup where appropriate
- Recovery
- Destruction

A system may use strong encryption but still have serious security problems if keys are stored insecurely or shared excessively.

---

# 38. Logging and Monitoring Architecture

Security architecture should generate sufficient telemetry to detect and investigate suspicious activity.

Important sources can include:

- Authentication logs
- Firewall logs
- Endpoint telemetry
- Application logs
- Cloud audit logs
- DNS logs
- Network flow data

The architecture should consider:

- What must be logged?
- Where should logs be stored?
- How are logs protected from tampering?
- How long should they be retained?
- Who can access them?

---

# 39. Security Architecture and SIEM

A SIEM can aggregate and correlate security events from different components.

For example:

**Identity provider → Firewall → Endpoint → Application → SIEM**

A centralized view can help analysts identify attack chains that would be difficult to see from a single system.

However, a SIEM cannot compensate for completely missing telemetry.

Architecture must therefore provide appropriate logging at the source.

---

# 40. Management Plane Security

Administrative interfaces are high-value targets.

The management plane should be separated and protected where appropriate.

Controls can include:

- Dedicated management networks
- VPN access
- Jump hosts
- MFA
- PAM
- Restricted source addresses
- Administrative logging
- Separate administrator identities

Management interfaces should not be unnecessarily exposed to untrusted networks.

---

# 41. Control Plane vs Data Plane

In network and infrastructure architecture, it can be useful to distinguish:

### Control plane

Responsible for decisions about how systems or networks operate.

### Data plane

Responsible for carrying or processing operational traffic.

Protecting administrative/control functions is important because compromise of the control plane can affect large portions of the environment.

---

# 42. Secure Remote Access Architecture

Remote access introduces additional trust-boundary considerations.

Secure remote access may use:

- VPN
- Zero-trust network access
- MFA
- Device posture checks
- Conditional access
- Restricted administrative paths

A secure architecture should avoid granting broad internal access simply because a user successfully connected remotely.

---

# 43. Third-Party Trust Boundaries

Organizations frequently share data and connectivity with:

- Vendors
- Managed service providers
- SaaS providers
- Contractors
- Business partners

Third-party connections create additional trust boundaries.

Controls can include:

- Least privilege
- Network segmentation
- Strong authentication
- Contractual security requirements
- Logging
- Monitoring
- Data minimization

The architecture should avoid granting unnecessary access simply because a third party is a trusted business partner.

---

# 44. Secure Architecture for Internet-Facing Applications

A common architecture is:

```text
Internet
   |
DDoS Protection / Edge Security
   |
Firewall / Load Balancer
   |
WAF / Reverse Proxy
   |
Web/Application Tier
   |
Restricted Service Tier
   |
Database Tier
```

Each layer can have a specific security purpose.

For example:

- Edge controls reduce unwanted traffic.
- Firewall rules restrict network access.
- WAF controls application-layer requests.
- Application controls enforce authentication and authorization.
- Database controls protect sensitive information.

---

# 45. Secure Architecture for Administrative Access

A secure administrative design may resemble:

```text
Administrator
     |
    MFA
     |
Privileged Access System / Jump Host
     |
Management Network
     |
Servers / Network Devices
```

This is generally safer than:

```text
Administrator Laptop
       |
       +---- Direct access to every server
       +---- Direct access to every network device
       +---- Direct access to critical databases
```

The first architecture creates stronger control over privileged access and improves monitoring opportunities.

---

# 46. Blast Radius

**Blast radius** describes the potential extent of damage or compromise after a security control fails or an attacker gains access.

Architecture can reduce blast radius through:

- Segmentation
- Least privilege
- Zero trust
- Application isolation
- Restricted credentials
- Microsegmentation
- Independent administrative boundaries

### Example

If one workstation is compromised, it should not automatically provide unrestricted access to every server in the organization.

---

# 47. Assume Breach

The **assume breach** principle recognizes that preventive controls can fail.

Architecture should therefore ask:

> **What happens if this system is compromised?**

This leads to controls such as:

- Segmentation
- Monitoring
- Least privilege
- EDR
- Credential isolation
- Backup and recovery
- Incident-response capability

Assume breach is closely related to zero-trust thinking and defense in depth.

---

# 48. Threat Modeling

**Threat modeling** is a structured process for identifying potential threats and designing controls before or during system development.

A simplified process is:

**Identify assets → Map data flows → Identify trust boundaries → Identify threats → Assess risk → Select controls → Validate**

Threat modeling is particularly useful for applications, APIs, cloud services, and complex enterprise architectures.

---

# 49. Data Flow Diagrams and Architecture

A **data flow diagram (DFD)** can help identify where information moves between components.

For example:

```text
User
  |
  v
Web Application
  |
  v
Application Service
  |
  v
Database
```

Security architects can then ask:

- Where does sensitive data cross boundaries?
- Where is authentication performed?
- Where is authorization enforced?
- Where should encryption be applied?
- Where should logging occur?
- What happens if one component is compromised?

---

# 50. Security Zones

A security zone groups systems with similar trust and protection requirements.

Example:

```text
Zone 1 — Internet-facing
Zone 2 — Application
Zone 3 — Internal user
Zone 4 — Restricted data
Zone 5 — Management
```

Communication between zones should be explicitly controlled.

The exact number and naming of zones depends on the organization's architecture.

---

# 51. Air-Gapped and Isolated Systems

An **air-gapped system** is intentionally separated from networks that could provide direct connectivity.

Air gaps can reduce certain remote attack paths, but they do not automatically eliminate risk.

Risks can still arise through:

- Removable media
- Supply-chain compromise
- Maintenance activities
- Insider threats
- Cross-connected systems

Air gaps should therefore be understood as a specific architectural isolation strategy, not as an absolute guarantee of security.

---

# 52. Physical Security as Architecture

Security architecture includes physical considerations.

Examples include:

- Server-room access control
- Badge systems
- Surveillance
- Environmental controls
- Locked network cabinets
- Secure equipment disposal
- Power protection

Physical compromise can bypass many logical security controls.

Therefore, logical and physical architecture must be considered together.

---

# 53. Environmental and Power Considerations

Availability architecture may need to account for:

- Power failure
- Cooling failure
- Fire
- Water damage
- Natural disasters
- Equipment failure

Controls can include:

- UPS systems
- Backup generators
- Redundant cooling
- Fire suppression
- Geographic redundancy
- Environmental monitoring

These controls support system availability and resilience.

---

# 54. Security Architecture Documentation

A well-designed architecture should be documented.

Documentation may include:

- Network diagrams
- Data-flow diagrams
- Trust boundaries
- Security zones
- Asset inventories
- Access-control models
- Data classifications
- Security requirements
- Control mappings
- Dependency diagrams

Documentation helps administrators and security teams understand how controls are intended to work.

---

# 55. Architecture Review

Security architecture should be reviewed when significant changes occur.

Examples include:

- New applications
- Cloud migrations
- Network redesign
- Mergers and acquisitions
- New third-party connections
- Major identity changes
- New sensitive data processing

Architecture review helps prevent new projects from creating unexpected attack paths.

---

# 56. Secure Architecture Lifecycle

A practical lifecycle is:

**Requirements → Design → Threat Modeling → Control Selection → Implementation → Validation → Monitoring → Review → Improvement**

### Requirements

Identify business and security needs.

### Design

Create the architecture and trust boundaries.

### Threat modeling

Identify likely threats and attack paths.

### Control selection

Select controls appropriate to the risks.

### Implementation

Deploy the architecture.

### Validation

Test whether controls work as intended.

### Monitoring

Observe operational behavior.

### Review

Reassess the architecture as the environment changes.

### Improvement

Modify controls and architecture based on findings.

---

# 57. Common Architectural Anti-Patterns

Several design choices can increase risk.

### Flat network

Large numbers of systems can communicate with one another without meaningful restrictions.

**Risk:** large lateral-movement opportunities.

### Shared privileged accounts

Multiple administrators use the same powerful account.

**Risk:** poor accountability and greater credential exposure.

### Internet-exposed management interfaces

Administrative services are directly reachable from untrusted networks.

**Risk:** increased attack surface and credential-attack exposure.

### Excessive permissions

Users or services have more privileges than required.

**Risk:** larger blast radius after compromise.

### Single security control

The architecture depends heavily on one defensive mechanism.

**Risk:** control failure can produce a major security gap.

### Publicly exposed sensitive data

Sensitive storage or services are unnecessarily accessible.

**Risk:** unauthorized disclosure or modification.

---

# 58. Defense in Depth vs Zero Trust

These concepts are complementary but different.

### Defense in depth

Focuses on **multiple layers of controls**.

Question:

> What additional controls can reduce risk if one control fails?

### Zero trust

Focuses on **minimizing implicit trust and continuously evaluating access**.

Question:

> Why should this identity or device receive this access right now?

An architecture can use both.

---

# 59. Zero Trust vs Network Segmentation

Network segmentation divides the environment into controlled zones.

Zero trust goes beyond segmentation by incorporating identity, device state, context, and policy into access decisions.

Segmentation can therefore be one component of a broader zero-trust architecture.

---

# 60. Least Privilege vs Separation of Duties

These concepts are frequently confused.

### Least privilege

Limits **how much access** an identity or process receives.

### Separation of duties

Limits **how much control one individual or role has over a sensitive process** by dividing responsibilities.

Example:

A developer may have permission to deploy code but not approve their own production change.

That combines access restriction with separation of duties.

---

# 61. Security+ Scenario — Flat Network

### Scenario

A company places employee workstations, public web servers, domain controllers, and databases on the same unrestricted network.

An attacker compromises a public web server.

### Analysis

The flat architecture creates unnecessary paths toward internal and highly sensitive systems.

### Architectural improvement

Use segmentation and restricted communication between security zones.

### Lesson

**Segmentation reduces lateral movement and blast radius.**

---

# 62. Security+ Scenario — Zero Trust

### Scenario

An employee is connected to the corporate network but requests access to a highly sensitive application.

The security architecture evaluates the user's identity, MFA status, device compliance, resource sensitivity, and access policy before granting access.

### Analysis

The architecture is not trusting the user merely because the device is on the internal network.

### Lesson

This reflects **zero-trust access principles**.

---

# 63. Security+ Scenario — Least Privilege

### Scenario

A reporting service only needs read access to a database, but its account has full database-administrator privileges.

### Analysis

The service has excessive privileges.

### Architectural improvement

Reduce the service account to the permissions necessary for its function.

### Lesson

**Least privilege limits potential impact if the service is compromised.**

---

# 64. Security+ Scenario — Defense in Depth

### Scenario

An attacker bypasses the perimeter firewall and compromises a public-facing application.

The database is still protected by network segmentation, database authorization, monitoring, and restricted credentials.

### Analysis

Multiple security layers remain after the perimeter control has failed.

### Lesson

This demonstrates **defense in depth**.

---

# 65. Security+ Scenario — Trust Boundary

### Scenario

A web application communicates with a database containing sensitive information.

The security architect requires authentication, authorization, restricted network communication, encryption, and logging between the application and database tiers.

### Analysis

The application-to-database transition represents an important trust boundary.

### Lesson

Trust boundaries should receive appropriate security controls.

---

# 66. Security+ Scenario — Secure by Design

### Scenario

A development team begins a new application. Before implementation, the team maps data flows, identifies trust boundaries, performs threat modeling, defines authentication requirements, and designs logging and authorization controls.

### Analysis

Security requirements are being incorporated during design rather than added after deployment.

### Lesson

This is **secure-by-design** thinking.

---

# 67. Security+ Scenario — Attack Surface Reduction

### Scenario

A server has several unused network services enabled and exposes management interfaces to a broad network.

### Analysis

The unnecessary services and broad management exposure increase the attack surface.

### Architectural improvement

Disable unused services and restrict management access to authorized administrative paths.

### Lesson

Reducing unnecessary exposure reduces attack surface.

---

# 68. Security+ Scenario — Privileged Access

### Scenario

Administrators currently manage critical servers directly from ordinary employee workstations.

### Analysis

Compromise of an administrator's workstation could expose highly privileged credentials and management paths.

### Architectural improvement

Use dedicated administrative identities, MFA, privileged access controls, and restricted management paths such as a jump host where appropriate.

### Lesson

Protect the administrative plane separately from ordinary user activity.

---

# 69. Security+ Scenario — Availability

### Scenario

A critical business application must remain available even if one server fails.

### Analysis

A single-server architecture creates a single point of failure.

### Architectural improvement

Use appropriate redundancy and failover mechanisms, potentially including clustering or load balancing.

### Lesson

Availability requirements influence architecture.

---

# 70. Common Exam Traps

### Trap 1: Zero trust means nobody can access anything

Incorrect.

Zero trust means access is not automatically trusted based on network location. Legitimate access is granted according to policy and context.

### Trap 2: Defense in depth means installing many security products

Incorrect.

Defense in depth means using meaningful layers of protection.

### Trap 3: Least privilege and separation of duties are identical

Incorrect.

Least privilege limits permissions; separation of duties divides sensitive responsibilities.

### Trap 4: A DMZ makes public systems completely safe

Incorrect.

A DMZ provides segmentation and controlled exposure but still requires secure configuration and access controls.

### Trap 5: Internal traffic is automatically trusted

Incorrect in a zero-trust architecture.

Internal systems can be compromised and internal access should still be appropriately controlled.

### Trap 6: Air-gapped means impossible to compromise

Incorrect.

Air gaps reduce certain network paths but do not eliminate risks such as removable media, supply-chain compromise, and insider activity.

### Trap 7: Authentication determines what a user can access

Not by itself.

Authentication establishes identity; authorization determines permissions.

### Trap 8: Redundancy automatically guarantees high availability

Incorrect.

Redundant components require appropriate architecture, failover mechanisms, monitoring, and operational procedures.

### Trap 9: Encryption alone solves data security

Incorrect.

Encryption must be combined with access control, key management, authentication, and appropriate architecture.

### Trap 10: Security architecture is only network design

Incorrect.

Enterprise security architecture includes identity, applications, data, cloud, endpoints, physical security, processes, and operational controls.

---

# 71. Security+ Architecture Decision Framework

When a Security+ question presents an architecture scenario, use this sequence.

### Step 1: Identify the business requirement

Is the primary requirement:

- Confidentiality?
- Integrity?
- Availability?
- Controlled access?
- Resilience?

### Step 2: Identify the critical assets

Determine what needs protection.

### Step 3: Identify trust boundaries

Ask where trust changes between:

- Users
- Networks
- Applications
- Databases
- Cloud services
- Third parties
- Privileged systems

### Step 4: Identify the threat or failure scenario

Consider:

- External compromise
- Insider misuse
- Credential theft
- Lateral movement
- Data exposure
- System failure
- Administrative compromise

### Step 5: Select the architectural principle

Look for:

- Defense in depth
- Zero trust
- Least privilege
- Segmentation
- Secure by design
- Attack-surface reduction
- Separation of duties
- Redundancy/high availability

### Step 6: Place the control at the correct boundary

Ask where the control will be most effective.

For example:

- Firewall → network boundary
- WAF → web/application boundary
- MFA → identity/authentication boundary
- Segmentation → network trust boundary
- PAM → privileged access boundary

### Step 7: Consider failure and compromise

Ask:

**If one control or system fails, what prevents the entire environment from being compromised?**

### Step 8: Validate the architecture

Use testing, monitoring, logging, configuration assessment, and security reviews to determine whether the design operates as intended.

---

# 72. Key Takeaways

1. Enterprise security architecture integrates security into business systems, networks, identities, applications, data, cloud services, endpoints, and operations.
2. Architecture should begin with business requirements and protected assets.
3. The CIA triad provides foundational confidentiality, integrity, and availability objectives.
4. Confidentiality protects against unauthorized disclosure.
5. Integrity protects against unauthorized or improper modification.
6. Availability ensures authorized access when required.
7. Defense in depth uses multiple meaningful security layers.
8. Zero trust minimizes implicit trust and evaluates access using identity, device, resource, and contextual information.
9. Least privilege limits permissions to what is necessary.
10. Separation of duties divides sensitive responsibilities to reduce excessive individual control.
11. Trust boundaries identify places where stronger security controls may be required.
12. Attack-surface reduction removes unnecessary exposure and access paths.
13. Secure-by-design thinking incorporates security during architecture and development.
14. Secure defaults reduce the likelihood of insecure deployment.
15. Fail-secure behavior can prevent unauthorized access when security mechanisms fail, although availability requirements must also be considered.
16. Segmentation limits lateral movement and reduces blast radius.
17. DMZs provide controlled separation for systems requiring less-trusted network exposure.
18. Microsegmentation provides more granular workload-level security boundaries.
19. Identity is an increasingly important security boundary in modern architectures.
20. Authentication establishes identity; authorization determines permitted actions.
21. RBAC assigns permissions through roles.
22. ABAC uses attributes and context to make access decisions.
23. Data classification helps determine appropriate protection requirements.
24. Encryption protects data at rest and in transit and may also protect data in use through specialized approaches.
25. Cryptographic keys require secure lifecycle management.
26. Security architecture should provide appropriate telemetry for monitoring and investigation.
27. Administrative and management interfaces deserve stronger protection because they provide high-impact access.
28. Third-party connections create additional trust boundaries.
29. Internet-facing applications benefit from layered architecture and restricted access to backend systems.
30. Blast-radius reduction is a major architectural objective.
31. Assume-breach thinking designs controls for the possibility that preventive defenses will fail.
32. Threat modeling helps identify attack paths and security requirements before deployment.
33. Data-flow diagrams help identify trust boundaries and sensitive data movement.
34. Security zones group systems with similar trust and protection requirements.
35. Air gaps reduce certain network attack paths but do not eliminate all compromise methods.
36. Physical security is part of enterprise security architecture.
37. Resilience requires planning for system, power, environmental, and security failures.
38. Redundancy can support high availability, but redundancy alone does not guarantee it.
39. Architecture should be documented and reviewed when major environmental changes occur.
40. Common architectural anti-patterns include flat networks, excessive privilege, shared privileged accounts, exposed management interfaces, and dependence on a single security control.
41. Defense in depth, zero trust, segmentation, least privilege, and secure-by-design practices complement one another.
42. Security+ architecture scenarios should be solved by identifying the **business requirement → asset → trust boundary → threat → architectural principle → control placement → failure scenario → validation**.
