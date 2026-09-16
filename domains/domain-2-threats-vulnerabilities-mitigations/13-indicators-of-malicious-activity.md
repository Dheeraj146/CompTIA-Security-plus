# 13 — Indicators of Malicious Activity

## 1. Introduction

A **security indicator** is an observable piece of evidence that may suggest suspicious, malicious, or otherwise abnormal activity.

Indicators are important because security teams rarely begin an investigation with complete certainty. Instead, analysts observe events and determine whether the available evidence is consistent with normal activity, suspicious behavior, or a confirmed security incident.

Examples include:

- Repeated failed logins
- An unusual privileged login
- A new process appearing on an endpoint
- Unexpected outbound network traffic
- Communication with suspicious infrastructure
- Abnormal DNS activity
- Large unexpected data transfers
- Security software being disabled
- Unexpected file encryption
- Unusual application behavior

An important principle is:

> **An indicator is evidence that deserves investigation; it is not automatically proof of compromise.**

Context, correlation, baselines, and investigation are required before determining what actually happened.

---

# 2. Indicator vs Event vs Alert vs Incident

These terms are related but should not be treated as synonyms.

### Event

An **event** is an observable occurrence in a system or environment.

Examples:

- User login
- Process creation
- Firewall connection
- DNS query
- File modification

An event may be completely normal.

### Indicator

An **indicator** is an observable characteristic that may suggest malicious or suspicious activity.

Example:

A workstation suddenly begins connecting to an unfamiliar external server every five minutes.

### Alert

An **alert** is a notification generated because a security rule, analytic, threshold, or detection mechanism identified activity that may require attention.

### Incident

A **security incident** is an event or series of events that has been determined to represent a security problem requiring response according to the organization's incident-response criteria.

### Simplified relationship

**Event → Potential indicator → Detection/alert → Investigation → Incident determination**

Not every event becomes an alert, and not every alert becomes a confirmed incident.

---

# 3. Indicators Are Not Automatically Proof

Security analysts must avoid treating every unusual event as malicious.

For example:

A user logs in from a different country.

Possible explanations include:

- The user is traveling.
- The user is using a corporate VPN.
- The organization routes traffic through another region.
- The account has been compromised.

The geographic difference is therefore an **indicator requiring context**, not automatic proof of account compromise.

Good analysis asks:

- Is the activity unusual for this user?
- Is the device known?
- Was MFA successfully completed?
- Does the VPN explain the source address?
- Are there other suspicious events?
- Does the activity match the user's normal behavior?

---

# 4. Categories of Malicious Activity Indicators

Indicators can be grouped according to where the evidence appears.

Common categories include:

1. Identity and account indicators
2. Endpoint indicators
3. Network indicators
4. Application indicators
5. Email indicators
6. Cloud indicators
7. File and data indicators
8. Physical indicators
9. Authentication indicators
10. Security-control indicators

A strong investigation correlates evidence across multiple categories.

---

# 5. Account and Identity Indicators

Identity telemetry is especially valuable because attackers frequently abuse legitimate accounts.

Potential indicators include:

- Repeated authentication failures
- Successful authentication after numerous failures
- Login from an unusual location
- Login from an unfamiliar device
- Impossible-travel patterns
- Unexpected password changes
- Unexpected MFA changes
- New privileged accounts
- Privilege changes
- Use of dormant accounts
- Login outside normal working patterns
- Unusual access to sensitive resources

These indicators become stronger when several occur together.

---

# 6. Repeated Authentication Failures

A large number of failed authentication attempts may indicate:

- Brute-force activity
- Password spraying
- User error
- Misconfigured applications
- Expired credentials
- Automated service failures

The analyst should investigate the source, timing, affected accounts, and subsequent successful authentication.

### Stronger indicator

A sequence such as:

**Many failed logins → successful login → unusual resource access**

may provide stronger evidence than failed authentication alone.

---

# 7. Successful Login After Repeated Failures

A successful login immediately following numerous failed attempts deserves attention.

Possible explanations include:

- The legitimate user finally entered the correct password.
- A password was discovered or guessed.
- An attacker obtained valid credentials.
- An automated process was misconfigured.

The security team should correlate the successful login with:

- Source IP
- Device
- Location
- MFA result
- Account privileges
- Subsequent activity

---

# 8. Impossible Travel

**Impossible travel** is a detection concept in which an account appears to authenticate from geographically distant locations within a time period that would make normal physical travel implausible.

