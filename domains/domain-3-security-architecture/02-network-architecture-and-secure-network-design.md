# 02 — Network Architecture and Secure Network Design

## 1. Introduction

**Network architecture** describes how network devices, communication paths, services, security boundaries, trust zones, and access policies are organized so that systems can communicate securely and reliably.

Secure network design is not simply about making devices communicate. A well-designed network answers several questions:

- Which systems need to communicate?
- Which systems must never communicate directly?
- Which services need to be exposed?
- Where should traffic be inspected?
- Where do trust boundaries exist?
- How should administrative access occur?
- How can lateral movement be limited?
- What happens if a network component is compromised or unavailable?

A useful design model is:

**Business requirements → Assets → Communication requirements → Trust zones → Network architecture → Security controls → Monitoring → Validation**

The objective is controlled connectivity rather than maximum connectivity.

---

# 2. Network Architecture and Security

A network can be technically functional while still being insecure.

For example, consider an organization where every workstation can directly communicate with:

- Domain controllers
- Databases
- Backup servers
- Network devices
- Security infrastructure

Connectivity may work correctly, but the architecture creates excessive attack paths.

If one workstation is compromised, an attacker may be able to probe or attack many other systems.

Secure network architecture therefore applies principles such as:

- Segmentation
- Least privilege
- Defense in depth
- Explicit access control
- Attack-surface reduction
- Secure administration
- Monitoring
- Resilience

---

# 3. Network Architecture Layers

An enterprise network can be viewed as several logical layers.

A simplified model is:

```text
Internet / External Networks
          |
     Edge Security
          |
    Perimeter Network
          |
   Public/DMZ Services
          |
 Application / Service Tier
          |
    Internal Services
          |
 Restricted Data Tier
```

A separate management architecture may provide controlled administrative access to these layers.

The exact design varies by organization, but the important principle is to avoid treating every system as belonging to one unrestricted trust domain.

---

# 4. Core Network Components

## Router

A **router** forwards packets between different networks based on routing information.

Routers primarily provide connectivity and path selection, although many modern routers can also implement security features such as access-control lists, filtering, and routing security mechanisms.

A router should not automatically be treated as equivalent to a dedicated firewall.

## Switch

A **switch** connects devices within a local network and forwards Ethernet frames based on MAC addresses.

Managed switches can provide security-related capabilities such as:

- VLANs
- Port security
- 802.1X authentication
- DHCP snooping
- Dynamic ARP inspection
- Spanning Tree protections

## Firewall

A **firewall** enforces traffic policies between networks, hosts, or applications depending on its capabilities.

It can make decisions using characteristics such as:

- Source
- Destination
- Protocol
- Port
- Connection state
- Application
- Identity

A firewall should enforce a documented security policy rather than simply allowing everything by default.

## Proxy

A **proxy** acts as an intermediary between a client and another service.

Depending on its type, it can provide:

- Traffic inspection
- Web filtering
- Access control
- Authentication integration
- Caching
- Content filtering
- Privacy or address abstraction

## Load Balancer

A **load balancer** distributes client requests across multiple backend systems.

It can improve:

- Availability
- Scalability
- Performance

Some load balancers can also provide capabilities such as TLS termination, health checks, and application-layer routing.

---

# 5. Firewall Architecture

A firewall establishes policy-controlled boundaries between network zones.

For example:

```text
Internet
   |
[Firewall]
   |
   +---- DMZ
   |
   +---- Internal Network
```

The firewall can enforce different policies for different zones.

For example:

- Internet → Web server: allowed on required ports
- Internet → Internal database: denied
- DMZ → Database: allowed only when required
- Guest → Internal network: denied
- Guest → Internet: allowed

This demonstrates an important principle:

> **Allow required communication; restrict unnecessary communication.**

---

# 6. Stateful Firewall

A **stateful firewall** tracks the state of network connections.

For example, when an internal host initiates an approved connection to an external service, the firewall can track the connection state and determine whether subsequent packets belong to that legitimate session.

Stateful inspection provides more context than simple stateless packet filtering.

---

# 7. Stateless Packet Filtering

A stateless firewall or filtering mechanism evaluates packets primarily against configured rules without maintaining full connection state.

Rules may consider:

- Source IP
- Destination IP
- Protocol
- Port

Stateless filtering can be useful, but it provides less connection context than stateful inspection.

---

