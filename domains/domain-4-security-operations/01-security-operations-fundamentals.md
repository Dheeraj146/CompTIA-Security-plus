# Security Operations Fundamentals

## 1. What Is Security Operations?

Security operations is the continuous process of protecting an organization's systems, networks, applications, identities, data, and users during normal day-to-day operation. Unlike security architecture, which primarily focuses on how an environment should be designed, security operations focuses on **how that environment is securely operated, monitored, maintained, and defended over time**.

A secure design can still become insecure when systems are misconfigured, patches are missing, accounts are not reviewed, logs are ignored, or security alerts are not investigated. Security operations provides the processes and technologies required to keep security controls effective after deployment.

## 2. Major Security Operations Activities

### Asset Management

Organizations need to know what systems and devices they own or operate. Asset management includes identifying hardware, software, cloud resources, applications, data stores, network devices, and other technology assets.

An unknown asset cannot be reliably protected. Asset visibility therefore provides the foundation for vulnerability management, patching, monitoring, incident response, and risk management.

### Secure Configuration

Systems should be configured according to approved security baselines. Configuration management reduces unnecessary services, insecure settings, excessive privileges, weak authentication, and other avoidable exposure.

### Patch and Vulnerability Management

Security teams identify vulnerabilities, determine their risk, prioritize remediation, apply patches or compensating controls, and validate that the weakness has actually been addressed.

### Logging and Monitoring

Security-relevant activity must generate useful telemetry. Logs can record authentication events, process execution, network connections, configuration changes, administrative actions, and other activity. Monitoring turns this telemetry into information that analysts can investigate.

### Detection and Response

Security operations must identify suspicious activity and respond appropriately. Detection may involve SIEM correlation, endpoint telemetry, IDS/IPS alerts, firewall events, identity signals, or other sources.

### Incident Response

When an event is confirmed or suspected to be a security incident, responders follow an established process to contain the threat, eradicate the cause, recover affected systems, preserve evidence, and learn from the incident.

## 3. Security Operations and the Control Lifecycle

A useful operational model is:

**Identify → Protect → Monitor → Detect → Analyze → Respond → Recover → Improve**

The process is continuous. Recovery does not mean security operations are finished. Lessons learned should influence future configurations, detection rules, procedures, training, and architecture.

## 4. Preventive, Detective, and Corrective Operations

### Preventive

Preventive controls attempt to stop an unwanted event before it occurs.

Examples include:

- Access control
- MFA
- Secure configuration
- Firewalls
- Network segmentation
- Application allowlisting
- Security awareness training

### Detective

Detective controls identify activity that has already occurred or is occurring.

Examples include:

- SIEM monitoring
- IDS
- EDR
- Audit logs
- File-integrity monitoring
- Security alerts

### Corrective

Corrective controls reduce the effect of an incident and restore secure operation.

Examples include:

- Malware removal
- Restoring from backup
- Rebuilding a compromised host
- Patching an exploited vulnerability
- Resetting compromised credentials

A single technology can support multiple control categories depending on how it is used.

## 5. Operational Security Requires Context

An alert does not automatically equal an incident. Analysts need context such as:

- Which user generated the activity?
- Which host was involved?
- Is the host critical?
- Is the activity expected for that user?
- Was the authentication successful?
- What process generated the activity?
- What happened immediately before and after it?
- Is there evidence of persistence or lateral movement?

This distinction is essential because security operations deals with large volumes of legitimate activity as well as malicious activity.

## 6. Security Operations Technologies

Common technologies include:

| Technology | Operational purpose |
|---|---|
| Firewall | Controls network traffic according to policy |
| IDS | Detects suspicious network activity |
| IPS | Detects and can actively block suspicious network activity |
| EDR | Provides endpoint telemetry, detection, investigation, and response capabilities |
| SIEM | Aggregates and correlates security-relevant logs and events |
| SOAR | Automates and orchestrates repetitive response workflows |
| Vulnerability scanner | Identifies potential weaknesses |
| IAM | Controls identities, authentication, authorization, and access |
| DLP | Helps prevent unauthorized disclosure or movement of sensitive data |

## 7. Operational Documentation

Security operations relies heavily on documentation. Important operational documents include:

- Security policies
- Procedures
- Standards
- Baselines
- Runbooks
- Incident response plans
- Disaster recovery plans
- Change records
- Asset inventories
- Network diagrams
- Contact and escalation lists

Documentation makes security activities repeatable and reduces dependence on individual employees.

## 8. Example Scenario

An organization discovers an unknown server connected to its internal network. Security operations should not immediately assume that it is malicious. The team should first identify the asset owner, determine its purpose, inspect its configuration, identify installed software, assess vulnerabilities, verify whether logging is enabled, and determine whether the system is authorized.

If the server is unauthorized, the organization can isolate it, investigate its origin, and determine whether it represents a security incident.

The important Security+ lesson is that **asset visibility and operational processes come before effective remediation**.

## 9. Security+ Exam Focus

Be able to distinguish:

- Security architecture from security operations
- An event from an alert
- An alert from an incident
- Preventive, detective, and corrective controls
- Monitoring from response
- Vulnerability identification from vulnerability remediation
- Security technology from the operational purpose for which it is used

## 10. Key Takeaways

- Security operations maintains security throughout the system lifecycle.
- Asset visibility is fundamental to operational security.
- Secure configuration and patch management reduce preventable exposure.
- Logs and telemetry provide evidence for detection and investigation.
- Alerts require analysis and context before being classified as incidents.
- Security operations is continuous and improves through lessons learned.
