# Logging, Monitoring, and SIEM

Logging and monitoring form the telemetry foundation of security operations. Security controls can prevent many attacks, but when suspicious activity occurs, analysts need evidence to understand what happened, when it happened, which identity and assets were involved, and whether the activity is still occurring.

A **Security Information and Event Management (SIEM)** platform brings security-relevant telemetry together so that events can be searched, normalized, correlated, detected, investigated, and reported.

The central operational model is:

**Generate → Collect → Transport → Parse/Normalize → Store → Correlate → Detect → Alert → Triage → Investigate → Respond → Document → Improve**

A major Security+ lesson is that collecting logs is not the same as monitoring an environment. Security value comes from having the **right telemetry, sufficient context, appropriate retention, reliable time, useful detection logic, and an operational process for acting on findings**.

---

# 1. What Is a Log?

A log is a record of an activity or state change produced by a system, application, security device, or service.

Examples include:

- User authentication
- Process creation
- File access
- Configuration changes
- Firewall decisions
- DNS queries
- VPN connections
- Web requests
- Database activity
- Cloud API calls
- Malware detections
- Network connections

A log answers questions such as:

```text
Who did something?
What happened?
When did it happen?
Where did it originate?
What resource was involved?
Was it successful?
What was the result?
```

These details become evidence during investigation.

---

# 2. Logs vs Events vs Alerts vs Incidents

These terms are related but should not be treated as synonyms.

### Log

A recorded piece of activity.

Example:

```text
2026-09-16 10:32:15
User: dheeraj
Authentication: failed
Source IP: 10.0.0.25
```

### Event

An occurrence that can be observed by a system. A log entry may represent that event.

### Alert

A notification generated when a rule, analytic, threshold, or detection mechanism identifies activity requiring attention.

### Incident

A confirmed or sufficiently substantiated security event that requires response according to the organization's incident-response process.

A useful progression is:

**Activity → Log/Event → Detection → Alert → Triage → Incident determination**

Not every event is an alert, and not every alert is a confirmed incident.

---

# 3. Why Logging Matters in Security Operations

Without useful logs, analysts may know that something is wrong but be unable to determine what happened.

For example, suppose an account is suspected of compromise.

Without logs:

```text
Account compromised?
Unknown
```

With authentication logs:

```text
Failed login × 80
Successful login
Unusual source IP
New device
Privileged action
```

The analyst now has evidence that can be correlated and investigated.

Logs support:

- Detection
- Investigation
- Incident response
- Threat hunting
- Forensics
- Compliance
- Troubleshooting
- Accountability
- Performance analysis

Security logging therefore has both security and operational value.

---

# 4. Common Security Log Sources

A mature monitoring architecture collects telemetry from multiple layers.

## Endpoint logs

Examples:

- Windows Event Logs
- Linux authentication logs
- Process activity
- Endpoint protection events
- EDR telemetry
- File activity
- Registry changes

## Network device logs

Examples:

- Firewall logs
- Router logs
- Switch logs
- VPN logs
- IDS/IPS alerts
- Network flow records

## Identity logs

Examples:

- Authentication attempts
- MFA events
- Password changes
- Account creation
- Account disablement
- Privilege changes
- SSO activity

## Application logs

Examples:

- Login events
- API calls
- Administrative actions
- Errors
- Transactions
- Authorization failures

## DNS logs

Examples:

- Domain queries
- Query source
- Response information
- Response codes

DNS telemetry can be useful for identifying suspicious domains and unusual query behavior.

## Cloud logs

Examples:

- Cloud control-plane API calls
- IAM activity
- Storage access
- Security-group changes
- Virtual machine activity
- Administrative changes

Cloud logging is particularly important because many administrative operations occur through APIs rather than traditional network devices.

## Email security logs

Examples:

- Sender/recipient information
- Delivery decisions
- Attachment detections
- URL detections
- Authentication results

---

# 5. Selecting the Right Log Sources

Organizations cannot necessarily collect every possible log forever. Logging strategy should therefore begin with security requirements.

Ask:

1. Which assets are critical?
2. Which identities are sensitive?
3. Which systems are internet-facing?
4. Which activities would indicate compromise?
5. Which evidence is needed for investigation?
6. Which regulatory or business requirements apply?
7. How much storage and processing capacity is available?

For example, a domain controller or identity provider is generally highly valuable to monitor because authentication and privilege activity can reveal account compromise and lateral movement.

---

# 6. Log Levels and Severity

Many platforms classify events by severity or importance.

Common conceptual levels include:

- Debug
- Informational
- Notice
- Warning
- Error
- Critical
- Alert
- Emergency

Exact names and meanings vary by platform.

A warning does not automatically mean a security incident. Severity is contextual.

For example:

```text
Failed login → Warning
```

may be routine.

But:

```text
500 failed logins
+ successful login
+ privileged account
+ unusual source
```

may warrant much greater attention.

---

# 7. Important Log Fields

Useful logs should contain enough context for analysis.

Common fields include:

- Timestamp
- Host/device
- Username or identity
- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Action
- Result
- Event type
- Process
- Application
- URL/domain
- Resource
- Session identifier
- Request identifier
- Severity

For example:

```text
Timestamp: 10:32:15
User: alice
Source IP: 10.10.10.25
Destination: server01
Action: login
Result: failure
```

The more useful context a log contains, the easier it is to correlate with other telemetry.

---

# 8. Time Synchronization

Accurate timestamps are essential during investigation.

Imagine three systems record the same attack:

```text
Firewall: 10:01:03
Endpoint: 09:56:03
SIEM:     10:06:03
```

If clocks are five minutes apart, an analyst may incorrectly conclude that events occurred in the wrong order.

Organizations therefore commonly synchronize systems using **Network Time Protocol (NTP)** or an equivalent time-synchronization architecture.

Time synchronization supports:

- Event correlation
- Incident timelines
- Forensics
- Authentication analysis
- Troubleshooting
- Distributed-system analysis

### Security+ trap

Time synchronization does not make logs trustworthy by itself. It improves temporal accuracy, while integrity controls help determine whether logs were altered.

---

# 9. Log Integrity

Logs can become evidence during an investigation, so unauthorized modification is a concern.

Controls can include:

- Centralized collection
- Restricted permissions
- Append-oriented storage
- Cryptographic integrity mechanisms
- Digital signatures where appropriate
- Immutable storage
- Write-once/read-many approaches
- Access auditing

For example, if an attacker compromises a server and can freely delete local logs, local logging alone may provide limited evidence.

Sending important logs to a separate protected system reduces the attacker's ability to erase all evidence from the source.

---

# 10. Centralized Logging

Centralized logging means collecting logs from multiple systems into a central platform or infrastructure.

A simplified architecture is:

```text
Windows ───────┐
Linux ──────────┤
Firewall ───────┤
DNS ────────────┤
VPN ────────────┼──→ Log Collection → SIEM
Cloud ──────────┤
EDR ────────────┤
Applications ───┘
```

Advantages include:

- Central search
- Correlation
- Consistent retention
- Centralized detection
- Easier investigation
- Reduced dependence on individual hosts
- Security monitoring at scale

Centralization also creates a dependency: the logging infrastructure itself must be protected and available.

---

# 11. Log Collection Methods

Logs can be collected using different mechanisms depending on the source.

Examples include:

- Agents installed on endpoints
- Syslog
- APIs
- Cloud-native log services
- Network collectors
- Event forwarding
- File-based collection
- Message queues or streaming systems

The correct mechanism depends on the platform and operational requirements.

For example, an endpoint may use an installed agent, while a network device may forward events using syslog.

---

# 12. Syslog

**Syslog** is a common mechanism for transmitting event messages, especially from network and Unix/Linux-oriented systems.

A simplified flow is:

```text
Firewall
   ↓
Syslog
   ↓
Collector
   ↓
SIEM
```

Syslog itself is a logging/transport mechanism, not a complete SIEM.

Security+ questions may test this distinction.

---

# 13. Parsing and Normalization

Different systems describe similar events differently.

