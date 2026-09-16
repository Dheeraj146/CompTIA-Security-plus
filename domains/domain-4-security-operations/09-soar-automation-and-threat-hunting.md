# SOAR, Automation, and Threat Hunting

Security operations generate large volumes of alerts, telemetry, enrichment requests, and repetitive response tasks. Analysts need mechanisms that reduce manual effort without sacrificing control, evidence quality, or sound judgment. This is where **Security Orchestration, Automation, and Response (SOAR)**, security automation, threat hunting, and detection engineering become important.

These concepts are related, but they solve different problems:

- **SIEM** primarily centralizes, searches, correlates, and analyzes security telemetry and generates detections/alerts.
- **SOAR** primarily orchestrates security tools and automates repeatable workflows.
- **Automation** performs defined actions with minimal manual intervention.
- **Threat hunting** proactively searches for suspicious activity that existing detections may have missed.
- **Detection engineering** develops and maintains logic that identifies meaningful malicious or risky behavior.

A useful operational model is:

**Telemetry → Detection → Alert → Enrichment → Decision → Response → Documentation → Improvement**

Threat hunting runs alongside this process rather than waiting for an alert:

**Hypothesis → Data → Search → Analysis → Validation → Detection/Response Improvement**

---

# 1. What Is SOAR?

**Security Orchestration, Automation, and Response (SOAR)** is a technology approach that connects security tools and coordinates repeatable workflows.

A SOAR platform can integrate with systems such as:

- SIEM
- EDR
- Firewalls
- Email security platforms
- Identity providers
- Threat-intelligence services
- Ticketing systems
- Vulnerability scanners
- Cloud platforms
- Case-management systems

The objective is not simply to automate everything. The objective is to make security operations **faster, more consistent, and less dependent on repetitive manual actions**.

---

# 2. Why Organizations Use SOAR

SOC analysts may repeatedly perform tasks such as:

1. Read an alert.
2. Copy an IP address.
3. Search threat intelligence.
4. Check the affected endpoint.
5. Look up the user.
6. Check whether the IP is known to be malicious.
7. Create a ticket.
8. Notify another team.

Doing this manually hundreds of times creates delays and introduces inconsistent results.

SOAR can automate appropriate parts of the workflow.

For example:

```text
SIEM alert
    ↓
SOAR receives alert
    ↓
Extract IP address
    ↓
Threat-intelligence lookup
    ↓
Check asset criticality
    ↓
Check endpoint status
    ↓
Create investigation case
    ↓
Notify analyst
```

The analyst can then focus on interpretation and decision-making rather than repetitive data collection.

---

# 3. Security Orchestration vs Automation vs Response

The three terms in SOAR describe related but distinct capabilities.

### Security orchestration

Coordinates multiple tools and processes so that they work together.

Example:

```text
SIEM → SOAR → Threat Intelligence → EDR → Ticketing
```

### Security automation

Performs defined actions automatically.

Example:

```text
Extract IP → reputation lookup → enrich alert
```

### Security response

Executes actions intended to contain, mitigate, investigate, or otherwise respond to security events.

Example:

```text
Compromised endpoint → isolate endpoint
```

---

# 4. SOAR Playbooks

A **playbook** is a predefined workflow describing how a particular type of alert or operational situation should be handled.

A simplified phishing playbook might be:

```text
Phishing alert
      ↓
Extract sender/domain/URL
      ↓
Check reputation
      ↓
Search for same message
      ↓
Identify recipients
      ↓
Check endpoint activity
      ↓
Create case
      ↓
Escalate or contain
```

Playbooks should be designed around documented procedures and approved actions.

A playbook is not merely a script. It represents an operational workflow that can include:

- Inputs
- Conditions
- Data enrichment
- Tool integrations
- Decisions
- Actions
- Exceptions
- Human approvals
- Logging
- Error handling

---

# 5. Automated vs Manual Decisions

Not every response action should be automatic.

Low-risk repetitive actions may be suitable for automation.

