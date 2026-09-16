# 08 — Wireless, Mobile, and Specialized Attacks

## 1. Introduction

Wireless, mobile, IoT, and other specialized technologies significantly expand an organization's attack surface.

A traditional wired endpoint generally requires physical or network connectivity through a controlled infrastructure. Wireless and mobile technologies introduce additional communication mechanisms, radio interfaces, sensors, proximity features, application ecosystems, and management dependencies.

Security+ questions commonly test whether you can identify:

- The technology being targeted
- The attack technique
- The trust relationship being abused
- The security weakness involved
- The appropriate defensive control

Important categories include:

- Wi-Fi attacks
- Bluetooth attacks
- Mobile-device attacks
- NFC and proximity attacks
- IoT attacks
- Specialized embedded systems
- Operational technology (OT) and industrial systems
- Wearables and connected devices

---

# 2. Wireless Network Fundamentals

Wireless LANs use radio communication rather than physical Ethernet connections between clients and access points.

A typical enterprise wireless environment contains:

**Wireless client → Access Point → Wireless infrastructure → Internal network/services**

Security can be applied at several points:

- Wireless authentication
- Wireless encryption
- Access-point configuration
- Network segmentation
- Endpoint security
- Identity management
- Monitoring

Wireless security is particularly important because an attacker does not necessarily need physical access to a network port to interact with radio-based communications.

---

# 3. Wireless Attack Surface

Wireless attack surfaces can include:

- Access points
- Wireless clients
- SSIDs
- Authentication mechanisms
- Encryption protocols
- Management frames
- Radio coverage areas
- Guest networks
- Bluetooth interfaces
- Mobile hotspots

An organization should therefore treat wireless infrastructure as an extension of the enterprise network rather than as an isolated convenience feature.

---

# 4. Evil Twin Attack

An **evil twin** is a fraudulent wireless access point designed to impersonate a legitimate wireless network.

The attacker attempts to make users believe that the malicious access point is the organization's legitimate network.

### Simplified attack flow

**Legitimate Wi-Fi exists → Attacker creates an impersonating AP → Victim connects → Attacker can observe or manipulate traffic depending on protections → Credentials or sensitive information may be exposed**

The exact impact depends on whether applications use TLS correctly, whether authentication is protected, and what traffic the victim sends.

### Why users may connect

An attacker may imitate:

- SSID name
- Network branding
- Expected location
- Captive portal appearance

### Mitigation

- Enterprise wireless authentication
- Certificate validation where applicable
- User awareness
- Wireless monitoring
- Network access controls
- Avoid trusting unknown networks
- Strong encryption

### Exam clue

If the attacker **impersonates a legitimate Wi-Fi network to deceive users**, think **evil twin**.

---

# 5. Rogue Access Point

A **rogue access point** is an unauthorized wireless access point operating within or connected to an organization's environment.

The critical issue is that the device creates an **unapproved wireless path into or around security controls**.

A rogue AP may be installed intentionally by an attacker or accidentally by an employee.

### Why it is dangerous

A rogue AP may:

- Bypass approved wireless security
- Provide unauthorized network access
- Create an unmanaged entry point
- Allow attackers to intercept traffic
- Circumvent segmentation

### Mitigation

- Wireless intrusion detection/prevention
- Access-point inventory
- Network access control
- Physical security
- Port security
- Regular wireless surveys
- Administrative policy prohibiting unauthorized APs

---

# 6. Evil Twin vs Rogue AP

These terms are related but should not be treated as identical.

| Characteristic | Evil Twin | Rogue AP |
|---|---|---|
| Primary purpose | Impersonate a legitimate network | Provide an unauthorized wireless connection |
| Main deception | Mimics a trusted SSID/network | May or may not impersonate another network |
| Typical target | Wireless users | Organization/network environment |
| Core problem | Deception | Unauthorized network access |

### Exam shortcut

**Impersonation → Evil Twin**

**Unauthorized AP → Rogue AP**