One system might record:

```text
src=10.0.0.5 dst=10.0.0.10 action=deny
```

Another might record:

```text
source_address=10.0.0.5
 destination_address=10.0.0.10
 decision=blocked
```

A SIEM or log-processing pipeline can parse these values and map them into a common structure.

This is **normalization**.

Normalization makes correlation easier because the platform can compare equivalent fields across different sources.

---

# 14. SIEM — Security Information and Event Management

A **SIEM** is a platform used to centrally collect, analyze, correlate, search, and report on security-relevant event data.

Typical SIEM capabilities include:

- Log collection
- Parsing
- Normalization
- Data enrichment
- Search
- Correlation
- Detection rules
- Alert generation
- Dashboards
- Reporting
- Investigation support
- Retention

The SIEM does not replace every security control in the environment.

It consumes telemetry generated by systems and security technologies and provides centralized analysis and monitoring.

---

# 15. SIEM Architecture

A simplified SIEM architecture can be visualized as:

```text
                 ┌── Windows
                 ├── Linux
                 ├── Firewall
                 ├── DNS
                 ├── VPN
                 ├── EDR
                 ├── Cloud
                 └── Applications
                        ↓
                Collection / Ingestion
                        ↓
                 Parsing / Normalization
                        ↓
                 Enrichment / Storage
                        ↓
                    Correlation
                        ↓
                 Detection Analytics
                        ↓
                      Alert
                        ↓
                    SOC Analyst
                        ↓
              Investigation / Response
```

Every stage has an operational purpose.

---

# 16. SIEM Correlation

Correlation is one of the most important SIEM concepts.

A single event may be harmless, but multiple related events may reveal an attack pattern.

Example:

```text
Event 1: 20 failed logins
Event 2: Successful login
Event 3: New device observed
Event 4: Privileged group membership changed
Event 5: Suspicious PowerShell execution
Event 6: Outbound connection to unusual destination
```

Individually, some events may not justify an alert.

Together, they form a much stronger detection pattern.

Correlation can consider:

- Time
- User
- Host
- IP address
- Process
- Domain
- Destination
- Asset criticality
- Threat intelligence
- Previous activity

---

# 17. Rule-Based Detection

SIEM detection rules define conditions under which activity should generate an alert.

Example conceptual rule:

```text
IF
    failed_logins > threshold
AND
    successful_login occurs
AND
    source is unusual
THEN
    generate high-priority alert
```

Rules should be carefully designed because overly broad rules create excessive alerts.

---

# 18. Threshold-Based Detection

Threshold detection triggers when activity exceeds a defined limit.

Example:

```text
More than 100 failed authentication attempts
from one source within 10 minutes
```

This can detect brute-force behavior.

However, threshold selection is important.

A threshold that is too low may generate excessive false positives.

A threshold that is too high may allow attacks to remain undetected.

---

# 19. Baseline-Based Monitoring

A baseline represents expected normal behavior for a system, user, network, or application.

Example:

A service account normally communicates with:

```text
Database01
Database02
```

Suddenly it begins communicating with:

```text
External-IP-Address
```

That deviation may warrant investigation.

Baselines can include:

- Normal login times
- Typical geographic locations
- Normal bandwidth
- Common destinations
- Typical process activity
- Standard DNS patterns
- Expected administrative behavior

A baseline does not prove malicious activity. It identifies something unusual that may require investigation.

---

# 20. Signature-Based Detection

Signature-based detection looks for known patterns associated with malicious activity.

Examples include:

- Known malware hashes
- Known malicious IPs
- Known domains
- Known exploit patterns
- Known attack signatures

Strength:

- Effective against known threats

Limitation:

- New or modified threats may not match existing signatures

This is why modern detection strategies combine signatures with behavioral and contextual analysis.

---

# 21. Behavioral Detection

Behavioral detection looks for suspicious activity rather than requiring an exact known malicious signature.

Examples:

- Unusual process execution
- Impossible or abnormal authentication patterns
- Sudden privilege changes
- Rare administrative activity
- Unexpected data transfer
- Abnormal DNS behavior