Examples:

- Enriching an IP address
- Looking up a file hash
- Creating a ticket
- Adding context to an alert
- Checking asset ownership

High-impact actions may require human approval.

Examples:

- Disabling an executive account
- Shutting down a production server
- Blocking a major business partner
- Deleting cloud resources
- Wiping an endpoint

The decision should consider:

**Confidence + impact + reversibility + business criticality + authorization**

---

# 6. Human-in-the-Loop Automation

Human-in-the-loop automation means the system performs analysis or preparation but requires a human decision before a consequential action.

Example:

```text
EDR detects ransomware
        ↓
SOAR validates detection
        ↓
SOAR identifies critical server
        ↓
SOAR prepares isolation action
        ↓
Analyst approves
        ↓
Endpoint isolated
```

This reduces the risk of an incorrect automated action causing significant business disruption.

---

# 7. Guardrails for Security Automation

Automation should have safeguards.

Important guardrails include:

- Authentication
- Authorization
- Least privilege
- Approval requirements
- Rate limits
- Scope restrictions
- Timeouts
- Error handling
- Rollback capability
- Logging
- Audit trails
- Secrets protection
- Exception handling

For example, an automated firewall-block workflow should not be allowed to modify unrestricted production firewall rules using an unrestricted service account.

The automation itself becomes a security-sensitive system and must be protected accordingly.

---

# 8. Automation Failure Handling

A playbook can fail because:

- API authentication failed
- Tool is unavailable
- Network connection failed
- Required field is missing
- API rate limit was reached
- Permission was insufficient
- Response format changed
- Integration timed out

A mature playbook should not silently fail.

It should:

```text
Detect failure
    ↓
Record error
    ↓
Preserve alert context
    ↓
Notify appropriate analyst
    ↓
Continue safely or stop
```

---

# 9. SOAR and APIs

Modern SOAR platforms commonly integrate with security technologies through APIs.

Example:

```text
SOAR
  ↓ API
Threat intelligence
  ↓
Reputation result
  ↓
SOAR
  ↓ API
EDR
  ↓
Endpoint status
```

API integrations allow tools to exchange data and execute actions programmatically.

This also creates security requirements:

- API authentication
- Token protection
- Least-privilege permissions
- Credential rotation
- Logging
- Rate limiting
- Secure error handling

---

# 10. SOAR and SIEM Relationship

SIEM and SOAR commonly work together.

A typical workflow is:

```text
Security telemetry
       ↓
SIEM
       ↓
Correlation/detection
       ↓
Alert
       ↓
SOAR
       ↓
Enrichment
       ↓
Automated workflow
       ↓
Response / ticket / notification
```

The SIEM may determine that an event pattern is suspicious. SOAR can then coordinate what happens next.

### Security+ distinction

**SIEM answers:** “What is happening across my environment, and what should I investigate?”

**SOAR answers:** “How can I consistently coordinate the workflow that follows this detection?”

The exact capabilities vary by product, but this distinction is useful for exam questions.

---

# 11. SOAR and EDR Relationship

EDR focuses on endpoint detection and response.

SOAR can use EDR as one component of a larger workflow.

Example:

```text
SIEM alert
    ↓
SOAR
    ↓
Query EDR
    ↓
Confirm endpoint status
    ↓
Request isolation
    ↓
Create case
```

SOAR does not replace EDR. It can orchestrate actions across EDR and other tools.

---

# 12. Security Automation Examples

Common automation opportunities include:

### Alert enrichment

Automatically retrieve:

- IP reputation
- Domain information
- Hash reputation
- Asset owner
- User details
- Vulnerability information

### Ticket creation

Automatically create an incident ticket when a high-confidence detection occurs.

### Notification

Notify appropriate responders through approved communication channels.

### Endpoint response

Trigger endpoint isolation when a predefined high-confidence condition is met.

### Credential response

Suspend or disable a compromised account when policy and confidence justify it.

### Indicator blocking