A device can potentially exhibit characteristics of both, so read the scenario carefully.

---

# 7. Deauthentication and Disassociation Attacks

Wireless networks use management frames to coordinate connections between clients and access points.

Attackers may abuse these mechanisms to disrupt wireless connectivity.

### Deauthentication attack

A malicious actor sends forged or otherwise unauthorized deauthentication messages to cause clients to disconnect from a wireless network.

### Disassociation attack

A malicious actor attempts to cause a client to stop being associated with an access point.

### Potential impact

- Wireless service disruption
- Forced reconnection attempts
- User inconvenience
- Opportunities for additional attacks in some scenarios

### Mitigation

Modern wireless deployments can use **Protected Management Frames (PMF)**, associated with IEEE 802.11 management-frame protection capabilities, to reduce exposure to certain management-frame attacks.

Wireless monitoring can also identify abnormal disconnection patterns.

---

# 8. Wi-Fi Security Protocols

Understanding the evolution of wireless security is important.

### WEP

**Wired Equivalent Privacy (WEP)** is an obsolete wireless security protocol with serious cryptographic weaknesses. It should not be used in modern secure deployments.

### WPA

**Wi-Fi Protected Access (WPA)** was introduced as an improvement over WEP but older WPA implementations should not be treated as equivalent to current standards.

### WPA2

WPA2 provides substantially stronger security than WEP and supports modern enterprise authentication architectures such as 802.1X/EAP.

### WPA3

WPA3 provides newer security mechanisms and is the current generation of Wi-Fi security for supported deployments.

### Enterprise authentication

Enterprise wireless networks commonly use **802.1X** with an authentication framework such as EAP and a backend authentication service.

This allows individual users/devices to authenticate rather than relying only on a shared wireless password.

---

# 9. Wireless Encryption vs Authentication

These concepts are different.

### Authentication

Determines whether a user or device is permitted to connect.

### Encryption

Protects wireless communications against unauthorized disclosure while data is transmitted.

A secure wireless architecture needs both appropriate authentication and appropriate cryptographic protection.

---

# 10. Wireless Credential Attacks

Wireless networks may also be targeted through credential attacks.

Potential weaknesses include:

- Weak pre-shared keys
- Reused passwords
- Weak enterprise authentication configuration
- Phishing for wireless credentials
- Misconfigured authentication servers

### Mitigation

- Strong unique credentials
- Enterprise authentication where appropriate
- MFA for associated enterprise identities where supported
- Certificate validation
- Credential monitoring
- User awareness

---

# 11. Bluetooth Security

Bluetooth provides short-range wireless communication between devices.

Examples include:

- Headsets
- Keyboards
- Mice
- Smartphones
- Vehicles
- Medical devices
- IoT devices

Bluetooth introduces an additional radio interface that must be secured.

### Potential weaknesses

- Weak or inappropriate pairing configurations
- Vulnerable Bluetooth implementations
- Unnecessary discoverability
- Unauthorized devices
- Outdated firmware
- Excessive permissions

### Defensive controls

- Disable Bluetooth when unnecessary
- Keep device firmware updated
- Use secure pairing mechanisms
- Restrict discoverability when practical
- Remove unused pairings
- Manage Bluetooth centrally on enterprise devices

---

# 12. Bluetooth Attack Concepts

Security+ may use general terms for Bluetooth-related attacks rather than requiring knowledge of a single exploit implementation.

Possible attack categories include:

- Unauthorized pairing
- Eavesdropping where protections are insufficient
- Device impersonation
- Malicious Bluetooth applications or devices
- Exploitation of vulnerable Bluetooth implementations

The important principle is to recognize Bluetooth as an additional attack surface rather than assuming short range makes it inherently secure.

---

# 13. Mobile Device Security

Mobile devices are particularly valuable targets because one device can contain:

- Corporate email
- Authentication tokens
- Password managers
- Contact information
- Documents
- Financial information
- Photos
- Location information
- Application data
- Hardware sensors

