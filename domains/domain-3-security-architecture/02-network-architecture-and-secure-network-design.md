# Network Architecture and Secure Network Design

## 1. Network Architecture

Network architecture describes how network components, communication paths, security boundaries, services, and trust zones are organized.

A secure design considers not only connectivity but also who or what is allowed to communicate, which services must be exposed, where inspection occurs, and how compromise in one segment can be contained.

## 2. Common Architectural Components

### Router

A router forwards traffic between different networks. It can also participate in access-control and routing policies, but a dedicated firewall normally provides more specialized security inspection.

### Switch

A switch connects devices within a network. Managed switches support security capabilities such as VLANs, port security, and traffic controls.

### Firewall

A firewall enforces traffic policies between network zones. It can allow, deny, or inspect traffic according to characteristics such as source, destination, protocol, port, identity, or application context depending on its capabilities.

### Proxy

A proxy acts as an intermediary between a client and a destination service. It can provide traffic inspection, access control, caching, filtering, and identity-aware policy enforcement.

### Load Balancer

A load balancer distributes client requests across multiple servers. It can improve availability and scalability and, depending on the implementation, terminate TLS or provide application-layer security features.

## 3. Security Zones

A secure network commonly divides systems according to their trust level and business function. Typical zones include:

- Internet or untrusted zone
- Public-facing services
- User workstation network
- Server network
- Management network
- Security infrastructure
- Highly restricted data systems
- Guest network

The purpose is to prevent unrestricted communication between systems that have different security requirements.

## 4. Secure Network Design Principles

### Minimize Exposure

Expose only services that must be reachable. Unnecessary public services increase attack surface.

### Restrict East-West Traffic

East-west traffic is communication between systems inside an environment. Restricting it helps prevent an attacker who compromises one endpoint from freely moving laterally.

### Separate Administrative Access

Administrative interfaces should not be broadly reachable from ordinary user networks. A dedicated management network or controlled administrative access path reduces exposure.

### Apply Explicit Rules

Network access should be based on defined business and security requirements rather than unrestricted connectivity.

## 5. Ingress and Egress Filtering

Ingress filtering controls traffic entering a network or security zone. Egress filtering controls traffic leaving it.

Egress controls are important because a compromised host may attempt to communicate with command-and-control infrastructure, exfiltrate data, or attack other systems. Restricting outbound traffic can therefore limit post-compromise activity.

## 6. North-South and East-West Traffic

**North-south traffic** generally moves between internal environments and external networks such as the internet.

**East-west traffic** moves between internal systems or segments.

Traditional perimeter defenses concentrate heavily on north-south traffic. Modern architectures also need strong east-west controls because attackers frequently attempt lateral movement after obtaining an initial foothold.

## 7. Secure Administrative Architecture

Administrative access should be separated from normal user activity. Common design principles include dedicated management networks, privileged access workstations, MFA, jump servers, restricted management protocols, logging, and just-in-time or time-limited privileges.

A jump server provides a controlled intermediary point from which administrators can access restricted systems instead of exposing management interfaces throughout the network.

## 8. Network Access Control

Network Access Control (NAC) can evaluate devices before or during network access. Depending on implementation, decisions may consider identity, device ownership, security posture, certificates, endpoint software, or location.

NAC can place noncompliant devices into restricted or remediation networks rather than granting normal access.

## 9. Security+ Scenario Example

If an organization needs to prevent guest laptops from accessing internal servers while still providing internet access, a dedicated guest network with appropriate firewall policies is more secure than placing guests on the employee LAN.

The key architectural idea is separation of trust zones and controlled communication between them.

## 10. Common Confusions

**Router vs firewall:** A router primarily forwards traffic between networks; a firewall primarily enforces security policy. Modern devices may combine functions.

**Proxy vs VPN:** A proxy generally intermediates specific application traffic; a VPN establishes an encrypted tunnel between endpoints or networks.

**East-west vs north-south:** East-west is internal lateral communication; north-south crosses the organizational perimeter or major external boundary.

## 11. Security+ Exam Focus

Scenario questions may describe a requirement and ask where a control should be placed. Focus on trust zones, management networks, ingress/egress controls, internal segmentation, firewall placement, NAC, proxies, and the principle of minimizing unnecessary connectivity.

## 12. Key Takeaways

- Secure network design is based on controlled communication, not unrestricted connectivity.
- Segment systems with different trust and security requirements.
- Protect management interfaces separately from ordinary user traffic.
- Control both inbound and outbound traffic.
- Restrict east-west traffic to limit lateral movement.
- Use NAC to enforce device and access policies where appropriate.