# 8. Next-Generation Firewall Concepts

A **next-generation firewall (NGFW)** can provide capabilities beyond traditional IP/port filtering.

Depending on the product, capabilities may include:

- Application awareness
- User identity integration
- Intrusion prevention
- URL filtering
- Malware inspection
- TLS inspection
- Threat intelligence integration

The important Security+ concept is that firewall capabilities can operate at multiple layers and use more context than basic packet filtering.

---

# 9. Security Zones

A **security zone** groups systems according to similar trust, exposure, function, or protection requirements.

Common zones include:

- Internet/untrusted zone
- DMZ/public-services zone
- Employee/user zone
- Server zone
- Database/restricted-data zone
- Management zone
- Security infrastructure zone
- Guest zone
- Development/test zone

The purpose is to prevent systems with different security requirements from sharing unrestricted connectivity.

---

# 10. Network Segmentation

**Network segmentation** divides a network into separate security or functional segments.

Example:

```text
             Firewall
                |
       +--------+--------+
       |        |        |
     Users     Servers   Guest
       |        |        |
       |      Database   Internet
```

Traffic between segments can be controlled through firewalls, ACLs, routing policies, or other security mechanisms.

Segmentation can reduce:

- Lateral movement
- Attack surface
- Broadcast scope
- Blast radius
- Unauthorized access

---

# 11. VLANs

A **Virtual Local Area Network (VLAN)** logically separates devices at the Layer 2 network level.

For example:

```text
VLAN 10 — Employees
VLAN 20 — Servers
VLAN 30 — Guests
VLAN 40 — Management
```

VLANs can support segmentation, but a VLAN alone should not be treated as a complete security boundary.

Communication between VLANs typically requires Layer 3 routing, where additional security controls such as ACLs or firewalls can be applied.

---

# 12. VLANs vs Security Segmentation

VLANs are a technical mechanism for logical network separation.

A security architecture may use VLANs as part of segmentation, but effective segmentation also requires appropriate access-control policies.

For example:

```text
Guest VLAN
     |
   Firewall
     |
 Internet
```

The firewall policy can prevent the guest VLAN from accessing internal resources.

Therefore:

**VLAN = logical Layer 2 separation mechanism**

**Security segmentation = broader architecture and policy controlling communication**

---

# 13. DMZ Architecture

A **DMZ (demilitarized zone)** is a network segment used for systems that need controlled exposure to less-trusted networks.

Typical DMZ systems include:

- Public web servers
- Reverse proxies
- Mail gateways
- Public DNS services
- Internet-facing application components

A simplified design is:

```text
Internet
   |
Firewall
   |
  DMZ
   |
Firewall / Internal Controls
   |
Internal Network
```

A compromised DMZ system should not automatically provide unrestricted access to internal systems.

---

# 14. Reverse Proxy

A **reverse proxy** receives requests from clients and forwards them to backend services.

It can provide:

- Backend abstraction
- TLS termination
- Request routing
- Access control integration
- Caching
- Logging
- Load distribution

A reverse proxy can also prevent direct exposure of backend application servers.

---

# 15. Web Application Firewall

A **Web Application Firewall (WAF)** is designed to inspect and filter HTTP/HTTPS traffic at the application layer.

It can help detect or block certain classes of malicious web requests, such as patterns associated with:

- SQL injection
- Cross-site scripting
- Malicious request manipulation

A WAF is not a replacement for secure application development.

Application vulnerabilities should still be fixed at the source.

---

# 16. Load Balancing and Security

Load balancers distribute traffic among backend systems.

A typical architecture may be:

```text
Internet
   |
Firewall
   |
Load Balancer
   |
+----------+----------+
|          |          |
Web 1     Web 2      Web 3
```

This architecture can improve availability because one backend server can fail while other servers continue serving requests, depending on the design.

Health checks can help the load balancer avoid sending traffic to unhealthy systems.

---

# 17. Network Access Control

**Network Access Control (NAC)** controls network access based on defined policies.

Depending on implementation, NAC may evaluate:

- User identity
- Device identity
- Device ownership
- Security posture
- Certificates
- Endpoint software
- Authentication status

A noncompliant device might be placed into:

- A remediation network
- A quarantine network
- A guest network

instead of receiving normal access.

---

# 18. 802.1X and Port-Based Authentication

**802.1X** provides port-based network access control and is commonly used with wired and wireless networks.

