# On-Premises, Cloud, and Hybrid Environments

## 1. Deployment Architecture

Organizations can host technology on infrastructure they own, in cloud environments operated by a provider, or through combinations of both. Security architecture must account for ownership, visibility, responsibility, connectivity, identity, data location, and operational dependencies.

## 2. On-Premises Architecture

In an on-premises environment, the organization generally owns or directly controls the physical infrastructure and many underlying security mechanisms.

Advantages can include greater direct control, predictable physical placement, and integration with existing infrastructure. Challenges include hardware costs, maintenance, capacity planning, physical security, patching, and disaster recovery responsibilities.

Security responsibilities commonly include physical access controls, network security, host security, identity management, patch management, backups, monitoring, and configuration management.

## 3. Cloud Computing

Cloud computing provides on-demand access to computing resources through a provider. Security architecture must account for a shared responsibility model: the provider and customer each have responsibilities, and those responsibilities vary by service model.

Cloud security is therefore not equivalent to transferring all security responsibility to the provider.

## 4. Infrastructure as a Service (IaaS)

IaaS provides fundamental computing resources such as virtual machines, storage, and networking.

The provider typically manages the underlying physical infrastructure and virtualization platform, while the customer has significant responsibility for guest operating systems, applications, identities, configurations, data, and network policies.

## 5. Platform as a Service (PaaS)

PaaS provides a managed application platform. The provider manages more of the underlying operating environment than with IaaS.

The customer remains responsible for areas such as application code, data, identities, and configuration according to the provider's specific service boundaries.

## 6. Software as a Service (SaaS)

SaaS delivers a complete application as a managed service. The provider manages most of the infrastructure and application platform.

Customers still need to secure identities, access policies, data usage, configuration, endpoints, and organizational processes.

## 7. Shared Responsibility

A useful way to understand shared responsibility is to ask:

- Who controls the physical hardware?
- Who maintains the hypervisor?
- Who patches the operating system?
- Who secures the application?
- Who manages identities?
- Who protects the data?
- Who configures network controls?

The exact answers depend on the service and provider contract. Security failures can occur when customers assume that a provider is responsible for a control that actually remains their responsibility.

## 8. Hybrid Architecture

A hybrid environment combines on-premises and cloud resources. Organizations may use hybrid architecture because of legacy applications, regulatory requirements, data residency concerns, migration strategies, performance requirements, or business continuity needs.

Hybrid architecture introduces additional security boundaries and dependencies. Identity federation, secure connectivity, consistent policy enforcement, logging, and data protection become especially important.

## 9. Multi-Cloud Architecture

Multi-cloud architecture uses services from more than one cloud provider. It can reduce dependency on a single provider or support specialized capabilities, but it also increases operational complexity.

Security teams must maintain consistent identity, configuration, logging, data protection, and governance across environments.

## 10. Managed Service Provider

A managed service provider (MSP) may operate infrastructure or security functions for an organization. This can provide specialized expertise but introduces third-party risk.

Security architecture should define responsibilities, access restrictions, contractual requirements, monitoring, incident notification, and termination procedures.

## 11. Security Considerations

Important architectural concerns include:

- identity federation and SSO
- MFA
- encryption in transit and at rest
- centralized logging
- cloud configuration management
- network segmentation
- least privilege
- data classification
- backup and recovery
- vendor risk management
- contractual security requirements

## 12. Security+ Scenario Example

An organization wants to move its application servers to IaaS but retain control of sensitive data on-premises. A hybrid architecture can support this design, provided the connection between environments is secured and responsibilities for identity, encryption, access control, monitoring, and backups are clearly assigned.

## 13. Common Confusions

**IaaS vs PaaS:** IaaS provides infrastructure resources; PaaS provides a more managed application platform.

**Cloud security vs provider security:** The provider secures the services and infrastructure within its responsibility; the customer still has configuration, identity, data, and other responsibilities.

**Hybrid vs multi-cloud:** Hybrid combines different infrastructure locations/models, commonly on-premises plus cloud; multi-cloud specifically uses multiple cloud providers.

## 14. Security+ Exam Focus

Expect questions that test service models, responsibility boundaries, hybrid architecture, third-party risk, and the security implications of moving resources between environments. When answering, identify what the customer actually controls before selecting a security responsibility.

## 15. Key Takeaways

- Hosting location changes the security architecture and responsibility model.
- IaaS gives customers more infrastructure responsibility than PaaS or SaaS.
- Cloud adoption does not eliminate customer security responsibilities.
- Hybrid environments require secure integration between trust domains.
- Multi-cloud can improve flexibility but increases governance complexity.
- Third-party services require explicit security responsibilities and risk management.
