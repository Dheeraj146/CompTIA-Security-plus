# IoT, ICS, and Embedded Systems

## Purpose

Internet of Things (IoT), Industrial Control Systems (ICS), Supervisory Control and Data Acquisition (SCADA), Operational Technology (OT), and embedded systems connect computing technology to physical environments. These systems can control machines, monitor industrial processes, operate building systems, manage utilities, and support transportation, healthcare, manufacturing, and other critical functions.

Their security architecture differs from conventional enterprise IT because a compromise may affect not only information systems but also **physical processes, equipment, production, human safety, and environmental conditions**.

A useful Security+ model is:

**Physical process → Device/controller → Network → Management system → Monitoring → Safety and recovery**

The central architectural challenge is balancing cybersecurity with availability, integrity, safety, reliability, and operational requirements.

---

## 1. Internet of Things (IoT)

**Internet of Things (IoT)** refers to connected physical devices that collect, process, transmit, or act on information.

Examples include:

- Smart cameras
- Smart locks
- Environmental sensors
- Smart appliances
- Wearable devices
- Connected vehicles
- Medical monitoring devices
- Building-management sensors
- Industrial sensors

An IoT device may contain:

- Sensors
- Embedded processors
- Firmware
- Network interfaces
- Local storage
- Web or mobile management interfaces
- Cloud connectivity

The device becomes part of the organization's attack surface once it is connected to a network.

---

## 2. Why IoT Security Is Challenging

IoT devices frequently have constraints that make traditional enterprise security controls difficult to implement.

Common challenges include:

- Limited CPU and memory
- Limited storage
- Proprietary firmware
- Infrequent updates
- Long operational lifetimes
- Default credentials
- Weak authentication
- Insecure communication
- Internet exposure
- Poor asset visibility
- Vendor dependency

A device may remain deployed for many years even though the vendor's security-update process is shorter than its expected operational life.

---

## 3. IoT Attack Surface

An IoT system can expose several attack surfaces:

```text
Physical Device
      |
      +── Firmware
      +── Local Interface
      +── Network Interface
      +── Web/API Interface
      +── Mobile Application
      +── Cloud Service
      +── Administrative Interface
```

An attacker does not necessarily need to attack the physical device directly. A vulnerable cloud API or management application can also provide a path into the IoT ecosystem.

Therefore, IoT security must consider the complete ecosystem rather than only the hardware.

---

## 4. Common IoT Vulnerabilities

### Default Credentials

Devices may ship with predefined usernames and passwords.

If these credentials are not changed, attackers can use publicly known or commonly tested credentials.

### Insecure Firmware

Firmware may contain exploitable vulnerabilities or outdated components.

### Unnecessary Services

Telnet, HTTP, debugging interfaces, or other unnecessary services increase attack surface.

### Weak Encryption

Sensitive device communications may be transmitted without adequate confidentiality or integrity protection.

### Poor Update Mechanisms

Some devices lack secure automatic updates or have difficult manual update processes.

### Weak Device Identity

If devices cannot be uniquely authenticated, unauthorized devices may communicate with trusted systems.

---

## 5. IoT Asset Inventory

An accurate inventory is fundamental to IoT security.

The organization should know:

- What devices exist
- Where they are located
- Who owns them
- What they control
- What firmware they run
- Which network they use
- What services they expose
- Which vendor supports them
- How they are updated
- What data they collect

Unknown devices represent unmanaged attack surface.

IoT asset inventory should therefore be integrated with broader asset-management processes.

---

## 6. IoT Network Segmentation

IoT devices should generally not be placed on the same unrestricted network as high-value enterprise systems.

A possible architecture is:

```text
Enterprise Users
      |
Corporate Network
      |
Firewall / Segmentation
      |
IoT Network
      |
IoT Devices
```

More granular designs may separate:

- Cameras
- Building systems
- Sensors
- Medical devices
- Industrial devices

Segmentation limits lateral movement if one device is compromised.

