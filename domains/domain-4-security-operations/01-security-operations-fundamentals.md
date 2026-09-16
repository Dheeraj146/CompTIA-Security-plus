# Security Operations Fundamentals

Security operations is the **continuous, day-to-day practice of operating and defending an organization's technology environment securely**. It connects security architecture and policy with the actual systems, users, devices, applications, networks, cloud services, and data that must be protected.

Security operations is not a single product or team activity. It is a lifecycle involving asset visibility, secure configuration, identity and access management, vulnerability management, logging, monitoring, detection, investigation, incident response, recovery, documentation, and continuous improvement.

A system can be securely designed and still become vulnerable later. New vulnerabilities are discovered, configurations drift, users change roles, software is installed, certificates expire, credentials are compromised, cloud resources are created, and attackers continuously change techniques. Security operations exists to manage these changes and maintain the intended security posture over time.

---

## 1. Security Operations vs. Security Architecture

Security architecture primarily answers:

> **How should the environment be designed so that security requirements are built into it?**

Security operations primarily answers:

> **How do we operate, monitor, maintain, investigate, and improve that environment securely every day?**

For example, architecture may specify that administrative systems must be isolated on a management network and protected with MFA. Operations must then ensure that:

- The management network actually exists and remains correctly segmented.
- Administrative accounts use MFA.
- Privileged access is reviewed.
- Firewall rules remain appropriate.
- Administrative activity is logged.
- Alerts are investigated.
- Compromised accounts are disabled or reset.
- Configuration changes are documented.

Therefore, architecture establishes the intended security design, while operations keeps that design effective in the real environment.

---

## 2. Objectives of Security Operations

A mature security operations function attempts to maintain several objectives simultaneously:

### Confidentiality

Only authorized users, applications, services, and systems should access protected information.

Operational activities supporting confidentiality include:

- Access reviews
- Encryption management
- DLP monitoring
- Privileged-access monitoring
- Data-access logging
- Account lifecycle management

### Integrity

Systems and information should remain accurate, trustworthy, and protected from unauthorized modification.

Operational activities supporting integrity include:

- File-integrity monitoring
- Configuration monitoring
- Change management
- Code-signing verification
- Database auditing
- Log integrity protection

### Availability

Systems and services should remain accessible when required by authorized users.

Operational activities supporting availability include:

- Health monitoring
- Capacity monitoring
- Redundancy
- Backup verification
- Failover testing
- Disaster recovery
- Incident response

Security operations therefore has to balance confidentiality, integrity, and availability rather than focusing exclusively on preventing attacks.

---

## 3. Core Security Operations Lifecycle

A useful operational model is:

**Identify → Protect → Monitor → Detect → Analyze → Respond → Recover → Improve**

These stages are connected rather than independent.

### Identify

Determine what exists and what must be protected.

Examples:

- Discover assets.
- Identify asset owners.
- Classify data.
- Identify critical services.
- Understand dependencies.
- Identify vulnerabilities and threats.

### Protect

Apply controls that reduce the likelihood or impact of security problems.

Examples include:

- MFA
- Secure configuration
- Network segmentation
- Endpoint protection
- Patching
- Least privilege
- Encryption

### Monitor

Collect and observe relevant security telemetry.

Examples include:

- Authentication logs
- Endpoint events
- Firewall logs
- DNS activity
- Network flows
- Cloud audit logs
- Application logs

### Detect

Identify activity that may represent a security problem.

Detection can use:

- SIEM correlation rules
- IDS/IPS
- EDR detections
- Behavioral analytics
- Threat intelligence
- File-integrity monitoring

### Analyze

Determine what an alert means by adding context and investigating related activity.

Analysts may examine:

- Source and destination IP addresses
- User accounts
- Processes
- Commands
- Authentication history
- DNS queries
- Network connections
- File hashes
- Timeline information
- Previous alerts

### Respond

Take appropriate action to contain and address the threat.

Examples include:

- Isolating an endpoint
- Disabling an account
- Blocking an indicator
- Removing persistence
- Applying a temporary firewall rule

### Recover

Restore affected systems and services to a trusted operational state.

Examples include:

- Rebuilding a compromised system
- Restoring data
- Rotating credentials
- Restoring services
- Validating system integrity

### Improve

Use lessons learned to strengthen the environment.