Add a confirmed malicious indicator to an approved security-control blocklist.

---

# 13. Automation Does Not Mean “No Human Needed”

Automation is most effective when applied to predictable, repeatable tasks.

For example:

```text
Hash lookup → automate
IP enrichment → automate
Ticket creation → automate
Evidence collection → automate where safe

Complex attribution → analyst
Business-impact decision → authorized human
Ambiguous compromise → analyst
Major production shutdown → authorized human
```

Automation should increase analyst capability rather than eliminate necessary judgment.

---

# 14. What Is Threat Hunting?

**Threat hunting** is a proactive security activity in which analysts deliberately search for evidence of malicious or suspicious activity that may not have triggered existing detections.

Traditional detection often looks like:

```text
Attack → Detection → Alert → Investigation
```

Threat hunting looks more like:

```text
Hypothesis → Search environment → Find evidence → Investigate → Improve detection
```

The key difference is that the hunter does not wait for a detection rule to tell them that something suspicious happened.

---

# 15. Why Threat Hunting Is Necessary

No detection system is perfect.

Attackers may:

- Use new techniques
- Modify malware
- Abuse legitimate tools
- Operate below detection thresholds
- Avoid known indicators
- Use compromised credentials
- Blend into normal activity

Threat hunting attempts to discover suspicious behavior that existing automated detections may have missed.

---

# 16. Threat Hunting Is Hypothesis-Driven

Effective hunting normally begins with a question or hypothesis.

Example:

> “Could attackers be using PowerShell to establish persistence in our environment without triggering our existing malware detections?”

The hunter then determines:

- What evidence would support the hypothesis?
- Which telemetry contains that evidence?
- What time period should be searched?
- What baseline should be expected?
- What systems are in scope?

The investigation might search endpoint telemetry for:

```text
PowerShell execution
+ encoded commands
+ unusual parent processes
+ network connections
+ persistence changes
```

---

# 17. Threat Hunting Data Sources

Threat hunters may use:

- EDR telemetry
- SIEM data
- Authentication logs
- DNS logs
- Firewall logs
- Proxy logs
- Network flow
- Packet captures
- Cloud logs
- Email telemetry
- Application logs
- Identity-provider logs
- Threat intelligence

The best source depends on the hypothesis.

For example, if the hypothesis concerns DNS-based command and control, DNS telemetry is particularly relevant.

---

# 18. Threat Hunting Using Threat Intelligence

Threat intelligence can provide starting points for a hunt.

Examples:

- Malicious IP addresses
- Domains
- URLs
- File hashes
- Malware families
- Known attacker techniques
- Behavioral patterns

Example:

```text
Known malicious domain
        ↓
Search DNS logs
        ↓
Identify querying hosts
        ↓
Search endpoint telemetry
        ↓
Investigate processes
        ↓
Determine scope
```

A threat-intelligence indicator is not necessarily sufficient evidence of compromise. Analysts must account for context, stale indicators, shared infrastructure, and false positives.

---

# 19. Threat Hunting With MITRE ATT&CK

Threat hunters can use the **MITRE ATT&CK** knowledge base as a framework for thinking about adversary behavior.

Instead of hunting only for a known malware hash, the hunter can search for techniques.

For example:

```text
Technique hypothesis
      ↓
Identify observable behavior
      ↓
Identify telemetry source
      ↓
Search environment
      ↓
Validate findings
      ↓
Create/improve detection
```

This is valuable because attackers can change malware while retaining similar behaviors.

---

# 20. IOC-Based vs Behavior-Based Hunting

### IOC-based hunting

Searches for known indicators such as:

- IP
- Domain
- Hash
- URL
- Email address

Advantage:

Fast and specific when indicators are reliable.

Limitation:

Attackers can change indicators.

### Behavior-based hunting

Searches for suspicious behaviors such as:

- Unusual process chains
- Credential dumping behavior
- Unexpected remote administration
- Rare persistence mechanisms
- Abnormal authentication

Advantage:

Can identify activity even when exact indicators change.

Limitation:

Requires more contextual analysis and may produce more candidates for investigation.

---

# 21. Threat Hunting Workflow

A structured hunting process can be:

**1. Define hypothesis**

State what suspicious behavior you are looking for.

**2. Define scope**

Determine systems, users, time period, and data sources.

**3. Identify observables**

Determine what evidence the behavior would produce.

**4. Query telemetry**

Search SIEM, EDR, DNS, network, identity, or cloud data.

**5. Investigate anomalies**

Determine whether unusual activity is legitimate or suspicious.

**6. Validate findings**

Confirm evidence and scope.

**7. Respond when required**

Escalate or contain according to procedures.

**8. Improve detection**

Turn repeatable findings into better detections.

**9. Document**

Record hypothesis, queries, evidence, findings, and lessons learned.

---

# 22. Example Threat Hunt — PowerShell Abuse

### Hypothesis

An attacker may be using PowerShell to execute commands on endpoints.

### Search

Look for:

```text
PowerShell process creation
      ↓
Unusual parent process
      ↓
Encoded command
      ↓
Network connection
      ↓
File creation
```

### Analysis

The hunter finds:

```text
WINWORD.EXE
   ↓
powershell.exe
   ↓
External network connection
```

This is suspicious because the process chain is unusual and should be investigated.

### Follow-up

The analyst checks:

- User
- Document source
- Command line
- Destination
- File hash
- Persistence
- Other affected endpoints

If malicious behavior is confirmed, the response process begins.

The resulting behavior may also become a new SIEM/EDR detection.

---

# 23. Example Threat Hunt — Credential Abuse

### Hypothesis

A compromised account may be used outside normal patterns.

The hunter searches for:

- Authentication from unusual locations
- New devices
- Unusual login times
- Repeated authentication failures
- Privilege changes
- Unusual resource access

The analyst then correlates identity, VPN, endpoint, and application logs.

The important point is that the hunter is looking for evidence **before an existing alert necessarily identifies the activity**.

---

# 24. Example Threat Hunt — Lateral Movement

### Hypothesis

An attacker may be moving between internal systems using legitimate administrative protocols.

Potential evidence includes:

- Unusual remote logons
- Administrative shares
- Remote service creation
- Unusual RDP activity
- SMB connections
- WinRM activity
- Remote PowerShell
- Authentication between systems that normally do not communicate

The hunter should establish what normal administrative behavior looks like before treating every remote connection as malicious.

---

# 25. Threat Hunting and Baselines

Baselines are important because hunting frequently involves finding deviations from expected behavior.

Example:

A database server normally communicates with:

```text
Application Server
Backup Server
Monitoring Server
```

A hunt discovers communication with:

```text
Unknown workstation
External destination
```

That deviation becomes an investigation candidate.

Again, unusual does not automatically mean malicious.

---

# 26. Detection Engineering

Threat hunting and detection engineering are closely connected.

A hunt may reveal a behavior that existing controls do not detect.

The organization can convert the lesson into a detection.

```text
Hunt
 ↓
New behavior discovered
 ↓
Determine reliable observable
 ↓
Create detection rule
 ↓
Test
 ↓
Deploy
 ↓
Tune
 ↓
Monitor
```

This creates a feedback loop between proactive hunting and automated detection.

---

# 27. Detection Rule Quality

A good detection should be:

- Relevant
- Actionable
- Understandable
- Testable
- Maintainable
- Based on useful telemetry
- Resistant to obvious evasion
- Tuned to acceptable false-positive levels

A detection that fires continuously for legitimate administrative activity is operationally weak even if the underlying behavior can sometimes be malicious.

---

# 28. Detection Tuning

Detection tuning attempts to improve the balance between useful detections and analyst workload.

Techniques include:

- Adjusting thresholds
- Adding contextual conditions
- Excluding known legitimate systems
- Adding user/asset context
- Combining multiple events
- Separating production from test environments
- Adding maintenance-window context