---

## 7. IoT Management Network

Management interfaces should be restricted to authorized administrators or management systems.

For example:

```text
Administrator
     ↓
Privileged Access Path
     ↓
Management Network
     ↓
IoT Management Interface
```

Ordinary user devices should not need direct access to administrative interfaces.

Controls can include:

- Firewall rules
- Network ACLs
- MFA where supported
- Dedicated management systems
- Jump hosts
- Role-based access
- Administrative logging

---

## 8. Secure IoT Communications

IoT communication should use secure protocols appropriate to the device's capabilities and operational requirements.

Security objectives include:

- Confidentiality
- Integrity
- Authentication
- Replay resistance where required

Examples of technologies that may support secure communication include TLS-protected application protocols and appropriately secured wireless protocols.

Legacy protocols without adequate protection may require compensating controls such as network isolation and controlled gateways.

---

## 9. IoT Firmware Security

Firmware is the software that controls an embedded device's hardware and core functionality.

Firmware security should consider:

- Vendor support
- Vulnerability history
- Secure update mechanisms
- Firmware authenticity
- Integrity verification
- Secure boot where supported
- Removal of debugging interfaces

A device that cannot securely receive updates may require stronger compensating controls elsewhere in the architecture.

---

## 10. Secure Boot

**Secure boot** is a mechanism designed to verify that authorized software or firmware is loaded during the device's startup process.

The goal is to reduce the risk of unauthorized or modified boot software executing.

It can contribute to platform integrity but does not replace:

- Network segmentation
- Authentication
- Patch management
- Application security
- Monitoring

---

## 11. Embedded Systems

An **embedded system** is a computing system designed as part of a larger device or product and usually performs a specific function.

Examples include:

- Automotive controllers
- Printers
- Routers
- Cameras
- Industrial controllers
- Medical equipment
- Appliances
- Building-control systems

Unlike general-purpose computers, embedded systems often have specialized hardware and software with strict operational requirements.

---

## 12. Embedded-System Security Constraints

Embedded systems may have:

- Limited processing resources
- Limited memory
- Specialized hardware
- Proprietary operating systems
- Long replacement cycles
- Limited security tooling
- Safety dependencies
- Difficult maintenance procedures

These constraints can prevent the use of conventional endpoint-security controls.

Security architecture may therefore require compensating controls.

---

## 13. Compensating Controls for Unpatchable Devices

If a legacy device cannot be patched, the organization should not simply ignore the vulnerability.

Possible compensating controls include:

- Network segmentation
- Firewall restrictions
- Application allowlisting where appropriate
- Protocol filtering
- Strict management access
- Monitoring
- Intrusion detection
- Physical access controls
- Controlled maintenance windows

The objective is to reduce the probability and impact of exploitation when the primary remediation option is unavailable.

---

## 14. Operational Technology (OT)

**Operational Technology (OT)** refers broadly to systems used to monitor or control physical processes.

Examples include systems used in:

- Manufacturing
- Energy
- Water treatment
- Transportation
- Building automation
- Industrial production

OT security has a strong relationship with safety and physical operations.

A cyber incident can potentially result in:

- Production interruption
- Equipment damage
- Unsafe conditions
- Environmental impact
- Physical injury

Therefore, security decisions must account for operational consequences.

---

## 15. Industrial Control Systems (ICS)

**Industrial Control Systems (ICS)** are systems used to monitor and control industrial processes.

ICS environments may contain:

- Sensors
- Actuators
- Programmable Logic Controllers (PLCs)
- Remote Terminal Units (RTUs)
- Human-machine interfaces
- Engineering workstations
- Control servers
- Network infrastructure

A simplified architecture is:

```text
Physical Process
      ↓
Sensors / Actuators
      ↓
PLC / RTU
      ↓
Control Network
      ↓
HMI / Supervisory Systems
      ↓
Operations Personnel
```

---

## 16. Programmable Logic Controllers (PLCs)

