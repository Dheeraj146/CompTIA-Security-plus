# Domain 5 — Module 2: Risk Management

Risk management is the structured process an organization uses to identify uncertainty, analyze its potential effect on business objectives, decide how that risk should be treated, and continuously monitor the result.

Security does not operate in a world where every risk can be eliminated. Organizations have limited money, people, time, technology, and operational capacity. Risk management therefore helps leadership determine **which risks require attention, what treatment is appropriate, who owns the decision, and what residual risk the organization is willing to accept**.

A useful Security+ mental model is:

**Asset → Threat → Vulnerability → Likelihood → Impact → Risk → Response → Residual Risk → Monitoring**

---

# 1. What Is Risk?

Risk is the possibility that an event or condition will negatively affect an organization's objectives.

In cybersecurity, risk may involve:

- Confidentiality loss.
- Integrity loss.
- Availability loss.
- Financial loss.
- Legal or regulatory consequences.
- Reputational damage.
- Operational disruption.
- Safety consequences.
- Loss of customer trust.

Risk is not the same thing as a threat or vulnerability.

A **threat** is a potential cause of harm.

A **vulnerability** is a weakness that can be exploited or otherwise contribute to harm.

**Risk** considers the possibility and consequences of that threat exploiting or interacting with weaknesses in a particular environment.

---

# 2. Threat vs Vulnerability vs Risk

Consider an Internet-facing web server.

```text
Threat:
Attacker
   ↓
Vulnerability:
Unpatched application
   ↓
Exploitation
   ↓
Potential Impact:
Unauthorized access
   ↓
Risk
```

The attacker is the **threat source**.

The unpatched application is the **vulnerability**.

The possibility and consequences of exploitation constitute the relevant **risk**.

A vulnerability therefore does not automatically mean that a damaging incident will occur.

---

# 3. Risk Management Objectives

Risk management attempts to support business objectives by keeping risk within an acceptable range.

It helps organizations:

- Prioritize security investments.
- Identify important exposures.
- Decide which vulnerabilities require remediation first.
- Evaluate security controls.
- Support business decisions.
- Allocate resources.
- Manage third-party risk.
- Prepare for potential incidents.
- Communicate security concerns to leadership.

The objective is not necessarily **zero risk**.

The practical objective is to make risk decisions deliberately and keep unacceptable risks under control.

---

# 4. Risk Management Lifecycle

A typical lifecycle is:

```text
Identify Risk
     ↓
Analyze Risk
     ↓
Evaluate / Prioritize
     ↓
Select Response
     ↓
Implement Treatment
     ↓
Monitor
     ↓
Communicate / Report
     ↓
Reassess
```

Risk management is continuous because assets, threats, vulnerabilities, controls, regulations, and business requirements change.

---

# 5. Risk Identification

Risk identification determines what could negatively affect organizational objectives.

Organizations may examine:

- Critical assets.
- Threat actors.
- Vulnerabilities.
- Existing controls.
- Business processes.
- Dependencies.
- Third parties.
- Cloud services.
- Physical facilities.
- People.
- Data.
- Applications.
- Network architecture.
- Historical incidents.

Sources of risk information can include:

- Vulnerability assessments.
- Penetration tests.
- Security incidents.
- Audits.
- Threat intelligence.
- Business impact analysis.
- Architecture reviews.
- Vendor assessments.
- Security monitoring.
- Employee reports.

---

# 6. Asset Criticality

Risk analysis must consider what is being protected.

A vulnerability on a test workstation and the same vulnerability on a core payment-processing server may have very different consequences.

Asset-related factors include:

- Business criticality.
- Data sensitivity.
- Availability requirements.
- Regulatory importance.
- Financial value.
- Dependencies.
- Exposure to external networks.

Therefore, vulnerability severity alone does not completely determine organizational risk.

---

# 7. Threat Identification

Threats can originate from many sources:

- Cybercriminals.
- Nation-state actors.
- Insiders.
- Hacktivists.
- Competitors.
- Unintentional users.
- Natural events.
- Hardware failures.
- Software failures.
- Supply-chain compromise.