Example:

Instead of:

```text
Alert on every PowerShell execution
```

a more useful detection might focus on:

```text
Office application
    ↓
PowerShell
    ↓
Encoded command
    ↓
External connection
```

The second approach provides more behavioral context.

---

# 29. False Positives and False Negatives in Automation

Automation makes detection quality especially important.

If an automated workflow treats every alert as malicious, a false positive can become an outage.

Example:

```text
False positive
   ↓
SOAR automatically isolates server
   ↓
Critical application becomes unavailable
```

Therefore, automation should be calibrated according to confidence and impact.

High-impact automated actions generally require stronger confidence and more safeguards than low-impact enrichment actions.

---

# 30. Automation Risk Classification

A useful conceptual classification is:

### Low-impact

Usually safe to automate:

- Data enrichment
- Reputation lookup
- Ticket creation
- Evidence collection

### Medium-impact

May require conditional automation:

- Adding a temporary block
- Disabling a suspicious token
- Quarantining a file

### High-impact

Often requires explicit approval:

- Production shutdown
- Critical server isolation
- Broad firewall blocking
- Mass account disablement
- Destructive remediation

The exact boundary depends on organizational policy and technical safeguards.

---

# 31. SOAR Case Management

Security cases should preserve the relationship between alerts, evidence, actions, and decisions.

A case may contain:

- Alert information
- Analyst notes
- Timeline
- Indicators
- Enrichment results
- Affected assets
- Users
- Actions taken
- Approvals
- Communications
- Final disposition

This creates an auditable investigation record.

---

# 32. Automation and Evidence Preservation

Automated response should consider evidence preservation.

For example, immediately deleting a suspicious file may remove useful forensic evidence.

Depending on the incident and procedure, the preferred action may be to:

```text
Identify file
   ↓
Collect relevant metadata/evidence
   ↓
Preserve evidence
   ↓
Quarantine or contain
   ↓
Continue investigation
```

Automation must therefore be designed with the incident-response and forensic process in mind.

---

# 33. Automation Security

The automation infrastructure itself can become an attack target.

If an attacker compromises a SOAR service account with excessive permissions, they may gain the ability to:

- Modify firewall rules
- Disable accounts
- Isolate systems
- Access security data
- Change security configurations

Therefore, SOAR should use:

- Least privilege
- Dedicated service accounts
- Strong authentication
- Secret management
- API scopes
- Logging
- Change control
- Segmentation

Security automation must itself be secured.

---

# 34. Threat Hunting vs Incident Response

These activities are related but different.

**Incident response:** responds to a suspected or confirmed security incident.

**Threat hunting:** proactively searches for threats or suspicious behavior that may not have generated an alert.

Example:

```text
Confirmed ransomware alert → Incident response

No alert, but hypothesis that attackers may be abusing RDP
→ Threat hunting
```

A threat hunt can discover an incident and transition into incident response.

---

# 35. Threat Hunting vs Vulnerability Scanning

These are also different.

**Vulnerability scanning** looks for known weaknesses or vulnerabilities in systems.

**Threat hunting** looks for evidence of malicious or suspicious activity.

Example:

```text
Open vulnerable service → Vulnerability scanning

Attacker appears to be using that service → Threat hunting
```

They can complement one another but answer different questions.

---

# 36. Threat Hunting vs Penetration Testing

**Penetration testing** intentionally attempts to exploit vulnerabilities under an authorized scope.

**Threat hunting** searches real organizational telemetry for evidence of suspicious or malicious activity.

A penetration test asks:

> “Can this weakness be exploited?”

Threat hunting asks:

> “Is there evidence that this suspicious behavior is occurring or has occurred?”

---

# 37. Common SOAR and Automation Failures

## Failure 1 — Automating before understanding the process

A poorly designed playbook can automate a flawed workflow.

Better approach: document and validate the process first.

## Failure 2 — Excessive permissions

A SOAR account with unrestricted access increases blast radius.