A **PLC** is an industrial controller designed to execute control logic and interact with physical equipment.

PLCs can control:

- Motors
- Valves
- Pumps
- Conveyors
- Manufacturing machinery
- Process controls

Security concerns include:

- Unauthorized programming changes
- Weak authentication
- Insecure protocols
- Network exposure
- Vulnerable firmware
- Unauthorized physical access

A malicious change to PLC logic can potentially affect a real physical process.

---

## 17. Remote Terminal Units (RTUs)

An **RTU** is a field device commonly used to collect sensor information and control equipment in geographically distributed environments.

RTUs are common in systems such as:

- Utilities
- Pipelines
- Energy infrastructure
- Water systems

Because RTUs may operate in remote locations, physical and network security both matter.

---

## 18. Human-Machine Interface (HMI)

An **HMI** provides operators with a graphical or other interface for viewing and controlling industrial processes.

An HMI may display:

- Sensor values
- Alarms
- Equipment state
- Process status
- Control options

Compromise of an HMI can mislead operators or provide unauthorized control capabilities.

Therefore, HMI systems should be appropriately segmented, authenticated, monitored, and maintained.

---

## 19. SCADA

**Supervisory Control and Data Acquisition (SCADA)** systems are used for supervisory monitoring and control, especially across geographically distributed industrial environments.

A simplified architecture is:

```text
Field Devices
    ↓
RTUs / PLCs
    ↓
Industrial Network
    ↓
SCADA Server
    ↓
HMI / Operator
```

SCADA systems can collect telemetry and allow authorized operators to supervise physical processes.

Security concerns include:

- Remote access
- Legacy protocols
- Centralized control systems
- Weak authentication
- Network exposure
- Vendor access
- Inadequate segmentation

---

## 20. ICS vs. SCADA

These terms are related but should not be treated as exact synonyms.

**ICS** is a broad category of industrial control systems.

**SCADA** is a type of supervisory control architecture commonly used for monitoring and controlling distributed processes.

A Security+ question may use the terms differently depending on the scenario, so focus on the architecture and function being described.

---

## 21. OT vs. IT

Traditional enterprise IT often focuses heavily on:

- Data confidentiality
- Data integrity
- Availability
- Rapid patching
- User productivity

OT environments may place especially strong emphasis on:

- Safety
- Availability
- Process integrity
- Reliability
- Deterministic behavior
- Controlled change

This does not mean confidentiality is unimportant in OT. It means security controls must account for operational and safety consequences.

---

## 22. The OT Security Trade-Off

Consider an industrial controller with a known vulnerability.

In ordinary IT, the organization may be able to patch it immediately.

In OT, immediately applying the patch could:

- Stop production
- Change system timing
- Cause equipment instability
- Require safety testing
- Violate maintenance procedures

Therefore, the correct response may involve a controlled maintenance window, compensating controls, vendor validation, and risk assessment rather than immediate untested patching.

---

## 23. Availability in OT

Availability is often critical because the system may be responsible for continuous physical operations.

A security control that causes repeated outages can itself become an operational risk.

Examples include:

- Aggressive vulnerability scans
- Uncontrolled network scans
- Unvalidated firmware updates
- Intrusive security testing
- Incorrect firewall changes

Security activities should therefore be planned around operational requirements.

---

## 24. Integrity in Industrial Systems

Integrity is especially important because unauthorized changes to process values or control logic can alter physical operations.

Examples include:

- Changing PLC logic
- Modifying sensor values
- Altering alarm thresholds
- Changing HMI configurations
- Modifying engineering workstation settings

Controls should protect both configuration integrity and operational data integrity.

---

## 25. Safety and Cybersecurity

In OT environments, cybersecurity can directly affect physical safety.

Security teams should consider:

- Safe operating states
- Emergency procedures
- Fail-safe mechanisms
- Manual overrides
- Safety instrumented systems
- Physical access controls
- Incident escalation procedures