Behavioral detection can identify previously unseen activity, but it may produce more false positives and therefore requires tuning and contextual analysis.

---

# 22. Anomaly Detection

Anomaly detection identifies activity that differs significantly from an established baseline or expected pattern.

For example:

```text
Normal:
User logs in from Bengaluru during business hours.

Observed:
Same account authenticates from another country shortly afterward.
```

This could be:

- Credential compromise
- VPN use
- Travel
- Corporate proxy
- Shared account
- False positive

Therefore, an anomaly is a **signal**, not automatically a confirmed incident.

---

# 23. Threat Intelligence Enrichment

SIEM data can be enriched with external or internal context.

Examples include:

- IP reputation
- Domain reputation
- Malware hashes
- Geolocation
- ASN information
- Asset criticality
- User role
- Known vulnerabilities

Example:

```text
Outbound connection
      ↓
Destination IP
      ↓
Threat intelligence lookup
      ↓
Known malicious infrastructure
      ↓
Detection confidence increases
```

Threat intelligence should be treated as context. A reputation result alone should not automatically determine the complete incident response without considering the environment and evidence.

---

# 24. Alert Generation

An alert is generated when detection logic identifies activity requiring attention.

Useful alerts should answer:

- What happened?
- Which asset is affected?
- Which user is involved?
- When did it happen?
- Why was it detected?
- What evidence supports it?
- How severe might it be?

A poor alert might say:

```text
Suspicious activity detected.
```

A useful alert might provide:

```text
User: alice
Host: FIN-PC-12
Detection: suspicious PowerShell download
Parent process: WINWORD.EXE
Destination: suspicious-domain.example
First observed: 10:32
```

Context dramatically reduces investigation time.

---

# 25. False Positives

A **false positive** occurs when legitimate activity is incorrectly identified as suspicious.

Example:

```text
Backup system performs 500 connections
Detection: possible network scan
```

The behavior resembles scanning, but the activity is authorized.

Too many false positives cause **alert fatigue**, where analysts become overwhelmed and may miss important alerts.

Common ways to reduce false positives include:

- Threshold tuning
- Allowlisting known legitimate activity
- Asset/user context
- Maintenance-window awareness
- Better correlation
- Detection refinement

---

# 26. False Negatives

A **false negative** occurs when malicious activity occurs but the detection mechanism fails to identify it.

Example:

```text
Attacker performs low-and-slow credential attacks
Detection threshold is too high
No alert generated
```

False negatives are dangerous because the security team may have no indication that the attack occurred.

The operational challenge is therefore to balance:

**Detection coverage ↔ False positives ↔ Analyst workload**

---

# 27. Alert Triage

When an alert arrives, an analyst should first determine its nature and priority.

A practical triage process is:

1. Validate the alert.
2. Identify the affected asset.
3. Identify the user or account.
4. Review supporting events.
5. Determine whether activity is expected.
6. Determine whether compromise is plausible.
7. Determine scope.
8. Assign appropriate priority.
9. Escalate or respond according to procedure.

The analyst should avoid treating the alert title as the conclusion.

The alert is the **starting point of investigation**, not necessarily the final verdict.

---

# 28. Alert Severity vs Incident Priority

These concepts can be related but are not identical.

A detection engine may classify an alert as high severity because it matched a suspicious rule.

The SOC may adjust priority based on:

- Asset criticality
- User privilege
- Evidence quality
- Scope
- Business impact
- Current attack activity
- Confidence

For example, the same malware detection on a disposable test machine and a domain controller can have very different operational consequences.

---

# 29. Log Retention

Retention determines how long logs are stored and available for analysis.

Retention requirements can be influenced by:

- Security investigation needs
- Compliance requirements
- Legal requirements
- Business requirements
- Storage capacity
- Data sensitivity

Longer retention provides a larger historical window but increases storage and management requirements.

### Hot vs cold data

Frequently accessed recent data may be stored in faster storage for rapid searching.

Older data may be moved to lower-cost archival storage.

The exact architecture varies by organization.

---

# 30. Log Storage and Privacy

