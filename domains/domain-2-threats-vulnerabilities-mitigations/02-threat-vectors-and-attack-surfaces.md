# 02 — Threat Vectors and Attack Surfaces

## 1. Attack Surface

An **attack surface** is the collection of points where an attacker could potentially interact with, enter, manipulate, or extract information from an organization's environment.

Examples include internet-facing servers, remote-access services, endpoints, wireless networks, APIs, web applications, cloud resources, user accounts, third-party integrations, removable media, and physical facilities.

Reducing the attack surface is a core defensive objective. Every unnecessary service, exposed port, unused account, unmanaged endpoint, excessive permission, or unmonitored connection can create additional opportunities for exploitation.

## 2. Threat Vector

A **threat vector** is the method or path used to deliver an attack or gain access to a target. Examples include phishing email, malicious attachment, compromised website, stolen credentials, exposed remote service, USB device, supply-chain compromise, and vulnerable API.

Attack surface describes **where an organization can be attacked**. Threat vector describes **how the attack reaches the target**.

## 3. Common Attack Vectors

### Phishing

An attacker sends a deceptive communication designed to persuade a user to disclose credentials, execute malicious content, transfer money, or visit a malicious site.

### Valid accounts

Attackers may acquire legitimate credentials through phishing, credential stuffing, malware, password reuse, or data breaches. Because authentication succeeds, malicious activity can initially look like normal user behavior.

### Exposed services

Internet-facing services such as remote administration, VPN gateways, web servers, and APIs can become attack entry points when they contain vulnerabilities or are poorly configured.

### Removable media

USB drives and other removable devices can introduce malware or facilitate unauthorized data transfer. Organizations may mitigate this with device control, endpoint security, and user policies.

### Supply chain

An attacker may compromise a supplier, software package, update mechanism, managed service provider, or dependency so that the attack reaches downstream victims through a trusted relationship.

### Physical access

Physical access can allow an attacker to steal equipment, connect unauthorized devices, bypass some network controls, recover data from storage, or tamper with infrastructure.

## 4. Attack Surface Categories

### Digital attack surface

Includes software, systems, applications, accounts, APIs, cloud resources, network services, and digital identities.

### Physical attack surface

Includes buildings, server rooms, workstations, network equipment, removable media, ports, and other physically accessible assets.

### Human attack surface

Includes employees, contractors, administrators, customers, and other people who can be manipulated through social engineering or whose mistakes can create security weaknesses.

### Third-party attack surface

Includes vendors, partners, managed service providers, SaaS platforms, software dependencies, and integrations. A trusted relationship can introduce risk even when the organization's own systems are hardened.

## 5. Exposure Versus Vulnerability

An exposed service is not automatically vulnerable, and a vulnerability is not necessarily exploitable from every location.

A useful reasoning model is:

**Asset → Exposure → Vulnerability → Exploit → Impact**

For example, an internet-facing web server is exposed. If it runs vulnerable software, the vulnerability may be exploitable remotely. Successful exploitation could result in unauthorized access or data disclosure.

## 6. Reducing the Attack Surface

Common defensive measures include:

- Disable unnecessary services.
- Remove unused accounts.
- Close unnecessary network ports.
- Restrict administrative interfaces.
- Apply security patches.
- Segment networks.
- Enforce least privilege.
- Use strong authentication and MFA.
- Maintain accurate asset inventories.
- Remove unsupported software.
- Monitor external exposure.
- Control third-party connections.
- Apply secure configuration baselines.

## 7. Security+ Exam Focus

When a question asks for the best way to reduce attack surface, look for an action that removes unnecessary exposure rather than merely detecting an attack.

Examples:

- Removing an unused service reduces exposure.
- Network segmentation limits reachable resources.
- Least privilege reduces what a compromised identity can access.
- MFA reduces the usefulness of stolen passwords.
- Patching removes known exploitable weaknesses.

## 8. Key Takeaways

1. Attack surface is the set of potential points of attack.
2. Attack vector is the method used to reach or exploit a target.
3. Human, physical, digital, and third-party surfaces can all introduce risk.
4. Reducing unnecessary exposure is generally preferable to relying exclusively on detection.
5. Asset inventory and configuration management are foundational to attack-surface reduction.
