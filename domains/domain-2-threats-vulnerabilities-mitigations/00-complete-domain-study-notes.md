# Domain 2 — Complete Study Notes: Threats, Vulnerabilities, and Mitigations

Domain 2 is about understanding **who attacks systems, why they attack, how attacks are delivered, what weaknesses they exploit, how malicious activity appears, and how defenders identify and reduce the resulting risk**. The important skill is not memorizing attack names independently. A Security+ scenario normally gives you an asset, weakness, attacker behavior, or symptom and expects you to connect it to the correct threat, vulnerability, detection method, or mitigation.

## 1. Threat Actors and Motivations

A **threat actor** is an individual, group, or organization capable of carrying out a malicious or unauthorized action. Threat actors differ in resources, technical skill, access, persistence, and motivation.

### Nation-state

Nation-state actors are associated with governments or government-supported interests. They can have substantial funding, intelligence resources, specialized teams, and long-term objectives. Their operations may target government systems, defense organizations, telecommunications, research, energy, or other strategically valuable infrastructure.

### Organized crime

Criminal groups normally pursue financial gain. They may operate ransomware campaigns, steal credentials, conduct payment fraud, sell access, or monetize stolen information. Modern criminal operations can resemble businesses, with specialized roles for initial access, malware development, infrastructure, and extortion.

### Hacktivists

Hacktivists use cyber activity to promote political or social causes. Defacement, denial-of-service attacks, information leaks, and unauthorized access may be used for visibility or disruption.

### Insider threats

An insider already has some legitimate access. The threat may be malicious, negligent, or compromised. This makes insider activity particularly important because conventional perimeter controls may not prevent an authorized account from accessing sensitive resources.

### Script kiddies and unskilled attackers

These attackers may use publicly available tools or exploit code without deeply understanding how the technology works. Low technical sophistication does not necessarily mean low impact because automated tools can still cause significant damage.

### Motivations

Common motivations include financial gain, espionage, political influence, ideological objectives, revenge, competitive advantage, disruption, and curiosity.

The exam distinction is important: **motivation explains why; capability explains what an actor can realistically accomplish.**

## 2. Threat Vectors and Attack Surfaces

An **attack vector** is the path or technique used to reach a target. An **attack surface** is the collection of exposed points through which an attacker could interact with an environment.

Attack vectors include phishing, exposed services, stolen credentials, malicious attachments, removable media, supply-chain compromise, vulnerable applications, wireless networks, and physical access.

Attack surfaces can be digital, physical, human, or third-party. An organization can reduce risk by removing unnecessary services, patching vulnerabilities, limiting privileges, segmenting networks, securing physical access, training users, and controlling third-party connections.

A useful chain is:

`Asset → Exposure → Vulnerability → Attack Vector → Exploitation → Impact`

## 3. Malware

Malware is software designed to perform unauthorized or harmful activity.

A **virus** normally attaches itself to a host file and requires execution of that host. A **worm** can self-propagate across systems or networks. A **Trojan** disguises itself as legitimate software or relies on the victim believing it is legitimate. **Ransomware** restricts access to data or systems and demands payment. **Spyware** collects information covertly, while a **keylogger** captures keystrokes.

A **rootkit** attempts to maintain privileged access while hiding its presence. A **botnet** is a collection of compromised systems controlled as part of a coordinated operation.

Modern malware may use **fileless techniques** or legitimate administrative tools, sometimes called living-off-the-land techniques, to reduce reliance on obvious malicious files.

From a defender's perspective, malware analysis should consider delivery, execution, persistence, privilege use, command and control, objectives, and indicators of compromise.

## 4. Social Engineering

Social engineering attacks the **human decision-making process** rather than relying exclusively on a technical vulnerability.

**Phishing** uses deceptive messages to manipulate victims. **Spear phishing** is targeted at a specific person or group. **Whaling** focuses on senior or high-value targets. **Vishing** uses voice communication, while **smishing** uses SMS or similar messaging.

**Pretexting** creates a fabricated scenario to obtain information or action. **Baiting** offers something attractive to encourage a victim to interact with a malicious object or service. **Quid pro quo** promises a benefit in exchange for information or action. **Tailgating** involves following an authorized person into a restricted area.

Business email compromise can combine impersonation, urgency, authority, and financial manipulation.

Defenses include awareness training, phishing-resistant authentication, verification procedures, email filtering, domain protection, least privilege, and clear reporting mechanisms.

## 5. Credential and Password Attacks

Credential attacks attempt to obtain or reuse authentication material.

A **brute-force attack** systematically tries combinations. A **dictionary attack** uses likely words and patterns. **Password spraying** tries one common password against many accounts to avoid repeated failures against a single account. **Credential stuffing** uses previously leaked username/password pairs against another service.

**Pass-the-hash** abuses a password hash instead of requiring the plaintext password. **Pass-the-ticket** abuses Kerberos authentication tickets. **Kerberoasting** targets service-account Kerberos tickets for offline password cracking. **AS-REP roasting** targets accounts configured without requiring Kerberos preauthentication.

Defenses include MFA, strong password policies, password managers, account lockout or throttling where appropriate, privileged account separation, credential monitoring, secure password storage, and detection of abnormal authentication patterns.

## 6. Network Attacks

Network attacks exploit communication protocols, network architecture, or trust relationships.

**Denial of service** attempts to make a service unavailable. Distributed denial of service uses multiple sources. SYN floods abuse TCP connection establishment. Reflection and amplification attacks cause third-party systems to generate traffic toward the victim.

