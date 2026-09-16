# 02 — Threat Vectors and Attack Surfaces

## 1. Introduction

After understanding **who the threat actors are and why they attack**, the next question is: **How can an attacker reach the organization?**

This is where the concepts of **attack surface** and **threat vector** become important.

An organization can have thousands of computers, applications, identities, network services, cloud resources, employees, suppliers, and physical locations. Every place where an attacker can interact with those assets represents potential exposure. Attackers then use a particular method or path to exploit that exposure.

Understanding these concepts allows a security professional to move from a general statement such as "the company is vulnerable" to a much more useful analysis:

**What is exposed? → How can it be reached? → What weakness exists? → What can happen if it is exploited? → How can the exposure or weakness be reduced?**

---

# 2. Attack Surface

An **attack surface** is the collection of points through which an attacker could potentially interact with, access, manipulate, disrupt, or extract information from an organization's environment.

Think of an organization's attack surface as all the doors, windows, entrances, and service entrances of a building. A building with one locked entrance has fewer possible entry points than a building with dozens of unlocked doors.

In cybersecurity, the doors may be:

- Internet-facing servers
- Open network ports
- VPN gateways
- Remote administration interfaces
- Web applications
- APIs
- Cloud storage
- User accounts
- Wireless networks
- Endpoints
- Mobile devices
- Third-party connections
- Software dependencies
- Physical ports
- Removable media

The goal is not to eliminate every attack surface because some exposure is required for normal business operations. The goal is to **reduce unnecessary exposure and appropriately protect the exposure that must remain**.

---

# 3. Why Attack Surface Matters

Every exposed component potentially creates another opportunity for an attacker.

Consider a company that operates:

- 500 laptops
- 20 servers
- 10 internet-facing applications
- 4 VPN gateways
- 3 cloud environments
- 100 SaaS integrations
- 50 privileged accounts
- 8 wireless networks

The security team cannot assume that protecting the firewall alone protects the organization. Each component can contain weaknesses or provide an attacker with a path toward a more valuable target.

For example:

`Internet → Vulnerable VPN → Internal Network → Compromised Workstation → Privileged Account → Critical Server`

The attacker may never directly attack the critical server from the internet. They can enter through a less protected part of the attack surface and move toward the valuable asset.

This is why **attack-surface management and asset inventory are foundational security activities**.

---

# 4. Threat Vector

A **threat vector** is the method, mechanism, or path used to deliver an attack or gain access to a target.

The distinction is:

**Attack surface = Where the organization can potentially be attacked.**

**Threat vector = How the attacker reaches or attacks the target.**

### Example

A company's employee email accounts are part of its attack surface.

The attacker sends a deceptive email containing a malicious link.

The **email account/user environment is part of the attack surface**.

The **phishing email is the threat vector**.

Another example:

A web server exposed to the internet is part of the attack surface. An attacker sends a malicious HTTP request exploiting a vulnerable application component. The malicious request is the threat vector.

---

# 5. Attack Surface vs Attack Vector

| Concept | Meaning | Example |
|---|---|---|
| Attack surface | Potential points of interaction or exposure | Internet-facing VPN, endpoint, API |
| Threat vector | Method/path used to attack | Phishing, stolen credentials, exploit |
| Vulnerability | Weakness that can be exploited | Unpatched software |
| Exploit | Technique/code that takes advantage of a weakness | Malicious request targeting the vulnerability |
| Impact | Result of successful exploitation | Data theft, outage, unauthorized access |

A complete attack chain can therefore look like:

**Asset → Exposure → Threat Vector → Vulnerability → Exploitation → Impact**

Not every exposed asset is vulnerable, and not every vulnerability is remotely exploitable. Context matters.

---

# 6. Digital Attack Surface

The **digital attack surface** consists of technology and information systems that can be interacted with electronically.

Examples include:

- Servers
- Workstations
- Mobile devices
- Operating systems
- Applications
- Databases
- APIs
- Network services
- Cloud resources
- User accounts
- Authentication systems
- Software dependencies
- DNS services
- Email systems