A simplified model is:

```text
Endpoint
   |
Authenticator
(Switch/AP)
   |
Authentication Server
   |
Access Decision
```

802.1X can help ensure that devices or users authenticate before receiving normal network access.

It is commonly associated with technologies such as EAP and RADIUS in enterprise environments.

---

# 19. Ingress Filtering

**Ingress filtering** controls traffic entering a network or security zone.

It can be used to:

- Block unauthorized sources
- Prevent spoofed traffic
- Restrict exposed services
- Enforce perimeter policies

Example:

```text
Internet → Firewall → Internal Network
```

The firewall controls what traffic is permitted to enter.

---

# 20. Egress Filtering

**Egress filtering** controls traffic leaving a network or security zone.

This is important because a compromised host may attempt to:

- Contact command-and-control infrastructure
- Exfiltrate sensitive information
- Attack external systems
- Download additional malicious content

Restricting outbound traffic can limit these activities.

Example policy concept:

```text
Workstation → Internet
        |
   Egress Policy
        |
Only approved services allowed
```

Egress filtering should be based on legitimate business requirements rather than blocking everything without consideration.

---

# 21. Ingress vs Egress

| Concept | Direction | Primary Purpose |
|---|---|---|
| Ingress filtering | Entering a network | Control incoming traffic |
| Egress filtering | Leaving a network | Control outbound traffic |

### Security+ memory aid

**Ingress = IN**

**Egress = EXIT**

---

# 22. North-South Traffic

**North-south traffic** generally moves between internal environments and external networks.

Examples:

- Employee → Internet
- Internet user → public web application
- Branch office → data center

Traditional perimeter security focuses heavily on north-south traffic.

---

# 23. East-West Traffic

**East-west traffic** occurs between internal systems or segments.

Examples:

- Workstation → Server
- Application server → Database
- Server → Server
- Cloud workload → Cloud workload

Attackers frequently attempt lateral movement using east-west paths after gaining an initial foothold.

Therefore, internal traffic should not automatically be considered trustworthy.

---

# 24. North-South vs East-West

| Traffic | Meaning | Example | Security Concern |
|---|---|---|---|
| North-south | External ↔ internal | Internet → web server | Perimeter exposure |
| East-west | Internal ↔ internal | Web server → database | Lateral movement |

Modern architectures need controls for both.

---

# 25. ACLs

An **Access Control List (ACL)** defines traffic or access rules associated with a network device or security boundary.

An ACL may specify:

- Source
- Destination
- Protocol
- Port
- Action

Example concept:

```text
ALLOW 10.10.20.0/24 → 10.10.50.10 TCP/443
DENY  ANY           → 10.10.50.10 ANY
```

ACL syntax and capabilities vary by technology.

The architectural principle is to explicitly restrict unnecessary communication.

---

# 26. Default Deny

A **default-deny** approach blocks traffic unless an explicit rule permits it.

Conceptually:

```text
Required traffic → ALLOW
Everything else  → DENY
```

This is often preferable for sensitive boundaries because it reduces accidental exposure.

However, rules must be carefully designed so that required business operations continue to function.

---

# 27. Any-to-Any Rules

A rule such as:

```text
Source: ANY
Destination: ANY
Service: ANY
Action: ALLOW
```

creates extremely broad connectivity.

Such rules should be avoided unless there is a well-understood and justified architectural requirement.

Security architecture should favor specific communication paths.

---

# 28. Secure Administrative Network

Administrative traffic should be separated from ordinary user traffic where appropriate.

Example:

```text
Administrator
      |
     MFA
      |
  Jump Host
      |
Management Network
      |
+-----+-----+-----+
|     |     |     |
Servers Network Devices Security Systems
```

This reduces the exposure of administrative interfaces.

---

# 29. Jump Server / Bastion Host

A **jump server** or **bastion host** is a controlled intermediary system used to access restricted resources.

Instead of allowing:

```text
Every workstation → Every server
```

the architecture can provide:

```text
Admin → Jump Host → Restricted Server
```

Benefits can include:

- Reduced management exposure
- Centralized logging
- Stronger authentication
- Restricted administrative paths
- Better monitoring

The jump host itself becomes a high-value security asset and must therefore be strongly protected.

---

# 30. Privileged Access Workstations

A **Privileged Access Workstation (PAW)** is a dedicated or specially secured endpoint used for sensitive administrative tasks.