Risk analysis should consider threats relevant to the organization's assets and environment rather than treating every theoretical threat equally.

---

# 8. Vulnerability Identification

Vulnerabilities may include:

- Missing patches.
- Weak authentication.
- Excessive permissions.
- Misconfiguration.
- Insecure protocols.
- Exposed services.
- Application flaws.
- Weak encryption.
- Unsupported software.
- Poor physical security.
- Inadequate backup controls.
- Human-process weaknesses.

Vulnerability scanners, configuration assessments, penetration tests, audits, code analysis, and operational monitoring can identify vulnerabilities.

---

# 9. Likelihood

**Likelihood** describes how probable a risk event is within the relevant context and time period.

Factors affecting likelihood can include:

- Threat capability.
- Threat motivation.
- Exposure.
- Exploit availability.
- Vulnerability severity.
- Existing controls.
- Attack complexity.
- Historical frequency.
- Accessibility of the target.

A vulnerability exposed directly to the Internet may have a different likelihood than an identical vulnerability on a strongly isolated internal system.

---

# 10. Impact

**Impact** describes the consequences if the risk event occurs.

Potential impacts include:

- Financial loss.
- Data disclosure.
- Data corruption.
- Service interruption.
- Safety consequences.
- Regulatory penalties.
- Contractual consequences.
- Reputation damage.
- Customer impact.

Impact should be evaluated in the context of the organization's objectives.

---

# 11. Likelihood vs Impact

These concepts are frequently tested together.

### Likelihood

> How probable is the event?

### Impact

> How severe would the consequences be if it occurred?

A risk can be:

```text
Low Likelihood + High Impact
```

or:

```text
High Likelihood + Low Impact
```

Both may require attention, but the appropriate response can differ.

---

# 12. Qualitative Risk Analysis

Qualitative risk analysis uses descriptive categories rather than primarily relying on monetary calculations.

Examples include:

- Low.
- Moderate.
- High.
- Critical.

A risk matrix may combine likelihood and impact:

| Likelihood | Impact | Typical Interpretation |
|---|---|---|
| Low | Low | Lower priority |
| Low | High | Significant consequence if realized |
| High | Low | Frequent but limited consequence |
| High | High | Significant priority |

The exact matrix and terminology vary by organization.

Qualitative analysis is useful when precise numerical data is unavailable or when a relative prioritization is sufficient.

---

# 13. Risk Matrix

A common conceptual model is:

**Risk Level ≈ Likelihood × Impact**

For example, an organization may assign numerical categories such as:

```text
Likelihood: 1–5
Impact:     1–5
```

and combine them into a matrix.

The matrix is a decision-support mechanism, not a universal mathematical law. Organizations should define how their scoring model works.

---

# 14. Quantitative Risk Analysis

Quantitative analysis attempts to express risk using numerical values, often financial values.

Common Security+ concepts include:

- Asset Value (AV).
- Exposure Factor (EF).
- Single Loss Expectancy (SLE).
- Annualized Rate of Occurrence (ARO).
- Annualized Loss Expectancy (ALE).

These formulas are commonly used in Security+ questions.

---

# 15. Asset Value (AV)

**Asset Value** represents the value assigned to the asset being analyzed.

For example, suppose an organization determines that a critical server represents an asset value of:

```text
AV = $100,000
```

This value may incorporate more than purchase price. Depending on the organization's methodology, it can reflect business value, replacement cost, data value, operational impact, or other relevant considerations.

---

# 16. Exposure Factor (EF)

**Exposure Factor** represents the percentage of asset value expected to be lost from a single occurrence of a particular risk.

Suppose:

```text
AV = $100,000
EF = 40%
```

Then:

```text
SLE = AV × EF
SLE = $100,000 × 0.40
SLE = $40,000
```

---

# 17. Single Loss Expectancy (SLE)

**SLE** represents the expected loss from one occurrence of a risk event.

Formula:

**SLE = AV × EF**

Example:

```text
Asset Value = $200,000
Exposure Factor = 25%

SLE = $200,000 × 0.25
SLE = $50,000
```

The SLE is associated with **one occurrence**.

---

# 18. Annualized Rate of Occurrence (ARO)

**ARO** estimates how many times a risk event is expected to occur per year.

For example:

```text
Expected events per year = 2
ARO = 2
```

If an event is expected once every two years:

```text
ARO = 0.5
```

ARO is an estimate, so its usefulness depends on the quality of the underlying assumptions.

---

# 19. Annualized Loss Expectancy (ALE)

**ALE** estimates the expected annual loss associated with a risk.

Formula:

**ALE = SLE × ARO**

Example:

```text
AV = $200,000
EF = 25%

SLE = $50,000

ARO = 2

ALE = $50,000 × 2
ALE = $100,000 per year
```

The sequence to remember is:

```text
AV × EF = SLE
SLE × ARO = ALE
```

---

# 20. Quantitative Risk Example

Suppose a company estimates:

```text
Asset Value (AV) = $500,000
Exposure Factor (EF) = 20%
Annualized Rate of Occurrence (ARO) = 0.5
```

First calculate SLE:

```text
SLE = AV × EF
SLE = $500,000 × 0.20
SLE = $100,000
```

Then calculate ALE:

```text
ALE = SLE × ARO
ALE = $100,000 × 0.5
ALE = $50,000
```

Therefore, the estimated annualized loss is **$50,000** under those assumptions.

---

# 21. Limitations of Quantitative Analysis

Numerical risk calculations can look precise while still depending on uncertain assumptions.

For example, estimating that a ransomware event will occur exactly 0.4 times per year does not mean the organization can predict the future with that precision.

Limitations can include:

- Incomplete historical data.
- Changing threats.
- Difficult-to-measure impacts.
- Uncertain probabilities.
- Changing asset values.
- Interdependent risks.

Quantitative models should therefore support decisions rather than create false certainty.

---

# 22. Risk Appetite

**Risk appetite** describes the broad amount and type of risk an organization is willing to pursue or retain in achieving its objectives.

Risk appetite is generally established at an organizational or leadership level.

For example, an organization may have a low appetite for risks involving:

- Regulatory violations.
- Exposure of highly sensitive customer data.
- Safety-critical systems.

Risk appetite provides strategic context for individual risk decisions.

---

# 23. Risk Tolerance

**Risk tolerance** describes the acceptable level of variation around objectives or the specific amount of risk the organization is willing to tolerate in a given context.

A simple conceptual relationship is:

```text
Risk Appetite
      ↓
Overall organizational direction
      ↓
Risk Tolerance
      ↓
Specific acceptable boundaries
```

Terminology and governance practices can vary, but Security+ questions generally expect you to distinguish broad organizational appetite from more specific tolerances or thresholds.

---

# 24. Risk Threshold

A risk threshold is a defined boundary that may trigger additional action.

For example:

> A risk score above a defined threshold must be escalated to senior management.

Thresholds can help standardize escalation and treatment decisions.

---

# 25. Inherent Risk

**Inherent risk** is the level of risk before considering the effect of security controls or other risk treatments.

Example:

```text
Internet-facing application
       ↓
Known vulnerability
       ↓
Inherent Risk
```

The organization then evaluates controls such as WAF protection, patching, segmentation, monitoring, and secure configuration.

---

# 26. Residual Risk

**Residual risk** is the risk remaining after controls have been implemented.

```text
Inherent Risk
      ↓
Security Controls
      ↓
Residual Risk
```

Controls rarely eliminate all risk.

For example, MFA can reduce account-compromise risk, but it may not eliminate phishing, token theft, social engineering, or other attack paths.

---

# 27. Risk Reduction

Risk reduction occurs when controls decrease the likelihood and/or impact of a risk.

Examples include:

- Patching.
- MFA.
- Network segmentation.
- Encryption.
- Backups.
- EDR.
- Access restrictions.
- Security awareness.
- Redundancy.

Risk reduction is commonly associated with **mitigation**.

---

# 28. Risk Response Options