### Example

Suppose a web application exposes an API endpoint to the internet. The API is required for business operations, so it cannot simply be removed.

The security objective becomes protecting the necessary exposure using controls such as:

- Strong authentication
- Authorization
- Input validation
- Rate limiting
- Secure coding
- TLS
- Logging
- API gateways
- Web application firewalls where appropriate
- Vulnerability management

This illustrates an important principle: **attack-surface reduction does not always mean removing the service. It can also mean reducing unnecessary functionality and protecting the exposure that must remain.**

---

# 7. Physical Attack Surface

The **physical attack surface** consists of locations, equipment, interfaces, and assets that can be physically accessed or manipulated.

Examples include:

- Server rooms
- Workstations
- Network switches
- Wireless access points
- USB ports
- Network wall ports
- Backup media
- Printed documents
- Security appliances
- Unattended laptops
- Building entrances

### Why physical security matters

A technically secure system can still be compromised if an attacker obtains physical access.

For example, an attacker who steals an unencrypted laptop may bypass many network security controls because they physically possess the storage device.

Physical controls include:

- Locks
- Badges
- Guards
- Cameras
- Mantraps
- Access logs
- Secure server rooms
- Cable locks
- Device encryption
- Port controls

---

# 8. Human Attack Surface

People are part of the security boundary.

Employees and administrators may be targeted because humans can be manipulated, deceived, pressured, or simply make mistakes.

Examples include:

- Phishing
- Spear phishing
- Vishing
- Smishing
- Pretexting
- Tailgating
- Credential disclosure
- Accidental data exposure
- Misconfiguration

### Example

A company may have strong firewalls and endpoint security, but an attacker convinces an employee to reveal an MFA code during a social-engineering call.

The technical controls may be functioning correctly; the attacker has instead targeted the human attack surface.

Reducing human attack-surface risk requires:

- Security awareness
- Phishing-resistant authentication
- Clear verification procedures
- Least privilege
- Reporting mechanisms
- Administrative controls
- Technical controls that reduce the consequences of human mistakes

---

# 9. Third-Party Attack Surface

Organizations increasingly depend on external entities.

Examples include:

- Cloud providers
- SaaS platforms
- Managed service providers
- Software vendors
- Contractors
- Business partners
- Payment processors
- Software libraries
- Hardware suppliers
- APIs

These relationships create a **third-party attack surface**.

### Why third parties create risk

Your organization may have excellent security while a connected supplier has weaker security.

An attacker may therefore target the supplier instead of attacking your organization directly.

### Example

Suppose a company receives software updates from a trusted vendor. If the vendor's update infrastructure is compromised, malicious code could potentially reach customers through a trusted distribution mechanism.

This is a supply-chain security problem.

Controls include:

- Vendor risk assessments
- Contractual security requirements
- Security questionnaires
- Independent assurance reports
- Software provenance controls
- Dependency management
- Monitoring
- Least-privilege integrations
- Third-party access reviews

---

# 10. Common Threat Vectors

## 10.1 Phishing

Phishing uses deceptive communications to manipulate a victim into performing an action.

The attacker may attempt to:

- Steal credentials
- Deliver malware
- Capture payment information
- Redirect a victim to a fake website
- Obtain MFA approval
- Initiate an unauthorized financial transaction

Phishing is especially effective because it targets both technology and human decision-making.

---

## 10.2 Stolen or Valid Accounts

A valid account can become a threat vector when an attacker obtains legitimate credentials.

Sources may include:

- Phishing
- Credential stuffing
- Password reuse
- Malware
- Data breaches
- Password spraying
- Social engineering

This is dangerous because traditional security controls may see a successful authentication rather than an obvious exploit.

Detection therefore requires contextual analysis such as:

- Login location
- Device identity
- Login time
- Authentication method
- Resource accessed
- Behavioral history

---

## 10.3 Exposed Network Services

Internet-facing services can provide direct entry points.