**ARP spoofing** can redirect local-network traffic. **DHCP spoofing** introduces a malicious DHCP service. **MAC flooding** attempts to overwhelm a switch's MAC address table. **VLAN hopping** attempts to cross VLAN boundaries. **DNS poisoning** manipulates name-resolution information. **Man-in-the-middle attacks** place an attacker between communicating parties.

Mitigation includes segmentation, secure switch configuration, DHCP snooping, dynamic ARP inspection, secure DNS practices, TLS, network monitoring, rate limiting, and appropriate firewall controls.

## 7. Application and Web Attacks

Application vulnerabilities often occur because input, authentication, authorization, sessions, or application state are handled incorrectly.

**SQL injection** occurs when attacker-controlled input is interpreted as database commands. **Cross-site scripting (XSS)** causes attacker-controlled script content to execute in a victim's browser. Stored XSS persists on the server; reflected XSS is returned as part of a request or response.

**CSRF** tricks an authenticated browser into performing an unwanted action. **Command injection** causes attacker input to be interpreted as operating-system commands. **Path traversal** attempts to access files outside the intended directory. **SSRF** causes a server to make requests chosen by an attacker. **Insecure deserialization** can lead to unauthorized behavior when untrusted serialized data is processed.

Defenses include parameterized queries, output encoding, input validation, secure session handling, authorization checks, CSRF protections, secure headers, dependency management, code review, and secure development practices.

## 8. Wireless, Mobile, IoT, and Specialized Attacks

Wireless environments introduce radio-based attack surfaces. An **evil twin** imitates a legitimate wireless network. **Deauthentication attacks** can disrupt wireless clients and may assist credential-capture scenarios. Rogue access points create unauthorized network entry points.

Mobile threats include malicious applications, insecure configuration, credential theft, SIM swapping, and loss or theft of devices. IoT devices often have limited processing capability, long lifecycles, weak default configurations, and inconsistent patching. Industrial control systems introduce additional safety and availability requirements because security actions must not create unsafe physical conditions.

## 9. Vulnerability Concepts

A **vulnerability** is a weakness that can be exploited. A **threat** is a potential cause of harm. An **exploit** is a method or code that takes advantage of a vulnerability. **Risk** combines the likelihood and impact of an adverse event.

A **zero-day vulnerability** is a vulnerability for which defenders have limited or no prior remediation opportunity before exploitation becomes known or occurs. CVE identifiers provide standardized references to publicly disclosed vulnerabilities, while CVSS provides a standardized severity scoring framework.

Severity is not identical to organizational risk. A technically severe vulnerability on an isolated system may represent less organizational risk than a moderately scored issue on a business-critical internet-facing system.

## 10. Vulnerability Identification and Scanning

Vulnerability scanning identifies weaknesses by examining systems, services, configurations, applications, or software versions.

**Authenticated scanning** uses credentials and can inspect internal configuration and installed software more deeply. **Unauthenticated scanning** views the target more like an external or unprivileged attacker.

Scanning can produce false positives and false negatives. Findings therefore require validation and prioritization rather than blind remediation.

A mature process is:

`Discover → Scan → Validate → Prioritize → Remediate → Rescan → Document`

## 11. Penetration Testing

A penetration test attempts to validate whether identified weaknesses can actually be exploited under an agreed scope.

**Black-box testing** provides little internal information. **White-box testing** provides substantial internal information. **Gray-box testing** provides limited internal knowledge.

Before testing, the organization defines rules of engagement, scope, authorized targets, timing, allowed techniques, communication procedures, and emergency stop conditions. After testing, findings should explain evidence, affected assets, impact, and remediation recommendations.

## 12. Vulnerability Remediation and Mitigation

**Remediation** removes or fixes the underlying weakness. **Mitigation** reduces the likelihood or impact without necessarily eliminating the root cause.

Patching is a common remediation method. Compensating controls can reduce risk when immediate patching is impossible. Examples include segmentation, access restrictions, virtual patching, additional monitoring, or temporary service isolation.

Prioritization should consider exploitability, exposure, asset criticality, data sensitivity, business impact, available controls, and active exploitation intelligence.

## 13. Indicators of Malicious Activity

Indicators are observable evidence that may suggest suspicious or malicious activity.

Endpoint indicators include unexpected processes, persistence mechanisms, unusual executables, disabled security controls, suspicious PowerShell activity, and unexpected system changes.

Network indicators include unusual outbound connections, beaconing, unexpected DNS requests, anomalous ports, large data transfers, and communication with suspicious infrastructure.

Identity indicators include impossible travel, unusual login times, repeated authentication failures, new privileged access, and authentication from unexpected devices.

An indicator is not automatically proof of compromise. Analysts should correlate multiple signals, establish context, investigate the affected asset, and determine whether the activity is benign, suspicious, or malicious.

## Security+ Scenario Method

When given an attack scenario, ask:

1. What asset is being targeted?
2. What weakness is present?
3. What attack vector is being used?
4. What threat actor behavior is described?
5. What evidence would appear in logs or endpoints?
6. What is the likely impact?
7. Is the appropriate response prevention, detection, mitigation, or remediation?

## Key Takeaways

Domain 2 connects the attacker, attack path, vulnerability, exploitation method, observable evidence, and defensive response. Learn the relationships rather than memorizing isolated definitions.
