# Domain 4 — Module 18: Incident Investigation Workflow

Incident investigation is the structured process of determining what happened, when it happened, which systems or identities were affected, how the activity occurred, what evidence supports the findings, and what actions are required to contain, eradicate, recover, and prevent recurrence.

A SOC investigation should be **evidence-driven rather than assumption-driven**.

A useful investigation model is:

**Validate → Scope → Preserve → Collect → Correlate → Analyze → Contain → Eradicate → Recover → Validate Recovery → Document → Lessons Learned**

The exact order can change when safety, active compromise, legal requirements, or evidence-preservation needs require a different priority. The investigator must understand the consequences of each action before taking it.

---

# 1. Investigation Begins With an Event or Alert

An investigation may begin with:

- A SIEM alert.
- An EDR detection.
- An IDS/IPS alert.
- A suspicious authentication event.
- A malware detection.
- A phishing report.
- A data-loss alert.
- A firewall event.
- A cloud-security alert.
- A user report.
- Threat-intelligence information.
- A vulnerability that appears to have been exploited.

An **event** is an observable occurrence. An **alert** is a notification generated because activity met a detection condition. An **incident** is a security event or series of events that requires response according to organizational criteria.

Not every alert is an incident.

For example:

```text
Failed Login
     ↓
SIEM Alert
     ↓
Investigation
     ↓
User confirms forgotten password
     ↓
False Positive / Benign Event
```

Another case may be:

```text
Multiple Failed Logins
        ↓
Successful Login
        ↓
Unusual Source
        ↓
MFA Change
        ↓
Suspicious Cloud Activity
        ↓
Compromised Account Investigation
```

The analyst must distinguish the two using evidence and context.

---

# 2. Step 1 — Validate the Alert

The first question is:

> **Is the observed activity actually suspicious?**

Validation involves examining:

- Source IP.
- Destination IP.
- Username.
- Hostname.
- Device identity.
- Process name.
- Command line.
- Timestamp.
- Network connection.
- Authentication result.
- File hash.
- URL or domain.
- Application context.
- User role.
- Asset criticality.

The analyst should determine whether the activity is:

- Expected and legitimate.
- Authorized administrative activity.
- A policy violation.
- Suspicious but unconfirmed.
- A confirmed security incident.

Do not declare compromise simply because a single indicator looks unusual.

---

# 3. Alert Enrichment

Alert enrichment means adding context to an alert so the analyst can make a better decision.

For an IP address, enrichment might include:

- Geolocation.
- ASN.
- Reputation.
- Historical activity.
- Threat-intelligence associations.

For a host, enrichment may include:

- Asset owner.
- Business function.
- Operating system.
- Criticality.
- Installed security controls.
- Recent vulnerabilities.

For an account, enrichment may include:

- Department.
- Role.
- Privilege level.
- Normal login locations.
- Recent password changes.
- MFA activity.

Enrichment supports investigation but does not automatically prove malicious activity.

---

# 4. Step 2 — Determine Scope

Once suspicious activity has been validated, determine the scope.

Scope answers:

- Which users are affected?
- Which endpoints are affected?
- Which servers are affected?
- Which applications are affected?
- Which network segments are involved?
- Which cloud resources are involved?
- What data may be affected?
- What time period is relevant?

A useful scope model is:

```text
Identity
   ↓
Endpoint
   ↓
Network
   ↓
Application
   ↓
Data
   ↓
Cloud / External Systems
```

Scope should expand when evidence establishes relationships between additional entities.

---

# 5. Build an Investigation Timeline

A timeline reconstructs events in chronological order.

Example:

```text
09:12 — Phishing email received
09:15 — User opens attachment
09:16 — Office process launches script
09:17 — PowerShell starts
09:18 — External connection established
09:21 — Credential access detected
09:26 — New authentication from unusual host
09:31 — File archive created
09:34 — Large outbound transfer
```

This timeline is more useful than examining each alert independently because it shows relationships between events.

---

# 6. Time Synchronization

Different systems may record timestamps differently.

For example:

- Endpoint uses local time.
- Cloud logs use UTC.
- Firewall uses another time zone.
- Application server has an incorrect clock.

Without reliable time synchronization, the investigator may construct an incorrect sequence of events.

Organizations commonly use NTP to synchronize system clocks.

When investigating, record:

- Original timestamp.
- Time zone.
- Converted timestamp if necessary.
- Source system.
- Any known clock discrepancy.

---