Examples include:

- Remote administration
- VPN gateways
- Web servers
- Mail servers
- APIs
- Remote desktop services
- Management interfaces

An exposed service is not automatically insecure. Exposure becomes dangerous when the service is unnecessary, poorly configured, weakly authenticated, unpatched, or vulnerable.

---

## 10.4 Removable Media

USB drives and other removable devices can introduce malware or facilitate unauthorized data transfer.

A malicious USB device may attempt to:

- Deliver malware
- Exploit a device interface
- Capture information
- Transfer sensitive files

Defensive measures include device-control policies, endpoint security, disabling unnecessary removable-media functionality, encryption, and user awareness.

---

## 10.5 Supply-Chain Compromise

A supply-chain attack targets a trusted supplier, software dependency, service provider, update mechanism, or other upstream relationship.

The attacker attempts to compromise the trusted path so that downstream victims receive malicious or compromised content.

The major security lesson is that **trust relationships can extend the attack surface beyond assets directly controlled by the organization**.

---

## 10.6 Physical Access

Physical access can bypass or weaken logical controls.

An attacker with physical access may attempt to:

- Steal devices
- Connect rogue hardware
- Access network ports
- Remove storage media
- Observe sensitive information
- Tamper with equipment
- Install unauthorized devices

Physical controls therefore form an important layer of defense in depth.

---

# 11. Exposure vs Vulnerability

These concepts are frequently confused.

### Exposure

Exposure means an asset or service is reachable or visible to a potential attacker.

### Vulnerability

A vulnerability is a weakness that can be exploited.

### Example

A web server is publicly reachable.

That means it is **exposed**.

Suppose the server runs an outdated application containing a remotely exploitable vulnerability.

Now there is both **exposure and vulnerability**.

The attacker may exploit the weakness through the exposed service.

Therefore:

**Exposure does not automatically mean vulnerability.**

However, unnecessary exposure increases the opportunities an attacker has to discover and potentially exploit weaknesses.

---

# 12. Attack Surface Reduction

Attack-surface reduction means decreasing unnecessary opportunities for unauthorized interaction.

## 12.1 Remove unnecessary services

If an organization does not need a service, disabling or removing it eliminates a potential attack path.

Example:

If a server does not require FTP, leaving FTP enabled creates unnecessary exposure.

## 12.2 Close unnecessary ports

Open ports are not automatically vulnerabilities, but unnecessary listening services increase exposure.

## 12.3 Remove unused accounts

Old accounts can become attractive targets because they may remain enabled without active owners.

## 12.4 Reduce privileges

Least privilege limits what a compromised identity can access.

## 12.5 Patch vulnerable systems

Patching removes known weaknesses and reduces the likelihood that exposed services can be exploited through known vulnerabilities.

## 12.6 Segment networks

Segmentation prevents an attacker who compromises one area from automatically reaching every other system.

## 12.7 Maintain asset inventory

An organization cannot secure assets it does not know exist.

Inventory should cover relevant:

- Hardware
- Software
- Cloud resources
- Accounts
- Applications
- Network services
- Third-party integrations

## 12.8 Secure remote access

Remote access should use strong authentication, authorization, encryption, monitoring, and appropriate access restrictions.

## 12.9 Control third-party access

External organizations should receive only the access they need, for only as long as needed.

---

# 13. Attack Surface Management Process

A mature approach can be viewed as a continuous cycle:

**Discover → Inventory → Classify → Assess → Reduce → Monitor → Reassess**

### Discover

Find assets and externally visible services.

### Inventory

Record ownership, location, software, purpose, and connectivity.

### Classify

Determine business criticality and data sensitivity.

### Assess

Identify vulnerabilities, misconfigurations, unnecessary exposure, and weak access controls.

### Reduce

Remove unnecessary services, close exposure, patch systems, segment networks, and reduce privileges.

### Monitor

Continuously look for newly exposed services, configuration changes, new assets, and suspicious activity.

### Reassess