Example:

A user authenticates from one country and shortly afterward authenticates from another distant country.

Possible explanations include:

- Credential compromise
- VPN or proxy use
- Cloud infrastructure
- Corporate network routing
- Inaccurate geolocation
- Shared credentials

Therefore, impossible travel is an indicator, not definitive proof of compromise.

---

# 9. New Privileged Accounts

Unexpected creation of an administrative or privileged account can be a significant indicator.

Attackers may attempt to establish additional access after compromising an environment.

An analyst should determine:

- Who created the account?
- Was the creation authorized?
- What privileges were assigned?
- Which system created it?
- Was there an approved change request?
- What actions did the account perform afterward?

---

# 10. Dormant Account Activity

A dormant account is an account that has not been used for a significant period.

Unexpected use can be suspicious because inactive accounts may:

- Be forgotten
- Have outdated passwords
- Have excessive privileges
- Lack current monitoring expectations

An unexpected login should be correlated with account ownership and business context.

---

# 11. Endpoint Indicators

Endpoint telemetry provides visibility into what is happening on workstations, servers, and other computing devices.

Potential indicators include:

- Unexpected processes
- Suspicious parent-child process relationships
- Unknown services
- Unexpected scheduled tasks
- Persistence mechanisms
- Security tools being disabled
- Unusual file modifications
- Unexpected executable files
- Abnormal CPU or memory usage
- Unexpected administrative tools
- New local accounts
- Suspicious outbound connections

EDR and endpoint logging can help analysts investigate these indicators.

---

# 12. Unexpected Processes

A process that is unusual for a particular system can be an indicator.

For example, a workstation that normally runs productivity applications suddenly launches an unfamiliar executable from an unusual directory.

The analyst should investigate:

- Process name
- File path
- Parent process
- User context
- Command-line information where available
- File hash
- Network connections
- Creation time
- Digital signature

A process name alone is rarely enough to determine maliciousness.

---

# 13. Suspicious Parent-Child Process Relationships

Process ancestry can reveal suspicious behavior.

For example, an unexpected document application spawning an interpreter or command shell may deserve investigation depending on the environment and expected workflows.

The key concept is **behavioral context**.

Analysts should ask:

**Is this process relationship normal for this application and user?**

EDR platforms often make process-tree analysis easier.

---

# 14. Unexpected Services and Scheduled Tasks

Attackers may establish persistence through services or scheduled execution mechanisms.

Potential indicators include:

- Newly created services
- Modified services
- Unexpected scheduled tasks
- Execution from unusual directories
- Tasks created by unusual accounts

These indicators should be correlated with change-management records and system-administration activity.

---

# 15. Security Controls Being Disabled

Unexpected attempts to disable security controls can be significant.

Examples include:

- Endpoint protection disabled
- Firewall disabled
- Logging stopped
- Audit settings changed
- Security agents terminated

Possible explanations include:

- Legitimate maintenance
- Troubleshooting
- Software conflicts
- Administrative changes
- Malicious activity

Change records and administrative logs help determine the context.

---

# 16. Unexpected Administrative Tools

The appearance of powerful administrative utilities on systems where they are not normally used may warrant investigation.

Examples conceptually include:

- Remote administration tools
- System-management utilities
- Scripting environments
- Credential-management utilities
- Network diagnostic tools

These tools are often legitimate, so their presence alone is not proof of malicious activity.

The analyst should consider:

- Who executed the tool?
- Why was it executed?
- Was it expected on the asset?
- What arguments or actions were associated with it?
- What happened afterward?

---

# 17. Abnormal File Modifications

Unexpected modifications to files can indicate:

- Malware activity
- Data tampering
- Unauthorized configuration changes
- Ransomware
- Legitimate software updates

Important contextual information includes:

- Which files changed?
- How many changed?
- Which account made the changes?
- When did the changes occur?
- What process made them?

A large number of rapid modifications can be particularly important when combined with other indicators.

---

# 18. Large-Scale File Encryption

Unexpected encryption of many files can indicate ransomware activity.

Possible indicators include:

- Rapid file modifications
- New encrypted file formats/extensions
- High disk activity
- Ransom-note files
- Multiple affected directories
- Endpoint security alerts

A single encrypted file may have a legitimate explanation. Large-scale unexpected encryption is much more significant when correlated with other evidence.

---

# 19. Unusual Resource Consumption