Mobile devices also move between trusted and untrusted environments.

### Common mobile risks

- Malicious applications
- Phishing
- Lost or stolen devices
- Outdated operating systems
- Weak device authentication
- Insecure Wi-Fi
- SIM-related attacks
- Excessive application permissions
- Malicious profiles/configurations
- Unauthorized device modification

---

# 14. Malicious Mobile Applications

A malicious application may abuse its permissions to access information or perform actions that the user did not intend.

### Potential impact

Depending on the platform and granted permissions, a malicious application may attempt to access:

- Contacts
- Messages
- Files
- Camera
- Microphone
- Location
- Credentials

### Mitigation

- Use trusted application sources
- Mobile application management
- Mobile Device Management (MDM)
- Application allowlisting where appropriate
- Permission management
- Endpoint/mobile threat protection
- User awareness
- Timely OS and application updates

---

# 15. Mobile Device Management (MDM)

**Mobile Device Management (MDM)** allows an organization to centrally manage supported mobile devices.

Depending on the platform and deployment, MDM can enforce policies such as:

- Screen-lock requirements
- Encryption requirements
- Application restrictions
- Configuration profiles
- Remote lock
- Remote wipe
- Certificate deployment
- Network configuration
- Device compliance checks

MDM is particularly important for organizations using BYOD or large mobile fleets.

---

# 16. Bring Your Own Device (BYOD)

**BYOD** allows employees to use personally owned devices for organizational work.

BYOD introduces a difficult security boundary because the organization must protect corporate information on a device it may not fully control.

### Risks

- Personal applications interacting with corporate data
- Lost or stolen devices
- Unsupported operating systems
- Unmanaged configurations
- Privacy concerns
- Data leakage

### Mitigation

- MDM or appropriate endpoint management
- Mobile application management
- Containerization/work profiles where supported
- Corporate data encryption
- Access policies based on device compliance
- Remote revocation of organizational access

---

# 17. SIM Swapping

**SIM swapping** occurs when an attacker convinces or manipulates a telecommunications provider into transferring a victim's mobile number to a SIM controlled by the attacker.

### Why it matters

If accounts rely on SMS messages for authentication or password recovery, control of the phone number may help an attacker receive those messages.

### Potential targets

- Email accounts
- Financial accounts
- Social media
- Cloud services
- Other systems using SMS-based authentication

### Mitigation

- Prefer phishing-resistant or stronger MFA where available
- Avoid relying solely on SMS for high-value authentication
- Protect carrier accounts
- Require additional verification for SIM/account changes
- Monitor unexpected loss of cellular service

### Exam clue

**Phone number transferred to an attacker-controlled SIM → SIM swapping.**

---

# 18. Mobile Phishing and Smishing

Mobile users are frequently targeted through messaging platforms.

### Smishing

**Smishing** is phishing delivered through SMS or similar messaging channels.

Examples include fraudulent messages claiming:

- A package requires action
- A bank account needs verification
- An account will be suspended
- A payment failed

### Defense

- Do not trust unexpected links
- Verify through an independently obtained official channel
- Use mobile/web security controls
- Report suspicious messages
- Use strong authentication

---

# 19. Mobile Device Loss and Theft

Physical loss can become a cybersecurity incident when a device contains sensitive information or active authentication sessions.

### Defensive controls

- Full-device encryption
- Strong screen-lock authentication
- Automatic locking
- Remote lock
- Remote wipe
- MDM enforcement
- Strong authentication
- Minimal local data storage

The goal is to reduce the value of the physical device to an attacker.

---

# 20. Rooting and Jailbreaking

**Rooting** and **jailbreaking** modify mobile operating systems to bypass or alter restrictions imposed by the platform vendor.

These modifications can increase user control but may weaken security assumptions and enterprise controls.

### Security concerns

- Bypassed application restrictions
- Reduced platform integrity
- Increased malware exposure
- Security-control circumvention
- Unsupported configurations

