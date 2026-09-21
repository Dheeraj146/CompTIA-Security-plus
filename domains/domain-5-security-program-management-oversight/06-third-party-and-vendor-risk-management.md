# Third-Party and Vendor Risk Management

## 1. Why Third-Party Risk Matters

Modern organizations rarely operate entirely within their own infrastructure.

They depend on:

- Cloud service providers
- SaaS platforms
- Managed service providers
- Managed security service providers
- Software vendors
- Hardware manufacturers
- Contractors
- Consultants
- Payment processors
- Logistics providers
- Telecommunications providers
- Data processors
- Outsourced IT teams
- Software libraries and open-source components

These relationships can improve efficiency and provide specialized capabilities, but they also extend the organization's **attack surface, trust relationships, and dependency chain**.

A third party may have access to:

- Corporate networks
- Applications
- APIs
- Customer data
- Credentials
- Source code
- Administrative interfaces
- Physical facilities
- Sensitive business processes

Therefore:

> **Outsourcing a service does not outsource the organization's accountability for managing the associated risk.**

Third-party risk management attempts to understand, reduce, monitor, and eventually terminate those risks when the relationship ends.

---

## 2. Third-Party Risk Categories

Vendor risk is not limited to cybersecurity.

A third party can create:

### Security Risk

Examples:

- Weak authentication
- Vulnerable software
- Poor access controls
- Inadequate logging
- Compromised vendor credentials

### Privacy Risk

Examples:

- Unauthorized processing of personal information
- Excessive data collection
- Improper data retention
- Cross-border data transfer issues

### Availability Risk

Examples:

- Vendor outage
- Cloud service failure
- Supplier disruption
- Telecommunications failure

### Compliance Risk

A vendor may fail to satisfy requirements imposed by:

- Laws
- Regulations
- Contracts
- Industry standards
- Customer commitments

### Financial Risk

Examples:

- Vendor bankruptcy
- Unexpected costs
- Contract disputes
- Business interruption

### Reputational Risk

A vendor security incident can affect the organization's customers even if the organization's own systems were not directly compromised.

---

## 3. Third-Party vs Fourth-Party Risk

### Third Party

A third party directly provides a service to the organization.

Example:

> Company A uses Cloud Provider B.

Cloud Provider B is a third party.

### Fourth Party

A third party may itself depend on another organization.

Example:

**Company → SaaS Provider → Cloud Provider**

The cloud provider becomes a **fourth-party dependency** from the perspective of the original organization.

This matters because an organization may believe it has evaluated its vendor while remaining unaware of critical downstream dependencies.

---

## 4. Vendor Risk Management Lifecycle

A practical vendor risk lifecycle is:

**Identify**
↓
**Classify**
↓
**Perform Due Diligence**
↓
**Assess Risk**
↓
**Define Requirements**
↓
**Contract**
↓
**Onboard**
↓
**Monitor**
↓
**Reassess**
↓
**Remediate or Accept Risk**
↓
**Offboard**

Third-party risk management should therefore be treated as a **lifecycle**, not a one-time questionnaire.

---

## 5. Vendor Identification and Inventory

An organization cannot manage vendor risk if it does not know which vendors exist.

A vendor inventory may include:

- Vendor name
- Service provided
- Business owner
- Security owner
- Data accessed
- Systems accessed
- Network connectivity
- Geographic location
- Contract information
- Renewal date
- Criticality
- Risk rating
- Subcontractors
- Compliance requirements
- Incident history

Shadow procurement or unauthorized SaaS usage can create unknown third-party dependencies.

Therefore, procurement, IT, security, legal, finance, and business teams may need coordinated visibility.

---

## 6. Vendor Classification

Not every vendor requires the same level of scrutiny.

A useful classification considers:

- Data sensitivity
- System access
- Privileged access
- Network connectivity
- Business criticality
- Availability requirements
- Regulatory impact
- Geographic exposure
- Volume of transactions
- Dependence on the vendor

For example:

### Low-Risk Vendor

Provides office supplies and has no system or sensitive-data access.

### Medium-Risk Vendor

Provides a business application with limited organizational data.

### High-Risk Vendor