Improvements may include:

- New detection rules
- Configuration changes
- Additional controls
- Updated runbooks
- Security awareness training
- Architecture changes
- Process improvements

---

## 4. Asset Management as an Operational Foundation

Security teams cannot reliably protect assets they do not know exist.

Asset management identifies and maintains information about technology and information resources such as:

- Servers
- Workstations
- Laptops
- Mobile devices
- Network equipment
- Virtual machines
- Containers
- Cloud resources
- Applications
- Databases
- Storage systems
- SaaS applications
- IoT devices
- Industrial systems
- Data repositories

An asset inventory should ideally contain information such as ownership, location, business purpose, operating system, software, criticality, network placement, and lifecycle status.

Asset visibility supports nearly every other security operation. For example, vulnerability scanning cannot be complete if an unknown server is omitted from the scan scope. Incident response is also more difficult when analysts cannot determine who owns the affected system or how critical it is.

---

## 5. Secure Configuration and Security Baselines

A security baseline defines an approved configuration for a particular system, device, application, or environment.

Examples include:

- Disabling unnecessary services
- Enforcing password and authentication requirements
- Enabling host firewalls
- Restricting administrative access
- Removing unnecessary software
- Configuring secure protocols
- Enabling appropriate logging
- Applying endpoint security controls

The baseline provides a known-good reference. Security operations can compare current configurations against that reference to identify configuration drift.

A baseline is not necessarily identical for every system. A database server, domain controller, web server, workstation, and network device have different operational requirements and therefore may require different secure configurations.

---

## 6. Vulnerability and Patch Management

Vulnerability management is the operational process of identifying, assessing, prioritizing, remediating, and validating security weaknesses.

A simplified workflow is:

**Discover → Scan/Identify → Validate → Prioritize → Remediate → Verify → Monitor**

A vulnerability scanner may identify a vulnerable service, but scanning itself does not remediate the vulnerability.

Remediation could involve:

- Installing a patch
- Upgrading software
- Removing vulnerable software
- Changing configuration
- Disabling an exposed service
- Applying a compensating control
- Segmenting the affected system

Priority should consider more than the existence of a vulnerability. Organizations may consider exploitability, exposure, asset criticality, business impact, active exploitation, compensating controls, and available remediation options.

---

## 7. Logging and Monitoring

Security operations requires reliable telemetry because analysts need evidence to determine what happened.

Common log sources include:

- Windows event logs
- Linux system logs
- Authentication logs
- Active Directory logs
- Firewall logs
- IDS/IPS alerts
- DNS logs
- DHCP logs
- VPN logs
- Proxy logs
- Web server logs
- Database audit logs
- Cloud audit logs
- EDR telemetry
- Application logs

Logging answers questions such as:

- Who performed an action?
- What action occurred?
- When did it happen?
- Which system was involved?
- Where did the activity originate?
- Was the action successful?
- What happened immediately before and after it?

Monitoring gives operational meaning to this telemetry by looking for abnormal conditions, policy violations, suspicious behavior, system failures, and security indicators.

---

## 8. Event, Alert, and Incident

These terms must be distinguished carefully.

### Event

An **event** is an observable occurrence in a system or environment.

Examples:

- A user logs in.
- A process starts.
- A firewall allows traffic.
- A file is created.
- A DNS query is generated.

An event is not automatically malicious.

### Alert

An **alert** is a notification generated because activity meets a detection rule, threshold, behavioral condition, or other security criterion.

For example, a SIEM might alert when a user has multiple failed logins followed by a successful login from an unusual location.

An alert is not automatically a confirmed incident. It requires analysis.

### Incident

A **security incident** is an event or series of events that has been determined to involve an actual or suspected violation of security policy or compromise of confidentiality, integrity, or availability.

The exact organizational definition can vary according to policy.

The operational progression is often:

**Event → Detection/Alert → Triage → Investigation → Incident determination → Response**

This distinction is extremely important in SOC operations and Security+ scenario questions.

---

## 9. Triage and Alert Analysis

Security operations teams receive more alerts than they can investigate deeply at the same time. Triage determines which alerts require immediate attention and what investigative path should be followed.

An analyst may ask:

1. What happened?
2. Which asset was involved?
3. Which user or identity was involved?
4. Is the activity expected?
5. Is the asset business-critical?
6. What detection generated the alert?
7. Is the indicator known malicious?
8. Are there related events?
9. Is there evidence of compromise?
10. Does the situation require escalation?