A cyber incident response plan should define how security teams coordinate with plant operators and safety personnel.

---

## 26. OT Network Segmentation

Segmentation is one of the most important OT security controls.

A simplified architecture is:

```text
Enterprise IT
     |
 Enterprise Firewall
     |
 OT DMZ
     |
 ICS Firewall
     |
 Control Network
     |
 PLCs / RTUs / HMIs
```

The exact architecture depends on the environment, but the objective is to avoid unrestricted connectivity between corporate IT and control systems.

---

## 27. Industrial DMZ

An **industrial DMZ** can act as a controlled boundary between enterprise IT and OT networks.

Systems that require controlled communication across the boundary may include:

- Data historians
- Remote-access gateways
- Update repositories
- Monitoring systems
- Jump servers

The industrial DMZ reduces direct connectivity between enterprise systems and sensitive control networks.

---

## 28. Purdue Model Concept

The **Purdue Enterprise Reference Architecture** is commonly used as a conceptual model for organizing industrial environments into levels.

A simplified representation is:

```text
Enterprise IT
     ↓
Industrial DMZ
     ↓
Supervisory Systems
     ↓
Control Systems
     ↓
PLCs / Controllers
     ↓
Sensors / Actuators
     ↓
Physical Process
```

The key security idea is **separation of zones and controlled communication between levels**.

Security+ questions may focus on segmentation and trust boundaries rather than requiring detailed knowledge of every Purdue level.

---

## 29. OT Remote Access

Remote access is a significant OT security concern because vendors, engineers, and operators may need access to geographically distributed systems.

A secure architecture should prefer:

- VPN or secure remote-access mechanisms
- MFA
- Dedicated jump hosts
- Least privilege
- Time-limited access
- Approval workflows
- Session logging
- Restricted protocols

Avoid exposing PLCs, HMIs, or control servers directly to the public internet.

---

## 30. Vendor Remote Access

Third-party vendors may require temporary access for maintenance.

Vendor access should be:

1. Approved
2. Authenticated
3. Restricted
4. Time-limited
5. Monitored
6. Logged
7. Revoked when maintenance ends

Permanent shared vendor credentials create accountability and security problems.

---

## 31. OT Protocol Security

Many legacy industrial protocols were designed for reliability and interoperability rather than modern cybersecurity.

Potential weaknesses include:

- Little or no encryption
- Weak authentication
- Limited integrity protection
- Trust-based communication
- Broadcast or plaintext communication

Where protocols cannot be replaced, compensating controls may include:

- Network segmentation
- Firewalls
- Protocol-aware monitoring
- Allowlisting
- Secure gateways
- Strict access control

---

## 32. Passive Monitoring in OT

Security monitoring in OT often needs to minimize operational disruption.

Passive monitoring can observe network traffic without actively sending large volumes of probes into sensitive systems.

This can be useful where active scanning could disrupt legacy equipment.

The correct approach depends on the device, protocol, vendor guidance, and operational risk.

---

## 33. Vulnerability Scanning in OT

Traditional vulnerability scanners can potentially create operational problems in sensitive industrial environments.

Before scanning, organizations should consider:

- Vendor recommendations
- System criticality
- Maintenance windows
- Protocol behavior
- Device stability
- Production impact

A safer approach may combine passive discovery, configuration review, vendor advisories, controlled testing, and carefully scoped active scanning.

---

## 34. Allowlisting in OT

Application or process allowlisting can be useful when systems perform a small, predictable set of functions.

Instead of attempting to detect every possible malicious program, the architecture can restrict execution to approved software.

This can be particularly useful for specialized systems with stable workloads.

However, allowlisting must be tested carefully because blocking legitimate control software can disrupt operations.

---

## 35. Legacy OT Systems

Legacy systems may remain operational for decades.

Problems can include:

- Unsupported operating systems
- Unsupported firmware
- Proprietary protocols
- Lack of modern authentication
- Inability to install endpoint agents
- Hardware compatibility constraints