Sudden changes in resource usage can indicate malicious activity, although many legitimate causes exist.

Examples include:

- High CPU usage
- High memory usage
- Unusual disk activity
- High network utilization

Potential causes include:

- Malware
- Cryptomining
- Data processing
- Software updates
- Backups
- Normal workload changes

Baseline comparison is important.

---

# 20. Network Indicators

Network telemetry can reveal communication patterns associated with malicious activity.

Potential indicators include:

- Unexpected outbound connections
- Beaconing
- Connections to known malicious infrastructure
- Large outbound data transfers
- Unusual DNS requests
- Unexpected protocols
- Unexpected ports
- Scanning behavior
- Repeated connections at regular intervals
- Remote-administration traffic that is unusual for the environment

Network indicators should be interpreted in the context of normal network behavior.

---

# 21. Beaconing

**Beaconing** describes repeated communication between a system and another endpoint at regular or characteristic intervals.

An infected system may periodically communicate with command-and-control infrastructure.

For example:

**Endpoint → external host → wait → endpoint → external host → wait**

Regularity can make beaconing useful as a detection signal.

However, legitimate software also communicates periodically, so analysts must establish whether the destination and behavior are expected.

---

# 22. Command-and-Control Indicators

Potential C2 indicators include:

- Connections to suspicious domains or IP addresses
- Periodic outbound communication
- Unusual encrypted traffic patterns
- Unexpected DNS activity
- Communication with infrastructure associated with malicious activity

Analysts can correlate:

**Endpoint process → network connection → destination → DNS resolution → user activity**

This can help identify which process generated suspicious traffic.

---

# 23. Large Outbound Data Transfers

Unexpected large outbound transfers may indicate:

- Data exfiltration
- Cloud synchronization
- Backups
- Software updates
- Legitimate business transfers

The important questions are:

- What data was transferred?
- Where was it sent?
- Which user or process initiated it?
- Was the destination authorized?
- Was the volume normal for the asset?

### Stronger evidence

A sensitive database server suddenly transmitting unusually large volumes of data to an unfamiliar external destination deserves immediate investigation.

---

# 24. DNS Indicators

DNS telemetry can reveal suspicious behavior.

Potential indicators include:

- Requests for suspicious domains
- High volumes of DNS queries
- Random-looking domain names
- Unusual record types
- DNS requests to unexpected resolvers
- Frequent requests for domains with short lifetimes

DNS activity can support detection of malware, command-and-control infrastructure, or other suspicious behavior.

---

# 25. DNS Tunneling Indicators

DNS can be abused to carry information through DNS queries and responses.

Potential indicators of DNS tunneling include:

- Unusually long DNS labels
- High-frequency DNS requests
- High-entropy/random-looking subdomains
- Large amounts of data encoded in DNS queries
- Repeated requests to a suspicious domain

These characteristics are indicators rather than definitive proof.

---

# 26. Network Scanning Indicators

A system contacting many hosts or many ports in a short period may indicate scanning.

Potential evidence includes:

- Sequential connection attempts
- Large numbers of failed connections
- Contact with many internal hosts
- Many destination ports
- Sudden changes from the host's normal network behavior

Scanning can be legitimate, especially for vulnerability-management tools, so the source should be identified and correlated with authorized scanning schedules.

---

# 27. Application Indicators

Application logs can reveal suspicious behavior that endpoint and network telemetry may not fully explain.

Potential indicators include:

- Repeated authorization failures
- Unexpected administrative actions
- Abnormal API requests
- Sudden configuration changes
- Unexpected data modification
- Unusual login patterns
- Abnormal input behavior
- Unexpected account creation

Application indicators are especially useful when investigating attacks against web applications and APIs.

---

# 28. Authentication vs Authorization Indicators

Analysts must distinguish authentication problems from authorization problems.

### Authentication

Authentication answers:

**Who are you?**

Indicators may include:

- Repeated login failures
- Unusual login locations
- Suspicious MFA activity
- Password changes

### Authorization

Authorization answers:

**What are you allowed to do?**

Indicators may include:

- A normal user accessing administrative functionality
- Access to another user's resources
- Unexpected privilege changes
- Access to restricted records

This distinction is important for Security+ scenario questions.

---

# 29. Privilege Escalation Indicators

Potential indicators include:

- Unexpected administrative group membership
- New privileged accounts
- Administrative activity from standard-user endpoints
- Sudden privilege changes
- Administrative actions outside normal workflows