Triage should reduce uncertainty rather than simply close alerts quickly.

---

## 10. Preventive, Detective, and Corrective Operations

Security controls can be categorized according to their operational purpose.

### Preventive Controls

Preventive controls attempt to stop an unwanted event before it occurs.

Examples:

- MFA
- Firewalls
- Network segmentation
- Secure configuration
- Least privilege
- Application allowlisting
- Security awareness training

### Detective Controls

Detective controls identify or provide evidence of activity that has occurred or is occurring.

Examples:

- SIEM monitoring
- IDS
- EDR detections
- Audit logs
- File-integrity monitoring
- Security alerts

### Corrective Controls

Corrective controls restore or improve the environment after an unwanted event.

Examples:

- Malware removal
- Credential resets
- Rebuilding compromised hosts
- Patching exploited systems
- Restoring from backup
- Correcting insecure configurations

The same technology can serve different control categories depending on how it is deployed and used.

---

## 11. Security Operations Technologies

| Technology | Primary operational purpose |
|---|---|
| Firewall | Enforces network traffic policy |
| IDS | Detects suspicious network activity |
| IPS | Detects and can block suspicious network activity |
| EDR | Collects endpoint telemetry and supports detection/investigation/response |
| SIEM | Centralizes and correlates security-relevant logs and events |
| SOAR | Automates and orchestrates security workflows |
| Vulnerability scanner | Identifies potential vulnerabilities |
| IAM | Manages identities, authentication, authorization, and access |
| DLP | Helps identify and prevent unauthorized handling or movement of sensitive data |
| NAC | Controls network access based on identity, device posture, or policy |
| WAF | Protects web applications from relevant application-layer attacks |
| Proxy | Mediates client/server communication and can enforce policy |

Security+ questions frequently test the **purpose and placement** of a technology rather than asking only what the acronym means.

---

## 12. Identity and Access Operations

Identity is a major part of security operations because compromised accounts are frequently used to access otherwise legitimate systems.

Operational IAM activities include:

- Account provisioning
- Account deprovisioning
- Role changes
- Access reviews
- Privileged account monitoring
- MFA enforcement
- Password and credential management
- Service-account management
- Federation management
- Authentication-log monitoring

The joiner-mover-leaver lifecycle is especially important.

### Joiner

When a new employee joins, the organization provisions only the access required for the employee's role.

### Mover

When an employee changes roles, old permissions should be removed and new permissions assigned according to the new role.

### Leaver

When employment or access authorization ends, accounts, tokens, sessions, credentials, and other access mechanisms should be disabled or revoked according to organizational procedures.

Failure to manage this lifecycle can result in orphaned accounts and excessive privileges.

---

## 13. Endpoint Security Operations

Endpoints are common targets because they interact directly with users, applications, files, and networks.

Endpoint operations may include:

- EDR deployment
- Antivirus/antimalware management
- Host firewall configuration
- Patch management
- Application control
- Disk encryption
- USB/device control
- Local privilege management
- Secure configuration
- Endpoint isolation
- Endpoint telemetry collection

An endpoint security platform may provide both preventive and detective capabilities. For example, it may block known malicious software while also recording process execution for investigation.

---

## 14. Network Security Operations

Network security operations maintains the controls and visibility needed to protect communications.

Operational activities can include:

- Firewall rule management
- IDS/IPS monitoring
- VPN administration
- Network segmentation
- NAC enforcement
- Proxy management
- DNS security
- Network-flow monitoring
- Secure remote access
- Configuration review

A network control should be evaluated not only by whether it exists but also by whether its configuration remains aligned with policy.

For example, a firewall is not automatically secure simply because it is installed. Excessively broad rules, stale exceptions, undocumented changes, and overly permissive outbound traffic can create significant exposure.

---

## 15. Configuration and Change Control

Security operations must control changes because unauthorized or poorly planned changes can introduce vulnerabilities or disrupt security controls.

A controlled change normally considers:

- What is changing?
- Why is it changing?
- Who requested it?
- Who approved it?
- What systems are affected?
- What security impact exists?
- What testing is required?
- What is the implementation window?
- What is the rollback plan?
- How will success be validated?