Attack surfaces change continuously. A new application, cloud resource, vendor, or remote-access service can create new exposure.

---

# 14. Attack Chain Example

Consider a company with an internet-facing VPN gateway.

### Step 1 — Exposure

The VPN gateway is intentionally reachable from the internet.

### Step 2 — Threat vector

An attacker sends phishing messages to employees and obtains a valid VPN credential.

### Step 3 — Initial access

The attacker authenticates to the VPN.

### Step 4 — Discovery

The attacker identifies internal systems that the account can reach.

### Step 5 — Privilege escalation

The attacker attempts to obtain greater privileges.

### Step 6 — Lateral movement

The attacker moves toward additional systems.

### Step 7 — Impact

The attacker steals data or disrupts operations.

Notice that the VPN itself was not necessarily the vulnerability. It was part of the **attack surface** and provided a path into the environment. The stolen credentials were the immediate attack vector.

This distinction is important in Security+ scenario questions.

---

# 15. Defense in Depth and Attack Surface

Attack-surface reduction and defense in depth work together.

Suppose an organization cannot remove an internet-facing application because customers require it.

The organization can reduce risk using multiple controls:

`Internet → Firewall → WAF → Application Authentication → Authorization → Input Validation → Database Access Controls → Logging/SIEM`

The application remains exposed because business requirements require it, but multiple layers reduce the probability and impact of successful exploitation.

This is a key security principle:

**Not every attack surface can be eliminated; necessary exposure must be controlled.**

---

# 16. Common Mistakes

### Mistake 1 — Treating attack surface and attack vector as synonyms

They are different.

**Surface = where.**

**Vector = how.**

### Mistake 2 — Assuming every exposed service is vulnerable

Exposure and vulnerability are separate concepts.

### Mistake 3 — Assuming closing one port secures the organization

Attackers can use other paths, including users, cloud resources, APIs, third parties, and stolen credentials.

### Mistake 4 — Ignoring the human attack surface

Users are part of the organization's security boundary.

### Mistake 5 — Ignoring third-party relationships

Trusted vendors and integrations can introduce significant exposure.

### Mistake 6 — Believing attack-surface reduction means disabling everything

Business systems must remain available. Security is about managing necessary exposure while removing unnecessary exposure.

---

# 17. Security+ Scenario Analysis

When a question asks about an attack path, work through the following sequence:

1. **What asset is exposed?**
2. **Who can reach it?**
3. **How can it be reached?**
4. **What vulnerability or weakness exists?**
5. **What privileges are available after access?**
6. **Can the attacker move laterally?**
7. **What impact could occur?**
8. **Which control reduces the relevant exposure or weakness?**

### Example question logic

If a company has an unnecessary internet-facing service and asks for the most direct attack-surface reduction measure, removing or disabling the unnecessary service is more directly related to reducing exposure than simply adding another detection mechanism.

If the service must remain available, then the appropriate answer may involve hardening, patching, access control, segmentation, monitoring, or another compensating control depending on the scenario.

---

# 18. Key Takeaways

1. The **attack surface** is the collection of potential points through which an attacker can interact with an environment.
2. A **threat vector** is the method or path used to reach or attack a target.
3. Digital, physical, human, and third-party environments can all form part of an organization's attack surface.
4. Exposure and vulnerability are related but different concepts.
5. An exposed service is not automatically vulnerable.
6. A vulnerability becomes more dangerous when it is reachable through an accessible attack surface.
7. Asset inventory is fundamental because unknown assets cannot be reliably secured.
8. Attack-surface reduction includes removing unnecessary services, closing unnecessary exposure, reducing privileges, patching, segmentation, and controlling third-party access.
9. Necessary business services may remain exposed, so security controls must protect the required attack surface.
10. Attack-surface management is continuous because new assets, applications, identities, vendors, and services constantly change the environment.
11. In scenario questions, remember: **surface = where; vector = how; vulnerability = weakness; exploit = method of taking advantage of the weakness; impact = result.**