The analyst should determine whether the privilege change was authorized.

---

# 30. Email Indicators

Email can provide important evidence during investigations.

Potential indicators include:

- Unexpected attachments
- Suspicious links
- Spoofed sender information
- Unusual sender domains
- Requests for credentials
- Unexpected financial requests
- Messages creating unusual urgency
- Similar messages delivered to many users

Email indicators can be correlated with endpoint activity.

For example:

**Suspicious email → attachment opened → unusual process → outbound connection**

This chain is stronger than any individual indicator alone.

---

# 31. Cloud Indicators

Cloud environments generate their own telemetry.

Potential indicators include:

- Unusual API calls
- Unexpected administrative changes
- New access keys
- New privileged identities
- Unusual cloud-region activity
- Unexpected storage access
- Public exposure changes
- Large data transfers
- Changes to security controls

Cloud activity should be compared against normal administrative behavior and approved change processes.

---

# 32. New Access Keys or Tokens

Unexpected creation or use of access keys, API tokens, or other machine identities can be suspicious.

Analysts should determine:

- Who created the credential?
- What permissions does it have?
- Where is it being used?
- Is its creation documented?
- Is the usage pattern normal?

Unexpected privileged credentials can create significant risk because attackers may use them for persistent access.

---

# 33. Security-Control Tampering

Attackers may attempt to weaken visibility or prevention mechanisms.

Indicators can include:

- Logging disabled
- Audit policies modified
- EDR agent stopped
- Firewall rules changed unexpectedly
- SIEM forwarding interrupted
- Security alerts suppressed

Security-control tampering can itself be an important detection signal.

---

# 34. Log Gaps

A sudden disappearance of expected logs may be suspicious.

For example:

A server normally sends authentication logs to the SIEM, but log forwarding unexpectedly stops immediately before suspicious administrative activity occurs.

Possible causes include:

- Network failure
- Agent failure
- Storage problem
- Configuration change
- Maintenance
- Deliberate tampering

Analysts should investigate the cause rather than automatically assuming malicious activity.

---

# 35. Indicators of Data Exfiltration

Potential exfiltration indicators include:

- Large outbound transfers
- Access to unusually large numbers of files
- Archive creation before outbound transfer
- Unexpected cloud uploads
- Unusual database queries
- Sensitive files accessed outside normal patterns
- Connections to unfamiliar external destinations

The strongest analysis correlates identity, endpoint, network, and data-access telemetry.

---

# 36. Indicators of Persistence

Persistence allows an attacker or malware to maintain access across reboots, sessions, or other changes.

Potential indicators include:

- New services
- Scheduled tasks
- Startup modifications
- Unexpected accounts
- New credentials
- Modified authentication mechanisms
- Suspicious application extensions

A persistence indicator should be correlated with the time of suspected initial compromise.

---

# 37. Indicators of Lateral Movement

Potential indicators include:

- One workstation accessing many internal systems
- Unusual administrative authentication
- Remote-access activity from unexpected hosts
- Authentication using privileged accounts from unusual endpoints
- Sudden access to servers that the user normally does not administer

The analyst should determine whether the activity matches legitimate administrative workflows.

---

# 38. Indicators of Command and Control vs Data Exfiltration

These two activities can produce different telemetry.

### C2

Often involves:

- Repeated outbound communication
- Suspicious destinations
- Beaconing
- DNS anomalies

### Exfiltration

Often involves:

- Large or unusual outbound data transfers
- Sensitive data access
- Archive creation
- Unusual external destinations

They can occur in the same intrusion but represent different stages or objectives.

---

# 39. Baselines

A **baseline** describes expected behavior for a system, user, network, application, or environment.

Without a baseline, detecting abnormal behavior can be difficult.

Examples include:

- Normal login locations
- Normal login times
- Typical network volume
- Normal applications
- Normal administrative actions
- Typical DNS activity
- Normal CPU utilization

### Example

A database server normally sends 50 MB of data externally per day but suddenly sends 20 GB overnight.

The deviation from the established baseline is itself a useful indicator.

---

# 40. Anomaly Detection

**Anomaly detection** identifies behavior that differs significantly from expected patterns.

Anomaly detection can use:

- Statistical baselines
- Behavioral models
- User and Entity Behavior Analytics (UEBA)
- Machine-learning techniques
- Thresholds