Hosts sensitive customer data and has privileged integration with critical systems.

The high-risk vendor should generally receive deeper assessment and stronger contractual requirements.

---

## 7. Vendor Criticality

**Vendor criticality** describes how important the vendor is to business operations.

A vendor may be critical because:

- Its service supports revenue
- Its outage stops an essential business process
- It handles sensitive data
- It provides an important security service
- There is no practical replacement
- Migration would take substantial time

Criticality should influence:

- Assessment depth
- Contract requirements
- Monitoring frequency
- Continuity requirements
- Exit planning

---

## 8. Due Diligence

**Due diligence** is the process of investigating and understanding risks associated with a third party.

It can occur before entering the relationship and throughout the relationship.

Questions may address:

- Security architecture
- Access control
- MFA
- Encryption
- Vulnerability management
- Incident response
- Logging
- Backup and recovery
- Business continuity
- Privacy
- Data retention
- Subcontractors
- Physical security
- Personnel security
- Compliance
- Secure development
- Supply-chain controls

The objective is to determine whether the vendor's security practices are appropriate for the risk created by the relationship.

---

## 9. Due Care

**Due care** means taking reasonable actions to address known risks.

A useful distinction is:

**Due diligence → investigate and understand**

**Due care → take reasonable protective action**

Example:

An organization performs a vendor assessment and discovers that a critical vendor lacks MFA for privileged access.

Due diligence helped identify the issue.

Requiring remediation, implementing compensating controls, or changing the relationship demonstrates due care.

---

## 10. Vendor Security Questionnaires

Questionnaires can be used to collect information about vendor security.

Topics may include:

- Security governance
- Access control
- Encryption
- Vulnerability management
- Incident response
- Business continuity
- Privacy
- Physical security
- Personnel security
- Secure development
- Third-party dependencies

However, questionnaires have limitations.

A vendor can provide answers that are:

- Incomplete
- Outdated
- Overly broad
- Difficult to verify

Therefore, high-risk vendors may require additional evidence.

---

## 11. Evidence-Based Vendor Assessment

Evidence may include:

- Independent audit reports
- Certification reports
- Penetration-test summaries
- Security assessment results
- Policies
- Incident-response documentation
- Business-continuity test results
- Vulnerability-management evidence
- Architecture documentation

The exact evidence required depends on the organization's risk and contractual requirements.

The principle is:

> **The higher the risk, the more important independent and verifiable evidence becomes.**

---

## 12. SOC 2 and Other Assurance Reports

Organizations may request independent assurance reports where appropriate.

For example, a SOC 2 report can provide information about controls relevant to security and other trust-service criteria, depending on the report's scope.

However, an assurance report should not automatically be treated as proof that every possible risk is eliminated.

The organization should examine:

- Scope
- Reporting period
- Control objectives
- Exceptions
- Complementary user entity controls
- Whether the assessed service actually matches the service being purchased

This is an important Security+ reasoning principle:

> **Evidence must be relevant to the actual service and risk being evaluated.**

---

## 13. Contractual Security Requirements

Security requirements should be reflected in contracts where appropriate.

Contracts can define:

- Security responsibilities
- Data ownership
- Data handling
- Encryption requirements
- Access controls
- Incident notification
- Audit rights
- Vulnerability management
- Security testing
- Business continuity
- Recovery objectives
- Data location
- Retention
- Data destruction
- Subcontractor requirements
- Service levels
- Exit requirements

Contracts turn security expectations into enforceable obligations.

---

## 14. Service-Level Agreements

A **Service-Level Agreement (SLA)** defines expected service performance.

Examples include:

- Availability
- Response time
- Support response
- Incident notification
- Recovery objectives
- Service performance

For a critical vendor, the organization may require specific recovery commitments.

However:

> **An SLA does not automatically guarantee security.**

An availability SLA may define uptime while saying nothing about authentication, encryption, vulnerability management, or breach notification.

Security requirements may therefore need to be explicitly included.

---

## 15. Security Clauses

Vendor contracts may include security clauses covering:

### Incident Notification

How quickly must the vendor notify the organization after discovering a security incident?

### Access Control

What vendor personnel may access organizational systems?

### Authentication

