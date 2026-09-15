# Enterprise Security Architecture

## 1. What Is Security Architecture?

Security architecture is the structured design of an organization's technology environment so that security requirements are incorporated into systems, networks, applications, identities, data flows, and operational processes.

A secure architecture does not depend on a single security product. It uses multiple layers of preventive, detective, corrective, and compensating controls. The objective is to reduce the probability and impact of compromise while maintaining required business functionality.

A useful model is:

**Business requirements → assets → threats → risks → security requirements → architecture → controls → validation → continuous improvement**

## 2. Core Security Objectives

### Confidentiality

Confidentiality prevents unauthorized disclosure of information. Encryption, access control, network segmentation, and data classification can support confidentiality.

### Integrity

Integrity ensures that information and systems are not improperly altered. Hashing, digital signatures, access controls, secure configuration, and change management support integrity.

### Availability

Availability ensures that authorized users can access systems and information when required. Redundancy, clustering, load balancing, backups, disaster recovery, and DDoS protections can improve availability.

Security architecture frequently requires balancing these objectives. A control that improves one property can introduce operational cost or complexity elsewhere.

## 3. Defense in Depth

Defense in depth uses multiple independent or partially independent security layers. If one control fails, another control can still reduce the likelihood or impact of compromise.

For example, an internet-facing application might be protected by:

1. Physical security
2. Network segmentation
3. Firewall rules
4. Web application firewall
5. Strong authentication
6. Application security controls
7. Endpoint protection
8. Logging and monitoring
9. Backups and recovery

Defense in depth is different from simply purchasing multiple security products. The controls should address different stages or consequences of an attack.

## 4. Zero Trust Architecture

Zero trust is an architectural approach based on the principle that network location alone should not establish trust. Access decisions should be continuously evaluated using identity, device posture, resource sensitivity, context, and policy.

Important ideas include:

- Verify explicitly.
- Apply least privilege.
- Assume breach.
- Minimize implicit trust.
- Continuously evaluate access and session context.
- Segment resources to limit lateral movement.

A user connected to an internal network is therefore not automatically considered trustworthy merely because the connection originates inside the corporate perimeter.

## 5. Least Privilege

Least privilege gives identities, applications, services, and devices only the permissions required to perform their authorized functions.

It reduces the potential impact of compromised credentials and compromised processes. Privileges should be reviewed periodically and removed when no longer necessary.

## 6. Secure by Design

Secure-by-design architecture considers security requirements during planning rather than treating security as a final deployment step.

Important practices include:

- threat modeling
- secure defaults
- strong authentication
- encryption
- input validation
- logging
- segmentation
- fail-safe behavior
- minimal attack surface
- secure configuration
- lifecycle management

## 7. Trust Boundaries

A trust boundary is a point where the level of trust changes. Examples include the boundary between the internet and an internal network, between users and privileged systems, or between a corporate environment and a third-party cloud service.

Crossing a trust boundary should trigger appropriate validation, authentication, authorization, filtering, or inspection.

## 8. Attack Surface Reduction

Attack surface is reduced by removing unnecessary services, disabling unused interfaces, limiting exposed ports, minimizing privileges, segmenting networks, retiring unsupported systems, and restricting administrative access.

The goal is not necessarily to eliminate every possible entry point. The objective is to reduce unnecessary exposure and make remaining access paths appropriately controlled.

## 9. Security+ Scenario Example

An organization has sensitive database servers, employee workstations, and public web servers. Placing all three groups on one unrestricted network creates unnecessary lateral-movement opportunities.

A stronger design separates public-facing services from internal systems, restricts database access to authorized application servers, and limits administrative paths. The architecture therefore reduces the blast radius if a public server is compromised.

## 10. Common Confusions

**Defense in depth vs least privilege:** Defense in depth uses multiple layers of protection; least privilege limits permissions.

**Zero trust vs no trust:** Zero trust does not mean refusing every connection. It means trust is not automatically granted based solely on network location.

**Attack surface vs vulnerability:** Attack surface describes exposed points that could be targeted; a vulnerability is a weakness that can be exploited.

## 11. Security+ Exam Focus

Be prepared to identify the architectural principle that best satisfies a scenario. Watch for requirements involving least privilege, segmentation, defense in depth, attack-surface reduction, trust boundaries, availability, and zero-trust access decisions.

## 12. Key Takeaways

- Security architecture translates security requirements into technical design.
- Confidentiality, integrity, and availability influence architectural decisions.
- Defense in depth prevents dependence on a single control.
- Zero trust minimizes implicit trust and continuously evaluates access.
- Least privilege limits permissions and potential blast radius.
- Trust boundaries identify locations where stronger controls may be required.
- Secure-by-design thinking begins before deployment.