Security logs may contain sensitive information such as:

- Usernames
- IP addresses
- Email addresses
- URLs
- Device identifiers
- Authentication metadata

Logging therefore needs appropriate:

- Access controls
- Retention policies
- Data minimization
- Encryption
- Privacy controls

More logging is not automatically better if unnecessary sensitive information is collected without a legitimate purpose.

---

# 31. Log Collection Gaps

A SIEM dashboard can appear healthy while important telemetry is missing.

For example:

```text
Firewall → SIEM ✓
DNS → SIEM ✓
EDR → SIEM ✓
Domain Controller → SIEM ✗
```

The environment may have a major visibility gap around identity activity.

Operational monitoring should therefore monitor the **logging pipeline itself**.

Useful checks include:

- Last event received
- Event volume
- Collector health
- Agent health
- Parsing failures
- Storage capacity
- Network connectivity
- Authentication failures

---

# 32. Detecting a Broken Logging Pipeline

Suppose a server normally generates 10,000 events per hour.

Suddenly:

```text
10,000 → 9,800 → 10,200 → 12 → 0
```

The absence of events may itself be suspicious.

Possible causes include:

- Agent failure
- Network failure
- Collector failure
- Configuration change
- Storage problem
- Service outage
- Deliberate log suppression

A mature monitoring architecture should therefore detect both **security events and telemetry failures**.

---

# 33. SIEM Data Normalization and Enrichment

A SIEM may transform raw telemetry into a consistent schema.

Example:

```text
Firewall field: src_ip
DNS field:      client_ip
EDR field:      remote_address
```

The SIEM can map these into a common conceptual field such as:

```text
source.ip
```

Enrichment can then add context:

```text
source.ip = 10.10.10.25
asset = Finance-Laptop-12
user = alice
criticality = high
location = Bengaluru
```

This makes detection and investigation more efficient.

---

# 34. Correlation Example — Brute Force

Consider this sequence:

```text
10:00 → Failed login
10:01 → Failed login
10:02 → Failed login
...
10:08 → Failed login × 100
10:09 → Successful login
10:10 → Privileged action
```

A SIEM correlation rule might identify the combination as suspicious.

The analyst should then investigate:

- Source IP
- User account
- Target system
- Authentication method
- Whether the successful login was legitimate
- What actions followed
- Whether other accounts were targeted

This is more useful than looking at each authentication event in isolation.

---

# 35. Correlation Example — Lateral Movement

Suppose the following occurs:

```text
Workstation A compromised
       ↓
Authentication to Server B
       ↓
Authentication to Server C
       ↓
Remote administrative execution
       ↓
New privileged account activity
```

Correlating endpoint, identity, and network telemetry may reveal lateral movement.

A single successful remote login may be normal. The sequence and context are what make the activity suspicious.

---

# 36. Correlation Example — Data Exfiltration

A possible exfiltration pattern could be:

```text
Sensitive database access
        ↓
Large data extraction
        ↓
Archive/compression activity
        ↓
Unexpected outbound connection
        ↓
Large encrypted transfer
```

Useful telemetry might come from:

- Database logs
- Endpoint telemetry
- Network flow
- Firewall logs
- Proxy logs
- DLP systems
- Identity logs

This illustrates why security monitoring should combine multiple telemetry sources.

---

# 37. Dashboards

SIEM dashboards provide visual summaries of security activity.

Useful dashboards may show:

- Authentication failures
- Critical alerts
- Top source IPs
- Top destination IPs
- Malware detections
- VPN activity
- Privileged-account actions
- Firewall denies
- High-risk assets
- Log-source health

Dashboards are useful for situational awareness, but a dashboard itself does not constitute detection.

An analyst still needs meaningful analytics and investigation procedures.

---

# 38. Reporting

SIEM platforms can support reports for different audiences.

### SOC analysts

Need detailed technical information.

### Security managers

May need trends, incident counts, response metrics, and risk indicators.

### Auditors

May require evidence that logging and monitoring controls operate as required.

### Executives

Usually need concise business-oriented information rather than raw event records.

