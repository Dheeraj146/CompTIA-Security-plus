# Domain 4 — Complete Study Notes: Security Operations

Domain 4 focuses on the day-to-day work of protecting and operating a security environment. This includes asset management, secure configuration, identity operations, endpoint and network security, logging, SIEM, automation, vulnerability management, incident response, forensics, malware handling, recovery, documentation, and security technology tuning.

The operational model is:

`Asset → Configuration → Telemetry → Detection → Analysis → Response → Recovery → Lessons Learned`

## 1. Security Operations Fundamentals

Security operations converts security policy into continuous technical and administrative activity. Analysts maintain systems, monitor events, investigate alerts, respond to incidents, and verify that security controls remain effective.

Operations should be repeatable and documented. Runbooks, playbooks, change procedures, escalation paths, and evidence-handling procedures reduce inconsistent responses.

## 2. Asset Management

An organization cannot protect assets it does not know exist. Asset management identifies hardware, software, cloud resources, identities, applications, data stores, and other technology resources.

An inventory should capture ownership, location, criticality, configuration, software versions, and lifecycle state where appropriate.

Asset classification allows security teams to prioritize controls. A critical database containing sensitive information should receive stronger protection and monitoring than an isolated test system.

## 3. Secure Baselines and Configuration Management

A secure baseline defines the approved configuration for a system. Examples include disabling unnecessary services, configuring logging, enforcing authentication requirements, applying secure permissions, and enabling endpoint protection.

Configuration drift occurs when systems gradually deviate from approved configurations. Drift can introduce vulnerabilities even when the original baseline was secure.

Configuration management continuously compares actual state with approved state and supports remediation.

## 4. Change Management

Security operations must control changes because unauthorized or poorly tested changes can create outages or vulnerabilities.

A normal change usually includes a request, risk assessment, testing, approval, implementation, validation, and documentation. Emergency changes may be implemented quickly during an incident or critical outage but should still be documented and reviewed afterward.

Change management also provides accountability and helps investigators distinguish expected activity from suspicious activity.

## 5. Identity and Access Management Operations

IAM operations manage the identity lifecycle: creation, modification, access review, suspension, and removal.

The joiner-mover-leaver process ensures access changes when employees join, change roles, or leave. Delayed removal of former employees is a common source of unnecessary access.

Privileged Access Management protects administrative accounts through controls such as separate privileged identities, approval workflows, credential vaulting, session monitoring, and just-in-time access.

Least privilege means granting only necessary permissions. Need-to-know limits access to information based on legitimate requirements.

## 6. Endpoint, Mobile, and Application Security

Endpoints are common attack targets because they interact with users, files, applications, and networks.

Endpoint controls include antivirus/antimalware, EDR, host firewalls, disk encryption, application control, patch management, secure configuration, and device monitoring.

EDR provides deeper telemetry and investigation capabilities than traditional signature-only antivirus. XDR extends correlation across multiple security domains.

Mobile security uses enrollment, configuration policies, application controls, encryption, remote lock/wipe, and conditional access.

Application security operations include vulnerability management, secure configuration, dependency monitoring, secrets protection, and monitoring of application behavior.

## 7. Network Security Operations

Network security operations maintain firewalls, IDS/IPS, secure gateways, proxies, VPNs, NAC, segmentation, and monitoring systems.

Firewall rules should be specific and justified. Overly broad rules increase attack surface. Unused rules should be reviewed and removed through controlled change processes.

IDS detects suspicious activity. IPS can block traffic. Analysts correlate network telemetry with endpoint and identity data to determine whether an alert represents a real incident.

## 8. Logging, Monitoring, and SIEM

Logs provide evidence about what systems and users are doing. Important properties include accurate timestamps, source information, event context, integrity, retention, and accessibility.

A SIEM aggregates and correlates security-relevant data from endpoints, network devices, applications, identity systems, cloud platforms, and other sources.

The basic SIEM workflow is:

`Collect → Normalize → Correlate → Detect → Alert → Investigate → Respond`

A single event may be harmless. Multiple related events can reveal an attack sequence. Analysts therefore investigate context rather than reacting blindly to isolated alerts.

## 9. SOAR, Automation, and Threat Hunting

SOAR platforms automate repetitive security workflows and coordinate actions across security tools.

Automation can enrich an IP address, retrieve reputation information, isolate an endpoint, create a ticket, or notify an analyst. Automated actions must have guardrails because an incorrect detection could otherwise cause unnecessary disruption.