# 7. Step 3 — Preserve Evidence

Evidence should be preserved before investigative or remediation actions alter it when practical.

Potential evidence includes:

- Disk images.
- Memory captures.
- Logs.
- PCAP files.
- EDR telemetry.
- Browser artifacts.
- Authentication records.
- Cloud audit logs.
- Email headers.
- Malware samples.
- Files.
- Registry artifacts.

Evidence preservation is particularly important when legal, regulatory, disciplinary, or law-enforcement requirements may apply.

---

# 8. Evidence Preservation vs Immediate Containment

Security teams sometimes face a conflict:

```text
Preserve Evidence
       ↕
Stop the Attack
```

For example, a compromised workstation may still be communicating with an attacker.

If the system is immediately powered off, volatile evidence such as memory-resident malware, active network connections, and running processes may disappear.

However, leaving the system connected may allow the attacker to continue operating.

The correct decision depends on:

- Active threat level.
- Safety and business impact.
- Evidence requirements.
- Available forensic capability.
- Organizational procedures.

There is no universal rule that every system must always be powered off or always remain online.

---

# 9. Volatile Evidence

Volatile evidence can disappear when a system is shut down or loses power.

Examples include:

- RAM contents.
- Running processes.
- Active network connections.
- Logged-in users.
- Temporary memory artifacts.
- Some cryptographic material.

When appropriate and authorized, volatile evidence may be collected before shutdown or isolation.

---

# 10. Non-Volatile Evidence

Non-volatile evidence persists after shutdown more readily.

Examples include:

- Disk contents.
- File-system metadata.
- Event logs.
- Registry data.
- Stored configuration.
- Some application databases.

Non-volatile evidence can still be modified or deleted, so preservation remains important.

---

# 11. Step 4 — Collect Relevant Data

The investigator should collect the data needed to answer the investigation questions.

Potential sources include:

### Endpoint

- EDR telemetry.
- Process trees.
- Command lines.
- File creation.
- Registry changes.
- Persistence mechanisms.
- Security logs.

### Identity

- Authentication logs.
- MFA events.
- Password changes.
- Privilege changes.
- Account creation.
- Group membership changes.

### Network

- Firewall logs.
- IDS/IPS alerts.
- DNS logs.
- Proxy logs.
- VPN logs.
- NetFlow/IPFIX.
- PCAP.

### Application

- Web-server logs.
- API logs.
- Database logs.
- Application audit trails.

### Cloud

- Control-plane audit logs.
- IAM events.
- Storage access.
- Network-flow data.
- Cloud security alerts.

The investigator should avoid collecting irrelevant data simply because it is available. Collection should support the investigation objectives while respecting privacy and retention requirements.

---

# 12. Step 5 — Correlate Data

Correlation means connecting observations from multiple sources.

For example:

```text
EDR:
PowerShell executed
      +
DNS:
Suspicious domain queried
      +
Firewall:
Outbound connection established
      +
Identity:
Privileged account used
      ↓
Strong evidence of suspicious activity
```

A single event may be ambiguous. Multiple independent sources can provide stronger context.

---

# 13. Investigation Pivots

A pivot is a new investigation path derived from an existing finding.

Suppose an analyst finds:

```text
Suspicious IP → Host A
```

The analyst can pivot from the IP to:

- Other hosts communicating with it.
- DNS queries involving the domain.
- Other users associated with the host.
- Other processes making the connection.
- Historical traffic.

Likewise, a suspicious hash can be pivoted to:

- Other endpoints containing the hash.
- EDR detections.
- File paths.
- Process executions.
- Related network activity.

Good investigations continuously use evidence to determine the next useful pivot.

---

# 14. Step 6 — Analyze the Attack Path

The investigator should attempt to reconstruct how the activity occurred.

Important questions include:

1. How did the attacker or malicious process gain initial access?
2. Which account or vulnerability was involved?
3. What process executed first?
4. Was persistence established?
5. Was privilege escalated?
6. Did lateral movement occur?
7. Was data accessed?
8. Was data exfiltrated?
9. Was command and control established?
10. What systems remain potentially affected?

The investigation should separate **observed facts** from **inferences**.

For example:

**Observed:** PowerShell executed from an Office process.

**Inference:** The user may have opened a malicious document.

The inference should be tested against additional evidence before being treated as a confirmed conclusion.

---

# 15. Initial Access Analysis

Initial access identifies how the incident may have started.

Possible mechanisms include:

- Phishing.
- Exploited vulnerability.
- Stolen credentials.
- Exposed remote service.
- Malicious download.
- Supply-chain compromise.
- Removable media.
- Valid-account abuse.

Useful evidence includes email logs, authentication records, vulnerability data, web logs, endpoint telemetry, and network activity.

---

# 16. Persistence Analysis

Persistence means maintaining access after the initial compromise.

Investigators may look for:

- Scheduled tasks.
- Services.
- Startup mechanisms.
- Registry persistence.
- Modified applications.
- Cloud access keys.
- New accounts.
- SSH keys.
- Web shells.
- Malicious extensions.

Persistence findings can explain why an attacker returned after an apparent cleanup.

---

# 17. Privilege Escalation Analysis

The investigator should determine whether the attacker obtained greater privileges.

Evidence may include:

- New administrative-group membership.
- Privileged authentication.
- Exploited vulnerabilities.
- Token or credential abuse.
- Service-account misuse.
- Administrative-tool execution.

Privilege escalation can significantly increase incident scope.

---

# 18. Lateral Movement Analysis

Lateral movement occurs when an attacker moves from one compromised system or identity to another.

Investigators can examine:

- Remote logons.
- RDP.
- SMB.
- WinRM.
- SSH.
- Remote administration tools.
- Authentication patterns.
- Service creation.
- Network connections.

Example:

```text
Workstation A
     ↓
Compromised User Credential
     ↓
Server B
     ↓
Privileged Credential
     ↓
Server C
```

The investigation must determine whether the later systems were actually compromised or merely contacted.

---

# 19. Command and Control Analysis

Command and control activity represents communication between compromised systems and attacker-controlled infrastructure.

Potential indicators include:

- Suspicious DNS queries.
- Rare domains.
- Beacon-like periodic connections.
- Unusual destination IPs.
- Unexpected encrypted traffic.
- Known malicious infrastructure.
- Unusual outbound protocols.

Useful sources include DNS, proxy, firewall, NetFlow, PCAP, and EDR telemetry.

A suspicious destination alone is not automatically proof of compromise; context and corroboration matter.

---

# 20. Data Access and Exfiltration Analysis

Investigators should determine whether sensitive data was accessed or transferred.

Potential evidence includes:

- Large outbound transfers.
- Unusual cloud-storage access.
- Database queries.
- Archive creation.
- DLP alerts.
- Proxy logs.
- Network-flow records.
- Cloud audit events.

For example:

```text
Database Access
      ↓
Archive Created
      ↓
Compression
      ↓
External Connection
      ↓
Large Outbound Transfer
```

The complete sequence is more meaningful than any individual event.

---

# 21. Step 7 — Containment

Containment limits the attacker's ability to continue operating or spreading.

Possible actions include:

- Isolating an endpoint.
- Disabling an account.
- Revoking sessions.
- Blocking malicious infrastructure.
- Removing a system from the network.
- Restricting firewall access.
- Disabling compromised credentials.
- Quarantining email.

Containment should be proportional to the incident and coordinated with relevant teams.

---

# 22. Short-Term vs Long-Term Containment

### Short-Term Containment

Designed to quickly limit immediate damage.

Examples:

- EDR isolation.
- Account disablement.
- Blocking an IP.
- Quarantining a malicious email.

### Long-Term Containment

Designed to maintain controlled operation while deeper remediation occurs.

Examples:

- Moving systems into restricted network segments.
- Replacing compromised credentials.
- Applying temporary access restrictions.
- Increasing monitoring.

Containment should not be confused with eradication.

---

# 23. Step 8 — Eradication

Eradication removes the cause or malicious presence associated with the incident.

Examples include:

- Removing malware.
- Removing persistence.
- Patching exploited vulnerabilities.
- Resetting compromised credentials.
- Removing unauthorized accounts.
- Rebuilding compromised systems.
- Removing malicious cloud resources.

Eradication should address the root cause rather than only the visible symptom.

---

# 24. Reimage vs Clean

If a system has been deeply compromised, especially where integrity cannot be trusted, rebuilding or reimaging may be preferable to attempting to remove every malicious artifact manually.

Factors include:

- Type of compromise.
- Level of privilege obtained.
- Evidence of persistence.
- System criticality.
- Availability of trusted images.
- Forensic requirements.

A reimage does not automatically mean the investigation is complete. Evidence should be preserved before destructive remediation when practical.

---

# 25. Step 9 — Recovery