The objective is to prevent administrators from performing privileged actions from ordinary endpoints that may be exposed to:

- Phishing
- Malware
- Browser compromise
- Untrusted applications

PAWs are an example of separating high-risk administrative activity from normal user activity.

---

# 31. Remote Access Architecture

Remote access should be treated as a security boundary.

Common technologies include:

- VPN
- Zero-trust network access
- Remote desktop gateways
- Secure application portals
- MFA
- Device posture checks

A remote user should not automatically receive unrestricted internal network access simply because the VPN connection succeeds.

Access should be limited according to identity, device, resource, and policy.

---

# 32. VPN Architecture

A **Virtual Private Network (VPN)** creates a protected communication tunnel across an untrusted or less-trusted network.

VPNs can provide confidentiality and integrity for traffic, depending on the protocol and configuration.

VPN architectures may be:

- Remote-access VPN
- Site-to-site VPN

### Important distinction

A VPN protects the communication path; it does not automatically guarantee that the endpoint, user, or destination resource is trustworthy.

Authentication, authorization, endpoint security, and segmentation remain important.

---

# 33. Site-to-Site VPN

A site-to-site VPN connects networks through an encrypted tunnel.

Example:

```text
Office A
   |
VPN Gateway
   |
Encrypted Tunnel
   |
VPN Gateway
   |
Office B
```

Security architecture should still restrict what systems and services can communicate across the tunnel.

A VPN connection should not automatically imply that every host in one site can access every host in another site.

---

# 34. Proxy vs VPN

These technologies are often confused.

### Proxy

Acts as an intermediary for particular application traffic.

### VPN

Creates an encrypted network tunnel between endpoints or networks.

A proxy may be used for web filtering or application-level mediation, while a VPN can protect broader network communication.

---

# 35. DNS Security Architecture

DNS translates names into network addresses and is critical to normal enterprise operation.

Security architecture should consider:

- DNS server placement
- Internal vs external DNS
- Access controls
- DNS logging
- DNS filtering
- Secure DNS administration

An organization may use internal DNS infrastructure for internal names while forwarding or resolving external names through controlled services.

---

# 36. Secure DNS Resolution

DNS traffic can be abused for:

- Malicious domain resolution
- Command-and-control
- Data exfiltration
- Phishing infrastructure

Controls can include:

- DNS filtering
- Domain reputation analysis
- DNS logging
- Restricted recursive resolvers
- Monitoring unusual DNS behavior

DNS security should be integrated into the overall network architecture rather than treated as an isolated service.

---

# 37. DHCP Security

DHCP automatically provides network configuration such as IP addresses and gateway information.

A rogue DHCP server can provide malicious or incorrect configuration to clients.

Switch security features such as DHCP snooping can help restrict which ports are permitted to send DHCP server responses, depending on the environment and implementation.

---

# 38. ARP Security

ARP maps IPv4 addresses to MAC addresses on local networks.

ARP does not inherently authenticate these mappings, creating opportunities for ARP spoofing/poisoning.

Architectural protections can include:

- Dynamic ARP Inspection
- DHCP snooping dependencies
- Network segmentation
- Monitoring
- Static configuration in specialized cases

---

# 39. Wireless Network Architecture

Enterprise wireless networks should separate different user populations and trust levels.

Example:

```text
Corporate SSID → Internal authenticated network
Guest SSID     → Guest segment → Internet only
IoT SSID       → Restricted IoT segment
```

Security controls can include:

- WPA2/WPA3 Enterprise
- 802.1X
- Strong authentication
- Network segmentation
- Rogue AP detection
- Client isolation where appropriate

---

# 40. Guest Network Architecture

Guest devices should generally not be placed directly on the employee LAN.

A typical architecture is:

```text
Guest Device
     |
 Guest SSID
     |
 Guest VLAN
     |
 Firewall
     |
 Internet
```

Internal resources remain separated.

This is an example of using a trust-zone boundary to restrict unnecessary access.

---

# 41. IoT Network Architecture

IoT devices often have limited security capabilities and may have long lifecycles.

A safer architecture can place them in dedicated segments.

For example:

```text
IoT Devices
     |
IoT Segment
     |
Firewall / ACL
     |
Only Required Services
```

IoT devices should not automatically receive broad access to employee or server networks.

---

# 42. Network Segmentation for Sensitive Systems