Better approach: least privilege and narrowly scoped API permissions.

## Failure 3 — No approval for destructive actions

A false positive can become an outage.

Better approach: human approval or strong conditional controls for high-impact actions.

## Failure 4 — No error handling

A failed API call may cause incomplete response.

Better approach: detect failures, log them, and escalate safely.

## Failure 5 — No audit trail

It becomes difficult to determine what automation did and why.

Better approach: record actions, inputs, outputs, approvals, and timestamps.

## Failure 6 — Automating evidence destruction

Immediate deletion may destroy forensic information.

Better approach: design response with evidence preservation in mind.

---

# 38. Common Threat Hunting Failures

## Failure 1 — Hunting without a hypothesis

Searching everything without a question produces enormous amounts of data and weak conclusions.

Better approach: define a specific hypothesis.

## Failure 2 — Searching only for known IOCs

Attackers can change hashes, domains, and IP addresses.

Better approach: combine IOC-based and behavior-based hunting.

## Failure 3 — No baseline

Normal administrative activity may appear suspicious without context.

Better approach: understand expected behavior.

## Failure 4 — No documentation

A successful hunt cannot be repeated or operationalized.

Better approach: document hypothesis, queries, findings, and lessons learned.

## Failure 5 — Finding a suspicious event and stopping

A single indicator may represent only one part of a larger attack.

Better approach: determine scope and pivot across related telemetry.

---

# 39. Security+ Technology Distinctions

| Technology/Activity | Primary purpose |
|---|---|
| SIEM | Centralized security telemetry, correlation, detection, alerting |
| SOAR | Security orchestration and automated workflows |
| EDR | Endpoint detection, investigation, and response |
| XDR | Cross-domain detection and response correlation |
| Threat intelligence | Threat context and indicators |
| Threat hunting | Proactive search for threats/suspicious activity |
| Vulnerability scanning | Identify known vulnerabilities/weaknesses |
| Penetration testing | Authorized exploitation to validate security |
| Detection engineering | Create and maintain useful detections |
| Playbook | Defined operational workflow |
| Automation | Programmatic execution of defined tasks |

---

# 40. Security+ Exam Traps

### Trap 1 — “SOAR is another SIEM”

Not primarily. SIEM focuses on security telemetry collection, correlation, analysis, and detection; SOAR focuses on orchestrating and automating response workflows.

### Trap 2 — “Threat hunting waits for alerts”

No. Threat hunting is proactive.

### Trap 3 — “Threat hunting is the same as vulnerability scanning”

No. Vulnerability scanning identifies weaknesses; threat hunting searches for evidence of suspicious or malicious activity.

### Trap 4 — “Every automated response should be fully automatic”

No. High-impact actions may require human approval.

### Trap 5 — “An IOC proves compromise”

Not necessarily. Indicators require contextual validation.

### Trap 6 — “Automation removes the need for analysts”

No. Automation reduces repetitive work; analysts remain important for ambiguous and high-impact decisions.

### Trap 7 — “A playbook is just a script”

A playbook is a broader operational workflow and can include conditions, integrations, approvals, exceptions, and documentation.

---

# 41. Practical SOC Workflow

A mature SOC can combine all these capabilities:

```text
Telemetry
   ↓
SIEM
   ↓
Detection
   ↓
Alert
   ↓
SOAR
   ↓
Enrichment
   ↓
Analyst triage
   ↓
Investigation
   ↓
Response
   ↓
Case documentation
   ↓
Detection improvement
```

Meanwhile, threat hunting operates proactively:

```text
Threat intelligence / ATT&CK / incidents
              ↓
          Hypothesis
              ↓
        Telemetry search
              ↓
          Analysis
              ↓
          Discovery
              ↓
     Detection improvement
              ↓
       Response if needed
```

This creates a continuous improvement cycle.

---

# 42. Complete Threat Hunting Example

Imagine the security team receives intelligence that attackers are increasingly abusing legitimate remote administration tools.

