# 01 — Threat Actors and Motivations

## 1. Introduction

Before studying individual attacks, a security professional must understand **who performs attacks, why they perform them, what resources they have, and what access they may already possess**. This is the foundation for threat analysis.

A **threat actor** is an individual, group, organization, or state-associated entity that intentionally performs, attempts, facilitates, or directs activity capable of negatively affecting an information system, network, application, device, or data.

The phrase **threat actor** describes the source of the threat. It does not automatically tell us what attack will be used. For example, an organized criminal group might use phishing, credential stuffing, ransomware, or business email compromise. A nation-state actor might use espionage, supply-chain compromise, credential theft, or exploitation of exposed infrastructure.

This distinction is important because Security+ scenarios often provide behavioral clues rather than directly naming the actor. You should learn to infer the likely actor from **resources, sophistication, access, intent, target selection, and behavior**.

---

## 2. Threat, Threat Actor, Vulnerability, and Risk

These terms are related but are not interchangeable.

### Threat

A **threat** is a potential cause of harm. It represents something that could negatively affect an asset.

Examples include:

- A ransomware operator
- A malicious insider
- A natural disaster
- A phishing campaign
- A hardware failure

### Threat Actor

A threat actor is the entity responsible for or capable of carrying out a malicious action.

For example, the ransomware itself is not the threat actor. The criminal group operating the ransomware campaign is the threat actor.

### Vulnerability

A **vulnerability** is a weakness that could be exploited.

Examples include:

- An unpatched operating system
- Weak authentication
- Excessive privileges
- A vulnerable web application
- Poor physical security
- An exposed management interface

### Risk

**Risk** represents the possibility of an adverse event and its consequences. A simplified model is:

**Risk ≈ Likelihood × Impact**

A threat actor may create the threat, a vulnerability may provide the opportunity, and exploitation may produce the actual impact.

A useful relationship is:

**Threat Actor → Threat → Vulnerability/Exposure → Attack → Impact → Risk**

This relationship will appear repeatedly throughout Domain 2.

---

# 3. Major Threat Actor Categories

## 3.1 Nation-State Actors

A **nation-state actor** is associated with a government or receives significant government support, direction, intelligence, or resources.

These actors can possess substantially greater resources than individual attackers. Their capabilities may include specialized personnel, intelligence collection, custom malware, advanced infrastructure, vulnerability research, and long-term operational planning.

### Typical motivations

Nation-state operations may pursue:

- Espionage
- Military intelligence
- Strategic advantage
- Political influence
- Intellectual property acquisition
- Disruption of strategic infrastructure
- Intelligence collection

The important point is that the objective may not be immediate financial profit. An operation may remain active for months or years because the information being collected has strategic value.

### Example

Imagine a technology company developing advanced semiconductor technology. An attacker secretly compromises an employee's account, establishes persistence, accesses internal research repositories, and slowly transfers selected documents over many months.

The long-term intelligence objective, significant resources, stealth, and strategic target are characteristics consistent with a highly capable state-associated actor.

### Defensive implications

Defending against highly capable actors requires more than perimeter security. Organizations may need:

- Strong identity security
- MFA and phishing-resistant authentication
- Network segmentation
- Endpoint detection and response
- Centralized logging
- Threat hunting
- Privileged access management
- Supply-chain security
- Detection of abnormal authentication and data movement
- Long-term monitoring and incident response capabilities

### Exam clue

If a scenario emphasizes **large resources, intelligence gathering, strategic targets, persistence, and long-term operations**, consider a nation-state actor.

---

## 3.2 Organized Crime

Organized criminal groups conduct cyber activity primarily for **financial gain**. Modern cybercrime can be highly structured, with different people or groups specializing in different parts of an operation.

For example, one criminal may obtain initial access, another may provide malware, another may operate infrastructure, and another may handle stolen data or extortion.

### Common activities

Organized crime may conduct:

- Ransomware
- Extortion
- Credential theft
- Credential sales
- Payment fraud
- Business email compromise
- Identity theft
- Data theft
- Malware distribution
- Sale of compromised systems

### Example

An attacker obtains access to a company's remote-access service using stolen credentials. The attacker moves laterally, steals sensitive files, encrypts systems, and demands payment.

The central motivation is financial. The organization may be targeted because the attacker believes the victim can pay or because the data has resale or extortion value.

### Exam clue

When the primary objective is **money**, especially through ransomware, fraud, extortion, or stolen credentials, organized crime is an important possibility.