Sensitive systems should have narrower communication requirements.

For example:

```text
Application Server
       |
       | TCP/443 or required DB protocol
       v
Database Server
```

rather than:

```text
Entire Corporate Network
       |
       v
Database Server
```

Specific communication requirements produce stronger security boundaries.

---

# 43. Microsegmentation

**Microsegmentation** applies granular security policies to individual workloads, applications, or systems.

Traditional segmentation might create:

```text
Server Network
```

Microsegmentation can create policies such as:

```text
Web Server A → App Server A : allowed
Web Server A → Database B   : denied
App Server A → Database B   : allowed
```

This can significantly reduce lateral movement opportunities.

---

# 44. Zero Trust and Network Architecture

Zero trust changes the architectural assumption that internal network location equals trust.

A zero-trust architecture may combine:

- Identity verification
- MFA
- Device posture
- Application-level access
- Microsegmentation
- Least privilege
- Continuous evaluation

The network remains important, but identity and resource policy become equally important decision factors.

---

# 45. Network Address Translation

**Network Address Translation (NAT)** translates addresses between network contexts.

NAT can conserve IPv4 address space and can affect how systems are exposed, but NAT should not be treated as a substitute for a firewall.

Security architecture should use explicit access-control mechanisms rather than relying on address translation alone.

---

# 46. Public and Private Addressing

Private IP address ranges are commonly used inside organizations and are not directly routable across the public internet.

Publicly reachable services generally require appropriate public addressing or translation mechanisms.

Security architecture should minimize direct public exposure and place necessary public services behind appropriate security controls.

---

# 47. IPv6 Architectural Considerations

IPv6 introduces different addressing and routing behavior from IPv4.

Security architecture should ensure that IPv6 traffic receives appropriate security controls.

A common architectural mistake is securing IPv4 paths while leaving IPv6 paths insufficiently monitored or filtered.

Organizations should account for:

- IPv6 firewall policies
- IPv6 routing
- Dual-stack environments
- IPv6 monitoring
- Address-management requirements

---

# 48. Network Monitoring Architecture

A secure architecture should provide visibility into important network activity.

Telemetry can include:

- Firewall logs
- DNS logs
- DHCP logs
- NetFlow/IPFIX
- IDS/IPS alerts
- Authentication logs
- VPN logs
- Proxy logs
- Endpoint telemetry

These sources can feed centralized monitoring and SIEM systems.

---

# 49. Network IDS and IPS Placement

An **IDS** detects suspicious activity and generates alerts.

An **IPS** can actively block or prevent certain traffic depending on its configuration and detection capability.

Placement depends on architecture.

Examples include:

- Internet edge
- Data-center boundaries
- Critical server segments
- Internal segmentation points

Sensors should be placed where they can observe meaningful traffic without creating unnecessary blind spots.

---

# 50. Traffic Inspection and Encryption

Encryption protects traffic confidentiality and integrity, but it can also reduce the visibility available to network security tools.

For example, encrypted HTTPS traffic may hide application contents from a simple network sensor.

Architectural decisions may therefore involve:

- TLS termination
- Secure inspection points
- Endpoint telemetry
- Application logging
- Appropriate decryption policies

Decryption should be carefully designed because it can introduce privacy, performance, and key-management considerations.

---

# 51. Network High Availability

Critical network components can become single points of failure.

Availability architecture may use:

- Redundant firewalls
- Multiple routers
- Multiple switches
- Redundant links
- Load balancers
- Multiple internet connections
- Dynamic routing
- Failover mechanisms

The objective is to prevent one hardware or connectivity failure from causing unnecessary business interruption.

---

# 52. Single Point of Failure

A **single point of failure (SPOF)** is a component whose failure can cause a critical service or path to become unavailable.

Example:

```text
Internet
   |
One Firewall
   |
Entire Organization
```

If the firewall fails, connectivity may be lost.

A resilient architecture may instead use redundant firewall instances with appropriate failover.

---

# 53. Redundant Network Paths

A network can also fail because the communication path itself is not redundant.

For example:

```text
Server → One Switch → One Router → Internet
```

Multiple independent paths can improve resilience:

```text
          +→ Switch A → Router A →+
Server ---+                        +--- Internet
          +→ Switch B → Router B →+
```

The effectiveness of redundancy depends on whether the components and paths are genuinely independent.

---

# 54. Out-of-Band Management