The appropriate strategy may be a combination of:

**Isolation + compensating controls + monitoring + controlled access + eventual replacement.**

---

## 36. Physical Security for OT and IoT

Cybersecurity does not replace physical security.

An attacker with physical access may be able to:

- Reset devices
- Connect unauthorized equipment
- Replace hardware
- Access debug ports
- Modify cabling
- Steal removable media
- Manipulate controllers

Controls include:

- Locked equipment rooms
- Restricted cabinets
- Badge access
- Surveillance
- Tamper detection
- Port protection
- Visitor controls

---

## 37. Supply Chain Security

IoT and embedded devices depend heavily on vendors and component suppliers.

Supply-chain risks include:

- Malicious firmware
- Vulnerable third-party libraries
- Compromised update mechanisms
- Counterfeit components
- Unsupported products
- Vendor discontinuation

Organizations should evaluate vendor security practices, update mechanisms, support periods, and vulnerability-disclosure processes.

---

## 38. Device Lifecycle Management

IoT and OT security should cover the complete lifecycle:

```text
Procurement
    ↓
Deployment
    ↓
Configuration
    ↓
Operation
    ↓
Maintenance
    ↓
Decommissioning
```

At procurement, security requirements should be considered before the device is purchased.

During decommissioning, credentials, certificates, stored data, and network access should be removed or revoked.

---

## 39. IoT and OT Identity

Every device should ideally have a unique identity that allows the organization to distinguish one device from another.

Possible mechanisms include:

- Device certificates
- Unique credentials
- Hardware-backed identities
- Secure enrollment mechanisms

Shared credentials across hundreds of devices make attribution, revocation, and incident response more difficult.

---

## 40. Network Access Control for IoT

Network Access Control (NAC) can help determine whether a device should be permitted onto a network.

Policy decisions may consider:

- Device identity
- Device type
- Authentication state
- Security posture
- Network location

An unmanaged IoT device can be placed into a restricted network instead of receiving unrestricted enterprise access.

---

## 41. Quarantine Networks

A compromised or suspicious device can be moved into a restricted quarantine network.

Example:

```text
Normal IoT Network
        ↓
Suspicious Device
        ↓
Quarantine VLAN
        ↓
Investigation / Remediation
```

The objective is to prevent the device from communicating freely with other systems while preserving the ability to investigate or remediate it.

---

## 42. Monitoring IoT and OT

Useful telemetry may include:

- Network traffic
- Authentication events
- Configuration changes
- Firmware versions
- Device health
- Process anomalies
- Command activity
- Administrative access
- Vendor connections

Monitoring should be designed around the environment's operational requirements.

Unexpected behavior can be significant even when traditional malware indicators are absent.

---

## 43. Anomaly Detection in OT

Industrial processes often have predictable behavior.

For example, a controller may normally communicate with a fixed set of systems using predictable protocols.

Anomalies could include:

- New communication partners
- Unexpected commands
- Unusual connection times
- Abnormal process values
- Unauthorized configuration changes
- Unexpected firmware changes

Behavioral monitoring can therefore complement traditional signature-based detection.

---

## 44. Incident Response for IoT and OT

Incident response should account for safety and operational continuity.

A simplified process is:

```text
Detect
  ↓
Validate
  ↓
Assess Safety/Operational Impact
  ↓
Contain Carefully
  ↓
Eradicate/Remediate
  ↓
Recover
  ↓
Validate Process Safety
  ↓
Lessons Learned
```

The containment step is particularly important. Disconnecting a system may be appropriate in one environment but dangerous in another.

---

## 45. OT Incident Containment

Containment decisions should involve relevant operational personnel.

Before disconnecting or shutting down a critical system, determine:

- What physical process it controls
- What happens if it stops
- Whether a safe state exists
- Whether manual control is available
- Whether safety systems are independent
- What maintenance procedures apply

Cybersecurity teams should not treat every OT device like an ordinary workstation.