---

## 3.3 Hacktivists

**Hacktivists** combine hacking activity with an ideological, political, or social objective.

Their objective may be to attract attention, embarrass an organization, protest a policy, distribute a message, or disrupt an organization associated with an opposing viewpoint.

### Common activities

Examples include:

- Website defacement
- Denial-of-service attacks
- Unauthorized disclosure of information
- Account compromise
- Public release of stolen material

### Example

A group launches a denial-of-service attack against an organization because it disagrees with the organization's publicly stated policy. The primary objective is political or ideological rather than financial.

### Exam clue

If the scenario emphasizes **political beliefs, social causes, public protest, or ideology**, consider hacktivism.

---

## 3.4 Script Kiddies / Unskilled Attackers

A **script kiddie** is an inexperienced attacker who relies heavily on tools, scripts, exploit code, scanners, malware builders, or tutorials created by others.

The attacker may have limited understanding of the underlying vulnerability but can still cause damage by using automated tools.

### Important distinction

Low attacker expertise does **not** mean low technical impact.

For example, a person with little knowledge of networking may download a publicly available vulnerability scanner and discover an unpatched internet-facing service. If the service is exploitable, the resulting compromise can still be serious.

### Defensive implication

Organizations must maintain basic security hygiene regardless of whether they believe sophisticated attackers are targeting them.

Important controls include:

- Patch management
- Secure configuration
- Removing unnecessary services
- Strong authentication
- Network filtering
- Vulnerability scanning

### Exam clue

Look for clues such as **limited skill, reliance on existing tools, publicly available exploit code, or automated attacks without evidence of custom development**.

---

## 3.5 Insider Threats

An **insider threat** involves someone who has legitimate organizational access and uses, misuses, or becomes a vehicle for that access in a way that creates security risk.

Insiders can be employees, contractors, administrators, temporary workers, partners, or other trusted users.

### Malicious insider

A malicious insider intentionally abuses access.

Examples:

- Stealing customer data before leaving the company
- Deleting important files
- Selling confidential information
- Creating unauthorized privileged accounts
- Sabotaging systems

### Negligent insider

A negligent insider does not intend to cause harm but creates exposure through unsafe behavior.

Examples:

- Sending confidential information to the wrong recipient
- Uploading company files to an unauthorized cloud service
- Leaving a laptop unsecured
- Clicking a malicious attachment
- Misconfiguring permissions

### Compromised insider account

An employee may be completely innocent while their credentials or endpoint have been compromised.

An attacker can then use the employee's legitimate identity to access systems. This is important because the activity may initially appear legitimate.

### Why insider threats are difficult

Traditional perimeter security assumes that the attacker is outside the organization. An insider or compromised account may already have valid access.

Therefore, organizations should use:

- Least privilege
- Privileged access management
- Access reviews
- User and entity behavior analytics
- Centralized logging
- Strong authentication
- Separation of duties
- Data loss prevention
- Rapid account deprovisioning

---

## 3.6 Shadow IT

**Shadow IT** is technology used within an organization without going through the organization's approved security, procurement, or IT processes.

Examples include:

- An employee creating an unauthorized cloud storage account
- A team deploying an unapproved SaaS application
- Employees installing unauthorized software
- A department purchasing a network device without security review

Shadow IT increases risk because security teams may not know that the asset exists.

### Example

Suppose an employee needs to share large files and creates a personal cloud-storage account. Company documents are uploaded there without security review.

The organization may now have:

- Unknown data location
- Unknown access controls
- Unknown retention policy
- Unknown encryption configuration
- Unknown logging
- Potential regulatory exposure

### Important distinction

Shadow IT is not itself a threat actor category. It is an **organizational technology-management problem and attack-surface concern**.

---

# 4. Threat Actor Characteristics

Security+ scenarios may describe an attacker through characteristics rather than naming the actor.

## 4.1 Resources

Resources include:

- Funding
- Personnel
- Computing infrastructure
- Intelligence
- Malware development capability
- Vulnerability research
- Access to specialized equipment
- Time

A well-funded actor can maintain infrastructure and personnel for longer periods and can develop customized capabilities.

## 4.2 Sophistication

Sophistication describes how technically and operationally capable the actor is.

A low-sophistication attacker may use a public exploit without understanding it. A highly sophisticated actor may develop custom malware, exploit previously unknown weaknesses, evade detection, and maintain multiple persistence mechanisms.