### Phase 1 — Hypothesis

“An attacker may be using legitimate remote administration software to maintain access while avoiding traditional malware detection.”

### Phase 2 — Identify telemetry

Search:

- EDR process telemetry
- Application inventory
- Network connections
- DNS logs
- Authentication logs

### Phase 3 — Establish expected behavior

Determine which systems legitimately use the software and which users are authorized.

### Phase 4 — Hunt

Search for:

```text
Remote administration software
+ unusual endpoint
+ unusual user
+ unexpected external connection
```

### Phase 5 — Investigate

Review process tree, command line, network destination, user identity, and persistence.

### Phase 6 — Validate

Determine whether the activity is legitimate administrative work or unauthorized use.

### Phase 7 — Respond

If malicious activity is confirmed, follow incident-response procedures.

### Phase 8 — Improve detection

Create a detection for the specific behavioral pattern discovered during the hunt.

This demonstrates how hunting can improve automated security operations.

---

# 43. Decision Framework for Security+ Questions

When a scenario appears, ask what the question is actually requesting.

### “Collect and correlate events from many systems”

Think **SIEM**.

### “Automatically coordinate several security tools”

Think **SOAR**.

### “Proactively search for activity that may have escaped detection”

Think **threat hunting**.

### “Create logic to detect a suspicious behavior”

Think **detection engineering**.

### “Automatically look up an IP and enrich an alert”

Think **automation/SOAR**.

### “Search for a known malicious hash across endpoints”

Think **IOC-based threat hunting**.

### “Search for suspicious behavior without relying on a known indicator”

Think **behavior-based threat hunting**.

### “Automatically isolate a system when a high-confidence condition is met”

Think **automated response through SOAR/EDR**, subject to policy and safeguards.

---

# 44. Key Takeaways

1. SOAR coordinates security tools and automates repeatable security workflows.
2. Automation reduces repetitive analyst work and improves consistency.
3. Automation must use appropriate authorization, logging, error handling, and safeguards.
4. High-impact actions may require human approval.
5. Playbooks define repeatable security workflows and can include conditions, integrations, approvals, and exceptions.
6. SIEM and SOAR complement one another but have different primary purposes.
7. EDR can be integrated into SOAR workflows for endpoint investigation and containment.
8. Threat hunting is proactive and does not depend on an existing alert.
9. Threat hunting should generally begin with a hypothesis.
10. Hunters use SIEM, EDR, identity, DNS, network, cloud, application, and other telemetry.
11. IOC-based hunting searches for known indicators.
12. Behavior-based hunting searches for suspicious activity patterns.
13. Threat intelligence can provide useful hunting leads but does not automatically prove compromise.
14. MITRE ATT&CK can help organize behavioral hunting hypotheses.
15. Baselines help distinguish expected behavior from suspicious deviations.
16. Hunting findings can become new detection rules.
17. Detection engineering requires testing, tuning, validation, and maintenance.
18. False positives can become especially dangerous when automated response is enabled.
19. The SOAR platform and its service accounts must themselves be secured.
20. Automation should preserve evidence where appropriate.
21. Threat hunting, vulnerability scanning, penetration testing, and incident response answer different operational questions.
22. Good security operations use automation for repeatability while preserving human judgment for ambiguous and high-impact decisions.

---

# Final Mental Model

Remember the roles like this:

```text
SIEM
  ↓
Find and correlate suspicious events

SOAR
  ↓
Coordinate and automate what happens next

Threat Hunting
  ↓
Proactively search for what detection may have missed

Detection Engineering
  ↓
Turn useful behavioral knowledge into repeatable detections
```

And remember the continuous security-operations loop:

**Detect → Enrich → Investigate → Respond → Hunt → Learn → Improve Detection → Automate Safely**

The goal is not maximum automation or maximum alerts. The goal is a security operation where **high-quality telemetry, reliable detections, proactive hunting, controlled automation, and analyst judgment work together to reduce detection and response time without creating unnecessary operational risk**.