An anomaly is not automatically malicious.

The analyst must investigate whether there is a legitimate explanation.

---

# 41. Correlation

Security events become more useful when correlated.

Consider these events individually:

- Failed login
- New process
- DNS query
- Outbound connection

Each may have a benign explanation.

Now consider the sequence:

**Phishing email → user opens attachment → unusual process → suspicious DNS query → periodic outbound connection → new persistence mechanism**

The combined evidence provides a much stronger basis for investigation.

This is why SIEM platforms correlate events from multiple data sources.

---

# 42. Indicators of Compromise vs Indicators of Attack

The terms are related but emphasize different evidence.

### Indicator of Compromise (IoC)

An **IoC** is evidence associated with a system that may indicate it has been compromised.

Examples can include:

- Known malicious hash
- Malicious IP address
- Malicious domain
- Suspicious file
- Unexpected persistence artifact

### Indicator of Attack (IoA)

An **IoA** focuses more on suspicious behavior or attack activity.

Examples can include:

- Suspicious process behavior
- Unusual authentication sequence
- Abnormal privilege escalation
- Unexpected lateral movement

### Important distinction

**IoC → evidence associated with compromise.**

**IoA → evidence of suspicious attack behavior.**

In practice, organizations may use both concepts together.

---

# 43. IoC Types

Common IoCs include:

### File-based

- File hash
- Filename
- File path
- Suspicious executable

### Network-based

- IP address
- Domain
- URL
- Network signature

### Host-based

- Registry/configuration changes
- New services
- Persistence artifacts
- Suspicious processes

### Identity-based

- Compromised account
- Suspicious authentication
- Unexpected privilege assignment

### Behavioral

- Beaconing
- Unusual data transfer
- Lateral movement
- Abnormal administrative activity

---

# 44. Hashes as Indicators

A file hash can be used to identify a specific file content.

Security teams may compare a suspicious file's hash against threat-intelligence information.

However, hash-based detection has limitations.

If malware changes even slightly, its hash can change.

Therefore, modern detection should not rely exclusively on static file hashes.

Behavioral indicators and endpoint telemetry are also important.

---

# 45. IP Addresses and Domains as Indicators

Threat intelligence may identify IP addresses or domains associated with malicious infrastructure.

If an endpoint communicates with such infrastructure, the connection can become an important indicator.

However, analysts should consider:

- Shared hosting
- Cloud infrastructure
- Compromised infrastructure
- IP reassignment
- False attribution

An IP address alone should therefore be investigated in context.

---

# 46. User and Entity Behavior Analytics

**UEBA** analyzes normal behavior of users and entities and identifies significant deviations.

Examples:

- User normally logs in during business hours but suddenly accesses systems overnight.
- User normally accesses a small set of servers but suddenly accesses many sensitive systems.
- A service account normally performs a predictable function but suddenly accesses large amounts of data.

UEBA can help identify compromised accounts and insider-risk indicators.

---

# 47. Insider Threat Indicators

Potential insider-threat indicators can include:

- Unusual access to sensitive data
- Large data downloads
- Access outside job responsibilities
- Repeated policy violations
- Unauthorized removable-media usage
- Attempts to bypass security controls
- Unusual after-hours activity

These indicators do not prove malicious intent.

Human-resource, business, and technical context may all be necessary for an appropriate investigation.

---

# 48. Indicators and Context

The same indicator can have different meanings in different environments.

Example:

### Port scanning

On a production server:

Potentially suspicious.

On a vulnerability-scanning platform:

Potentially expected.

### Administrative tool

On an administrator's workstation:

Potentially normal.

On a standard employee workstation without an expected administrative role:

Potentially suspicious.

### Large data transfer

During an approved backup:

Expected.

From a sensitive database to an unfamiliar external host:

Potentially malicious.

This is why context is central to security analysis.

---

# 49. Security Telemetry Sources

Useful data sources include:

### Endpoint

- EDR
- Antivirus
- Process telemetry
- File events
- Windows Event Logs
- Linux logs

### Network

- Firewall logs
- IDS/IPS
- DNS logs
- Proxy logs
- NetFlow/flow data
- VPN logs

### Identity

- Authentication logs
- MFA logs
- Directory services
- IAM platforms

### Application

- Web-server logs
- API logs
- Database logs
- Application audit logs

### Cloud

- Cloud audit logs
- IAM logs
- API activity
- Storage access logs

