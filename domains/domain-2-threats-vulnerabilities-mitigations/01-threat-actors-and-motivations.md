# 01 — Threat Actors and Motivations

## 1. Why Threat Actors Matter

A security analyst cannot properly assess a threat without understanding who is capable of carrying it out, what resources they possess, what they want to achieve, and what level of access they may already have. A **threat actor** is an individual, group, organization, or state-sponsored entity that intentionally performs actions capable of compromising the confidentiality, integrity, or availability of information systems or data.

Security+ uses threat-actor characteristics to help determine likely attack behavior. A highly resourced nation-state may have capabilities, persistence, intelligence, and access that are very different from those of an inexperienced attacker using publicly available tools.

## 2. Threat Actor Categories

### Nation-state

A nation-state actor operates on behalf of, or with substantial support from, a government. These actors commonly have significant financial resources, intelligence capabilities, technical expertise, specialized tooling, and patience.

Typical objectives include espionage, military intelligence, strategic advantage, disruption, influence, and theft of intellectual property. Nation-state operations may remain undetected for long periods because persistence and stealth can be more important than immediate financial gain.

**Security implication:** organizations should consider advanced persistent threats, credential theft, supply-chain compromise, living-off-the-land techniques, and long-term persistence when defending against highly capable actors.

### Unskilled attacker / script kiddie

An unskilled attacker has limited technical knowledge and often relies on tools, exploit code, scanners, malware builders, or attack frameworks developed by others. The important distinction is that the attacker may have low expertise even though the tools they use can be technically sophisticated.

This is why exposed and unpatched systems remain dangerous even when an organization is not specifically targeted.

### Hacktivist

Hacktivists use technical attacks to advance ideological, political, or social objectives. Their activity may include website defacement, denial-of-service attacks, information disclosure, or unauthorized access intended to attract public attention.

Their motivation is generally not primarily financial. Public visibility and messaging may be part of the objective.

### Organized crime

Organized criminal groups generally pursue financial gain. They may operate ransomware campaigns, steal payment information, conduct business email compromise, sell stolen credentials, perform identity theft, or monetize compromised systems.

These groups may have structured operations in which different participants specialize in initial access, malware development, infrastructure, credential theft, laundering, or extortion.

### Insider threat

An insider threat originates from someone with legitimate organizational access. The insider may be a current employee, contractor, administrator, partner, or another trusted user.

Insider threats can be:

- **Intentional:** the user deliberately steals data, sabotages systems, or abuses privileges.
- **Unintentional:** the user accidentally exposes data, clicks a malicious link, misconfigures a system, or mishandles sensitive information.
- **Compromised insider:** an attacker takes control of a legitimate employee account or endpoint and uses that trusted identity.

Insider threats are particularly difficult because legitimate credentials and approved access can make malicious activity appear normal.

### Shadow IT

Shadow IT refers to systems, applications, cloud services, or devices used by employees without the organization's formal approval or security governance. Shadow IT expands the attack surface because security teams may not know that the asset exists or may be unable to apply organizational controls.

## 3. Threat Actor Characteristics

Security+ scenarios can describe actors using characteristics rather than explicitly naming them. Important characteristics include:

### Resources

Resources include money, computing infrastructure, personnel, intelligence, tooling, and access to specialized capabilities. More resources generally allow an actor to conduct more complex and sustained operations.

### Level of sophistication

Sophistication describes technical capability and operational maturity. An actor using automated commodity malware is different from one developing custom malware and exploiting previously unknown vulnerabilities.

### Intent

Intent describes what the actor wants to accomplish. Common objectives include financial gain, espionage, disruption, political messaging, revenge, competitive advantage, or destruction.

### Opportunity

Attackers frequently exploit opportunities created by exposed services, weak credentials, unpatched vulnerabilities, misconfigurations, leaked secrets, or human error. An organization can become a target simply because it presents an easy opportunity.

### Internal versus external access

An external attacker begins outside the trusted environment and must obtain access. An insider or compromised account may already have some level of legitimate access, changing the defensive problem considerably.

## 4. Common Motivations

### Financial gain

The attacker seeks money directly or indirectly. Examples include ransomware, extortion, payment fraud, credential theft, cryptocurrency theft, and selling stolen information.

### Espionage

Espionage focuses on obtaining information that provides intelligence or strategic advantage. The victim may be a government, defense organization, technology company, research institution, or competitor.

### Ideology

An ideological attacker wants to promote a political, religious, social, or other cause. Hacktivism is a common example.

### Revenge

A disgruntled employee or former employee may attempt to damage systems, delete information, expose confidential data, or disrupt operations.

### Competitive advantage

An organization or actor may steal intellectual property, business plans, research, source code, or other proprietary information to gain an advantage.

### Disruption or destruction

Some attacks are designed primarily to interrupt operations or destroy systems and data rather than steal information.

## 5. Threat Actor Capability Versus Motivation

Do not confuse **motivation** with **capability**.

For example, two attackers may both want financial gain, but one may be an inexperienced individual using a public ransomware tool while another may be an organized criminal group with dedicated infrastructure and specialized operators.

The motivation explains **why** the attack is performed. Capability helps explain **what the attacker is realistically able to do**.

## 6. Practical Security Scenario

Suppose a company discovers that a former administrator used still-active credentials to access a file server and delete business data.

The important observations are:

- The actor has legitimate historical access.
- The account is associated with an internal identity.
- The activity is intentional.
- The likely motivation could be revenge or sabotage.
- The vulnerability is weak account lifecycle management.

Potential mitigations include immediate account deprovisioning, privileged access management, centralized authentication, least privilege, logging, monitoring, and periodic access reviews.

## 7. Security+ Exam Focus

When a scenario gives clues about the actor, identify the strongest combination of **actor type + motivation + capability**.

Remember:

- Nation-state → strategic objectives, espionage, substantial resources.
- Organized crime → financial gain.
- Hacktivist → ideology or political/social objectives.
- Insider → trusted organizational access.
- Script kiddie → limited expertise, reliance on existing tools.
- Shadow IT → unauthorized technology or services introduced into the environment.

## 8. Key Takeaways

1. A threat actor is the entity performing or attempting the malicious action.
2. Motivation explains why the actor attacks.
3. Capability and resources help determine what attacks are feasible.
4. Insider threats are dangerous because legitimate access can bypass traditional external defenses.
5. A compromised legitimate account can create an insider-like attack without the employee being malicious.
6. Understanding the actor helps security teams prioritize realistic threats and controls.