The same telemetry can therefore support different reporting layers.

---

# 39. SIEM vs SOAR

These technologies are related but serve different primary functions.

**SIEM:** collects, correlates, analyzes, and alerts on security telemetry.

**SOAR:** orchestrates and automates security workflows and response actions.

Example:

```text
SIEM detects suspicious login
        ↓
Alert created
        ↓
SOAR playbook starts
        ↓
Enrich IP reputation
        ↓
Check user context
        ↓
Create ticket
        ↓
Request/perform containment action
```

A SIEM can trigger automation, but SIEM and SOAR should not be treated as identical technologies.

---

# 40. SIEM vs Log Management

**Log management** primarily focuses on collecting, transporting, storing, searching, and managing logs.

A **SIEM** adds security-focused analysis such as:

- Correlation
- Detection rules
- Security alerting
- Security investigation
- Security dashboards

There can be overlap between modern platforms, but Security+ questions commonly distinguish the primary purpose.

---

# 41. SIEM vs EDR

**EDR** focuses primarily on endpoint telemetry, detection, investigation, and response.

**SIEM** provides centralized analysis and correlation across many sources.

For example:

```text
EDR → process tree on workstation
SIEM → correlate workstation process + identity + DNS + firewall + cloud activity
```

EDR can feed telemetry into a SIEM.

---

# 42. SIEM Operational Tuning

A SIEM that generates thousands of low-value alerts can become less useful than a smaller, well-tuned detection set.

Tuning may involve:

- Adjusting thresholds
- Excluding known legitimate activity
- Improving correlation conditions
- Adding asset context
- Adding identity context
- Updating threat intelligence
- Retiring obsolete rules
- Reviewing false-positive rates

Tuning should not simply suppress difficult alerts. Every exception should have a documented reason and appropriate review.

---

# 43. Detection Engineering Lifecycle

Detection rules should be treated as operational content that requires maintenance.

A useful lifecycle is:

**Requirement → Data source → Detection logic → Testing → Deployment → Monitoring → Tuning → Validation → Retirement**

For example, if a detection depends on a firewall field that later changes format, the rule may silently stop working.

Therefore, detection content must be monitored just like other security technology.

---

# 44. Monitoring the Monitoring System

A common operational mistake is to monitor the environment while ignoring the health of the monitoring infrastructure.

Important questions include:

- Are logs still arriving?
- Are collectors healthy?
- Are agents online?
- Are parsing rules working?
- Is storage full?
- Are detection rules executing?
- Are alerts being delivered?
- Are timestamps correct?

A broken SIEM pipeline can create a dangerous **false sense of security**.

---

# 45. Common Logging and SIEM Failures

## Failure 1 — Collecting everything without a strategy

This can create enormous storage and processing requirements while burying analysts in low-value data.

Better approach: prioritize telemetry based on assets, threats, detection requirements, and retention needs.

## Failure 2 — No time synchronization

Events cannot be reliably ordered.

Better approach: maintain centralized and monitored time synchronization.

## Failure 3 — No log integrity protection

An attacker may alter or delete evidence.

Better approach: centralize critical logs and protect access and storage.

## Failure 4 — Excessive false positives

Analysts become overloaded.

Better approach: tune detections using context and legitimate-activity analysis.

## Failure 5 — Overly high thresholds

Low-volume attacks may never trigger alerts.

Better approach: combine thresholds with behavioral and contextual detection.

## Failure 6 — Ignoring missing logs

A silent collector failure can look like a quiet environment.

Better approach: implement health monitoring for log sources and collectors.

## Failure 7 — Treating every alert as an incident

This wastes response resources.

Better approach: triage and investigate before declaring an incident, except where established procedures require immediate containment.

## Failure 8 — No asset context

The same event can have very different significance depending on the affected system.

Better approach: enrich SIEM data with asset criticality and ownership.

---

# 46. Practical SOC Investigation Workflow

When investigating a SIEM alert, use a structured approach.

### Step 1 — Read the detection

Understand exactly what rule fired and why.

### Step 2 — Identify the affected asset