**Out-of-band management** provides a separate management path for infrastructure devices.

This can be useful when the production network is unavailable or compromised.

For example, administrators may use a dedicated management network to access network devices even when the normal data path has failed.

Out-of-band management must itself be strongly protected because it provides powerful administrative access.

---

# 55. Network Architecture for Legacy Systems

Legacy systems may not support modern security controls.

Replacing them may not be immediately possible because of:

- Cost
- Vendor dependencies
- Operational requirements
- Specialized software
- Hardware constraints

Compensating architectural controls can include:

- Network isolation
- Strict ACLs
- Restricted administrative access
- Monitoring
- Application allowlisting
- Limited communication paths

This is an example of adapting architecture to technology constraints.

---

# 56. Third-Party Connectivity

Third-party connections create additional trust boundaries.

A secure design should avoid broad network access when only a small set of services is required.

For example:

```text
Partner Network
      |
   VPN / Secure Gateway
      |
 Firewall / ACL
      |
Specific Application
```

Instead of:

```text
Partner Network
      |
Entire Corporate Network
```

The first approach limits unnecessary trust and connectivity.

---

# 57. Cloud Network Architecture

Cloud environments use logical network constructs such as:

- Virtual networks
- Subnets
- Security groups
- Network ACLs
- Routing tables
- Load balancers
- Private endpoints

The same architectural principles still apply:

- Segment workloads.
- Restrict inbound access.
- Restrict outbound access where appropriate.
- Protect management interfaces.
- Minimize public exposure.
- Monitor network activity.

Cloud does not eliminate the need for network architecture.

---

# 58. Public vs Private Cloud Workloads

A common cloud design separates internet-facing and internal components.

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

The database should not require direct public exposure merely because the application is public.

---

# 59. Secure Service-to-Service Communication

Modern applications often consist of multiple services.

Architecture should define:

- Which service can call another service
- Which protocol is allowed
- How identity is established
- How authorization is enforced
- How communication is encrypted
- What is logged

This becomes particularly important in microservices and cloud environments.

---

# 60. Network Architecture and Blast Radius

A major objective of segmentation is reducing blast radius.

Suppose an attacker compromises one employee workstation.

In a flat network:

```text
Workstation → Many Internal Systems
```

In a segmented architecture:

```text
Workstation
    |
User Segment
    |
Restricted Firewall Policy
    |
Limited Approved Services
```

The second design can make lateral movement more difficult and limit the number of systems exposed to the compromised host.

---

# 61. Secure Network Design Lifecycle

A practical design process is:

### Step 1 — Identify requirements

Determine business services, users, availability requirements, and regulatory obligations.

### Step 2 — Identify assets

Inventory servers, endpoints, applications, network devices, data, and dependencies.

### Step 3 — Map communication flows

Determine which systems legitimately need to communicate.

### Step 4 — Define trust zones

Group systems according to trust and security requirements.

### Step 5 — Design boundaries

Determine where firewalls, ACLs, proxies, gateways, and other controls should be placed.

### Step 6 — Minimize connectivity

Remove unnecessary communication paths.

### Step 7 — Protect administration

Separate privileged management access from ordinary traffic.

### Step 8 — Add monitoring

Ensure important traffic and security events are visible.

### Step 9 — Design resilience

Identify single points of failure and provide appropriate redundancy.

### Step 10 — Validate

Test access rules, segmentation, failover, monitoring, and expected application communication.

---

# 62. Security+ Scenario — Guest Network

### Scenario

A company wants visitors to access the internet but prevent them from accessing employee systems.

### Analysis

Guest devices are a different trust population and should not share unrestricted connectivity with employee systems.

### Architectural solution

Use a dedicated guest network/VLAN and firewall policies that allow internet access while restricting internal resources.

### Lesson

**Separate trust zones and explicitly control communication.**

---

# 63. Security+ Scenario — Egress Filtering

### Scenario

A compromised workstation is repeatedly attempting outbound connections to suspicious external destinations.

### Analysis

Outbound communication is part of the attack path.

### Architectural control

Use egress filtering and monitoring to restrict unnecessary outbound traffic and detect suspicious connections.

### Lesson

**Security architecture should control both incoming and outgoing traffic.**

---

# 64. Security+ Scenario — Lateral Movement

### Scenario

An attacker compromises one employee workstation and begins scanning internal servers.

### Analysis

The attack is moving through east-west traffic.