The four major risk responses are:

1. **Avoid**
2. **Mitigate**
3. **Transfer**
4. **Accept**

Security+ questions frequently ask you to identify which response is being described.

---

# 29. Risk Avoidance

**Avoidance** means eliminating the activity, condition, or exposure that creates the risk.

Example:

An organization determines that a high-risk legacy Internet-facing service is not necessary and permanently removes it.

The risky activity is eliminated rather than controlled.

Avoidance can have business consequences because the organization gives up the associated activity or capability.

---

# 30. Risk Mitigation

**Mitigation** reduces the likelihood or impact of a risk through controls.

Example:

A vulnerable application must remain available, so the organization:

- Patches it.
- Places it behind a WAF.
- Segments it.
- Restricts administrative access.
- Monitors it.

The risk has not necessarily disappeared; it has been reduced.

---

# 31. Risk Transfer

**Transfer** shifts some financial or contractual consequences of a risk to another party.

Examples include:

- Cyber insurance.
- Outsourcing under contractual arrangements.
- Certain contractual indemnification provisions.

Transfer does **not** necessarily eliminate the underlying security risk.

For example, purchasing cyber insurance does not prevent an attacker from compromising a system.

It may shift some financial consequences.

---

# 32. Risk Acceptance

**Acceptance** means knowingly retaining the risk after appropriate evaluation and authorization.

Acceptance should be:

- Deliberate.
- Documented.
- Owned by an authorized person.
- Based on an understanding of potential impact.
- Reviewed when circumstances change.

Risk acceptance is not the same as ignoring a vulnerability.

---

# 33. Risk Treatment Example

Suppose a legacy server cannot be patched immediately.

Possible responses include:

### Avoid

Retire the server and eliminate the risky service.

### Mitigate

Segment it, restrict access, monitor it, and apply compensating controls.

### Transfer

Use contractual or insurance mechanisms for some consequences where appropriate.

### Accept

An authorized risk owner formally accepts the residual risk for a defined period.

The correct answer depends on the scenario.

---

# 34. Risk Register

A **risk register** is a structured record of identified risks and their management status.

Typical fields include:

- Risk identifier.
- Risk description.
- Affected asset/process.
- Threat.
- Vulnerability.
- Likelihood.
- Impact.
- Risk level.
- Risk owner.
- Existing controls.
- Treatment decision.
- Residual risk.
- Due date.
- Status.
- Exception information.
- Review date.

The risk register provides centralized visibility and accountability.

---

# 35. Risk Owner

The **risk owner** is the person or organizational role accountable for managing a particular risk and deciding how it should be treated within their authority.

The risk owner may not be the same person who implements the technical control.

For example:

```text
Risk Owner
    ↓
Makes / approves risk decision

Security Team
    ↓
Implements controls

System Owner
    ↓
Manages affected system
```

The exact division of responsibilities varies by organization.

---

# 36. Risk Treatment Plan

A risk treatment plan defines how a risk will be addressed.

It may include:

- Selected response.
- Required controls.
- Responsible owner.
- Implementation deadline.
- Resources.
- Milestones.
- Expected residual risk.
- Validation requirements.

This converts a risk decision into actionable work.

---

# 37. Risk Communication

Risk management requires communicating information to appropriate stakeholders.

Technical teams may need details such as:

- Vulnerability.
- Affected systems.
- Attack paths.
- Required controls.

Executives may need:

- Business impact.
- Financial exposure.
- Risk trends.
- Residual risk.
- Required decisions.

Effective communication translates technical risk into business-relevant information.

---

# 38. Risk Assessment vs Vulnerability Assessment

### Risk Assessment

Evaluates broader uncertainty, including likelihood, impact, threats, vulnerabilities, assets, controls, and business consequences.

### Vulnerability Assessment

Primarily identifies weaknesses that could be exploited.

A vulnerability scan may identify a critical vulnerability, but risk assessment determines how that vulnerability affects the organization's specific environment.

---

# 39. Risk Assessment vs Penetration Testing

### Risk Assessment