---

## 46. Backup and Recovery for OT

Recovery planning should consider:

- PLC logic backups
- HMI configurations
- SCADA configurations
- Engineering workstation images
- Network-device configurations
- Firmware versions
- Vendor documentation
- Spare hardware
- Recovery procedures

Backups should be protected from unauthorized modification and periodically validated.

For critical systems, having a backup file is insufficient if the organization cannot restore the system safely.

---

## 47. High Availability and Redundancy

Critical industrial environments may use redundant:

- Controllers
- Network paths
- Servers
- Power supplies
- Communication links
- Monitoring systems

Redundancy can improve availability, but duplicated systems must also be secured.

An insecure redundant component can become an alternate path into the environment.

---

## 48. Safety Instrumented Systems

Safety-related systems may be designed to bring equipment into a safe state when dangerous conditions are detected.

Security architecture should consider the relationship between:

- Basic process control
- Safety systems
- Cybersecurity controls
- Physical safety procedures

Cybersecurity changes should not unintentionally disable or interfere with safety functions.

---

## 49. IoT and Cloud Dependency

Many IoT devices communicate with cloud services.

A secure architecture should consider:

```text
IoT Device
    ↓
Local Network
    ↓
Internet
    ↓
Cloud API
    ↓
Application / Management Platform
```

Security concerns can exist at every stage:

- Device identity
- Network security
- TLS
- API authentication
- Cloud IAM
- Data protection
- Application security

Securing the device alone is insufficient if the cloud management service is vulnerable.

---

## 50. IoT Botnets

Large numbers of poorly secured IoT devices can be compromised and controlled as a **botnet**.

Attackers may use compromised devices for:

- Distributed denial-of-service attacks
- Proxying malicious traffic
- Credential attacks
- Malware distribution
- Other unauthorized activity

Strong default-credential management, patching, segmentation, and monitoring reduce this risk.

---

## 51. Common IoT, ICS, and OT Security Failures

### Internet-Exposed Control Systems

Sensitive control interfaces are directly reachable from untrusted networks.

### Default Credentials

Devices continue operating with vendor-default passwords.

### Flat Networks

IoT, enterprise systems, and OT devices share unrestricted network access.

### Unsupported Firmware

Known vulnerabilities remain because the device cannot be updated.

### Uncontrolled Vendor Access

Third parties retain permanent remote access.

### Aggressive Security Scanning

Security tools disrupt fragile industrial devices.

### Missing Asset Inventory

The organization does not know which devices exist or what they control.

### Shared Device Credentials

Multiple devices use the same administrative identity, reducing accountability.

### Weak Physical Security

Attackers can access controllers, cabinets, ports, or removable media.

---

## 52. Security+ Scenario Examples

### Scenario 1 — Smart Cameras

An organization deploys hundreds of IP cameras on the corporate user network. One camera is compromised.

**Architecture improvement:** place cameras in a dedicated IoT segment and restrict their communication to required management and recording systems.

**Concept:** network segmentation and attack-surface reduction.

---

### Scenario 2 — Unpatchable Controller

A legacy controller has a known vulnerability, but the vendor does not provide a patch.

**Possible approach:** isolate the controller, restrict communication, monitor traffic, control administrative access, and implement other compensating controls.

**Concept:** compensating controls for legacy systems.

---

### Scenario 3 — Critical Production System

A security team wants to run an aggressive vulnerability scan against an industrial controller during production.

**Concern:** active scanning may disrupt a sensitive device.

**Approach:** coordinate with operations, review vendor guidance, and use a carefully controlled assessment method.

**Concept:** OT availability and safety considerations.

---

### Scenario 4 — Vendor Maintenance

A vendor requires remote access to an industrial control environment.

**Security architecture:** secure remote access, MFA, restricted permissions, approval, time-limited access, and logging.

---

### Scenario 5 — PLC Modification

An attacker changes the logic running on a PLC.