### Architectural control

Use segmentation, host-based controls, ACLs, and monitoring to restrict unnecessary internal communication.

### Lesson

**East-west security is essential for limiting lateral movement.**

---

# 65. Security+ Scenario — Administrative Access

### Scenario

Administrators currently access all servers directly from normal employee laptops.

### Analysis

A compromised employee laptop could expose privileged credentials and management paths.

### Architectural improvement

Use dedicated administrative workstations, MFA, a jump host, and a restricted management network.

### Lesson

**Protect the management plane separately.**

---

# 66. Security+ Scenario — DMZ

### Scenario

A company hosts a public web server that must be accessible from the internet while the database remains internal.

### Architectural solution

Place the public-facing service in a controlled DMZ and restrict communication from the DMZ to only required internal services.

### Lesson

**Public exposure should not imply unrestricted internal access.**

---

# 67. Security+ Scenario — NAC

### Scenario

An organization wants to prevent unmanaged laptops from receiving normal corporate network access.

### Architectural solution

Use NAC to evaluate device identity or security posture and place noncompliant devices into a restricted or remediation network.

### Lesson

**NAC can enforce access decisions based on device and identity characteristics.**

---

# 68. Security+ Scenario — Single Point of Failure

### Scenario

A critical organization uses one firewall. A hardware failure would disconnect the entire environment from required networks.

### Analysis

The firewall is a single point of failure.

### Architectural improvement

Use an appropriately designed redundant firewall architecture with failover and operational monitoring.

### Lesson

**Availability requirements influence network architecture.**

---

# 69. Security+ Scenario — Third-Party Access

### Scenario

A vendor requires access to one application but requests access to the entire corporate network.

### Analysis

The requested access is broader than the business requirement.

### Architectural approach

Provide only the required application or service path through controlled connectivity.

### Lesson

**Third-party access should follow least privilege and explicit trust boundaries.**

---

# 70. Security+ Scenario — Legacy System

### Scenario

A legacy industrial system cannot support modern endpoint security software but must remain operational.

### Architectural approach

Isolate the system, restrict communication to required services, protect administration, and increase monitoring.

### Lesson

**Compensating architectural controls can reduce risk when technology cannot be replaced immediately.**

---

# 71. Common Exam Traps

### Trap 1: A router is the same as a firewall

Not necessarily.

A router primarily forwards traffic, while a firewall is designed to enforce security policy. Modern devices may combine capabilities.

### Trap 2: A VLAN alone is a complete security boundary

A VLAN provides logical Layer 2 separation, but secure communication between networks requires appropriate routing and security policy.

### Trap 3: A VPN makes internal access completely trusted

Incorrect.

A VPN protects the communication tunnel, but authentication, authorization, endpoint security, and segmentation remain necessary.

### Trap 4: DMZ systems are completely isolated

Not necessarily.

The DMZ is a controlled zone. Firewall rules must still restrict communication to internal resources.

### Trap 5: Only inbound traffic matters

Incorrect.

Outbound traffic can support C2 communication, data exfiltration, and attacks against external systems.

### Trap 6: Internal traffic is trusted

Modern architectures should not automatically trust internal east-west traffic.

### Trap 7: NAT is a firewall

NAT and firewalling are different functions.

### Trap 8: NAC is only an antivirus system

NAC is a network-access policy mechanism that can evaluate identities, devices, and security posture.

### Trap 9: Load balancing is only for performance

Load balancing can also support availability, health checking, and sometimes security functions.

### Trap 10: One large network is easier and therefore better

Operational simplicity does not automatically justify a large unrestricted trust domain.

---

# 72. Important Security+ Distinctions

| Concept | Meaning |
|---|---|
| Router | Forwards traffic between networks |
| Switch | Connects devices within a LAN and forwards frames |
| Firewall | Enforces traffic security policies |
| Proxy | Intermediates application traffic |
| VPN | Creates a protected tunnel across an untrusted network |
| VLAN | Provides logical Layer 2 network separation |
| DMZ | Controlled zone for systems requiring less-trusted exposure |
| NAC | Controls network access based on defined policy |
| IDS | Detects suspicious activity |
| IPS | Can actively block detected malicious traffic |
| WAF | Filters web/application-layer requests |
| Load balancer | Distributes traffic among backend systems |
| North-south | External ↔ internal traffic |
| East-west | Internal ↔ internal traffic |
| Ingress | Traffic entering a zone |
| Egress | Traffic leaving a zone |
| Segmentation | Separates systems and controls communication |
| Microsegmentation | Applies granular workload-level security policies |
| Jump host | Controlled intermediary for administrative access |