Asks:

> What risks does the organization face and how should they be treated?

### Penetration Testing

Attempts to safely demonstrate whether vulnerabilities can be exploited and what impact may result.

Penetration-testing results can provide evidence for risk assessment, but the activities have different objectives.

---

# 40. Risk Assessment vs Business Impact Analysis

### Risk Assessment

Focuses on threats, vulnerabilities, likelihood, impact, and risk treatment.

### Business Impact Analysis (BIA)

Focuses on the consequences of disruption to business processes and helps determine priorities such as recovery requirements.

A BIA can therefore provide important impact information used by broader risk and continuity processes.

---

# 41. Third-Party Risk

Organizations inherit risks from vendors and service providers.

Examples include:

- Cloud providers.
- SaaS platforms.
- Managed service providers.
- Payment processors.
- Software suppliers.
- Contractors.

Third-party risk analysis may examine:

- Data access.
- Security controls.
- Compliance obligations.
- Incident notification.
- Availability.
- Subcontractors.
- Business continuity.
- Supply-chain dependencies.

A vendor's security posture can affect the organization's own risk.

---

# 42. Supply-Chain Risk

A security incident can originate through a supplier, software dependency, hardware component, or managed service.

Risk management should therefore consider:

```text
Organization
   ↓
Vendor
   ↓
Subcontractor
   ↓
Software / Service / Infrastructure
```

The organization should understand critical dependencies and the controls used to manage them.

---

# 43. Risk Inheritance

In cloud and third-party environments, some security risks are influenced by another organization's controls.

For example, a SaaS customer may depend on the provider for:

- Infrastructure security.
- Physical security.
- Platform availability.
- Certain logging capabilities.

This does not mean the customer has no responsibilities. It means risk and responsibility are distributed and should be understood explicitly.

---

# 44. Risk Monitoring

Risk management does not end when a treatment is implemented.

Organizations should monitor:

- New vulnerabilities.
- Threat intelligence.
- Security incidents.
- Control effectiveness.
- Asset changes.
- Business changes.
- Regulatory changes.
- Third-party changes.
- Residual risk.

A previously acceptable risk can become unacceptable when circumstances change.

---

# 45. Control Effectiveness

A control should be evaluated based on whether it actually reduces the intended risk.

For example, an organization may have an MFA policy, but if privileged accounts are excluded or unenrolled, the practical risk reduction may be lower than expected.

Control effectiveness can be evaluated through:

- Testing.
- Auditing.
- Monitoring.
- Metrics.
- Assessments.
- Incident analysis.

---

# 46. Risk Dependencies

Risks may be interconnected.

Example:

```text
Identity Provider Failure
        ↓
Authentication Failure
        ↓
Application Unavailability
        ↓
Business Disruption
```

Another example:

```text
Vendor Compromise
        ↓
Malicious Software Update
        ↓
Internal Compromise
        ↓
Data Exposure
```

Risk analysis should consider dependencies rather than evaluating every risk completely in isolation.

---

# 47. Risk Aggregation

Multiple small risks can combine into a significant organizational exposure.

For example, several individually moderate weaknesses may collectively create a dangerous attack path:

```text
Weak MFA
   +
Excessive Privilege
   +
Poor Segmentation
   +
Weak Monitoring
   ↓
Large Combined Exposure
```

Risk management should therefore consider systemic and aggregated risk.

---

# 48. Risk vs Issue

A **risk** is a potential future event or condition that could affect objectives.

An **issue** is a problem that has already occurred or is currently occurring.

Example:

> "This unpatched server could be exploited." → Risk.

> "The server has been compromised and is actively communicating with an attacker." → Current issue/incident requiring response.

The exact terminology may vary between organizations, but the future-potential versus current-problem distinction is useful.

---

# 49. Common Risk Management Failures

## Failure 1 — Treating every vulnerability equally

A vulnerability's technical severity does not automatically determine organizational priority.

**Better:** consider exposure, exploitability, asset criticality, business impact, and existing controls.

## Failure 2 — Assuming zero risk is possible