Threat hunting is proactive investigation for suspicious activity that may not have generated a high-confidence alert. Hunters develop hypotheses, search telemetry, validate findings, and convert useful discoveries into improved detections.

## 10. Vulnerability Management Operations

Vulnerability management is a continuous lifecycle:

`Identify → Validate → Prioritize → Remediate → Verify → Report`

Prioritization should consider technical severity, exploitability, exposure, asset criticality, business impact, and available mitigations.

Patch management must balance security urgency with operational stability. Critical patches should be tested where practical, deployed according to risk, and verified afterward.

Exceptions should be documented rather than silently leaving known vulnerabilities unresolved.

## 11. Incident Response

Incident response provides an organized method for handling security incidents.

Preparation establishes tools, contacts, procedures, logging, backups, and training. Detection and analysis determine whether suspicious activity is actually an incident and establish scope.

Containment limits damage. Eradication removes the root cause. Recovery restores trusted operations and monitors for recurrence. Post-incident activities capture lessons learned and improve controls.

A common sequence is:

`Preparation → Detection/Analysis → Containment → Eradication → Recovery → Lessons Learned`

## 12. Digital Forensics and Evidence

Digital forensics involves collecting, preserving, examining, and reporting digital evidence.

Evidence may come from endpoints, memory, disks, network captures, cloud services, logs, email, mobile devices, and application records.

Evidence integrity is essential. Analysts should preserve originals where possible, document handling, use appropriate acquisition methods, calculate hashes when applicable, and maintain a chain of custody.

Volatile evidence such as memory and active network connections may disappear when a system is powered down, so collection order matters.

## 13. Malware Analysis and Response

Malware handling begins with safe containment and preservation of evidence.

**Static analysis** examines a sample without executing it. Analysts can inspect hashes, metadata, strings, imports, headers, and embedded information.

**Dynamic analysis** observes behavior in a controlled environment. Analysts can examine processes, files, registry changes, network connections, persistence, and command-and-control behavior.

Malware analysis should be performed in isolated environments with appropriate safety controls.

## 14. Backup, Recovery, and Business Continuity Operations

Backups protect data from accidental deletion, corruption, hardware failure, and attacks such as ransomware.

Full backups contain all selected data. Incremental backups contain changes since the previous backup of any type. Differential backups contain changes since the last full backup.

Recovery requires more than having backup files. Teams must verify backup integrity, maintain appropriate retention, protect backups from unauthorized access, and periodically test restoration.

Recovery operations should be aligned with RTO and RPO requirements established by business needs.

## 15. Operational Documentation and Automation

Documentation provides repeatability. Runbooks contain operational procedures. Playbooks provide structured response actions for specific scenarios. System documentation describes architecture and dependencies.

Automation reduces repetitive manual work but should include validation, logging, access control, error handling, and rollback mechanisms.

Scripts that modify production systems should be tested and operated under appropriate change controls.

## 16. Security Data Sources and Analysis

Security teams use multiple telemetry sources because no single source provides complete visibility.

Endpoint telemetry can reveal processes and file activity. Network telemetry shows connections and traffic patterns. Identity logs show authentication and authorization events. Application logs show transactions and errors. Cloud logs reveal API activity and resource changes.

Correlation across sources can transform isolated events into an attack timeline.

## 17. Security Technology Implementation and Tuning

Security technologies require appropriate deployment and continuous tuning. Incorrect configuration can create blind spots, excessive alerts, or operational failures.

Firewall and IDS/IPS rules should be reviewed for accuracy and relevance. SIEM detections should be tuned to reduce false positives while preserving meaningful coverage.

Tuning should be based on measured results, known threats, business requirements, and observed environment behavior rather than simply disabling noisy detections.

## 18. Incident Investigation Workflow

Investigation begins by validating the alert and establishing scope. Analysts identify affected users, devices, accounts, applications, and time periods.

Next, they build a timeline from reliable telemetry, preserve relevant evidence, identify initial access and subsequent activity, determine impact, and contain the incident according to response procedures.

Investigation should distinguish facts from assumptions. Every conclusion should be supported by evidence.

## Security+ Operational Scenario Method

For an operational scenario, determine:

1. What happened?
2. What evidence is available?
3. Which security control or data source should be used?
4. Is this an event, alert, vulnerability, or incident?
5. What action is appropriate now?
6. What evidence must be preserved?
7. How should recovery be validated?
8. What control should be improved afterward?

## Key Takeaways

Security operations is a continuous cycle rather than a single activity. Strong operations combine accurate asset knowledge, secure configuration, identity control, telemetry, detection, disciplined investigation, response, recovery, documentation, and continuous improvement.