**Potential impact:** physical process manipulation.

**Controls:** strict engineering access, network segmentation, configuration integrity monitoring, authentication, logging, and controlled change management.

---

### Scenario 6 — OT Ransomware

Malware reaches an industrial network from the enterprise network.

**Architecture lesson:** strong separation between enterprise IT and OT can reduce the attack path and blast radius.

Containment must also account for physical safety and production requirements.

---

### Scenario 7 — Device With Default Password

A smart sensor still uses its vendor-default administrative password.

**Issue:** weak authentication.

**Control:** change default credentials, use stronger authentication where supported, restrict management access, and segment the device.

---

### Scenario 8 — Suspicious Industrial Traffic

A controller begins communicating with a system it has never contacted before.

**Potential detection:** network anomaly monitoring.

The event should be investigated in the context of expected industrial communication patterns.

---

## 53. Common Security+ Exam Traps

### Trap 1 — Treating OT Like Ordinary IT

OT systems may have safety and availability requirements that make immediate patching or shutdown inappropriate.

### Trap 2 — Internet Exposure Is Acceptable Because a Device Is Specialized

Specialized devices are still attack surfaces. Internet exposure should be avoided unless explicitly required and strongly protected.

### Trap 3 — Segmentation Is Optional for IoT

IoT devices can be compromised and used for lateral movement. Segmentation is an important architectural control.

### Trap 4 — Vulnerability Scanning Is Always Safe

Active scanning can affect fragile devices. Testing must consider operational and safety risks.

### Trap 5 — No Patch Means No Solution

Compensating controls such as isolation, firewall restrictions, monitoring, and controlled access can reduce risk when patching is impossible.

### Trap 6 — SCADA and ICS Are Identical Terms

ICS is the broader category; SCADA describes a supervisory control architecture commonly used for distributed environments.

### Trap 7 — Security Should Always Take Priority Over Availability

Security objectives must be balanced with safety and operational requirements, particularly in OT environments.

### Trap 8 — Remote Vendor Access Can Be Permanent

Third-party access should be restricted, authenticated, monitored, and removed when no longer required.

### Trap 9 — Network Segmentation Alone Solves OT Security

Segmentation is important but must be combined with identity, secure configuration, monitoring, physical security, change management, and recovery.

---

## 54. Important Distinctions

| Concept | Key idea |
|---|---|
| IoT | Network-connected physical devices and sensors |
| Embedded system | Specialized computing component built into a larger device |
| OT | Technology used to monitor/control physical processes |
| ICS | Industrial systems used to control physical processes |
| SCADA | Supervisory monitoring/control architecture, often distributed |
| PLC | Industrial controller executing control logic |
| RTU | Field device used for remote monitoring/control |
| HMI | Interface through which operators monitor/control processes |
| Industrial DMZ | Controlled boundary between enterprise IT and OT networks |
| Purdue model | Conceptual industrial architecture organized into levels/zones |
| Secure boot | Verifies authorized boot software/firmware |
| Compensating control | Alternative control used when the preferred control cannot be implemented |
| Allowlisting | Restricts execution or communication to approved items |
| Quarantine network | Restricted network for suspicious or compromised devices |
| Passive monitoring | Observes activity with minimal active interaction |
| Device identity | Unique identity used to authenticate and distinguish devices |
| Safety | Protection of people, equipment, and physical processes |

---

## 55. IoT/OT Security Architecture Checklist

When reviewing an IoT or OT environment, ask:

- Do we have a complete asset inventory?
- Does every device have a known owner?
- Are default credentials removed?
- Is firmware supported and current where possible?
- Can devices receive secure updates?
- Are devices segmented from enterprise users?
- Are management interfaces isolated?
- Are industrial control networks separated from corporate networks?
- Is remote vendor access controlled?
- Is MFA used where supported?
- Are administrative activities logged?
- Are industrial protocols appropriately protected or isolated?
- Can security scanning be performed safely?
- Are unpatchable systems protected with compensating controls?
- Are physical access controls adequate?
- Are PLC and HMI configurations backed up?
- Are recovery procedures tested?
- Are safety implications included in incident response?