Determine hostname, IP, asset owner, and criticality.

### Step 3 — Identify the identity

Determine which user, service account, or workload identity was involved.

### Step 4 — Establish the timeline

Use synchronized timestamps to reconstruct events.

### Step 5 — Pivot through related telemetry

Search:

- Authentication
- Endpoint
- DNS
- Firewall
- VPN
- Proxy
- Application
- Cloud

### Step 6 — Determine scope

Look for the same indicator or behavior elsewhere.

### Step 7 — Determine whether the activity is legitimate

Check change records, maintenance windows, known administrative activity, and user context.

### Step 8 — Assess compromise

Determine whether the evidence supports malicious activity.

### Step 9 — Respond according to procedure

Contain, escalate, investigate further, or close as appropriate.

### Step 10 — Document

Record evidence, actions, conclusions, and lessons learned.

---

# 47. Practical Example — Suspicious PowerShell

Suppose the SIEM generates:

```text
Alert: Suspicious PowerShell execution
Host: DESKTOP-01
User: alice
```

Do not immediately conclude that the endpoint is compromised.

Investigate:

```text
Who launched PowerShell?
        ↓
What was the parent process?
        ↓
What command was executed?
        ↓
Was the user authorized to run it?
        ↓
Was a file downloaded?
        ↓
What domain/IP was contacted?
        ↓
Was persistence created?
        ↓
Did similar activity occur elsewhere?
```

A system administrator running an approved script may generate a similar event to an attacker using PowerShell for execution.

Context determines the significance.

---

# 48. Practical Example — Impossible Travel

A SIEM detects:

```text
08:00 → User authenticates from Bengaluru
08:20 → Same account authenticates from London
```

This appears anomalous, but possible explanations include:

- VPN
- Corporate proxy
- Cloud service routing
- Travel with inaccurate source attribution
- Shared credentials
- Compromised account

The analyst should examine device information, authentication method, source infrastructure, VPN logs, and other contextual evidence before determining the appropriate response.

---

# 49. Practical Example — Firewall Alert

Suppose the SIEM receives:

```text
Firewall: denied inbound connection
Source: 203.0.113.20
Destination: public-server
Port: 22
```

One denied connection is not necessarily an incident.

But suppose the SIEM correlates:

```text
5,000 connection attempts
        ↓
Multiple ports
        ↓
Multiple internal targets
        ↓
Known scanning source
```

The activity is more consistent with reconnaissance or scanning and may warrant investigation.

---

# 50. Security+ Exam Distinctions

| Concept | Primary purpose |
|---|---|
| Logging | Record activity |
| Log management | Collect, transport, store, and manage logs |
| SIEM | Centralize, correlate, analyze, detect, and alert on security telemetry |
| IDS | Detect suspicious network/system activity |
| EDR | Endpoint telemetry, detection, investigation, response |
| XDR | Cross-domain detection and response correlation |
| SOAR | Automate/orchestrate security workflows |
| Syslog | Common event logging/transport mechanism |
| NTP | Time synchronization |
| Threat intelligence | Context about threats/indicators |
| Dashboard | Visualize security information |
| Alert | Notification generated by detection logic |
| Incident | Security event requiring formal response |

---

# 51. Security+ Exam Traps

### Trap 1 — “Every log entry is an alert”

False. Logs are records. Detection logic determines when activity becomes an alert.

### Trap 2 — “Every alert is an incident”

False. Alerts require triage and investigation unless established procedures dictate immediate response.

### Trap 3 — “SIEM prevents attacks”

Not primarily. SIEM is primarily a monitoring, analysis, correlation, and alerting platform.

### Trap 4 — “More logs automatically mean better security”

Not necessarily. Poorly selected telemetry can increase cost and analyst workload without improving detection.

### Trap 5 — “An anomaly proves compromise”

False. Anomaly means deviation from expected behavior.

### Trap 6 — “High alert severity always means highest incident priority”

Not necessarily. Asset criticality, confidence, scope, and business impact also matter.

### Trap 7 — “NTP provides log integrity”