Enterprise environments may therefore block access from modified devices.

---

# 21. NFC and Proximity Technologies

**Near Field Communication (NFC)** enables short-range communication between compatible devices or tags.

Uses include:

- Contactless payments
- Access badges
- Device pairing
- Identification
- Information exchange

### Security considerations

Because NFC often supports transactions or authentication-related interactions, attackers may target:

- Malicious tags
- Unauthorized transactions
- Relay scenarios
- Weak application authorization
- Device configuration weaknesses

### Defensive controls

- Transaction confirmation
- Secure application design
- Device authentication
- Platform security controls
- User awareness

---

# 22. Relay Attacks

A **relay attack** extends communication between two legitimate parties so that they believe they are communicating directly even though an attacker is forwarding the communication.

Relay concepts can appear in proximity technologies, authentication systems, and wireless environments.

The defining characteristic is that the attacker **relays legitimate communication** rather than necessarily breaking the underlying cryptography.

### Defense

Depending on the technology, controls can include:

- Distance or proximity verification
- Transaction confirmation
- Time/distance constraints
- Strong protocol design
- Additional authentication factors

---

# 23. IoT Security

**Internet of Things (IoT)** devices include connected sensors, cameras, appliances, environmental systems, smart devices, and industrial or commercial equipment.

IoT devices often have security challenges caused by:

- Limited computing resources
- Long operational lifetimes
- Infrequent patching
- Default credentials
- Proprietary software
- Weak management interfaces
- Poor asset visibility
- Limited logging
- Physical exposure

---

# 24. IoT Default Credentials

One of the common IoT weaknesses is the use of default usernames and passwords.

If devices are deployed without changing default credentials, an attacker may gain unauthorized access using credentials that are publicly known or easily discoverable.

### Mitigation

- Change default credentials before deployment
- Use unique credentials
- Disable unnecessary accounts
- Restrict management interfaces
- Use centralized identity controls where supported

---

# 25. IoT Network Segmentation

IoT devices should generally not have unrestricted access to the same network resources as critical servers and administrative systems.

A common architecture is:

**IoT devices → Dedicated network/VLAN → Controlled firewall rules → Required services only**

### Benefits

Segmentation can limit lateral movement if an IoT device is compromised.

It also makes monitoring and access-control policies easier to apply.

---

# 26. IoT Firmware and Patch Management

IoT devices may run firmware rather than a traditional desktop operating system.

Organizations should therefore track:

- Device model
- Firmware version
- Vendor support status
- Vulnerability status
- Update availability
- Maintenance requirements

Unsupported devices should be replaced or isolated when appropriate.

---

# 27. Embedded Systems

An **embedded system** is a computing system designed to perform a specific function within a larger device.

Examples include:

- Automotive control systems
- Medical devices
- Industrial controllers
- Smart appliances
- Network equipment

Security challenges may include:

- Long lifecycles
- Limited resources
- Specialized operating environments
- Difficult patching
- Physical access
- Safety requirements

Security must therefore be considered across the entire lifecycle.

---

# 28. Industrial Control Systems (ICS) and OT

**Operational Technology (OT)** refers broadly to systems that monitor or control physical processes.

**Industrial Control Systems (ICS)** are a major category of OT.

Examples include systems controlling:

- Manufacturing
- Energy
- Water treatment
- Transportation
- Industrial processes

### Security priority

Traditional IT environments often prioritize confidentiality, integrity, and availability according to business requirements.

In OT/ICS, **safety and continuous availability can be especially critical** because a security event may affect physical processes.

### Security considerations

- Network segmentation
- Strict change control
- Asset inventory
- Controlled remote access
- Monitoring
- Vendor access management
- Specialized patch testing
- Physical security

Security controls must be implemented carefully because aggressive changes can disrupt physical operations.

---

# 29. Supervisory Control and Data Acquisition (SCADA)

**SCADA** systems support monitoring and control of distributed industrial processes.

A simplified architecture may contain:

**Sensors/field devices → Controllers → SCADA system → Operator interface**

Security concerns include:

- Legacy systems
- Remote connectivity
- Weak authentication
- Inadequate segmentation
- Vendor access
- Limited patching opportunities

The appropriate response should account for operational and safety requirements.

---

# 30. Specialized Medical Devices

Medical devices may contain software, network connectivity, sensitive patient information, and safety-critical functionality.

Security controls must therefore consider both cybersecurity and patient safety.

Potential controls include:

- Asset inventory
- Network segmentation
- Vendor coordination
- Secure configurations
- Controlled administrative access
- Monitoring
- Risk-based patch management

An organization should not blindly apply a security update to a safety-critical device without understanding operational and vendor implications.

---

# 31. Wearable Technology

Wearables may collect or transmit information through Bluetooth, Wi-Fi, cellular connectivity, or companion applications.

Potential risks include:

- Unauthorized access
- Data leakage
- Weak authentication
- Malicious applications
- Privacy exposure
- Lost devices

Organizations should evaluate whether wearables are permitted and how corporate information can interact with them.

---

# 32. Specialized Vehicle and Automotive Systems

Modern vehicles may contain numerous interconnected electronic control systems and wireless interfaces.

Potential security concerns include:

- Wireless interfaces
- Bluetooth
- Cellular connectivity
- Diagnostic interfaces
- Third-party applications
- Insecure firmware

Because vehicle systems can influence physical operations, compromise can have consequences beyond traditional data theft.

---

# 33. Physical Security and Specialized Devices

Wireless and IoT security cannot be separated completely from physical security.

An attacker with physical access may be able to:

- Reset a device
- Connect unauthorized hardware
- Extract removable storage
- Access exposed ports
- Tamper with sensors
- Install unauthorized devices

Therefore, specialized technology security may require:

- Locked equipment rooms
- Tamper protection
- Port controls
- Surveillance
- Restricted maintenance access
- Asset tracking

---

# 34. Wireless and Specialized Attack Detection

Detection should combine technical telemetry with physical and administrative information.

### Wireless monitoring

Can identify:

- Unauthorized access points
- Unexpected SSIDs
- Abnormal management-frame activity
- Rogue devices
- Unusual wireless clients

### Endpoint/mobile telemetry

Can identify:

- Malicious applications
- Configuration changes
- Unsupported devices
- Rooted/jailbroken devices
- Suspicious authentication activity

### Network telemetry

Can identify:

- Unexpected IoT connections
- Lateral movement
- Unusual outbound communication
- Unauthorized protocols

### Asset management

Can identify:

- Unknown devices
- Unsupported firmware
- Devices missing security updates
- Unexpected hardware changes

---

# 35. Specialized Device Security Architecture

A practical security architecture can follow this sequence:

**Discover → Inventory → Classify → Assess → Segment → Harden → Monitor → Patch/Replace → Reassess**

### Discover

Identify wireless, mobile, IoT, and specialized systems.

### Inventory

Record ownership, location, model, software/firmware, and connectivity.

### Classify

Determine the sensitivity and operational importance of each device.

### Assess

Identify vulnerabilities, unsupported software, weak credentials, and unnecessary services.

### Segment

Place devices into appropriate network zones.

### Harden

Remove unnecessary services, change defaults, and enforce secure configurations.

### Monitor

Collect available telemetry and detect unexpected behavior.

### Patch or replace

Maintain supported firmware and replace devices that cannot be securely maintained.

### Reassess

Security requirements change as devices and threats change.

---

# 36. Detailed Security+ Scenario — Evil Twin

### Scenario

Employees at a conference see a wireless network with the same name as their company's normal SSID. Several employees connect and are presented with a convincing login page.

### Analysis

The defining clue is **impersonation of a legitimate wireless network**.

This indicates an **evil twin** attack.

### Defensive response

- Enterprise authentication
- Certificate validation
- Wireless monitoring
- User awareness
- Avoidance of untrusted captive portals