Security controls reduce risk but rarely eliminate every possible threat.

**Better:** manage residual risk deliberately.

## Failure 3 — Informal risk acceptance

A technician decides not to patch something without documenting the decision.

**Better:** use authorized risk ownership and formal acceptance processes.

## Failure 4 — Confusing transfer with elimination

Insurance does not prevent the cyberattack.

**Better:** understand what consequence is actually being transferred.

## Failure 5 — Ignoring business context

A technically serious weakness may have a different priority depending on the affected asset and exposure.

**Better:** connect technical findings to business impact.

## Failure 6 — Never updating the risk register

Risk information becomes stale.

**Better:** review risks as threats, assets, controls, and business requirements change.

## Failure 7 — False precision

Numerical models are treated as exact predictions.

**Better:** document assumptions and recognize uncertainty.

## Failure 8 — Focusing only on individual risks

Interdependent risks may create larger systemic exposure.

**Better:** examine attack paths, dependencies, and aggregate risk.

---

# 50. Security+ Scenario — High-Impact Rare Event

A company faces a threat that is unlikely but could cause severe regulatory and operational consequences.

Do not dismiss the risk solely because likelihood is low.

The correct analysis considers both likelihood and impact. A low-probability event can still require treatment when the consequences are sufficiently severe.

---

# 51. Security+ Scenario — Risk Acceptance

A legacy system cannot be upgraded for six months. The security team documents the weakness, applies segmentation and monitoring, and presents the residual risk to an authorized risk owner.

If the authorized owner formally agrees to retain the residual risk for the defined period, this is **risk acceptance**.

The security team implementing compensating controls is not necessarily the party authorized to accept the business risk.

---

# 52. Security+ Scenario — Risk Transfer

An organization purchases cyber insurance to reduce the financial consequences of certain security incidents.

This is an example of **risk transfer**.

The insurance does not eliminate the vulnerability or prevent compromise. It changes how certain financial consequences are handled.

---

# 53. Security+ Scenario — Risk Mitigation

A company cannot immediately replace a vulnerable legacy server. It places the server in an isolated network segment, restricts access, monitors it, and limits exposed services.

These actions **mitigate** the risk by reducing exposure and/or potential impact.

---

# 54. Security+ Scenario — Risk Avoidance

An organization permanently stops using an unnecessary Internet-facing service because the security risk is not justified by its business value.

This is **risk avoidance** because the activity creating the exposure is eliminated.

---

# 55. Security+ Scenario — Quantitative Calculation

Given:

```text
AV = $400,000
EF = 25%
ARO = 0.5
```

Calculate SLE:

```text
SLE = AV × EF
SLE = $400,000 × 0.25
SLE = $100,000
```

Calculate ALE:

```text
ALE = SLE × ARO
ALE = $100,000 × 0.5
ALE = $50,000
```

Therefore:

**SLE = $100,000**

**ALE = $50,000**

Remember that SLE represents one occurrence, while ALE represents the estimated annualized loss.

---

# 56. Security+ Exam Distinctions and Traps

### Threat vs Vulnerability

- **Threat:** potential cause of harm.
- **Vulnerability:** weakness that can contribute to exploitation or harm.

### Vulnerability vs Risk

- **Vulnerability:** weakness.
- **Risk:** potential consequence considered in context of likelihood and impact.

### Likelihood vs Impact

- **Likelihood:** probability or expected frequency.
- **Impact:** consequence or severity.

### Inherent vs Residual Risk

- **Inherent risk:** before controls.
- **Residual risk:** after controls.

### Avoid vs Mitigate

- **Avoid:** eliminate the risky activity or condition.
- **Mitigate:** reduce likelihood and/or impact through controls.

### Transfer vs Accept

- **Transfer:** shift some consequences to another party.
- **Accept:** knowingly retain the risk.

### SLE vs ALE

- **SLE:** loss from one occurrence.
- **ALE:** expected annualized loss.

### Qualitative vs Quantitative

- **Qualitative:** descriptive categories and relative prioritization.
- **Quantitative:** numerical analysis, often financial.