Are MFA and strong authentication required?

### Data Protection

How must organizational data be protected?

### Encryption

What encryption requirements apply?

### Security Testing

Can the organization require vulnerability assessments or penetration testing?

### Audit Rights

Can the organization review evidence of controls?

### Subcontractors

Can the vendor use additional providers?

### Data Destruction

What happens to data when the relationship ends?

These requirements should reflect risk rather than being copied blindly into every contract.

---

## 16. Shared Responsibility

Third-party services often create **shared responsibility**.

For example, a cloud provider may secure certain underlying infrastructure while the customer remains responsible for:

- Account configuration
- Identity
- Access policies
- Data
- Applications
- Some network controls

The exact division depends on the service.

Security responsibilities should therefore be explicitly understood.

A common failure is:

> "The vendor handles security."

That statement is usually too broad.

The organization must determine **which party is responsible for which control**.

---

## 17. Responsibility Matrix

A responsibility matrix can document:

| Security Area | Organization | Vendor |
|---|---|---|
| Customer data classification | ✓ | |
| Underlying infrastructure | | ✓ |
| Account configuration | ✓ | |
| Vendor personnel security | | ✓ |
| Customer IAM | ✓ | |
| Service availability | Shared | Shared |
| Incident notification | | ✓ |
| Incident coordination | ✓ | Shared |
| Data deletion at termination | Shared | Shared |

The exact responsibilities depend on the service.

A documented responsibility model reduces ambiguity during an incident.

---

## 18. Vendor Access Management

Third-party access should follow:

- Least privilege
- Need-to-know
- MFA
- Time-limited access where possible
- Separate accounts
- Logging
- Monitoring
- Approval workflows
- Periodic access reviews

Avoid giving a vendor permanent broad access simply because it is convenient.

For example, a support vendor may need administrative access for two hours to troubleshoot a system.

A controlled workflow could provide:

**Approved request → Temporary privileged access → Monitoring → Work completed → Access removed**

This is safer than maintaining a permanent shared administrator account.

---

## 19. Remote Vendor Access

Vendor remote access creates a significant trust boundary.

Controls may include:

- VPN or zero-trust access
- MFA
- Privileged access management
- Jump hosts
- Network segmentation
- Session logging
- Time-limited access
- Device posture checks
- Approval requirements

Vendor access should ideally reach only the systems required for the vendor's task.

---

## 20. Vendor Identity Management

Vendor accounts should be included in the organization's identity lifecycle.

When a vendor employee:

- Joins a project
- Changes responsibilities
- Leaves the vendor
- No longer needs access

their access should be reviewed or removed.

Organizations should avoid **orphaned third-party accounts**.

Vendor access should be linked to:

- Named individuals
- Approved roles
- Contractual need
- Expiration dates where possible

Shared vendor accounts reduce accountability and complicate investigations.

---

## 21. Third-Party Privileged Access

Privileged vendor access presents elevated risk.

Controls may include:

- PAM
- MFA
- Just-in-time access
- Session recording
- Approval workflows
- Command logging
- Restricted administrative networks
- Separate administrative credentials

The objective is to reduce the risk that compromise of a vendor account becomes compromise of the organization.

---

## 22. Vendor Data Access

Before sharing data with a vendor, determine:

- What data is required?
- Why is it required?
- How sensitive is it?
- Where is it stored?
- Who can access it?
- How long is it retained?
- Can the vendor use it for other purposes?
- Can subcontractors access it?
- How is it destroyed after termination?

A vendor should generally receive only the information necessary to perform the contracted service.

---

## 23. Data Minimization

**Data minimization** reduces risk by limiting the amount of sensitive information shared with third parties.

Example:

A vendor needs to verify customer age.

If the vendor only needs a yes/no eligibility result, sending the customer's complete identity profile may create unnecessary exposure.

The security objective is:

> **Provide the minimum information required for the business purpose.**

---

## 24. Vendor Network Connectivity

Vendor connections should be designed according to least privilege.

Controls may include:

- Segmentation
- Firewalls
- VPN
- Private connectivity
- API gateways
- Allowlisted source networks
- Restricted ports
- Network access control
- Monitoring

