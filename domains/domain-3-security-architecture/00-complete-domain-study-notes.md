# Domain 3 — Complete Study Notes: Security Architecture

Domain 3 explains how security is designed into enterprise environments. Instead of beginning with a security product, architecture begins with business requirements, assets, trust boundaries, threats, data flows, availability requirements, and operational constraints. The objective is to build an environment where security controls are placed deliberately and work together.

## 1. Enterprise Security Architecture

Security architecture defines how systems, networks, identities, applications, data, and security controls are arranged. A secure architecture protects confidentiality, integrity, and availability while supporting legitimate business operations.

Important design principles include least privilege, defense in depth, secure defaults, segmentation, zero trust, redundancy, centralized visibility, and minimizing unnecessary attack surface.

### Zero Trust

Zero trust does not automatically trust a user or device because it is inside a corporate network. Access is continuously evaluated using identity, device posture, resource sensitivity, context, and policy. The principle is commonly summarized as **never trust, always verify**.

### Trust boundaries

A trust boundary separates environments with different trust levels or security requirements. Examples include a user network and a server network, an internet-facing DMZ and an internal network, or an application tier and a database tier.

## 2. Network Architecture and Secure Design

Network architecture determines how communication is organized and controlled.

A secure design considers routing, switching, firewalls, proxies, intrusion detection and prevention, network access control, VPNs, DNS, remote access, and monitoring.

A **DMZ** is a controlled network segment commonly used for systems that must be reachable from less-trusted networks. Internet-facing web servers can be isolated from internal systems so compromise of the public service does not automatically provide direct access to internal resources.

A layered architecture can separate:

`Internet → Edge Controls → DMZ → Application Tier → Database Tier`

Each boundary can enforce appropriate controls.

## 3. On-Premises, Cloud, and Hybrid Environments

On-premises infrastructure gives an organization direct control over physical equipment, networks, and many infrastructure decisions. Cloud environments transfer some operational responsibilities to a provider.

### IaaS

Infrastructure as a Service provides virtualized compute, networking, and storage. The customer generally manages operating systems, applications, identities, and configuration while the provider manages underlying physical infrastructure.

### PaaS

Platform as a Service provides a managed application platform. The provider handles more of the underlying infrastructure, while the customer focuses primarily on applications, data, and configuration.

### SaaS

Software as a Service provides a complete application managed by the provider. Customers still remain responsible for identities, access, data handling, configuration, and organizational governance.

The exact boundary depends on the service and provider. This is the **shared responsibility model**.

## 4. Segmentation and Isolation

Segmentation divides an environment into security zones. The purpose is to limit unnecessary communication and contain compromise.

**VLANs** logically separate network traffic. A **DMZ** isolates externally exposed services. **Microsegmentation** applies fine-grained controls between workloads. An **air gap** creates strong physical or logical separation from another network.

Segmentation is not simply a performance design. It is a security control because it limits lateral movement.

## 5. Virtualization and Containers

Virtualization allows multiple logical systems to run on shared physical infrastructure. A **hypervisor** manages virtual machines.

Type 1 hypervisors run directly on hardware. Type 2 hypervisors run on top of a host operating system.

Virtualization introduces risks such as hypervisor vulnerabilities, insecure management interfaces, VM escape, snapshot exposure, excessive privileges, and poor isolation.

Containers share the host operating-system kernel and are generally lighter than full virtual machines. Container security requires image scanning, trusted registries, least privilege, secret management, runtime monitoring, and secure orchestration.

## 6. Cloud Security Architecture

Cloud architecture requires identity-centric security because traditional network boundaries are less reliable. Strong IAM, MFA, encryption, logging, secure configuration, network controls, workload isolation, and continuous monitoring are essential.

Cloud-specific risks include exposed storage, excessive permissions, insecure APIs, compromised credentials, configuration drift, insecure images, and provider dependency.

A common cloud security principle is to grant each identity and workload only the permissions required for its task.

## 7. IoT, ICS, and Embedded Systems

IoT devices connect physical objects to networks. Embedded systems are specialized computing components built into larger products. Industrial Control Systems manage physical processes and can include SCADA components, PLCs, sensors, and controllers.

These environments create unique security requirements. Availability and safety can be more important than rapid patching. A security control that interrupts a manufacturing process may create physical danger.

Security architecture therefore considers asset criticality, lifecycle, vendor support, segmentation, secure management, monitoring, and safe maintenance procedures.

## 8. Secure Protocols and Network Security Technologies

Secure protocols protect communications against interception, modification, and impersonation.

**TLS** protects application-layer communications. **SSH** provides secure remote administration. **IPsec** can protect IP communications and is commonly used for VPNs.

Firewalls enforce traffic policies. IDS identifies suspicious traffic and generates alerts. IPS can actively block or prevent traffic. A proxy acts as an intermediary. A WAF protects web applications from HTTP-based attacks. NAC evaluates whether devices should receive network access.

The technology must match the security requirement; no single control provides complete protection.

## 9. Resilience, Redundancy, and High Availability

**Resilience** is the ability to continue operating or recover after disruption. **Redundancy** provides additional components so one failure does not necessarily stop the service.

High availability can use active-active or active-passive architectures. Load balancing distributes workload and can improve availability. Clustering allows multiple systems to provide a service.

Architecture must consider failure domains. Two servers in the same physical rack may provide less resilience than two servers separated across failure domains.

## 10. Disaster Recovery and Backup Architecture

Disaster recovery restores technology services after disruptive events. Recovery architecture is based on business requirements.

**RTO** defines how quickly a service should be restored. **RPO** defines how much data loss measured in time is acceptable.

Backup types include full, incremental, and differential. Recovery sites may be hot, warm, or cold depending on readiness and cost.

Backups should be protected against unauthorized access, corruption, and ransomware. Recovery must be tested rather than assumed to work.

## 11. Secure Application Development and Deployment

Secure development integrates security throughout the software lifecycle instead of waiting for final testing.

Activities include threat modeling, secure coding, peer review, dependency management, vulnerability scanning, secrets management, testing, and controlled deployment.

CI/CD pipelines require access control and protection because compromise of a build pipeline can become a supply-chain attack. Infrastructure as Code should be reviewed and scanned for insecure configurations.

## 12. Cryptographic Architecture

Cryptography protects information through mathematical techniques.

**Symmetric encryption** uses the same secret key for encryption and decryption and is efficient for large volumes of data. **Asymmetric cryptography** uses a public/private key pair and supports secure key exchange, digital signatures, and identity mechanisms.

**Hashing** produces a fixed-length digest and is normally used for integrity verification and password storage designs rather than reversible encryption.

**Digital signatures** provide integrity and signer authentication. **PKI** manages certificates and trust relationships. Certificate authorities issue certificates that bind identities to public keys.

Key management is critical. Strong algorithms are ineffective if keys are exposed, poorly stored, improperly rotated, or never revoked when compromised.

## Architecture Scenario Method

For an architecture question, identify:

1. Business requirement.
2. Critical assets.
3. Trust boundaries.
4. Threats and attack paths.
5. Required security properties.
6. Appropriate controls.
7. Availability and recovery requirements.
8. Operational and cost constraints.

## Key Takeaways

Secure architecture is the deliberate placement of controls around assets, trust boundaries, communication paths, identities, applications, and recovery requirements. Security+ questions often test whether you understand **why** a technology belongs in an architecture rather than simply recognizing its name.