Correlation across these sources is often more valuable than relying on one source alone.

---

# 50. Timeline Analysis

Security investigations benefit from establishing a timeline.

For example:

**10:02 — Suspicious email delivered**

**10:07 — Attachment opened**

**10:07 — Unusual process created**

**10:08 — DNS request to unfamiliar domain**

**10:09 — Outbound connection established**

**10:11 — New persistence mechanism created**

A timeline helps analysts determine relationships between events and reconstruct possible attack sequences.

---

# 51. Indicator Severity and Confidence

Not all indicators have the same evidentiary value.

An analyst can consider:

- Reliability of the data source
- Specificity of the indicator
- Confidence in attribution
- Number of correlated indicators
- Historical behavior
- Business context

For example, communication with a known malicious infrastructure address may be more specific than a generic high-CPU alert.

Even high-confidence indicators should be investigated appropriately before conclusions are documented.

---

# 52. False Positives

A **false positive** occurs when a detection identifies activity as suspicious or malicious when it is actually benign.

Examples:

- Authorized vulnerability scanning triggers IDS alerts.
- Administrative scripts trigger endpoint detections.
- Backup traffic appears as unusual large outbound traffic.

Excessive false positives can cause **alert fatigue**.

---

# 53. False Negatives

A **false negative** occurs when malicious activity occurs but the detection system fails to identify it.

Possible causes include:

- Missing telemetry
- Poor detection rules
- Encrypted traffic
- New attack techniques
- Incomplete endpoint coverage
- Incorrect configuration

False negatives can allow attacks to remain undetected.

Security teams therefore need continuous detection improvement.

---

# 54. Alert Fatigue

**Alert fatigue** occurs when analysts receive excessive alerts, particularly low-value or repetitive alerts.

Consequences can include:

- Missed high-priority events
- Slower investigation
- Reduced analyst attention
- Increased operational workload

Mitigation strategies include:

- Detection tuning
- Alert prioritization
- Correlation
- Suppression of known benign patterns
- Automation
- Better baselines

The objective is not simply to reduce alert volume; it is to improve useful signal.

---

# 55. Detection Tuning

Detection rules should be continuously reviewed.

Tuning may involve:

- Adjusting thresholds
- Adding contextual conditions
- Excluding known legitimate activity
- Correlating multiple events
- Increasing severity for high-confidence combinations

Example:

Instead of alerting on every failed login, a rule might consider:

**Multiple failures + successful authentication + unusual source + privileged account**

This can produce a more meaningful detection.

---

# 56. Mitigation Based on Indicators

Once malicious activity is confirmed or sufficiently supported, response actions may include:

- Isolating an endpoint
- Disabling compromised accounts
- Revoking credentials or tokens
- Blocking malicious infrastructure
- Removing persistence
- Quarantining malicious files
- Increasing monitoring
- Segmenting affected systems

The response should be based on the investigation and incident-response procedures.

---

# 57. IoC Lifecycle

Indicators should be managed throughout their lifecycle.

A simplified process is:

**Collect → Validate → Enrich → Correlate → Detect → Respond → Review → Retire**

### Collect

Obtain indicators from internal investigations and trusted intelligence sources.

### Validate

Determine whether the indicator is relevant and reliable.

### Enrich

Add context such as asset, user, reputation, ownership, or historical activity.

### Correlate

Search other telemetry for related activity.

### Detect

Use the indicator in appropriate security controls.

### Respond

Take appropriate action when malicious activity is confirmed or sufficiently supported.

### Review

Determine whether the indicator remains useful.

### Retire

Remove stale indicators that no longer provide meaningful detection value.

---

# 58. Indicator Enrichment

An indicator becomes more useful when additional context is attached.

For an IP address, enrichment might include:

- Reputation
- Autonomous System information
- Geolocation
- Historical sightings
- Associated domains
- Internal connection history

For a file hash, enrichment may include:

- Malware classification
- First-seen time
- Related samples
- Endpoint sightings

Enrichment helps analysts make better investigation decisions.

---

# 59. Threat Intelligence and Indicators

Threat intelligence can provide information about known or suspected malicious infrastructure and techniques.

Examples include:

- Malicious domains
- IP addresses
- File hashes
- Malware families
- Tactics and techniques

Threat intelligence should be validated and contextualized before being used as the sole basis for blocking or attribution.

---

# 60. Detailed Security+ Scenario — Account Indicator