## 4.3 Intent

Intent describes what the attacker wants to accomplish.

Possible objectives include:

- Financial gain
- Espionage
- Disruption
- Destruction
- Ideological messaging
- Revenge
- Competitive advantage
- Intelligence gathering

## 4.4 Opportunity

Attackers frequently exploit opportunities created by poor security.

Examples include:

- Internet-facing vulnerable services
- Weak passwords
- Exposed cloud storage
- Misconfigured firewalls
- Leaked API keys
- Excessive privileges
- Unpatched applications

An organization does not necessarily need to be specifically selected by an attacker. Automated scanning means exposed vulnerable systems may be discovered opportunistically.

## 4.5 Access

Access is another important characteristic.

An external attacker may need to obtain initial access through phishing or exploitation. An insider may already possess authorized access. A compromised vendor account may provide third-party access.

The initial access position strongly affects the defensive strategy.

---

# 5. Common Threat Motivations

## 5.1 Financial Gain

Financial motivation is one of the most common drivers of cybercrime.

Examples include:

- Ransomware
- Extortion
- Payment fraud
- Credential theft
- Cryptocurrency theft
- Selling stolen information
- Selling access to compromised systems

## 5.2 Espionage

Espionage focuses on collecting information that provides intelligence or strategic advantage.

Targets may include:

- Government agencies
- Defense organizations
- Research institutions
- Technology companies
- Telecommunications providers
- Critical infrastructure organizations

## 5.3 Ideology

Ideological attackers seek to advance a cause or message.

This is strongly associated with hacktivism, although ideology can motivate other types of attackers as well.

## 5.4 Revenge

A disgruntled employee or former employee may attack an organization because of a personal grievance.

Potential activity includes:

- Data deletion
- System sabotage
- Information disclosure
- Account abuse
- Website disruption

## 5.5 Competitive Advantage

An attacker may attempt to obtain proprietary information to gain an economic or strategic advantage.

Examples include:

- Source code theft
- Research theft
- Business strategy theft
- Intellectual property theft
- Customer information theft

## 5.6 Disruption or Destruction

Some attackers are primarily interested in making systems unavailable or destroying data.

The distinction from financial attacks is important. A ransomware attack may combine financial extortion with disruption, while another destructive attack may have no payment component at all.

---

# 6. Motivation vs Capability

These concepts must be separated.

**Motivation = Why the actor wants to attack.**

**Capability = What the actor is capable of doing.**

Consider two attackers who both want money.

- Attacker A uses publicly available ransomware and has limited technical skill.
- Attacker B operates a criminal organization with specialized malware developers, stolen credentials, infrastructure, and dedicated operators.

Their motivation is similar, but their capability is very different.

This distinction helps security teams build realistic threat models instead of assuming every attacker has the same resources.

---

# 7. Threat Actor Comparison

| Actor | Common Motivation | Typical Characteristics |
|---|---|---|
| Nation-state | Espionage, strategic advantage, disruption | Highly resourced, persistent, sophisticated |
| Organized crime | Financial gain | Structured operations, monetization |
| Hacktivist | Ideology, political/social objectives | Public messaging, disruption, information exposure |
| Insider | Revenge, financial gain, negligence, sabotage | Legitimate access |
| Script kiddie | Curiosity, reputation, experimentation, opportunism | Limited expertise, existing tools |
| Shadow IT | Not an actor category | Unauthorized technology increases exposure |

The table should be used for recognition, not as a substitute for understanding the scenario.

---

# 8. Detailed Scenario Analysis

### Scenario

A company discovers that a former administrator accessed a file server three weeks after leaving the organization. The administrator's account remained active. Sensitive files were deleted and some configuration settings were changed.

### Step 1 — Identify the actor relationship

The person is a former administrator, so they previously had legitimate access.

### Step 2 — Identify the security weakness

The account was not disabled after termination. This indicates a failure in the identity lifecycle and offboarding process.

### Step 3 — Identify the likely motivation

The deletion of files and configuration changes may be consistent with revenge or sabotage, although motivation should not be assumed without evidence.

### Step 4 — Identify the impact

The primary impact may involve:

- Availability
- Integrity
- Operational disruption
- Potential data loss

### Step 5 — Identify controls

Relevant controls include:

- Immediate account deprovisioning during offboarding
- Centralized identity management
- Access reviews
- Privileged access management
- Least privilege
- Logging and monitoring
- Separation of duties
- Backup and recovery controls

