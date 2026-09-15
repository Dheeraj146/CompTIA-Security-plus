# 3. Zero Trust and Architecture Principles

## 3.1 Zero Trust

Zero Trust is a security model based on the principle that access should not be automatically trusted merely because a user, device, or application is inside an organization's network.

The traditional perimeter model often assumed that internal traffic was more trustworthy than external traffic. Modern environments make this assumption unreliable because users work remotely, applications are hosted in cloud environments, contractors require access, and an attacker who compromises one endpoint may attempt lateral movement.

Zero Trust changes the question from:

> Is the user inside the network?

To:

> Is this specific access request authorized based on identity, device, resource, context, and policy?

## 3.2 Core Zero Trust Ideas

A Zero Trust implementation generally emphasizes:

- Verify explicitly.
- Use least privilege.
- Assume breach.
- Continuously evaluate trust and access conditions.

Authentication is not necessarily a one-time decision. Access can depend on identity, device security posture, location, requested resource, time, risk signals, and other contextual information.

## 3.3 Continuous Verification

Continuous verification means security decisions can be reevaluated as circumstances change.

For example, a user may successfully authenticate from a managed laptop during normal working hours. If the same session suddenly exhibits suspicious behavior, moves to an unusual location, or the device becomes noncompliant, policy may require additional authentication or block access.

This reduces dependence on a single successful login event.

## 3.4 Least Privilege in Zero Trust

Least privilege limits access to only what is required. In Zero Trust architecture, this principle applies to users, devices, applications, services, APIs, and workloads.

An application should not receive unrestricted access simply because it operates inside the corporate network. A service account should receive only the permissions required by its function.

## 3.5 Assume Breach

Assume breach does not mean that compromise is certain at every moment. It means the architecture should be designed on the assumption that an attacker may eventually bypass a control.

Therefore, organizations should minimize blast radius through segmentation, strong identity controls, monitoring, application isolation, and rapid detection and response.

## 3.6 Defense in Depth vs Zero Trust

These concepts are related but not identical.

**Defense in depth** focuses on multiple layers of security controls so that failure of one layer does not automatically result in compromise.

**Zero Trust** focuses on eliminating implicit trust and continuously enforcing access decisions based on identity, context, policy, and least privilege.

A Zero Trust architecture can use defense-in-depth controls, but the concepts should not be treated as synonyms.

## 3.7 Segmentation

Segmentation divides a network or environment into security zones. It can limit communication between systems and reduce lateral movement.

Traditional segmentation may divide networks by VLAN, subnet, firewall zone, or physical network. More granular microsegmentation can apply policies to individual workloads or application groups.

For example, a workstation network should not automatically have unrestricted access to a database network. A firewall or policy enforcement point can permit only the specific traffic required by the business application.

## 3.8 Honeypots and Honeynets

A honeypot is a deliberately deployed system intended to attract, detect, or study unauthorized activity. It is not normally used to host legitimate production workloads.

A honeynet is a collection of interconnected honeypot systems designed to simulate a larger environment.

Because legitimate users should have little or no reason to interact with a properly isolated honeypot, activity against it can be a valuable detection signal. These technologies are examples of deception capabilities.

## 3.9 Honeytokens

A honeytoken is a decoy object or piece of information designed to trigger an alert when accessed or used.

Examples include a fake credential placed where an attacker might discover it, a decoy database record, or a monitored document containing a unique identifier.

The value of a honeytoken comes from the fact that legitimate users should normally have no reason to use it.

## 3.10 Secure-by-Design Thinking

Security should be incorporated into architecture and development rather than added only after deployment. Secure-by-design thinking considers authentication, authorization, input validation, encryption, logging, secrets management, failure behavior, and recovery requirements during design.

Security architecture should also consider how a system behaves when a component fails. A secure design should avoid turning a failure into an unrestricted-access condition.

## 3.11 Resilience

Security architecture should maintain or restore critical services despite disruption. Resilience can involve redundancy, backups, clustering, failover, alternate infrastructure, disaster recovery procedures, and tested recovery processes.

A system that is secure against unauthorized access but cannot recover from a destructive incident has an incomplete security strategy.

## Security+ Exam Focus

- Zero Trust does not mean "trust nobody" in the simplistic sense; it means no implicit trust based solely on network location.
- Understand least privilege and continuous verification.
- Know the purpose of segmentation and microsegmentation.
- Distinguish Zero Trust from defense in depth.
- Know honeypot, honeynet, and honeytoken concepts.
- Understand that security architecture should account for compromise, lateral movement, and recovery.

## Key Takeaways

1. Zero Trust removes implicit trust.
2. Access decisions should consider identity, device, resource, context, and policy.
3. Least privilege is central to Zero Trust.
4. Assume-breach thinking limits blast radius.
5. Segmentation restricts unnecessary communication and lateral movement.
6. Deception technologies can create high-value detection opportunities.
7. Resilience ensures critical services can withstand and recover from disruption.