### Scenario

A user's account generates 25 failed login attempts followed by a successful login from an unfamiliar device. Shortly afterward, the account accesses sensitive files it has never previously accessed.

### Analysis

The failed attempts alone could have several explanations.

However, the combination of:

**Repeated failures + successful unusual login + unfamiliar device + unusual sensitive-data access**

creates a much stronger indicator of possible account compromise.

### Lesson

Correlation increases confidence.

---

# 61. Detailed Security+ Scenario — Endpoint Indicator

### Scenario

An employee opens an unexpected email attachment. Shortly afterward, an unfamiliar process starts, establishes an outbound connection, and creates a new persistence mechanism.

### Analysis

The sequence contains multiple related indicators:

**Email → process → network connection → persistence**

This is much more suspicious than any one event individually.

### Lesson

Attack-chain correlation is important for detecting malicious activity.

---

# 62. Detailed Security+ Scenario — Network Indicator

### Scenario

A workstation that normally communicates with a small set of corporate services suddenly makes repeated connections to an unfamiliar external destination every five minutes.

### Analysis

The repeated pattern may represent beaconing.

The analyst should investigate:

- Destination reputation
- Process generating the connection
- DNS history
- User activity
- Timing
- Other endpoint indicators

### Lesson

Beaconing is an indicator, not automatic proof of C2.

---

# 63. Detailed Security+ Scenario — Data Exfiltration

### Scenario

A database server normally sends very little external traffic. It suddenly transfers several gigabytes to an unfamiliar external destination shortly after an unusual administrative login.

### Analysis

The combination of:

**Unusual authentication + sensitive system access + abnormal outbound transfer**

provides a strong basis for immediate investigation.

### Lesson

Identity, endpoint, and network telemetry should be correlated.

---

# 64. Detailed Security+ Scenario — Legitimate Scanning

### Scenario

An IDS generates thousands of port-scan alerts from an internal server. The server belongs to the organization's vulnerability-management team and the activity occurs during the approved scanning window.

### Analysis

The activity resembles malicious scanning, but the context indicates that it is authorized.

### Lesson

Security indicators must be interpreted against known business activity and baselines.

---

# 65. Detailed Security+ Scenario — Impossible Travel

### Scenario

A cloud identity system reports that an account authenticated from India and then from Europe shortly afterward.

### Analysis

This is an impossible-travel-style indicator, but the analyst should first determine whether:

- The user is traveling.
- A VPN is involved.
- Corporate proxies are involved.
- Cloud authentication infrastructure affects geolocation.
- The account is compromised.

### Lesson

An anomaly requires investigation and context.

---

# 66. Detailed Security+ Scenario — Security-Control Tampering

### Scenario

An endpoint's EDR agent stops reporting shortly before unusual administrative activity occurs.

### Analysis

The loss of telemetry may be caused by a technical failure, maintenance, or malicious tampering.

The timing makes it important to investigate immediately and correlate with endpoint and administrative logs.

### Lesson

Loss of security visibility can itself be an important indicator.

---

# 67. Detailed Security+ Scenario — False Positive

### Scenario

A vulnerability scanner performs an authorized scan and generates thousands of IDS alerts.

### Analysis

The IDS alerts are genuine observations of scanning behavior, but the activity is authorized and expected.

### Lesson

A security alert does not automatically mean a malicious incident occurred.

---

# 68. Detailed Security+ Scenario — False Negative

### Scenario

A workstation is compromised, but the endpoint agent was never successfully deployed to the system.

### Analysis

The organization has a telemetry coverage gap. The absence of endpoint alerts cannot be interpreted as evidence that the system is clean.

### Lesson

**No alert ≠ no attack.**

Visibility limitations must be considered during investigation.

---

# 69. Common Exam Traps

### Trap 1: Every indicator proves compromise

Incorrect.

Indicators require validation and context.

### Trap 2: A failed login means an attacker is present

Incorrect.

Users, applications, and misconfigurations can generate failed authentication.

### Trap 3: Impossible travel proves account compromise

Incorrect.

VPNs, proxies, cloud infrastructure, travel, and geolocation errors can produce similar patterns.

### Trap 4: A known malicious IP proves the endpoint is compromised

Not automatically.

The connection should be investigated and correlated with endpoint and user activity.

### Trap 5: High CPU usage means malware

Incorrect.

Legitimate workloads can also consume significant resources.