---

## 56. Scenario Reasoning Framework

When a Security+ scenario involves IoT, ICS, SCADA, or embedded systems, use this process.

### Step 1 — Identify the System

Determine whether it is:

- IoT
- Embedded system
- PLC
- RTU
- HMI
- SCADA
- ICS
- Other OT system

### Step 2 — Identify the Physical Consequence

Ask what happens if the system is compromised or unavailable.

Could it affect:

- Production?
- Safety?
- Equipment?
- Environment?
- Critical services?

### Step 3 — Identify the Constraint

Determine whether the system has:

- No patch available
- Limited resources
- Legacy protocols
- Long lifecycle
- Vendor dependency
- Safety restrictions

### Step 4 — Select the Architecture

Common controls include:

- Segmentation
- Industrial DMZ
- Restricted remote access
- Allowlisting
- Monitoring
- Secure management
- Compensating controls

### Step 5 — Consider Operational Safety

Before recommending shutdown, patching, scanning, or isolation, consider the physical process and safe-state requirements.

### Step 6 — Protect the Management Path

Ask who can change:

- Firmware
- PLC logic
- HMI configuration
- SCADA settings
- Network configuration

### Step 7 — Plan Recovery

Verify that configurations, firmware, documentation, and necessary hardware can be restored safely.

---

## 57. Key Takeaways

- IoT, embedded systems, and OT connect cybersecurity to physical environments.
- IoT devices increase attack surface because sensors, controllers, appliances, and other devices become network-connected assets.
- Default credentials, insecure firmware, weak authentication, exposed management interfaces, and poor update mechanisms are common concerns.
- Asset inventory is fundamental because unknown devices represent unmanaged attack surface.
- IoT devices should generally be segmented from ordinary enterprise systems and high-value assets.
- Embedded systems may have resource, hardware, lifecycle, and vendor constraints that limit conventional security controls.
- Compensating controls are important when legacy systems cannot be patched.
- OT environments require careful consideration of availability, integrity, reliability, and safety.
- ICS is a broad category of industrial control systems, while SCADA is a supervisory control architecture commonly used for distributed environments.
- PLCs execute industrial control logic and therefore require strong protection against unauthorized modification.
- RTUs commonly support remote monitoring and control in distributed environments.
- HMIs provide operators with interfaces for monitoring and controlling industrial processes.
- Industrial DMZs can provide a controlled boundary between enterprise IT and sensitive OT networks.
- Remote vendor access should be authenticated, restricted, time-limited, monitored, and revoked when no longer needed.
- Legacy industrial protocols may lack modern security features and therefore require compensating architectural controls.
- Passive monitoring can be valuable where active scanning could disrupt sensitive systems.
- Security testing in OT must consider vendor guidance, maintenance windows, device stability, and safety requirements.
- Application allowlisting can be useful for predictable specialized systems but must be carefully validated.
- Physical security remains important because direct access can bypass or undermine logical controls.
- Device identities should be unique where practical to improve authentication and accountability.
- IoT and OT monitoring should consider expected communication patterns and process behavior, not only conventional malware indicators.
- Incident response in OT must account for physical safety before aggressive containment actions.
- Recovery requires more than data backups; organizations may need PLC logic, HMI configurations, firmware, documentation, and compatible hardware.
- Redundancy improves availability but must itself be secured.
- IoT ecosystems may depend on cloud APIs, so cloud identity and API security are part of the overall architecture.

The central Security+ concept is:

**When cybersecurity controls interact with physical systems, security architecture must protect the device, network, management plane, and data while also preserving safe and reliable operation. In OT and embedded environments, the technically strongest control is not automatically the correct operational control; the architecture must account for safety, availability, integrity, lifecycle constraints, and controlled change.**