Emergency changes may follow an accelerated process, but they should still be documented and reviewed according to organizational procedures.

---

## 16. Security Monitoring and Context

A single event rarely provides enough information to determine whether an attack occurred.

Suppose a SIEM reports a successful login from an unusual IP address. An analyst should not automatically classify the event as compromise.

Additional context might include:

- Was the user traveling?
- Is the IP associated with a corporate VPN?
- Was MFA completed?
- Is the device known and compliant?
- Were there previous failed logins?
- What resources were accessed afterward?
- Did the account perform unusual administrative actions?
- Did the same credentials authenticate from another location simultaneously?

Correlation across multiple data sources can transform an isolated event into a meaningful attack narrative.

---

## 17. Operational Documentation

Documentation allows security processes to be repeatable, auditable, and understandable by multiple analysts.

Important operational documents include:

- Policies
- Standards
- Procedures
- Security baselines
- Runbooks
- Playbooks
- Incident response plans
- Disaster recovery plans
- Change records
- Asset inventories
- Network diagrams
- Escalation procedures
- Contact lists
- Recovery procedures

### Runbook vs. Playbook

A **runbook** generally provides detailed operational instructions for a specific repeatable task.

A **playbook** generally describes how to respond to a particular type of security situation or incident.

For example, a runbook might explain how to isolate an endpoint in an EDR platform, while a phishing-response playbook may describe the overall investigation and response process for suspected phishing.

---

## 18. Automation in Security Operations

Automation reduces repetitive manual work and can improve consistency and response speed.

Examples include:

- Automatically enriching an IP address with threat intelligence
- Disabling a confirmed compromised account
- Isolating a compromised endpoint
- Creating a ticket from a high-confidence alert
- Blocking a malicious domain
- Collecting standard evidence from a host
- Sending notifications to an escalation group

Automation should be controlled carefully. An incorrect detection rule combined with an automatic containment action can disrupt legitimate business activity.

A common operational principle is:

**Automate repetitive, well-understood tasks; require human judgment for ambiguous or high-impact decisions.**

---

## 19. Security Operations and the Principle of Least Privilege

Security operations personnel themselves require controlled access.

A SOC analyst does not necessarily need unrestricted administrative access to every production system. Access should be based on role and operational need.

Examples include:

- Read-only SIEM access for junior analysts
- Controlled EDR response permissions
- Separate privileged accounts
- MFA for administrative access
- Just-in-time privilege where supported
- Privileged access monitoring
- Administrative jump hosts

This reduces the damage that can result from compromised analyst accounts or accidental actions.

---

## 20. Security Operations and Time Synchronization

Accurate time is essential for investigation.

Suppose an attacker authenticates at 10:03:14 on a domain controller, launches a process at 10:03:20 on an endpoint, and transfers data at 10:04:02 through a proxy. If systems have inconsistent clocks, analysts may construct an incorrect timeline.

Organizations therefore commonly use centralized time synchronization such as NTP and monitor significant clock drift.

Time synchronization supports:

- Incident timelines
- Log correlation
- Authentication analysis
- Forensic investigation
- Distributed-system troubleshooting

---

## 21. Security Operations and Data Protection

Operational security also includes protecting the telemetry itself.

Security logs may contain sensitive information such as usernames, IP addresses, hostnames, URLs, command lines, and authentication information. Therefore, organizations should consider:

- Access controls for logs
- Encryption in transit
- Encryption at rest
- Retention requirements
- Integrity protection
- Centralized collection
- Secure backups
- Time synchronization
- Appropriate handling of sensitive data

An attacker who can modify or delete security logs can make investigation significantly more difficult. Log infrastructure therefore needs its own security controls.

---

## 22. Security Operations Scenario: Unknown Internal Server

Consider an organization that discovers an unknown server connected to an internal network.

A weak response would be to immediately delete or shut down the system without collecting context.

A structured operational approach is:

1. Identify the system and its IP address.
2. Determine whether the asset is authorized.
3. Identify the owner and business purpose.
4. Determine what services and software it provides.
5. Review its configuration and exposure.
6. Check vulnerability and patch status.
7. Examine logs and security telemetry.
8. Determine whether suspicious activity occurred.
9. Isolate the system if risk warrants containment.
10. Investigate whether the system represents a security incident.
11. Remediate the underlying problem.
12. Update inventory and documentation.

