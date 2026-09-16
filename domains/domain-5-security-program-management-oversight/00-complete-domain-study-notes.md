# Domain 5 — Complete Study Notes: Security Program Management and Oversight

Domain 5 moves from technical security into the organizational systems that make security sustainable. Security programs require governance, policies, risk decisions, continuity planning, compliance, privacy, third-party oversight, awareness, documentation, and measurable outcomes.

A useful model is:

`Governance → Policy → Risk → Control → Measurement → Assurance → Improvement`

## 1. Governance and Security Policies

Security governance establishes authority, accountability, direction, and oversight. It connects organizational objectives with security requirements and determines who can make security decisions.

A **policy** expresses management intent and establishes mandatory expectations. A **standard** defines specific mandatory requirements that support a policy. A **procedure** explains how a task is performed. A **guideline** provides recommended practices and flexibility.

The hierarchy can be remembered as:

`Policy → Standard → Procedure → Guideline`

Policies should be approved, communicated, reviewed, updated, and retired when necessary. Exceptions should be formally documented, approved, time-limited where appropriate, and accompanied by compensating controls when possible.

## 2. Risk Management

Risk management determines what could go wrong, how likely it is, what the consequences could be, and what the organization should do about it.

A simplified model is:

`Risk ≈ Likelihood × Impact`

**Inherent risk** exists before controls are applied. **Residual risk** remains after controls are applied.

Risk responses commonly include:

- **Mitigate:** reduce likelihood or impact.
- **Transfer:** shift some financial or contractual consequences to another party, such as through insurance or a contract.
- **Avoid:** stop the activity creating unacceptable risk.
- **Accept:** consciously retain the risk within approved tolerance.

### Quantitative Risk Concepts

**Single Loss Expectancy (SLE)** estimates loss from one occurrence.

`SLE = Asset Value × Exposure Factor`

**Annualized Rate of Occurrence (ARO)** estimates expected frequency per year.

`ALE = SLE × ARO`

These calculations help compare potential losses and security investments, although real-world risk decisions also require qualitative context.

## 3. Business Impact Analysis and Continuity

A **Business Impact Analysis (BIA)** identifies critical business functions and determines the consequences of their disruption.

A BIA asks which processes are most important, what dependencies they have, how quickly they must be restored, and what level of data loss is acceptable.

**RTO** is the target time for restoring a service. **RPO** is the acceptable amount of data loss measured in time.

For example, an RPO of 15 minutes means the organization is designing recovery so that it can tolerate approximately 15 minutes of data loss under the defined scenario.

Business continuity focuses on maintaining essential operations during disruption. It is broader than simply restoring servers.

## 4. Disaster Recovery and Incident Response Planning

Disaster recovery focuses on restoring technology and services after a disruptive event. Incident response focuses on handling security incidents.

A disaster recovery plan can define recovery priorities, dependencies, recovery sites, backup requirements, communication paths, responsibilities, and restoration procedures.

Incident response planning establishes preparation, detection, analysis, containment, eradication, recovery, and lessons-learned activities.

Plans must be tested. Tabletop exercises test decision-making and coordination. Technical recovery exercises test whether systems and procedures actually work.

## 5. Security Awareness and Training

Users are part of the security environment. Awareness programs teach people how to recognize and report suspicious activity and how organizational policies apply to their behavior.

Training should address phishing, password security, MFA, data handling, removable media, physical security, reporting procedures, social engineering, and role-specific responsibilities.

Security awareness should be measurable. Organizations can examine reporting rates, training completion, simulation results, repeat failures, and incident trends.

The goal is not simply to punish mistakes. A mature program uses observed behavior to improve processes and reduce risk.

## 6. Third-Party and Vendor Risk Management

Organizations often depend on cloud providers, software vendors, managed service providers, contractors, and other third parties. These relationships create supply-chain and data-security risks.

Third-party risk management should evaluate a provider before engagement and continue throughout the relationship.

Important considerations include security capabilities, data handling, access requirements, incident notification, subcontractors, geographic processing, business continuity, vulnerability management, audit rights, termination requirements, and secure data disposal.

Contracts can establish security requirements and responsibilities. Security reviews and assessments provide additional assurance, but third-party risk cannot be eliminated simply by signing a contract.

## 7. Compliance, Auditing, and Assurance

**Compliance** means meeting applicable laws, regulations, contractual requirements, standards, or organizational requirements.

An **audit** systematically evaluates whether defined requirements are being met. Auditors examine evidence rather than relying only on statements of compliance.

Evidence can include policies, configuration records, logs, access reviews, vulnerability reports, training records, change tickets, and incident documentation.

A control can exist on paper but still be ineffective if it is not implemented consistently.

## 8. Privacy and Data Governance

Privacy concerns how personal information is collected, used, shared, stored, retained, and disposed of.

Data governance establishes ownership, classification, handling requirements, retention, access, quality, and lifecycle management.

Common classifications may include public, internal, confidential, and restricted, although organizations define their own classification schemes.

Sensitive data should receive controls appropriate to its classification. Security mechanisms may include encryption, access control, tokenization, masking, DLP, retention controls, and secure disposal.

Privacy requirements differ by jurisdiction and context. Security professionals should identify which laws, regulations, contracts, and organizational requirements actually apply rather than assuming one privacy framework applies everywhere.

## 9. Security Documentation and Records

Documentation allows organizations to communicate, operate, audit, and improve security consistently.

Important documentation can include policies, standards, procedures, system inventories, network diagrams, data-flow diagrams, risk registers, incident records, business continuity plans, disaster recovery plans, vendor assessments, and audit evidence.

Documentation should have owners, version control, approval processes, retention requirements, and appropriate access restrictions.

A document containing sensitive architecture or recovery information can itself become a security asset requiring protection.

## 10. Security Metrics and Reporting

Security metrics convert operational activity into information that decision-makers can use.

A useful metric should have a clear definition, reliable data source, appropriate measurement period, and decision-making purpose.

Examples include mean time to detect, mean time to respond, vulnerability remediation time, patch compliance, phishing reporting rates, MFA coverage, privileged account review completion, and incident recurrence.

A metric should not be selected merely because it is easy to count. A large number of blocked attacks, for example, does not automatically prove that security improved.

Reports should be tailored to the audience. Technical teams may need detailed event information, while executives may need risk trends, business impact, major control gaps, and resource requirements.

## 11. Security Program Management

A security program coordinates people, processes, technology, governance, and resources over time.

Program management includes defining objectives, assigning ownership, budgeting, managing risk, tracking initiatives, measuring control effectiveness, reviewing incidents, coordinating audits, and improving security capabilities.

Security maturity should improve through feedback. Incidents, audit findings, vulnerability trends, exercises, and operational metrics should influence future priorities.

## Security+ Governance Scenario Method

For a program-management scenario, ask:

1. What organizational requirement exists?
2. Who owns the risk or decision?
3. What policy, standard, or procedure applies?
4. What is the business impact?
5. What risk treatment is appropriate?
6. What evidence demonstrates that the control works?
7. What needs to be measured?
8. How should the organization improve afterward?

## Key Takeaways

Domain 5 is about making security an organizational discipline rather than a collection of technical tools. Governance establishes direction, risk management prioritizes decisions, continuity protects business operations, compliance and auditing provide assurance, privacy and data governance protect information, third-party management controls external dependencies, and metrics show whether the security program is achieving its objectives.