This illustrates why understanding the actor, weakness, and motivation together is more useful than simply labeling the incident as an insider attack.

---

# 9. Another Scenario — Compromised Insider

Suppose an employee normally logs in from India during business hours. Security monitoring suddenly detects the same account authenticating from another country, followed by access to sensitive systems and large data transfers.

The employee may not actually be malicious. The account may have been compromised through phishing or credential theft.

The correct analytical approach is therefore:

**Identity → Authentication event → Device/context → Resource access → Behavior → Correlation → Investigation**

Do not automatically accuse the employee simply because the account is associated with an insider. The account, endpoint, or credentials may have been compromised.

---

# 10. Defensive Strategy Based on Actor Type

The actor type can influence defensive priorities.

### Against opportunistic attackers

Strong baseline security is essential:

- Patch systems
- Remove unnecessary services
- Secure configurations
- Use MFA
- Scan for vulnerabilities
- Filter network exposure

### Against insider threats

Focus strongly on identity and accountability:

- Least privilege
- Access reviews
- PAM
- Logging
- Separation of duties
- DLP
- Offboarding

### Against highly capable persistent actors

Defense should include deeper visibility and layered controls:

- EDR/XDR
- Threat hunting
- Network monitoring
- Centralized SIEM
- Strong identity controls
- Segmentation
- Supply-chain monitoring
- Incident response capability

The principle is not that one actor receives one technology. Security controls should be selected according to the organization's risk and threat model.

---

# 11. Security+ Scenario Recognition

When reading a question, look for multiple clues instead of relying on one word.

### Clue: Government intelligence collection

Think about **nation-state activity**.

### Clue: Ransomware operation demanding payment

Think about **financially motivated criminal activity**.

### Clue: Political protest combined with website disruption

Think about **hacktivism**.

### Clue: Employee intentionally stealing company information

Think about a **malicious insider**.

### Clue: Employee account used by an attacker

Consider a **compromised insider identity**, not automatically a malicious employee.

### Clue: Unauthorized cloud application used by employees

Think about **shadow IT** and the resulting attack-surface and governance problem.

### Clue: Attacker uses publicly available tools with little technical understanding

Consider an **unskilled attacker/script kiddie**.

---

# 12. Common Mistakes to Avoid

### Mistake 1: Treating malware as the threat actor

Ransomware is a type of malware. The criminal group deploying it is the threat actor.

### Mistake 2: Assuming every insider is malicious

Insider threat includes malicious, negligent, and compromised situations.

### Mistake 3: Assuming sophisticated tools require sophisticated attackers

An inexperienced attacker can use sophisticated tools created by someone else.

### Mistake 4: Confusing motivation with capability

Financial motivation does not tell you how technically capable the attacker is.

### Mistake 5: Treating shadow IT as an attacker

Shadow IT is unauthorized technology usage that expands exposure; it is not itself a threat actor.

### Mistake 6: Assuming the identified account owner is the attacker

Credentials can be stolen. Investigate identity, device, authentication context, and behavior before assigning responsibility.

---

# 13. Security+ Exam Focus

For scenario-based questions, determine:

1. **Who** is performing or enabling the activity?
2. **Why** are they doing it?
3. **What resources and capabilities** do they have?
4. **What access** do they possess?
5. **What target** are they interested in?
6. **What weakness or opportunity** enabled the activity?
7. **What security controls** reduce the associated risk?

The strongest answer is usually the one that matches the complete scenario rather than a single keyword.

---

# 14. Key Takeaways

1. A threat actor is the entity capable of performing or directing harmful activity.
2. A threat is a potential cause of harm; a vulnerability is a weakness that can be exploited; risk considers likelihood and impact.
3. Nation-state actors commonly have substantial resources and may pursue strategic or intelligence objectives.
4. Organized crime commonly pursues financial gain.
5. Hacktivists commonly pursue ideological, political, or social objectives.
6. Script kiddies often depend on existing tools and have limited technical expertise.
7. Insider threats involve legitimate organizational access and may be malicious, negligent, or compromised.
8. Shadow IT creates unmanaged technology and increases the organization's attack surface.
9. Motivation explains why an actor attacks; capability explains what the actor can realistically accomplish.
10. Threat-actor identification should be based on multiple contextual clues rather than a single characteristic.
11. Understanding the actor helps defenders build a realistic threat model and choose appropriate controls.