The important lesson is that **asset identification, context, and evidence should guide the response**.

---

## 23. Security Operations Scenario: Suspicious Authentication

A SIEM generates an alert because a privileged account successfully authenticated from an unusual source.

The alert should trigger investigation rather than automatically proving compromise.

The analyst should examine:

- Source IP and geographic context
- Authentication method
- MFA result
- Device identity
- Previous authentication activity
- Failed authentication attempts
- Privileged actions after login
- Related endpoint and network events
- Whether the source is an approved administrative system

If evidence indicates compromise, appropriate containment may include terminating sessions, disabling or restricting the account, rotating credentials, isolating affected systems, and escalating according to the incident-response process.

---

## 24. Security Operations Scenario: Vulnerable Critical Server

Suppose a vulnerability scanner identifies a high-risk vulnerability on a critical production server.

The correct operational response is not always simply “patch immediately.” The team should consider:

- Whether the vulnerability is exploitable in the organization's environment
- Whether active exploitation exists
- Asset criticality
- Exposure to attackers
- Availability requirements
- Patch compatibility
- Testing requirements
- Compensating controls
- Maintenance windows
- Rollback options

A compensating control might temporarily reduce exposure when immediate patching is not feasible.

The key distinction is:

**Identification tells you that a weakness exists; remediation is the action taken to reduce or eliminate the risk.**

---

## 25. Security Operations Scenario: Malware Alert

An EDR platform detects suspicious PowerShell execution on a workstation.

The detection is an alert requiring triage.

An analyst may investigate:

- Parent and child processes
- Command-line arguments
- User account
- File paths
- Hashes
- Network connections
- Persistence mechanisms
- Similar activity on other hosts
- EDR detections before and after the alert

If malicious activity is confirmed, responders may isolate the endpoint, preserve relevant evidence, remove persistence, eradicate malware, reset compromised credentials, and recover the system.

The response should be driven by evidence and the organization's incident-response procedures.

---

## 26. Common Operational Failures

### Unknown Assets

If systems are missing from inventory, they may also be missing patches, monitoring, backups, and access controls.

### Excessive Privilege

Unnecessary permissions increase the impact of compromised accounts and insider misuse.

### Incomplete Logging

Without appropriate telemetry, analysts may be unable to reconstruct activity.

### Poor Time Synchronization

Inconsistent timestamps can make correlation and forensic timelines unreliable.

### Stale Detection Rules

Attack techniques and infrastructure change. Detection logic must be reviewed and tuned.

### Alert Fatigue

Excessive false positives can overwhelm analysts and cause important alerts to receive insufficient attention.

### Configuration Drift

Systems can gradually deviate from approved baselines, creating security gaps.

### Uncontrolled Changes

Poorly documented or unauthorized changes can introduce vulnerabilities or disable security controls.

### Over-Automation

Automatically taking disruptive action on low-confidence detections can create business impact.

### Insufficient Documentation

If operational knowledge exists only in one person's memory, response quality can decline when that person is unavailable.

---

## 27. Security Operations Metrics

Operational teams may use metrics to understand security performance.

Examples include:

- Mean time to detect (MTTD)
- Mean time to respond (MTTR)
- Mean time to contain
- Patch compliance
- Vulnerability remediation time
- Endpoint coverage
- Logging coverage
- MFA coverage
- Alert volume
- False-positive rate
- Incident recurrence

Metrics should be interpreted carefully. A lower alert count, for example, is not automatically evidence of better security because it could result from broken telemetry or disabled detections.

Useful metrics should measure meaningful security outcomes and operational performance rather than encourage teams to optimize a number without improving security.

---

## 28. Operational Security Decision Framework

For Security+ scenario questions, use the following reasoning process:

### Step 1 — Identify the asset

What system, account, application, network, or data is involved?

### Step 2 — Identify the activity

What happened or what condition was detected?

### Step 3 — Determine the operational objective

Is the question asking about prevention, detection, investigation, response, recovery, or improvement?

### Step 4 — Add context

Who, what, when, where, how, and why?

### Step 5 — Select the appropriate control or process

Choose the technology or procedure that directly addresses the requirement.

### Step 6 — Consider business impact

Do not recommend an operational action without considering availability, criticality, and dependencies when the scenario provides those constraints.