A vendor should not automatically receive unrestricted access to the corporate network simply because it needs access to one application.

---

## 25. API and Integration Security

Third-party integrations increasingly use APIs.

Security requirements can include:

- Strong authentication
- OAuth where appropriate
- Mutual TLS where appropriate
- API keys or tokens
- Least privilege
- Rate limiting
- Input validation
- Logging
- Monitoring
- Secret rotation
- Network restrictions

API credentials should be treated as sensitive security assets.

---

## 26. Supply-Chain Risk

Modern products may depend on many organizations.

For software:

**Organization → Application Vendor → Open-Source Libraries → Build Tools → Cloud/Infrastructure**

For hardware:

**Organization → Hardware Vendor → Manufacturer → Component Supplier → Raw Material Supplier**

A weakness or compromise anywhere in the chain can affect downstream organizations.

Supply-chain risk management attempts to increase visibility and reduce this dependency risk.

---

## 27. Software Supply-Chain Security

Software suppliers may use:

- Open-source libraries
- Commercial libraries
- Third-party APIs
- Build systems
- CI/CD pipelines
- Package repositories
- Container images

Organizations should consider:

- Software composition analysis
- Dependency inventories
- SBOMs
- Code signing
- Package integrity
- Trusted repositories
- Vulnerability monitoring
- Secure build pipelines

A vulnerable dependency can become an indirect vulnerability in the organization's application.

---

## 28. Hardware Supply-Chain Risk

Hardware risks may include:

- Counterfeit components
- Tampered equipment
- Malicious firmware
- Compromised manufacturing
- Unauthorized modifications
- Insecure default configurations

Controls may include:

- Supplier assessment
- Procurement controls
- Trusted sourcing
- Hardware authenticity verification
- Firmware validation
- Secure boot
- Chain-of-custody procedures

---

## 29. Software Bill of Materials (SBOM)

An **SBOM** provides information about software components and dependencies.

It can help organizations determine:

- Which libraries are present?
- Which versions are used?
- Which applications depend on a vulnerable component?
- Which products are affected by a newly discovered vulnerability?

Example:

A critical vulnerability is discovered in a popular open-source library.

Without dependency visibility, the organization may not know whether its applications use the affected component.

An SBOM can accelerate impact analysis.

---

## 30. Vendor Vulnerability Management

Organizations should understand how vendors manage vulnerabilities.

Questions can include:

- How are vulnerabilities discovered?
- How quickly are critical vulnerabilities remediated?
- How are customers notified?
- How are patches distributed?
- How are emergency vulnerabilities handled?
- Are security advisories published?
- Is penetration testing performed?
- How are third-party dependencies monitored?

For critical vendors, vulnerability-management performance may become part of ongoing vendor monitoring.

---

## 31. Vendor Incident Response

Vendor incidents can affect the organization even when the organization's infrastructure is not directly compromised.

Vendor contracts should define:

- Incident notification
- Notification timeframes
- Points of contact
- Evidence sharing
- Investigation cooperation
- Containment responsibilities
- Regulatory coordination
- Customer communication
- Recovery expectations

A vendor's incident may become the organization's incident.

---

## 32. Fourth-Party Incident Example

Consider:

**Company → SaaS Provider → Cloud Provider**

If the cloud provider experiences a major outage, the SaaS provider may become unavailable.

The original company may have no direct contractual relationship with the cloud provider.

This is why critical vendors should be evaluated for important downstream dependencies.

Questions include:

- Which subcontractors are critical?
- Where is data hosted?
- What cloud providers are used?
- What happens if a subcontractor fails?
- Can the vendor switch providers?

---

## 33. Business Continuity and Vendor Risk

Critical vendors should be evaluated for continuity capabilities.

Questions include:

- What is the vendor's RTO?
- What is its RPO?
- Does it have redundant facilities?
- Does it have backup suppliers?
- How does it handle regional outages?
- How does it handle workforce disruption?
- How often does it test its recovery plan?

The organization's RTO may be shorter than the vendor's capability.

That creates a continuity risk.

---

## 34. Vendor Risk and Concentration Risk

**Concentration risk** occurs when too much organizational dependence is placed on one provider, platform, region, or supplier.