### Trap 6: Large outbound traffic always means exfiltration

Incorrect.

Backups, cloud synchronization, and business transfers can generate large traffic volumes.

### Trap 7: A scanner triggering IDS alerts means the organization is under attack

Not necessarily.

Authorized security scanning can look similar to malicious scanning.

### Trap 8: No logs means no suspicious activity

Incorrect.

Logging failures and visibility gaps can themselves be significant issues.

### Trap 9: An IoC is always permanent

Incorrect.

Indicators can become stale or lose relevance and should be reviewed.

### Trap 10: Reducing alert count is always the goal

Incorrect.

Detection tuning should improve the quality and usefulness of alerts rather than simply minimize their number.

---

# 70. Security+ Scenario Reasoning Framework

When a question presents suspicious activity, use this process.

### Step 1: Identify the observable event

What actually happened?

- Login?
- Process creation?
- DNS query?
- Network connection?
- File modification?
- Privilege change?

### Step 2: Determine whether it is abnormal

Compare it with:

- User baseline
- System baseline
- Network baseline
- Application baseline
- Approved change activity

### Step 3: Identify the indicator category

Is it primarily:

- Identity
- Endpoint
- Network
- Application
- Cloud
- Email
- Data
- Security-control related?

### Step 4: Correlate

Look for related events before and after the indicator.

### Step 5: Check legitimate explanations

Could the behavior be caused by:

- Administration?
- Backup?
- Vulnerability scanning?
- Maintenance?
- User travel?
- VPN?
- Software update?

### Step 6: Assess confidence

Consider source reliability, specificity, and number of correlated indicators.

### Step 7: Investigate impact

Determine whether:

- Credentials were compromised
- Systems were accessed
- Data was modified
- Data was exfiltrated
- Persistence was established

### Step 8: Respond according to procedure

If malicious activity is confirmed or sufficiently supported, follow the organization's incident-response process.

### Step 9: Improve detection

After investigation, determine whether new indicators or detection rules should be added or tuned.

---

# 71. Key Takeaways

1. An indicator is observable evidence that may suggest suspicious or malicious activity.
2. An indicator is not automatically proof of compromise.
3. Events, indicators, alerts, and incidents are related but distinct concepts.
4. Identity telemetry can reveal credential compromise and abnormal account behavior.
5. Repeated authentication failures can indicate several different conditions and require context.
6. Successful authentication after repeated failures can become more significant when correlated with unusual activity.
7. Impossible travel is an anomaly that requires investigation rather than automatic conclusions.
8. Unexpected privileged accounts and privilege changes can be important indicators.
9. Endpoint indicators include unexpected processes, services, persistence, file changes, and security-control tampering.
10. Network indicators include beaconing, suspicious destinations, scanning, unusual DNS activity, and abnormal data transfers.
11. Application indicators include unusual authentication, authorization, API, administrative, and data activity.
12. Cloud environments provide additional identity, API, storage, and administrative indicators.
13. Large outbound transfers should be investigated in relation to the asset, user, destination, and baseline.
14. DNS anomalies can support detection of suspicious infrastructure and possible DNS tunneling.
15. Baselines are essential for distinguishing abnormal behavior from normal activity.
16. Correlation across multiple telemetry sources can significantly increase detection confidence.
17. IoCs provide evidence associated with possible compromise, while IoAs emphasize suspicious attack behavior.
18. Common IoCs include hashes, IP addresses, domains, URLs, persistence artifacts, and suspicious accounts.
19. IoC enrichment adds context that improves investigation quality.
20. Threat intelligence can provide useful indicators but should be validated and contextualized.
21. False positives occur when benign activity is incorrectly identified as suspicious.
22. False negatives occur when malicious activity is not detected.
23. Alert fatigue can reduce analyst effectiveness when detection systems produce excessive low-value alerts.
24. Detection tuning should improve signal quality rather than simply reduce alert volume.
25. Loss of logging or security telemetry can itself be an important indicator.
26. Authorized administrative and security activities can resemble attacks, making context essential.
27. Security investigations should establish timelines and correlate related events.
28. Indicators should be validated before making strong conclusions about compromise.
29. Confirmed malicious activity should be handled through the organization's incident-response process.
30. Indicators can feed detection engineering, threat hunting, and future security improvements.
31. The core analytical model is:

**Observe → Baseline → Identify Indicator → Correlate → Validate → Investigate → Respond → Improve Detection**