### Step 7 — Verify the result

After remediation or response, confirm that the desired security state was actually achieved.

---

## 29. Common Security+ Distinctions

| Concept | Meaning |
|---|---|
| Event | Observable occurrence |
| Alert | Notification generated by a detection condition |
| Incident | Confirmed or suspected security-policy/security-impacting event requiring response |
| Vulnerability | Weakness that can be exploited or otherwise create risk |
| Threat | Potential cause or source of harm |
| Risk | Potential for loss or adverse impact arising from uncertainty |
| Detection | Identifying potentially malicious or undesirable activity |
| Response | Actions taken to contain, investigate, and address a security event/incident |
| Recovery | Restoring systems and services to an acceptable trusted state |
| Runbook | Detailed instructions for a repeatable operational task |
| Playbook | Structured response guidance for a particular security scenario |
| Baseline | Approved reference configuration or security state |
| Change management | Controlled process for modifying systems or configurations |

---

## 30. Security+ Exam Traps

### Trap 1 — Treating every alert as an incident

An alert requires analysis. It is not automatically proof of compromise.

### Trap 2 — Confusing detection with prevention

A control that identifies malicious activity is not necessarily a preventive control.

### Trap 3 — Confusing vulnerability scanning with remediation

A scanner identifies potential weaknesses; remediation addresses them.

### Trap 4 — Ignoring context

A suspicious-looking event may be legitimate administrative or business activity. Context determines the appropriate response.

### Trap 5 — Choosing the most disruptive response first

Isolation, account disabling, or system shutdown may be appropriate in some situations, but the scenario's evidence and business requirements determine the correct action.

### Trap 6 — Assuming technology alone provides security

A deployed SIEM, firewall, EDR, or vulnerability scanner still requires configuration, monitoring, maintenance, tuning, and operational processes.

### Trap 7 — Forgetting validation

A change is not necessarily successful merely because it was implemented. Verify that the vulnerability was fixed, the control works, and the intended security state exists.

---

## 31. Practical SOC Connection

Security operations fundamentals form the foundation of SOC analyst work.

A typical SOC workflow can look like this:

**Log source → Event → Detection rule → Alert → Triage → Enrichment → Investigation → Incident determination → Containment → Eradication → Recovery → Lessons learned**

For example:

1. A Windows endpoint generates a process-creation event.
2. The SIEM receives the event.
3. A detection rule identifies suspicious PowerShell behavior.
4. The SIEM creates an alert.
5. The analyst examines the user, host, command line, process tree, and network activity.
6. Threat intelligence and endpoint telemetry provide additional context.
7. The analyst determines whether the behavior is malicious.
8. If confirmed, the incident-response process begins.
9. The endpoint may be isolated.
10. Malicious persistence is removed.
11. Credentials may be reset if compromise is confirmed.
12. The system is recovered and validated.
13. Detection logic and security controls are improved based on lessons learned.

This demonstrates why security operations is a lifecycle rather than a collection of individual tools.

---

## 32. Key Takeaways

- Security operations is the continuous practice of securely operating, monitoring, maintaining, and defending technology environments.
- Security architecture defines how an environment should be designed; security operations keeps that design effective over time.
- Asset visibility is foundational to vulnerability management, monitoring, patching, and incident response.
- Secure baselines provide approved configurations against which operational systems can be evaluated.
- Vulnerability management includes identification, prioritization, remediation, and validation.
- Logs and telemetry provide the evidence required for detection and investigation.
- An event is not automatically an alert, and an alert is not automatically an incident.
- Triage adds context so analysts can determine appropriate action.
- Preventive, detective, and corrective controls have different operational purposes.
- Security technologies must be correctly configured, monitored, maintained, and tuned.
- IAM operations are critical because compromised identities can provide legitimate-looking access.
- Change management reduces the risk of unauthorized or poorly planned changes.
- Accurate time synchronization is important for correlation and forensic investigation.
- Automation can improve speed and consistency but should be applied carefully to high-impact actions.
- Documentation makes operational processes repeatable and auditable.
- Recovery should be followed by validation and lessons learned.
- Security operations continuously feeds improvements back into architecture, configuration, detection, and procedures.

**Core operational model:**

> **Asset → Configuration → Telemetry → Detection → Analysis → Response → Recovery → Lessons Learned**