### Risk Owner vs Control Implementer

- **Risk owner:** accountable for the risk decision.
- **Control implementer:** performs the technical or operational work.

---

# 57. Security+ Risk Decision Framework

When analyzing a risk scenario, work through the following sequence.

### 1. What asset or business objective is affected?

Determine what the organization is trying to protect.

### 2. What is the threat?

Identify the potential source or event that could cause harm.

### 3. What vulnerability or weakness exists?

Identify the condition that enables or contributes to the threat.

### 4. What is the likelihood?

Consider exposure, exploitability, threat capability, controls, and historical information.

### 5. What is the impact?

Consider confidentiality, integrity, availability, financial, legal, regulatory, operational, safety, and reputational consequences.

### 6. What is the current risk?

Combine likelihood and impact using the organization's risk methodology.

### 7. What controls already exist?

Determine the inherent risk and current residual risk.

### 8. What response is appropriate?

Choose among avoidance, mitigation, transfer, or acceptance.

### 9. Who owns the decision?

Identify the authorized risk owner.

### 10. What evidence supports the decision?

Use assessments, scans, incidents, audits, metrics, and other reliable information.

### 11. What is the residual risk?

Determine what remains after treatment.

### 12. Does the residual risk fit appetite and tolerance?

If not, additional treatment or escalation may be required.

### 13. How will the risk be monitored?

Define metrics, review dates, triggers, and reassessment conditions.

---

# 58. Complete Risk Management Workflow

```text
Business Objectives
       ↓
Identify Assets
       ↓
Identify Threats
       ↓
Identify Vulnerabilities
       ↓
Identify Existing Controls
       ↓
Analyze Likelihood
       ↓
Analyze Impact
       ↓
Determine Risk
       ↓
Prioritize
       ↓
Select Response
       ↓
Implement Treatment
       ↓
Determine Residual Risk
       ↓
Authorized Decision
       ↓
Monitor
       ↓
Reassess
```

This is a continuous process rather than a one-time assessment.

---

# 59. Key Takeaways

- Risk management connects cybersecurity decisions to business objectives.
- Risk involves potential adverse effects on organizational objectives.
- Threats are potential causes of harm; vulnerabilities are weaknesses; risk considers likelihood and impact in context.
- Asset criticality and business impact are essential to prioritization.
- Likelihood describes how probable an event is; impact describes its consequences.
- Qualitative analysis uses descriptive categories; quantitative analysis uses numerical values.
- **SLE = AV × EF**.
- **ALE = SLE × ARO**.
- SLE represents one occurrence; ALE represents annualized expected loss.
- Quantitative calculations depend on assumptions and should not create false precision.
- Risk appetite provides broad organizational direction regarding acceptable risk.
- Risk tolerance defines more specific acceptable boundaries.
- Inherent risk exists before controls; residual risk remains after controls.
- Avoidance eliminates the activity or condition creating the risk.
- Mitigation reduces likelihood and/or impact.
- Transfer shifts some consequences to another party.
- Acceptance deliberately retains risk through an authorized decision.
- A risk register provides centralized visibility, ownership, treatment, status, and residual-risk tracking.
- Risk owners make or approve risk decisions; technical teams may implement the resulting controls.
- Exceptions and risk acceptance should be documented and periodically reviewed.
- Third-party and supply-chain dependencies can introduce organizational risk.
- Risk must be monitored because threats, assets, vulnerabilities, controls, and business conditions change.
- Multiple individually moderate risks can combine into significant systemic exposure.
- Compliance, vulnerability management, penetration testing, BIA, and risk assessment provide related but different perspectives.

## Core Security+ Mental Model

**Asset → Threat → Vulnerability → Likelihood → Impact → Risk → Treatment → Residual Risk → Acceptance/Escalation → Monitoring → Reassessment**

The central principle is: **risk management is not about eliminating every possible threat; it is about identifying and understanding risk, prioritizing it according to business context, selecting an appropriate response, assigning accountability, documenting decisions, and continuously verifying that residual risk remains acceptable.**