Recovery returns affected systems to trusted operational states.

Recovery may include:

- Restoring systems.
- Rebuilding endpoints.
- Restoring data.
- Rotating credentials and keys.
- Re-enabling services.
- Removing temporary restrictions.
- Increasing monitoring.

Before returning systems to normal operation, verify that the underlying cause has been addressed.

---

# 26. Validate Recovery

A recovered system should not simply be returned to production because it appears functional.

Validate:

- Security configuration.
- Patches.
- Authentication.
- EDR/AV status.
- Logging.
- Network connections.
- Persistence mechanisms.
- Application functionality.
- Data integrity.

Recovery should restore both **business functionality and security trust**.

---

# 27. Step 10 — Documentation

Every significant investigation should be documented.

Record:

- Incident identifier.
- Date and time.
- Detection source.
- Analyst actions.
- Evidence collected.
- Affected assets.
- Scope decisions.
- Containment actions.
- Eradication actions.
- Recovery actions.
- Communications.
- Approvals.
- Findings.
- Remaining uncertainty.

Documentation should be factual and traceable.

---

# 28. Chain of Custody

When evidence may be used for legal, disciplinary, or regulatory purposes, maintain a chain of custody.

The record should establish:

- What evidence was collected.
- Who collected it.
- When it was collected.
- How it was handled.
- Where it was stored.
- Who accessed or transferred it.
- What happened to it afterward.

The purpose is to demonstrate that evidence remained controlled and its integrity was maintained.

---

# 29. Hashing Evidence

Cryptographic hashes can help verify evidence integrity.

For example:

```text
Original Evidence
      ↓
SHA-256
      ↓
Hash A

Copied Evidence
      ↓
SHA-256
      ↓
Hash B

Hash A = Hash B
      ↓
Evidence contents are consistent with the hash comparison
```

A matching hash supports integrity verification, but hashing alone does not establish the entire legal chain of custody.

---

# 30. Investigation Communication

Incident investigations often require communication among:

- SOC analysts.
- Incident responders.
- System administrators.
- Network teams.
- Identity teams.
- Application owners.
- Management.
- Legal.
- Privacy teams.
- Human resources.
- External responders or law enforcement where appropriate.

Communication should follow the incident-response plan and need-to-know principles.

If normal communication systems may be compromised, an out-of-band communication method may be necessary.

---

# 31. Investigation vs Threat Hunting

These activities overlap but have different purposes.

### Incident Investigation

Starts from a known alert, event, report, or suspected incident and seeks to determine what happened.

### Threat Hunting

Proactively searches for malicious activity that may not have generated a known alert.

Example:

```text
SIEM Alert
   ↓
Incident Investigation
```

versus:

```text
Hypothesis
   ↓
Search Telemetry
   ↓
Potential Undetected Activity
   ↓
Threat Hunt
```

---

# 32. Investigation vs Vulnerability Management

Vulnerability management asks:

> What weaknesses exist that could be exploited?

Incident investigation asks:

> Did suspicious activity occur, what happened, and what was affected?

A vulnerable system is not automatically compromised.

However, vulnerability data can become important evidence when investigating a suspected exploit.

---

# 33. Investigation vs Digital Forensics

Incident investigation is the broader operational process of determining what happened and responding to it.

Digital forensics focuses on systematic acquisition, preservation, examination, and interpretation of digital evidence.

Forensics may therefore be one component of a larger incident investigation.

---

# 34. Investigation vs Incident Response

Incident response includes the complete coordinated response process, including preparation, detection, analysis, containment, eradication, recovery, and lessons learned.

Investigation is primarily concerned with understanding the incident through evidence and analysis.

The two activities occur together during many real incidents.

---

# 35. Scenario — Compromised Endpoint

A user reports that their workstation is behaving unusually. EDR reports PowerShell execution followed by a connection to a suspicious external domain.

A strong investigation proceeds as follows:

1. Validate the alert.
2. Examine the process tree and command line.
3. Identify the user and endpoint.
4. Check DNS and network telemetry.
5. Search for the same domain or hash across the environment.
6. Determine whether persistence exists.
7. Preserve relevant evidence.
8. Isolate the endpoint if appropriate.
9. Determine whether credentials were exposed.
10. Remove malware or rebuild the system as appropriate.
11. Reset affected credentials.
12. Restore and validate the endpoint.
13. Increase monitoring.
14. Document findings and improve detections.

---

# 36. Scenario — Compromised Account