No. NTP provides time synchronization.

### Trap 8 — “Centralized logs cannot be altered”

Not automatically. Centralized logging still requires access control, integrity protection, and secure storage.

### Trap 9 — “A broken log source means nothing happened”

The opposite may be true. Missing telemetry can represent a technical failure or deliberate suppression.

---

# 52. Security Monitoring Decision Framework

When a Security+ question presents a monitoring scenario, work through these steps:

### 1. What happened?

Identify the event or behavior.

### 2. Where did the evidence originate?

Endpoint, identity, firewall, DNS, cloud, application, etc.

### 3. Is the telemetry available?

If not, the first requirement may be logging or collection rather than detection.

### 4. Is the data normalized and correlated?

If multiple sources need to be analyzed together, centralized correlation becomes important.

### 5. What detection method fits?

Consider:

- Signature
- Threshold
- Behavior
- Baseline/anomaly
- Correlation
- Threat intelligence

### 6. What happened after detection?

Determine whether the requirement is:

- Alerting
- Triage
- Investigation
- Containment
- Automation

### 7. What operational limitation exists?

Consider:

- False positives
- False negatives
- Storage
- Retention
- Privacy
- Missing telemetry
- Time synchronization
- Detection tuning

---

# 53. End-to-End SIEM Example

Consider a suspected account compromise.

```text
User authentication failure
        ↓
Identity provider logs event
        ↓
Log collector receives event
        ↓
SIEM parses and normalizes event
        ↓
Second authentication failure
        ↓
Successful authentication
        ↓
Source reputation enriched
        ↓
New device observed
        ↓
Privileged action detected
        ↓
Correlation rule matches
        ↓
Alert generated
        ↓
SOC analyst triages
        ↓
Endpoint + DNS + firewall telemetry reviewed
        ↓
Compromise assessed
        ↓
Response initiated
        ↓
Incident documented
        ↓
Detection tuned using lessons learned
```

This is the operational purpose of SIEM: turning large amounts of distributed telemetry into actionable security information.

---

# 54. Key Takeaways

1. Logs are records of system or application activity.
2. Events are observable occurrences; alerts are generated by detection mechanisms; incidents require response according to organizational criteria.
3. Logging supports detection, investigation, forensics, compliance, and troubleshooting.
4. Important sources include endpoints, identity systems, applications, firewalls, DNS, VPNs, cloud platforms, and security technologies.
5. Useful logs require accurate timestamps and sufficient context.
6. Time synchronization is essential for reliable event timelines.
7. Log integrity protects evidence from unauthorized modification.
8. Centralized logging improves visibility and correlation.
9. Parsing and normalization allow different log sources to be analyzed consistently.
10. SIEM provides centralized security telemetry collection, correlation, analysis, detection, alerting, search, dashboards, and reporting.
11. Correlation can reveal attack patterns that are not visible in individual events.
12. Threshold detection is useful but requires careful tuning.
13. Baseline and anomaly detection identify deviations from expected behavior.
14. Threat intelligence can enrich events with additional context.
15. False positives create analyst workload and alert fatigue.
16. False negatives represent missed malicious activity.
17. Alert severity and incident priority are not necessarily identical.
18. Retention must balance investigation requirements, compliance, privacy, and cost.
19. The logging pipeline itself must be monitored for failures.
20. SIEM, SOAR, EDR, and log management have different primary purposes.
21. A SIEM does not replace endpoint, network, identity, or application security controls.
22. Good SOC investigation uses the SIEM as a pivot point across multiple telemetry sources.
23. Security monitoring should continuously improve through tuning, validation, and lessons learned.

---

# Final Mental Model

Remember the complete security-monitoring pipeline as:

**Generate → Collect → Transport → Parse → Normalize → Store → Enrich → Correlate → Detect → Alert → Triage → Investigate → Respond → Document → Tune**

And remember the most important distinction:

> **Logs provide evidence. Detection logic identifies suspicious patterns. Alerts bring those patterns to analyst attention. Investigation determines what actually happened.**

That distinction is fundamental to Security+ and to real-world SOC operations.