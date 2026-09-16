# Domain 2 — Threats, Vulnerabilities, and Mitigations

Domain 2 develops the ability to understand **who attacks, why attacks occur, how attacks reach targets, which weaknesses are exploited, what malicious activity looks like, how vulnerabilities are assessed, and how defenders reduce risk**.

The domain is organized as a progression rather than a collection of isolated definitions. The early modules establish the attacker and attack surface, the middle modules examine common attacks and vulnerabilities, and the later modules focus on assessment, penetration testing, remediation, and indicators of malicious activity.

---

## Complete Study Sequence

1. [Threat Actors and Motivations](01-threat-actors-and-motivations.md)
2. [Threat Vectors and Attack Surfaces](02-threat-vectors-and-attack-surfaces.md)
3. [Malware](03-malware.md)
4. [Social Engineering](04-social-engineering.md)
5. [Credential and Password Attacks](05-credential-and-password-attacks.md)
6. [Network Attacks](06-network-attacks.md)
7. [Application and Web Attacks](07-application-and-web-attacks.md)
8. [Wireless, Mobile, and Specialized Attacks](08-wireless-mobile-and-specialized-attacks.md)
9. [Vulnerability Concepts](09-vulnerability-concepts.md)
10. [Vulnerability Identification and Scanning](10-vulnerability-identification-and-scanning.md)
11. [Penetration Testing](11-penetration-testing.md)
12. [Vulnerability Remediation and Mitigation](12-vulnerability-remediation-and-mitigation.md)
13. [Indicators of Malicious Activity](13-indicators-of-malicious-activity.md)

---

## How to Study Domain 2

Do not memorize attack names without understanding the security problem behind them. For each attack, vulnerability, or malicious behavior, work through the complete chain:

**Asset → Weakness → Threat Actor → Attack Vector → Exploitation → Impact → Indicator → Detection → Mitigation/Remediation**

For example, when studying a network attack, do not stop at knowing its name. Be able to explain:

- What asset is being targeted?
- What weakness makes the attack possible?
- Which type of threat actor might use it?
- What attack vector is involved?
- What happens during exploitation at a conceptual level?
- What security property is affected?
- What evidence might appear in logs or network traffic?
- Which controls can detect the activity?
- Which mitigation or remediation reduces the risk?

This approach is particularly useful for scenario-based Security+ questions.

---

## Core Conceptual Distinctions

Several concepts in Domain 2 are easy to confuse. Keep these relationships clear:

### Threat

A potential cause of harm to an asset or environment.

### Threat Actor

The person, group, organization, or other entity capable of carrying out a threat.

### Threat Vector

The path or mechanism used to reach a target.

### Attack Surface

The collection of exposed points through which an attacker could potentially interact with an environment.

### Vulnerability

A weakness that can potentially be exploited.

### Exploit

A technique, code, or method used to take advantage of a vulnerability.

### Indicator

Observable evidence that may suggest suspicious or malicious activity.

### Risk

The potential for loss or adverse impact resulting from a threat exploiting a vulnerability in a particular context.

---

## Assessment and Response Progression

The later modules follow an operational progression:

**Identify vulnerabilities → Scan and assess → Validate through authorized testing → Prioritize → Remediate or mitigate → Verify → Monitor**

This distinction is important because identifying a vulnerability does not automatically mean it has been exploited, and applying a remediation does not automatically prove that the vulnerability is gone.

---

## Security+ Scenario Reasoning

When presented with a scenario, identify the **observable facts first** and then determine which security concept explains them.

A useful sequence is:

1. **Identify the asset** — What is being protected?
2. **Identify the weakness** — What condition creates exposure?
3. **Identify the attacker or threat** — Who or what could cause harm?
4. **Identify the vector** — How could the target be reached?
5. **Identify the activity** — What attack or suspicious behavior is occurring?
6. **Identify the evidence** — What logs, network activity, endpoint behavior, or application activity support the conclusion?
7. **Identify the impact** — What could be affected?
8. **Select the control** — What security measure addresses the problem?
9. **Distinguish mitigation from remediation** — Does the control reduce exposure or remove the underlying weakness?
10. **Verify** — How would the organization confirm that the problem was addressed?

Avoid selecting an answer merely because a keyword appears in the scenario. First determine the underlying security concept.

---

## Important Exam Distinctions

| Concept A | Concept B | Core distinction |
|---|---|---|
| Threat | Vulnerability | Potential cause of harm vs. weakness that can be exploited |
| Attack surface | Attack vector | Where exposure exists vs. how the target is reached |
| Vulnerability scan | Penetration test | Identify potential weaknesses vs. authorized controlled validation |
| Remediation | Mitigation | Correct the weakness vs. reduce its likelihood or impact |
| Authentication | Authorization | Prove identity vs. determine permitted access |
| False positive | False negative | Benign activity detected as suspicious vs. malicious activity missed |
| IoC | IoA | Evidence associated with compromise vs. evidence of suspicious attack behavior |
| DoS | DDoS | Denial of service from one/few sources vs. distributed sources |
| Password spraying | Credential stuffing | Few passwords across many accounts vs. reuse of previously stolen credential pairs |
| ARP poisoning | DNS poisoning | Manipulation of local address resolution vs. manipulation of DNS resolution |

---

## Domain 2 Learning Model

For every topic, aim to understand five levels:

### Level 1 — Definition

Know what the term means.

### Level 2 — Mechanism

Understand how the attack, vulnerability, or defensive control works conceptually.

### Level 3 — Evidence

Know what an analyst might observe in endpoint, identity, network, application, or cloud telemetry.

### Level 4 — Defense

Understand which preventive, detective, and corrective controls reduce the associated risk.

### Level 5 — Scenario Application

Be able to recognize the concept when the Security+ question describes the situation without directly naming it.

The objective is not simply to memorize terminology. It is to develop the ability to move from **symptoms and evidence → security concept → appropriate response**.

---

## Domain 2 Completion Checklist

- [x] Threat actors and motivations
- [x] Threat vectors and attack surfaces
- [x] Malware
- [x] Social engineering
- [x] Credential and password attacks
- [x] Network attacks
- [x] Application and web attacks
- [x] Wireless, mobile, and specialized attacks
- [x] Vulnerability concepts
- [x] Vulnerability identification and scanning
- [x] Penetration testing
- [x] Vulnerability remediation and mitigation
- [x] Indicators of malicious activity

All thirteen individual study modules have been expanded into detailed, standalone notes. The modules are intended to be studied progressively and revisited for scenario-based revision.