---

# 37. Detailed Security+ Scenario — Rogue AP

### Scenario

A security team discovers an unauthorized wireless access point connected to an Ethernet port inside an office.

### Analysis

The central issue is an **unauthorized AP connected to the organization's environment**.

This is a **rogue access point**.

### Defensive response

- Remove/quarantine the unauthorized device
- Identify how it was connected
- Investigate associated clients
- Deploy wireless monitoring
- Restrict network access
- Enforce policy and physical controls

---

# 38. Detailed Security+ Scenario — Deauthentication

### Scenario

A wireless monitoring system detects a large number of abnormal management frames causing clients to repeatedly disconnect from an access point.

### Analysis

The repeated disconnections combined with management-frame activity indicate a likely **deauthentication/disassociation attack**.

### Defensive controls

- Protected Management Frames where supported
- Wireless monitoring
- Appropriate AP configuration
- Investigation of the source and affected clients

---

# 39. Detailed Security+ Scenario — SIM Swapping

### Scenario

A user's phone suddenly loses cellular service. Shortly afterward, the user receives notifications that an account's password-reset process has occurred using SMS verification.

### Analysis

Unexpected loss of cellular service combined with suspicious SMS-based account activity can indicate **SIM swapping**.

### Defensive response

- Contact the carrier through an independently verified channel
- Secure affected accounts
- Revoke active sessions where appropriate
- Replace SMS-only authentication with stronger methods
- Review account-recovery settings

---

# 40. Detailed Security+ Scenario — IoT Segmentation

### Scenario

An organization deploys hundreds of network-connected cameras. The security team places them on the same unrestricted network as domain controllers and sensitive application servers.

### Analysis

The primary architectural weakness is inadequate segmentation.

If a camera is compromised, unrestricted connectivity could make lateral movement easier.

### Better architecture

Place IoT devices into a dedicated network segment and permit only the communication required for their operation.

---

# 41. Detailed Security+ Scenario — OT/ICS

### Scenario

A manufacturing organization discovers a vulnerability in a controller that manages a production process. A security administrator proposes immediately rebooting and patching the controller during production.

### Analysis

The vulnerability should be addressed, but OT environments may have safety and availability requirements that make immediate uncontrolled changes inappropriate.

The organization should follow its OT change-management process, coordinate with the vendor where necessary, assess operational risk, and schedule controlled remediation.

### Exam lesson

For specialized systems, the technically obvious action may not be the operationally appropriate first step.

---

# 42. Wireless and Mobile Security Comparison

| Technology/Issue | Main Risk | Typical Defense |
|---|---|---|
| Evil twin | Wireless impersonation | Enterprise authentication, certificate validation, monitoring |
| Rogue AP | Unauthorized wireless path | Wireless monitoring, NAC, inventory |
| Deauthentication | Wireless disruption | Protected Management Frames, monitoring |
| Weak Wi-Fi security | Unauthorized access/interception | WPA2/WPA3, strong authentication |
| Bluetooth weakness | Unauthorized device interaction | Secure pairing, updates, restricted discoverability |
| Malicious mobile app | Data/permission abuse | Managed sources, MDM, permission controls |
| SIM swapping | Number/account takeover | Strong MFA, carrier protections |
| Lost mobile device | Data exposure | Encryption, screen lock, remote wipe |
| NFC/proximity abuse | Unauthorized transactions/relay | Secure protocol design, confirmation |
| IoT default credentials | Unauthorized device access | Unique credentials, hardening |
| IoT compromise | Lateral movement | Segmentation and restricted access |
| Unsupported firmware | Known vulnerabilities | Patch or replace |
| OT/ICS weakness | Operational/safety impact | Segmentation, controlled change, monitoring |

---

# 43. Common Exam Traps

### Trap 1: Evil twin vs rogue AP

Do not automatically call every unauthorized AP an evil twin.

- **Evil twin:** impersonates a legitimate network.
- **Rogue AP:** unauthorized access point in the environment.