Example:

A company uses one cloud provider for:

- Applications
- Identity
- Backups
- Monitoring
- Disaster recovery

If that provider experiences a major disruption, multiple business capabilities may fail simultaneously.

Possible strategies include:

- Multi-provider architecture
- Alternate suppliers
- Geographic diversity
- Independent backups
- Exit plans

The appropriate approach depends on cost and business requirements.

---

## 35. Vendor Lock-In

**Vendor lock-in** occurs when switching away from a provider becomes difficult or expensive.

Contributing factors include:

- Proprietary APIs
- Proprietary data formats
- Large migration effort
- Specialized services
- Contractual restrictions
- Lack of alternative suppliers

Lock-in is not automatically a security failure, but it can create:

- Availability risk
- Continuity risk
- Cost risk
- Strategic dependency

Organizations should consider portability and exit requirements for critical services.

---

## 36. Vendor Monitoring

Vendor risk management continues after onboarding.

Monitoring may include:

- Security incidents
- Service availability
- Vulnerabilities
- Audit findings
- Certification status
- Contract compliance
- Access reviews
- Changes in ownership
- Changes in subcontractors
- Changes in architecture
- Regulatory changes
- Financial stability
- Threat intelligence

Monitoring frequency should reflect vendor criticality and risk.

---

## 37. Continuous Monitoring vs Periodic Assessment

A vendor questionnaire performed once per year may not identify important changes that occur the next day.

Continuous or event-driven monitoring can identify:

- New vulnerabilities
- Breaches
- Ownership changes
- New subcontractors
- Service changes
- Expired certifications
- Major outages

Periodic formal reassessment still has value, but it should not be the only source of vendor risk information.

---

## 38. Vendor Security Ratings

External security ratings can provide additional information about a vendor's observable security posture.

However, they should not automatically replace direct due diligence.

A rating may:

- Be based on limited external observations
- Miss internal controls
- Contain stale information
- Not reflect the exact service being purchased

Use external ratings as one input among multiple evidence sources.

---

## 39. Contractual Audit Rights

For higher-risk vendors, contracts may provide audit rights.

These can allow the organization to:

- Review security evidence
- Request assessment results
- Examine compliance documentation
- Verify contractual controls

The organization should balance audit rights with practical constraints and the vendor's security requirements.

For large providers, customers may receive independent assurance reports rather than performing unrestricted onsite audits.

---

## 40. Vendor Risk Acceptance

Sometimes a vendor presents risk that cannot immediately be eliminated.

The organization may:

- Mitigate
- Transfer
- Avoid
- Accept

If risk is accepted, the decision should be:

- Explicit
- Documented
- Approved by the appropriate authority
- Time-bounded where appropriate
- Revisited when circumstances change

A procurement team should not silently accept major security risk simply because the business wants the vendor quickly.

---

## 41. Compensating Controls

If a vendor cannot satisfy a preferred security requirement, compensating controls may reduce the risk.

Example:

A vendor cannot provide a specific network-control capability.

The organization may:

- Restrict vendor access through a dedicated gateway
- Limit access to specific systems
- Require stronger authentication
- Monitor sessions
- Use additional segmentation

The compensating control should address the relevant risk rather than merely checking a compliance box.

---

## 42. Vendor Offboarding

Offboarding is one of the most important and frequently neglected stages.

When a contract ends, the organization should address:

- Account removal
- Credential revocation
- API-token revocation
- VPN termination
- Network-access removal
- Asset return
- Certificate revocation where applicable
- Data return
- Data destruction
- Backup copies
- Subcontractor access
- Documentation
- Contract closure

The objective is:

> **The vendor should no longer have unnecessary access after the business relationship ends.**

---

## 43. Data Destruction at Offboarding

Simply asking a vendor to "delete the data" may be insufficient.

The organization may need to define:

- Which data must be returned
- Which data must be deleted
- Retention requirements
- Backup retention
- Destruction methods
- Destruction evidence
- Legal holds
- Regulatory requirements

For sensitive information, contractual requirements may include a certificate or other evidence of destruction.

---

## 44. Vendor Asset Recovery

Offboarding may require recovery of:

- Laptops
- Tokens
- Smart cards
- Badges
- Mobile devices
- Hardware appliances
- Cryptographic keys
- Documentation

Asset recovery should be coordinated with access revocation.

For example:

> Recovering a vendor laptop without disabling its credentials is incomplete offboarding.

---

## 45. Vendor Offboarding Verification

Offboarding should be verified rather than assumed.

Verification may include:

- IAM account review
- VPN review
- Firewall rule review
- API-token inventory
- Certificate inventory
- Asset inventory
- Cloud account review
- Data-deletion confirmation

This is particularly important when a vendor had privileged or persistent access.

---

## 46. Vendor Risk Documentation

Vendor records should document:

- Assessment results
- Risk rating
- Business owner
- Security requirements
- Contract status
- Exceptions
- Accepted risks
- Audit evidence
- Incidents
- Remediation items
- Review dates
- Offboarding status

Documentation provides evidence of governance and supports future risk decisions.

---

## 47. Common Third-Party Risk Failures

### Failure 1: Assuming outsourcing removes responsibility

A vendor is responsible for part of the service, but the organization still has risk and governance responsibilities.

**Better approach:** define responsibilities explicitly.

### Failure 2: One-time assessment

The vendor passes an initial questionnaire and is never reviewed again.

**Better approach:** continuously monitor and periodically reassess.

### Failure 3: Excessive vendor access

A vendor receives broad network access for convenience.

**Better approach:** least privilege, segmentation, MFA, and monitored access.

### Failure 4: Ignoring subcontractors

The vendor relies on another provider that was never considered.

**Better approach:** understand material fourth-party dependencies.

### Failure 5: Weak contracts

Security expectations are discussed verbally but not documented.

**Better approach:** incorporate appropriate security requirements into contracts.

### Failure 6: Treating certifications as proof of zero risk

A vendor has a certification, so the organization stops evaluating risk.

**Better approach:** verify scope, relevance, exceptions, and complementary controls.

### Failure 7: No secure offboarding

Vendor accounts remain active after the contract ends.

**Better approach:** make access revocation and data handling part of the formal offboarding process.

### Failure 8: Ignoring concentration risk

The organization depends on one provider for multiple critical services.

**Better approach:** evaluate dependency and failure-domain risk.

---

## 48. Detailed Security+ Scenario 1 — Vendor with Sensitive Data

An organization wants to outsource customer-data processing to a vendor.

Before onboarding, the organization should evaluate:

- Data sensitivity
- Vendor security controls
- Access requirements
- Encryption
- Privacy practices
- Incident response
- Compliance requirements
- Data retention
- Subcontractors
- Business continuity

This is an example of **third-party due diligence and risk assessment**.

---

## 49. Detailed Security+ Scenario 2 — Vendor Privileged Access

A software vendor needs temporary administrative access to troubleshoot a production application.

A stronger design is:

**Approved request → MFA → time-limited privileged access → restricted network path → session monitoring → access removal**

This follows least privilege and reduces persistent third-party access.

---

## 50. Detailed Security+ Scenario 3 — Vendor Breach

A SaaS provider reports that attackers accessed a database containing organizational customer information.

The organization should:

1. Activate its vendor-incident process.
2. Determine what data was affected.
3. Coordinate with the vendor.
4. Involve legal/privacy teams as required.
5. Review contractual notification requirements.
6. Assess organizational impact.
7. Determine whether credentials or integrations must be rotated.
8. Monitor for downstream abuse.
9. Document the incident and lessons learned.

The fact that the breach occurred at the vendor does not eliminate the organization's need to respond.

---

## 51. Detailed Security+ Scenario 4 — Vendor Offboarding

A contractor's engagement ends.

The contractor previously had:

- VPN access
- Cloud account
- API token
- Administrative account
- Physical badge

A complete offboarding process should revoke all of these access paths and recover applicable assets.

Deleting only the VPN account is insufficient.

---

## 52. Detailed Security+ Scenario 5 — Vendor Questionnaire

A critical SaaS provider completes a security questionnaire but refuses to provide meaningful evidence about its controls.

The organization should not automatically conclude that the vendor is secure.

Possible actions include:

- Request independent assurance evidence
- Review contractual controls
- Perform additional assessment
- Add compensating controls
- Escalate the risk
- Require remediation
- Reconsider the vendor

The appropriate response depends on the risk and business requirements.

---

## 53. Detailed Security+ Scenario 6 — Fourth-Party Dependency

A critical SaaS provider hosts its platform entirely on another cloud provider.

The organization should consider:

- Cloud-region dependency
- Availability
- Data location
- Subcontractor controls
- Recovery capability
- Contractual obligations
- Exit strategy

This demonstrates why third-party risk can extend into the vendor's own supply chain.

---

## 54. Detailed Security+ Scenario 7 — Vendor Lock-In

An organization wants to use a proprietary platform that would make future migration extremely difficult.

Before committing, it should consider:

- Data portability
- API portability
- Migration cost
- Contract termination terms
- Export capabilities
- Alternate suppliers
- Business continuity impact

The issue is not necessarily "never use proprietary technology."

The issue is understanding the resulting **dependency and exit risk**.

---

## 55. Detailed Security+ Scenario 8 — Vendor Security Requirement Cannot Be Met

A vendor cannot support the organization's preferred network restriction.

The organization may evaluate compensating controls such as:

- Dedicated gateway
- Strong MFA
- Segmentation
- Restricted access
- Monitoring
- Time-limited sessions

If residual risk remains, the appropriate authority may need to formally accept or otherwise treat that risk.

---

## 56. Security+ Exam Distinctions

### Due Diligence vs Due Care

**Due diligence → investigate and understand risk**

**Due care → take reasonable action to address risk**

### Vendor Assessment vs Vendor Monitoring

**Assessment → evaluate controls and risk**

**Monitoring → observe changes and ongoing performance**

### Third Party vs Fourth Party

**Third party → direct vendor**

**Fourth party → vendor's own provider/dependency**

### SLA vs Security Requirement

**SLA → defines service performance**

Security clauses may separately define:

- Security controls
- Incident notification
- Audit rights
- Data handling
- Access requirements

### Vendor Risk vs Vendor Compliance

A vendor can satisfy a contractual or compliance requirement while still presenting other business or security risks.

### Offboarding vs Contract Termination

Ending a contract is not enough.

Technical and data-access removal must also occur.

### Questionnaire vs Assurance Evidence

A questionnaire provides self-reported information.

Independent evidence can provide stronger assurance depending on scope and relevance.

---

## 57. Security+ Decision Framework

When a Security+ question presents a vendor scenario, reason through it in this order.

### Step 1 — Identify the Dependency

What does the organization receive from the vendor?

### Step 2 — Identify the Exposure

What can the vendor access?

- Data
- Network
- Applications
- Credentials
- Facilities
- APIs

### Step 3 — Determine Criticality

How badly would the organization be affected if the vendor failed or were compromised?

### Step 4 — Perform Due Diligence

What evidence is required to understand the vendor's controls and risks?

### Step 5 — Define Security Requirements

Consider:

- IAM
- MFA
- Encryption
- Logging
- Vulnerability management
- Incident response
- Privacy
- Continuity

### Step 6 — Contract the Requirements

Document appropriate requirements, responsibilities, SLAs, notification, audit, data handling, and exit terms.

### Step 7 — Control Access

Use:

- Least privilege
- Segmentation
- MFA
- Temporary access
- Monitoring

### Step 8 — Monitor

Watch for:

- Incidents
- Vulnerabilities
- Ownership changes
- Subcontractors
- Compliance changes
- Service degradation

### Step 9 — Reassess

Repeat assessment based on risk and significant changes.

### Step 10 — Offboard Securely

Revoke access, recover assets, return/delete data, and verify that access paths are closed.

---

## 58. Complete Third-Party Risk Workflow

**Identify vendor**
↓
**Determine service and dependency**
↓
**Classify data and access**
↓
**Determine vendor criticality**
↓
**Perform due diligence**
↓
**Assess risk**
↓
**Define security requirements**
↓
**Contract requirements**
↓
**Onboard securely**
↓
**Provision least-privilege access**
↓
**Monitor continuously**
↓
**Reassess periodically and after material changes**
↓
**Remediate, mitigate, transfer, or accept residual risk**
↓
**Offboard securely**
↓
**Verify access and data removal**