---

# 73. Security+ Network Architecture Reasoning Framework

When solving a network architecture scenario, use this process.

### Step 1 — Identify the requirement

Is the question about:

- Preventing lateral movement?
- Protecting public services?
- Restricting guest access?
- Securing administration?
- Controlling outbound traffic?
- Improving availability?
- Protecting sensitive systems?

### Step 2 — Identify the trust relationship

Determine which systems are:

- Untrusted
- User-controlled
- Public-facing
- Internal
- Privileged
- Highly sensitive

### Step 3 — Identify the communication flow

Ask:

**Who needs to communicate with whom?**

### Step 4 — Remove unnecessary paths

Apply least privilege to network connectivity.

### Step 5 — Select the appropriate control

Examples:

- Firewall → zone boundary
- ACL → specific traffic policy
- NAC → device/network access decision
- WAF → web application traffic
- Proxy → application mediation
- VPN → protected remote/site connectivity
- Segmentation → trust isolation
- Jump host → controlled administration

### Step 6 — Consider compromise

Ask:

> If one system is compromised, how far can the attacker move?

### Step 7 — Consider availability

Ask:

> What happens if this network component fails?

### Step 8 — Consider visibility

Ask:

> Can the organization detect and investigate suspicious traffic?

---

# 74. Key Takeaways

1. Secure network architecture is based on controlled connectivity rather than unrestricted communication.
2. Network design should begin with business requirements and legitimate communication flows.
3. Routers provide network forwarding; firewalls enforce security policy.
4. Switches can provide security features such as VLANs and 802.1X.
5. Proxies act as intermediaries for application traffic.
6. Load balancers improve scalability and can contribute to availability.
7. Security zones group systems according to trust, function, or protection requirements.
8. Segmentation reduces lateral movement and blast radius.
9. VLANs provide logical Layer 2 separation but should not automatically be treated as complete security boundaries.
10. DMZs provide controlled placement for systems requiring external exposure.
11. Reverse proxies can hide and protect backend services.
12. WAFs inspect web/application-layer traffic and complement secure application development.
13. NAC can enforce network access policies based on device, identity, and security posture.
14. 802.1X provides port-based network access control.
15. Ingress filtering controls incoming traffic.
16. Egress filtering controls outbound traffic and can limit C2 and exfiltration paths.
17. North-south traffic crosses major external boundaries; east-west traffic moves internally.
18. East-west controls are important for limiting lateral movement.
19. ACLs should implement specific communication requirements rather than broad unrestricted access.
20. Default-deny architecture blocks traffic unless explicitly permitted.
21. Administrative access should use protected management paths.
22. Jump hosts and privileged access workstations reduce exposure of administrative interfaces.
23. Remote access should be treated as a security boundary.
24. VPNs protect communication paths but do not replace authentication, authorization, or endpoint security.
25. DNS and DHCP are important infrastructure services that require security controls and monitoring.
26. Wireless, IoT, and guest devices should be placed into appropriately controlled network zones.
27. Microsegmentation provides granular workload-level communication policies.
28. Zero trust reduces reliance on internal network location as a trust signal.
29. NAT should not be treated as a replacement for firewall policy.
30. IPv6 traffic must receive appropriate security controls and monitoring.
31. Network monitoring should provide visibility through firewalls, DNS, DHCP, VPN, proxy, IDS/IPS, flow, and endpoint telemetry where appropriate.
32. Encryption can reduce network inspection visibility and requires deliberate architecture.
33. Critical network components should be evaluated for single points of failure.
34. Redundant paths and devices can improve availability when correctly designed.
35. Legacy systems may require segmentation and compensating controls.
36. Third-party connectivity should provide only required access across controlled trust boundaries.
37. Cloud networks still require segmentation, access control, monitoring, and attack-surface reduction.
38. Secure service-to-service communication requires explicit identity, authorization, encryption, and logging considerations.
39. Network architecture should be documented, tested, monitored, and reviewed as requirements change.
40. Security+ network scenarios should be analyzed using **requirement → trust boundary → communication flow → segmentation → control placement → compromise containment → visibility → availability**.