An administrator account authenticates from an unusual location and then performs privileged actions.

The analyst should investigate:

- Whether the login was expected.
- MFA events.
- Source IP and device.
- Recent password changes.
- Session information.
- Privileged actions.
- Other systems accessed.
- Creation or modification of accounts.
- Cloud control-plane activity.

Possible containment could include disabling or restricting the account, revoking sessions, resetting credentials, and investigating systems accessed by the identity.

---

# 37. Scenario — Suspected Data Exfiltration

A workstation creates a large archive and shortly afterward transfers a large volume of data externally.

The investigator should correlate:

```text
File Access
   ↓
Archive Creation
   ↓
Process Execution
   ↓
Network Connection
   ↓
Large Transfer
```

Then determine:

- What data was accessed?
- Who accessed it?
- Where was it sent?
- Whether the destination is authorized.
- Whether other hosts performed similar activity.
- Whether credentials were compromised.

Do not label the event confirmed exfiltration solely from transfer size without examining context.

---

# 38. Scenario — Ransomware

An endpoint begins modifying large numbers of files and EDR detects suspicious process behavior.

The priority may be rapid containment because continued execution can increase damage.

Possible actions include:

1. Isolate affected systems.
2. Protect unaffected systems.
3. Identify the ransomware process and scope.
4. Preserve evidence where practical.
5. Identify compromised accounts and credentials.
6. Determine initial access.
7. Eradicate malicious presence.
8. Recover from trusted backups.
9. Validate systems before reconnecting them.
10. Monitor for recurrence.

Recovery should not begin from an untrusted state merely because a backup exists.

---

# 39. Common Investigation Failures

## Failure 1 — Jumping to conclusions

A single IOC is treated as proof of compromise.

**Better:** corroborate indicators with additional telemetry.

## Failure 2 — Ignoring scope

The first compromised host is treated as the only affected system.

**Better:** search for related identities, hashes, domains, IPs, processes, and authentication activity.

## Failure 3 — Destroying evidence

Systems are immediately wiped without considering forensic requirements.

**Better:** understand evidence-preservation requirements before destructive actions when circumstances permit.

## Failure 4 — Ignoring time zones

Events appear out of order because timestamps are interpreted incorrectly.

**Better:** normalize timestamps and record the source time zone.

## Failure 5 — Containing without understanding dependencies

A critical server is disconnected without considering business impact.

**Better:** balance containment with availability, safety, and incident severity.

## Failure 6 — Eradicating only the malware file

The visible malicious file is removed while persistence or stolen credentials remain.

**Better:** investigate root cause, persistence, credentials, and lateral movement.

## Failure 7 — Returning systems too quickly

A system is restored because it appears functional.

**Better:** validate security controls, configuration, credentials, logging, and persistence before returning it to normal operation.

## Failure 8 — Poor documentation

Actions and decisions are not recorded.

**Better:** document evidence, decisions, actions, approvals, communications, and conclusions throughout the investigation.

---

# 40. Security+ Exam Distinctions

### Event vs Alert vs Incident

- **Event:** observable occurrence.
- **Alert:** notification generated because a detection condition was met.
- **Incident:** event or group of events requiring security response according to organizational criteria.

### Indicator vs Finding

- **Indicator:** clue suggesting possible malicious activity.
- **Finding:** evidence-supported result of investigation.

### Containment vs Eradication

- **Containment:** limits damage or attacker activity.
- **Eradication:** removes the malicious presence or underlying cause.

### Eradication vs Recovery

- **Eradication:** removes the threat.
- **Recovery:** restores trusted operation.

### Short-Term vs Long-Term Containment

- **Short-term:** immediate limitation of damage.
- **Long-term:** sustained controlled operation while deeper remediation occurs.

### Threat Hunting vs Incident Investigation

- **Threat hunting:** proactive search for previously undetected threats.
- **Incident investigation:** evidence-driven examination of a known alert or suspected incident.

### Vulnerability vs Compromise

- **Vulnerability:** weakness that could be exploited.
- **Compromise:** evidence that unauthorized activity or access occurred.

### Backup vs Forensic Image

- **Backup:** intended primarily for restoration of data or systems.
- **Forensic image:** acquired to preserve and examine evidence.

---

# 41. Security+ Decision Framework

When given an incident-investigation scenario, work through these questions:

### 1. What triggered the investigation?

Identify the alert, report, anomaly, or suspected compromise.

### 2. Is it actually suspicious?