This lifecycle ensures vendor security does not stop when the contract is signed.

---

## 59. Practical Vendor Risk Example

Consider an organization that wants to deploy a cloud-based HR platform.

### Step 1 — Identify Data

The platform will process:

- Employee identity information
- Payroll information
- Employment records

This creates significant data sensitivity.

### Step 2 — Identify Access

The provider will have access to sensitive organizational data and administrative interfaces.

### Step 3 — Determine Criticality

Payroll and HR operations may be business-critical.

### Step 4 — Due Diligence

The organization evaluates:

- IAM
- MFA
- Encryption
- Logging
- Vulnerability management
- Incident response
- Privacy
- Continuity
- Subcontractors

### Step 5 — Contract

The agreement defines:

- Security responsibilities
- Incident notification
- Data handling
- Retention
- Data destruction
- Availability requirements
- Audit/assurance requirements
- Exit procedures

### Step 6 — Onboarding

Vendor access is restricted and monitored.

### Step 7 — Continuous Monitoring

The organization tracks:

- Security incidents
- Availability
- Assurance evidence
- Subcontractor changes
- Vulnerabilities

### Step 8 — Offboarding

When the organization changes providers:

- Accounts are revoked
- API credentials are removed
- Data is migrated
- Data deletion is verified
- Vendor connectivity is terminated

This demonstrates the complete third-party risk lifecycle.

---

## 60. Final Mental Model

Remember:

**Vendor**
→ What service are we outsourcing?

**Data**
→ What information does the vendor receive?

**Access**
→ What systems can the vendor reach?

**Criticality**
→ What happens if the vendor fails?

**Due Diligence**
→ What risks and controls exist?

**Due Care**
→ What reasonable actions are taken to address those risks?

**Contract**
→ What responsibilities and requirements are enforceable?

**Least Privilege**
→ What access does the vendor actually need?

**Monitoring**
→ What is changing after onboarding?

**Fourth-Party Risk**
→ Who does the vendor depend on?

**Continuity**
→ What happens if the vendor becomes unavailable?

**Offboarding**
→ How do we remove access, recover assets, and handle data?

The central Security+ principle is:

> **Third-party risk is an extension of organizational risk. Outsourcing a service does not eliminate the security, privacy, availability, or compliance responsibilities associated with that dependency.**

## Key Takeaways

- Third parties can introduce security, privacy, availability, compliance, financial, and reputational risks.
- Vendor risk management should follow a complete lifecycle from **identification through secure offboarding**.
- **Due diligence** means investigating and understanding risk.
- **Due care** means taking reasonable action to address known risk.
- Vendor assessment should consider data, access, security controls, incident response, continuity, privacy, compliance, and subcontractors.
- Vendor criticality should influence assessment depth and monitoring frequency.
- Contracts should define appropriate security requirements, responsibilities, notification, audit, data handling, and exit conditions.
- An SLA defines service expectations but does not automatically define every security requirement.
- Third-party access should use **least privilege, MFA, monitoring, segmentation, and time-limited access where practical**.
- Vendor accounts and credentials must be included in identity lifecycle management.
- Sensitive data shared with vendors should follow **data minimization** principles.
- Supply-chain risk includes software, hardware, subcontractors, and other dependencies.
- **SBOMs** can improve software dependency visibility.
- Fourth-party dependencies can create hidden availability and security risks.
- Vendor risk must be monitored throughout the relationship rather than assessed only during procurement.
- Security certifications and assurance reports are useful evidence but must be evaluated for scope, relevance, and exceptions.
- Vendor incidents may require organizational incident-response, legal, privacy, and regulatory actions.
- Critical vendors should be evaluated for business continuity, recovery capability, and concentration risk.
- Vendor lock-in can create strategic, continuity, and migration risks.
- Risk acceptance should be explicit, documented, and approved by the appropriate authority.
- Secure offboarding includes **account removal, credential/token revocation, connectivity termination, asset recovery, and data return/destruction**.
- The goal is not to eliminate every vendor relationship; it is to understand and manage the risks created by each dependency.