### Trap 2: Wi-Fi encryption vs authentication

Encryption protects communications; authentication determines who or what is permitted to connect.

### Trap 3: SIM swapping vs phishing

Phishing may be the social-engineering technique used to steal credentials, while SIM swapping specifically involves transferring the victim's mobile number to another SIM.

### Trap 4: IoT security vs traditional endpoint security

IoT devices may have different patching, logging, lifecycle, and resource constraints. Inventory and segmentation are particularly important.

### Trap 5: OT patching

Do not assume that immediate patching without operational assessment is always the correct first action for safety-critical or availability-sensitive systems.

### Trap 6: Bluetooth range

Short-range communication does not mean zero security risk. Bluetooth remains an attack surface.

### Trap 7: BYOD

BYOD is not simply an employee convenience issue. It creates a governance, privacy, data-protection, and endpoint-management challenge.

---

# 44. Security+ Scenario Reasoning Framework

When a question involves wireless, mobile, or specialized technology, use this process.

### Step 1: Identify the technology

Is the scenario about:

- Wi-Fi?
- Bluetooth?
- Mobile phone?
- NFC?
- IoT?
- Embedded system?
- OT/ICS?

### Step 2: Identify the attack mechanism

Ask whether the attacker is:

- Impersonating a network
- Installing an unauthorized AP
- Disrupting wireless communication
- Stealing a phone number
- Abusing an application
- Exploiting default credentials
- Using an exposed management interface
- Attacking an unsegmented device

### Step 3: Identify the affected trust boundary

Determine whether the weakness affects:

- User identity
- Device identity
- Wireless network
- Internal network
- Application
- Physical process

### Step 4: Identify the most direct control

Examples:

**Evil twin → enterprise authentication/certificate validation**

**Rogue AP → wireless monitoring and network access controls**

**SIM swapping → stronger authentication and carrier protections**

**IoT compromise → segmentation and restricted access**

**Default credentials → change/remove defaults**

**Unsupported device → replace or isolate**

### Step 5: Consider operational requirements

For medical, industrial, automotive, and other specialized systems, consider:

- Safety
- Availability
- Vendor support
- Maintenance windows
- Change control

---

# 45. Key Takeaways

1. Wireless, mobile, IoT, and specialized technologies are part of the organization's attack surface.
2. Wireless security requires appropriate authentication, encryption, configuration, monitoring, and segmentation.
3. An **evil twin** impersonates a legitimate wireless network.
4. A **rogue AP** is an unauthorized access point operating in or connected to the environment.
5. Deauthentication and disassociation attacks abuse wireless management mechanisms to disrupt connections.
6. Protected Management Frames can reduce exposure to certain management-frame attacks.
7. WEP is obsolete and should not be used for modern secure wireless deployments.
8. WPA2 and WPA3 provide stronger security than WEP; enterprise environments can use 802.1X/EAP-based authentication.
9. Bluetooth is an additional attack surface and should be secured through appropriate pairing, updates, and configuration.
10. Mobile devices can contain credentials, corporate data, tokens, and sensitive personal information.
11. MDM provides centralized policy and device-management capabilities for organizational mobile fleets.
12. **SIM swapping** transfers a victim's mobile number to an attacker-controlled SIM and can undermine SMS-based authentication.
13. NFC and other proximity technologies require secure protocol design and transaction controls.
14. IoT devices commonly require strong inventory, unique credentials, segmentation, restricted management access, and lifecycle management.
15. Embedded and specialized systems may have long lifecycles and difficult patching requirements.
16. OT/ICS security must account for safety and operational availability in addition to conventional cybersecurity objectives.
17. Security controls for specialized systems should be implemented through controlled, risk-based processes.
18. The strongest general architecture for connected specialized devices is **inventory → harden → segment → monitor → maintain**.
19. Security+ scenarios are often solved by identifying the technology, attack mechanism, affected trust boundary, and most direct mitigation.