Validate the evidence before declaring an incident.

### 3. What is the scope?

Identify affected identities, endpoints, applications, networks, cloud resources, and data.

### 4. What evidence is available?

Identify endpoint, identity, network, application, cloud, email, and forensic sources.

### 5. What is the timeline?

Normalize timestamps and correlate events.

### 6. What is the attack path?

Determine initial access, execution, persistence, privilege escalation, lateral movement, C2, data access, and exfiltration where supported by evidence.

### 7. What must be preserved?

Consider volatile evidence, forensic requirements, legal requirements, and destructive remediation.

### 8. What containment is appropriate?

Select actions that limit damage while considering business continuity and evidence.

### 9. Has the root cause been removed?

Eradication must address malware, persistence, vulnerabilities, compromised credentials, and other causes as applicable.

### 10. Can the system be trusted again?

Validate security configuration, patches, credentials, logging, endpoint protection, and application functionality.

### 11. What must be documented?

Record evidence, actions, decisions, communications, approvals, findings, and remaining uncertainty.

### 12. What should improve afterward?

Update detections, controls, procedures, training, segmentation, or other defenses based on lessons learned.

---

# 42. Complete Investigation Workflow

```text
Alert / Report / Suspicion
          ↓
Validate
          ↓
Enrich
          ↓
Determine Scope
          ↓
Preserve Evidence
          ↓
Collect Relevant Data
          ↓
Build Timeline
          ↓
Correlate Events
          ↓
Analyze Attack Path
          ↓
Contain
          ↓
Eradicate
          ↓
Recover
          ↓
Validate Recovery
          ↓
Document
          ↓
Lessons Learned
          ↓
Detection / Control Improvements
```

This workflow should not be treated as a rigid checklist where every action always occurs in exactly the same order. Active threats, safety concerns, evidence volatility, legal requirements, and business-critical dependencies can change priorities.

---

# 43. Core Investigation Questions

A strong analyst should continually ask:

**What happened?**

Identify the observable activity.

**When did it happen?**

Construct a reliable timeline.

**How did it happen?**

Determine the probable attack path.

**Who or what was involved?**

Identify accounts, hosts, applications, processes, and infrastructure.

**What was affected?**

Determine scope and business impact.

**What evidence supports the conclusion?**

Separate facts from assumptions.

**Is the attacker still present?**

Look for active sessions, persistence, C2, and additional compromised systems.

**Can the environment be trusted again?**

Validate eradication and recovery.

**How can recurrence be prevented or detected earlier?**

Convert lessons learned into security improvements.

---

# 44. Key Takeaways

- Incident investigation is evidence-driven.
- Not every alert is an incident.
- Validate before making conclusions.
- Enrichment provides context but does not automatically prove compromise.
- Scope must include identities, endpoints, applications, networks, cloud resources, and data where relevant.
- Timelines are essential for understanding attack sequences.
- Time synchronization and time-zone handling are important for accurate investigations.
- Preserve relevant evidence before destructive remediation when practical.
- Volatile evidence can disappear when a system is shut down.
- Correlation across multiple telemetry sources produces stronger investigative context.
- Pivots allow investigators to expand from one indicator to related activity.
- Investigators should distinguish observed facts from assumptions and conclusions.
- Initial access, persistence, privilege escalation, lateral movement, C2, data access, and exfiltration are important investigation areas.
- Containment limits damage; eradication removes the malicious presence or root cause; recovery restores trusted operation.
- Reimaging can be appropriate when system integrity cannot be trusted, but evidence should be preserved when required.
- Recovery requires validation, not merely restoring functionality.
- Chain of custody helps demonstrate controlled evidence handling.
- Hashing supports integrity verification but does not replace chain-of-custody procedures.
- Incident investigation, threat hunting, vulnerability management, digital forensics, and incident response are related but distinct activities.
- Security actions must balance security, evidence preservation, safety, availability, privacy, and business requirements.
- Every significant investigation should produce documentation and lessons learned.
- Investigation findings should improve future detection, prevention, response, and recovery capabilities.

## Core Security+ Mental Model

**Validate → Scope → Preserve → Collect → Correlate → Analyze → Contain → Eradicate → Recover → Validate Recovery → Document → Improve**

The central principle is: **investigate from evidence, continuously test assumptions against independent telemetry, understand the full scope and attack path, preserve important evidence, contain appropriately, remove the underlying cause, restore a trusted state, and convert lessons learned into measurable security improvements.**