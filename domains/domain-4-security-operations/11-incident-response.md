# Domain 4 — Module 11: Incident Response

Incident response is the structured process an organization uses to prepare for, detect, analyze, contain, eradicate, recover from, and learn from security incidents. For Security+, the important skill is not simply memorizing the names of phases. You must understand **what the responder is trying to accomplish at each phase, what actions belong there, what evidence should be preserved, and what should happen next**.

A useful operational model is:

**Preparation → Detection and Analysis → Containment → Eradication → Recovery → Post-Incident Activity**

The exact terminology can vary between organizations and frameworks, but the underlying objectives remain similar.

---

## 1. What Is a Security Incident?

A **security event** is an observable occurrence in a system or network. Most events are not security incidents. Examples include a user successfully logging in, a server receiving a DNS request, a firewall allowing traffic, or an administrator restarting a service.

A **security alert** is a notification generated because an event or group of events matches a detection rule, threshold, behavioral pattern, or other condition that may require investigation.

A **security incident** is an event or series of events that has, or may have, a meaningful security impact and requires a coordinated response. The impact may involve confidentiality, integrity, availability, authentication, authorization, or policy/compliance requirements.

For example, one failed login might simply be a user entering the wrong password. Hundreds of failed logins followed by a successful login from the same source could become a high-priority incident because the pattern may indicate credential attack activity.

### Event → Alert → Incident

The distinction is important:

| Term | Meaning | Example |
|---|---|---|
| Event | Something happened | User authentication attempt |
| Alert | Detection system reports suspicious activity | 100 failed logins detected |
| Incident | Confirmed or sufficiently suspected security problem requiring response | Account compromised through credential attack |

Not every alert becomes an incident. **Triage and analysis determine whether escalation is justified.**

---

## 2. Incident Response Objectives

The purpose of incident response is not merely to remove malware. A mature response process attempts to:

- Limit damage and prevent further spread.
- Protect confidentiality, integrity, and availability.
- Identify affected users, hosts, applications, accounts, and data.
- Determine how the attacker or malicious activity gained access.
- Preserve evidence for investigation and possible legal or disciplinary processes.
- Remove malicious artifacts and persistence.
- Restore trustworthy business operations.
- Detect recurrence or related activity.
- Improve controls so the same failure is less likely to happen again.

A common mistake is to focus only on **“How do I clean this machine?”** Incident response asks a larger question: **“What happened, how far did it spread, what remains compromised, and how do we safely return the environment to a trusted state?”**

---

# 3. Incident Response Lifecycle

## 3.1 Preparation

Preparation occurs **before the incident**. It establishes the capabilities required to respond quickly and consistently.

Important preparation activities include:

- Incident response policy and procedures.
- Defined roles and responsibilities.
- Escalation criteria.
- Contact lists and communication channels.
- SIEM, EDR, IDS/IPS, firewall, email, identity, and cloud logging.
- Centralized and synchronized timestamps.
- Evidence collection procedures.
- Forensic tooling.
- Backup and recovery capability.
- Incident response playbooks.
- Malware-analysis capability where appropriate.
- Training and exercises.
- Legal, regulatory, privacy, and contractual requirements.
- Relationships with external incident-response providers.
- Pre-approved containment actions where appropriate.

### Why preparation matters

During an active compromise, responders may have very little time. If nobody knows who can isolate a server, disable an account, contact legal counsel, communicate with management, or authorize emergency changes, the organization can lose valuable time.

Preparation therefore converts incident response from an improvised activity into a controlled operational process.

---

## 4. Incident Response Roles and Responsibilities

Incident response normally involves more than the SOC analyst.

Potential participants include:

- SOC analysts
- Incident responders
- Security engineers
- Network administrators
- System administrators
- Endpoint administrators
- Cloud administrators
- Identity and access teams
- Application owners
- Data owners
- Management
- Legal counsel
- Privacy officers
- Human resources
- Public relations/communications
- Compliance teams
- External forensic or incident-response specialists

The exact structure depends on the organization.

### Separation of responsibilities

A technical responder may determine that a host is compromised, while legal or management personnel determine how certain communications should be handled. The security team should not independently make decisions that belong to legal, HR, privacy, or executive stakeholders.

This is particularly important when an incident may involve regulated data, employees, customers, or law enforcement.

---

# 5. Detection and Analysis

Detection begins when suspicious activity is identified through security telemetry or another reporting mechanism.

Potential sources include:

- SIEM alerts
- EDR detections
- IDS/IPS alerts
- Firewall logs
- Authentication logs
- Cloud logs
- DNS logs
- Email security alerts
- Application logs
- User reports
- Threat-intelligence matches
- Vulnerability information
- Network traffic analysis

The first alert is **not automatically the complete story**. Analysts need to investigate context.

### Key analysis questions

1. What happened?
2. When did it happen?
3. Which account was involved?
4. Which endpoint, server, application, or cloud resource was involved?
5. What source initiated the activity?
6. What destination was contacted?
7. Is there evidence of execution or persistence?
8. Was data accessed or transferred?
9. Are additional systems affected?
10. What is the likely attack path?
11. What is the current business impact?
12. What evidence must be preserved?

---

## 6. Triage

**Triage** is the process of rapidly determining the significance, scope, and priority of an alert or suspected incident.

A SOC analyst may initially classify an alert as:

- Benign activity
- False positive
- Suspicious activity requiring monitoring
- Confirmed security incident
- High-priority incident requiring immediate escalation

Severity should not be based only on the alert name.

For example, an endpoint alert may be technically severe, but if the endpoint is an isolated test machine with no sensitive data, its business impact may differ from the same detection on a production database server.

Useful triage factors include:

- Asset criticality
- Data sensitivity
- Number of affected systems
- Privilege level of the account
- Evidence of lateral movement
- Evidence of persistence
- Evidence of data access or exfiltration
- Internet exposure
- Active attacker behavior
- Business impact
- Regulatory implications

---

# 7. Establishing Scope

Determining **scope** is one of the most important incident-response activities.

Suppose EDR identifies malware on one workstation. The responder should not immediately assume only one workstation is affected.

The investigation should examine:

- Other hosts with the same file hash.
- Other users with similar authentication activity.
- Other systems contacted by the compromised endpoint.
- Similar command-line activity.
- Persistence mechanisms.
- Related DNS requests.
- Network connections.
- Email messages that may have delivered the payload.
- Shared credentials.
- Cloud resources accessed by the compromised identity.

This is where SIEM, EDR, network telemetry, identity logs, DNS logs, and threat intelligence become valuable together.

---

# 8. Timeline Construction

A timeline organizes the incident chronologically.

A simplified example might look like:

```text
09:12 — User receives phishing email
09:15 — User opens malicious attachment
09:16 — Office process launches PowerShell
09:17 — PowerShell downloads payload
09:18 — EDR detects suspicious execution
09:20 — Endpoint contacts command-and-control infrastructure
09:25 — Account authenticates to another internal host
09:31 — Suspicious administrative activity observed
09:35 — SOC begins containment
```

Timeline analysis helps responders understand **initial access → execution → persistence → privilege escalation → lateral movement → collection → exfiltration**, where applicable.

It also helps identify gaps. If the first known malicious activity occurred at 09:15 but the attacker had authenticated to a server at 08:50, the investigation must determine whether the compromise started earlier than initially believed.

---

# 9. Containment

**Containment limits the immediate impact and prevents the incident from spreading while investigation and eradication continue.**

Containment is not the same as removing the attacker.

### Short-term containment

Short-term containment is intended to quickly reduce immediate risk.

Examples:

- Isolate an endpoint using EDR.
- Disconnect a compromised host from the network.
- Disable a compromised account.
- Block a malicious IP address.
- Block a malicious domain.
- Block a malicious file hash.
- Remove a malicious email from mailboxes.
- Restrict network communication.
- Temporarily disable an exposed service.

The objective is speed and risk reduction.

### Long-term containment

Long-term containment creates a more stable controlled environment while deeper remediation is prepared.

Examples include:

- Moving affected systems into a quarantine network.
- Applying temporary firewall restrictions.
- Rebuilding affected infrastructure in an isolated environment.
- Implementing additional monitoring.
- Restricting privileged access.
- Applying temporary compensating controls.

### Containment trade-offs

Containment can itself affect availability.

For example, shutting down a critical production server may stop attacker activity but may also interrupt a business-critical service. The response team therefore considers both security risk and operational impact.

---

# 10. Eradication

**Eradication removes the malicious presence and addresses the mechanisms that allowed the incident to continue.**

Possible actions include:

- Removing malware.
- Removing persistence mechanisms.
- Deleting malicious accounts.
- Resetting compromised credentials.
- Revoking stolen tokens or sessions.
- Removing malicious scheduled tasks.
- Removing unauthorized services.
- Closing exploited vulnerabilities.
- Correcting insecure configurations.
- Removing unauthorized access paths.
- Rebuilding compromised systems when trust cannot be restored.

Eradication should address the **root cause**, not just the visible symptom.

For example, deleting a malicious executable without fixing the vulnerability that allowed the attacker to execute code may leave the organization exposed to reinfection.

---

# 11. Containment vs Eradication vs Recovery

This distinction is one of the most important Security+ exam concepts.

| Phase | Primary objective | Example |
|---|---|---|
| Containment | Stop or limit ongoing damage | Isolate compromised endpoint |
| Eradication | Remove malicious presence and root cause | Remove persistence and patch exploited vulnerability |
| Recovery | Restore normal trusted operation | Rebuild/restore system and return it to production |

### Example

A ransomware-infected workstation is disconnected from the network.

That is **containment**.

The malware and persistence mechanisms are removed, compromised credentials are reset, and the exploited vulnerability is fixed.

That is **eradication**.

The workstation is rebuilt from a trusted image, validated, monitored, and returned to service.

That is **recovery**.

---

# 12. Recovery

Recovery restores systems and services to a trusted operational state.

Typical activities include:

1. Restore from a known-good backup or rebuild from a trusted image.
2. Apply required patches and security configurations.
3. Reset or rotate compromised credentials.
4. Validate security controls.
5. Confirm logging and monitoring are functioning.
6. Test application and business functionality.
7. Return the system to production in a controlled manner.
8. Increase monitoring for recurrence.

Recovery should not simply mean **“the system is running again.”** A system can be operational while still compromised.

The responder must establish reasonable confidence that the system is secure enough to return to normal service.

---

# 13. Validation During Recovery

Before returning a recovered system to normal operation, validate:

- Operating-system and application integrity.
- Security patches.
- Configuration baseline.
- Endpoint protection.
- Firewall configuration.
- Authentication and authorization.
- Logging.
- Network connectivity.
- Application functionality.
- Backup/recovery capability.
- Relevant detection rules.

Post-recovery monitoring is important because attackers may attempt to regain access after the original foothold has been removed.

---

# 14. Evidence Preservation During Incident Response

Incident response and forensic investigation overlap, but they are not identical.

Responders should preserve relevant evidence before actions that could destroy or modify it when feasible and consistent with the response objective.

Potential evidence includes:

- Disk images
- Memory captures
- System logs
- EDR telemetry
- Network captures
- Firewall logs
- Authentication records
- Email headers
- Malware samples
- File metadata
- Browser artifacts
- Cloud audit logs
- Command history
- Authentication tokens and session information

A responder must consider whether an action will alter evidence.

For example, immediately rebooting a compromised system may eliminate useful volatile-memory evidence. However, in a rapidly spreading attack, immediate containment may take priority. Incident response therefore requires balancing **evidence preservation against immediate risk reduction**.

---

# 15. Chain of Custody

When evidence may be used for legal, disciplinary, regulatory, or other formal purposes, the organization may need to maintain **chain of custody**.

Chain of custody documents who collected evidence, when it was collected, how it was handled, where it was stored, and who subsequently accessed or transferred it.

The purpose is to demonstrate that the evidence remained controlled and was not improperly altered or substituted.

Important practices may include:

- Unique evidence identification.
- Collection date and time.
- Collector identity.
- Evidence description.
- Hash values where appropriate.
- Secure storage.
- Transfer records.
- Access records.

---

# 16. Communication During an Incident

Communication is an operational control during incident response.

The response team should know:

- Who must be notified.
- What information can be shared.
- Which communication channels are trusted.
- Who can communicate externally.
- When management must be escalated.
- When legal or privacy teams must be involved.
- When customers, partners, regulators, or law enforcement may need notification.

### Why communication channels matter

If an attacker has compromised corporate email, using normal corporate email to discuss sensitive response activities may expose those discussions to the attacker.

Organizations may therefore maintain out-of-band communication methods for significant incidents.

---

# 17. Incident Response Playbooks

A **playbook** provides structured guidance for responding to a particular type of incident.

Examples include:

- Phishing playbook
- Malware playbook
- Ransomware playbook
- Compromised-account playbook
- Data-exfiltration playbook
- DDoS playbook
- Cloud-account compromise playbook
- Lost-device playbook

A playbook can specify:

```text
Detection
   ↓
Triage
   ↓
Validate
   ↓
Identify affected assets/accounts
   ↓
Contain
   ↓
Preserve evidence
   ↓
Eradicate
   ↓
Recover
   ↓
Monitor
   ↓
Document and improve
```

Playbooks improve consistency and reduce the amount of decision-making required during stressful incidents.

They should still allow human judgment because real incidents frequently differ from predefined scenarios.

---

# 18. Incident Response Automation

Automation can accelerate repetitive actions.

Examples:

- Automatically enrich an IP address with threat intelligence.
- Automatically collect endpoint information.
- Automatically create an incident ticket.
- Automatically disable a clearly compromised account under approved conditions.
- Automatically isolate a confirmed malicious endpoint.
- Automatically block a known malicious indicator.

Automation must have appropriate safeguards.

A poorly designed automation can cause significant damage. For example, automatically disabling every account associated with a suspicious login pattern could lock out legitimate users during a false positive.

High-impact actions should therefore use appropriate approval, confidence thresholds, rollback mechanisms, and audit logging.

---

# 19. Incident Severity and Escalation

Organizations commonly define severity levels to determine response priority.

Severity may depend on:

- Number of affected systems.
- Criticality of affected assets.
- Sensitivity of data involved.
- Privilege level of compromised identities.
- Evidence of active attacker control.
- Business disruption.
- Regulatory obligations.
- Public exposure.
- Potential financial or operational impact.

A compromised domain administrator account is generally operationally different from a single low-privilege workstation account because the potential blast radius is much larger.

The important Security+ concept is **contextual prioritization**, not a universal severity scale.

---

# 20. Incident Response Metrics

Metrics help organizations determine whether response capability is improving.

Useful metrics include:

### Mean Time to Detect — MTTD

How long it takes to identify suspicious or malicious activity.

### Mean Time to Respond — MTTR/response time

How long it takes to begin and execute appropriate response actions, depending on the organization's exact metric definition.

### Mean Time to Contain

How long it takes to limit the incident's spread or impact.

### Mean Time to Recover

How long it takes to restore affected services to an acceptable operational state.

Other useful measurements include:

- Number of incidents by category.
- Recurring incidents.
- False-positive rates.
- Detection coverage.
- Percentage of incidents with complete documentation.
- Percentage of corrective actions completed.
- Playbook effectiveness.

Metrics should support improvement rather than encourage teams to manipulate numbers.

---

# 21. Lessons Learned and Post-Incident Activity

After the immediate incident is resolved, the organization should determine what can be improved.

Questions include:

- What was the initial access vector?
- Why did existing controls fail to prevent or detect it?
- Why was the activity detected when it was?
- Were logs available and sufficiently detailed?
- Was the scope determined quickly?
- Did containment work as expected?
- Were communication paths effective?
- Were backups usable?
- Were response roles clear?
- Did the playbook match reality?
- What vulnerabilities or configuration weaknesses contributed?
- What controls should be changed?

Corrective actions may include:

- Patching.
- Configuration changes.
- New detection rules.
- Better segmentation.
- Stronger authentication.
- Additional logging.
- User awareness improvements.
- Playbook updates.
- Architectural changes.
- Access-control changes.
- Additional monitoring.

The incident should therefore feed improvements back into the security program.

---

# 22. Root Cause Analysis

**Root cause analysis** attempts to determine the underlying conditions that allowed the incident to occur or persist.

Consider a ransomware incident where an attacker exploited an unpatched internet-facing application.

The visible problem is ransomware.

A deeper analysis may identify:

```text
Ransomware execution
        ↓
Compromised server
        ↓
Unpatched application
        ↓
Patch-management failure
        ↓
Incomplete asset inventory
```

Removing the ransomware addresses the immediate problem. Fixing the vulnerability addresses one technical cause. Improving asset inventory and patch governance may address deeper organizational causes.

---

# 23. Incident Response vs Business Continuity vs Disaster Recovery

These concepts are related but different.

| Concept | Primary question |
|---|---|
| Incident Response | How do we handle the security incident? |
| Business Continuity | How do we keep critical business functions operating? |
| Disaster Recovery | How do we restore technology/services after disruption? |

A ransomware incident may require all three.

Incident response contains and investigates the compromise.

Business continuity keeps essential business functions operating through alternate processes or resources.

Disaster recovery restores systems and services.

Do not assume that restoring a backup alone constitutes incident response.

---

# 24. Incident Response vs Vulnerability Management

Vulnerability management is generally **proactive risk reduction**.

It identifies and prioritizes weaknesses before or independent of confirmed compromise.

Incident response is primarily concerned with **handling active or suspected security incidents**.

Example:

> A scanner finds an unpatched web server.

This is a vulnerability-management issue.

> The server is confirmed to have been exploited through that vulnerability.

Now incident response is required as well.

---

# 25. Incident Response vs Threat Hunting

Threat hunting proactively searches for evidence of malicious activity that may have escaped existing detections.

Incident response reacts to a suspected or confirmed incident and works to contain, eradicate, and recover from it.

A threat hunt may discover an incident that had not previously generated an alert.

Therefore:

**Threat hunting can discover incidents; incident response handles them.**

---

# 26. Incident Response Scenario — Compromised Endpoint

Suppose EDR reports that a workstation executed a suspicious PowerShell command and contacted a known malicious domain.

A disciplined response could be:

### Step 1 — Validate

Review the EDR alert, process tree, command line, user, timestamps, destination, and file information.

### Step 2 — Determine scope

Search SIEM and EDR for the same indicators across other endpoints.

### Step 3 — Contain

Isolate the endpoint if compromise is sufficiently likely and immediate isolation is operationally acceptable.

### Step 4 — Preserve evidence

Collect relevant telemetry and forensic artifacts before destructive actions where practical.

### Step 5 — Investigate

Determine initial access, execution, persistence, lateral movement, and potential data access.

### Step 6 — Eradicate

Remove malicious artifacts, persistence, unauthorized access, and the exploited weakness.

### Step 7 — Recover

Rebuild or restore the system, apply secure configuration, validate controls, and return it to service.

### Step 8 — Monitor

Watch for recurring indicators or related attacker activity.

### Step 9 — Lessons learned

Improve detection, endpoint controls, email security, patching, or user awareness based on the root cause.

---

# 27. Incident Response Scenario — Compromised Account

Suppose an employee's account authenticates from an unusual location and then accesses several systems it normally never uses.

The analyst should not automatically conclude that the account is compromised. The activity needs contextual analysis.

Potential actions include:

- Review authentication history.
- Check MFA events.
- Examine source IP and device information.
- Review impossible-travel or unusual-location indicators.
- Examine privileged actions.
- Search for password changes.
- Check token/session activity.
- Review accessed resources.
- Look for mailbox rules or forwarding changes.
- Check for lateral movement.

If compromise is confirmed, containment may include disabling the account, revoking sessions/tokens, resetting credentials, and restricting associated access.

Eradication may require removing persistence mechanisms such as unauthorized application registrations, malicious mailbox rules, or stolen credentials.

---

# 28. Incident Response Scenario — Ransomware

Consider an organization where several endpoints suddenly begin encrypting files.

The response priority is not to individually repair every workstation immediately.

The team should first determine whether the attack is actively spreading.

Potential containment actions include:

- Isolating affected endpoints.
- Restricting lateral movement.
- Disabling compromised accounts.
- Blocking known command-and-control infrastructure.
- Restricting dangerous administrative protocols.
- Protecting backup infrastructure.

The organization then investigates the initial access vector, persistence, scope, and attacker activity.

Recovery requires trusted restoration or rebuilding, validation, and monitoring.

A critical lesson is that **ransomware response includes protecting the ability to recover**. If attackers can access backup systems, the organization may lose an important recovery capability.

---

# 29. Common Incident Response Failures

## Failure 1 — Immediately deleting malware

Deleting the suspicious file may remove useful evidence and may not eliminate persistence.

**Better approach:** contain first when appropriate, preserve relevant evidence, investigate persistence, then eradicate systematically.

## Failure 2 — Rebooting immediately

A reboot can destroy volatile-memory evidence.

**Better approach:** consider evidence requirements and incident urgency before rebooting.

## Failure 3 — Isolating only the first host

The initial infected machine may not be the only compromised asset.

**Better approach:** search for related indicators and determine scope.

## Failure 4 — Treating the alert as the incident

An alert is evidence that something may be wrong, not necessarily proof of the complete incident.

**Better approach:** validate and investigate.

## Failure 5 — Recovering without fixing root cause

Restoring a system without closing the vulnerability can result in reinfection.

**Better approach:** eradicate the cause before or as part of recovery.

## Failure 6 — Poor documentation

Without timestamps, actions, evidence references, and decisions, responders may be unable to reconstruct what happened.

**Better approach:** maintain an incident record throughout the response.

## Failure 7 — Excessive automation

An incorrect automated containment rule can disrupt legitimate business activity.

**Better approach:** use confidence thresholds, guardrails, approvals where appropriate, and rollback procedures.

## Failure 8 — Using compromised communication channels

Attackers may monitor compromised email or collaboration accounts.

**Better approach:** maintain trusted or out-of-band communication mechanisms for serious incidents.

---

# 30. Security+ Exam Distinctions

### Containment vs Eradication

- **Containment:** limit spread or damage.
- **Eradication:** remove malicious presence and address the cause.

### Eradication vs Recovery

- **Eradication:** remove the threat.
- **Recovery:** restore trusted operation.

### Event vs Alert vs Incident

- **Event:** something occurred.
- **Alert:** detection system flags activity.
- **Incident:** security problem requiring coordinated response.

### Incident Response vs Threat Hunting

- **Incident response:** handles suspected/confirmed incidents.
- **Threat hunting:** proactively searches for hidden threats.

### Incident Response vs Vulnerability Management

- **Vulnerability management:** identify and reduce weaknesses.
- **Incident response:** handle active/suspected compromise.

### Incident Response vs Disaster Recovery

- **Incident response:** security investigation and response.
- **Disaster recovery:** restoration of technology/services.

### Short-Term vs Long-Term Containment

- **Short-term:** rapidly reduce immediate danger.
- **Long-term:** maintain a controlled state while eradication is prepared.

---

# 31. Security+ Scenario Decision Framework

When given an incident-response question, use this sequence:

### Question 1 — What stage are we in?

Is the organization preparing, detecting, containing, eradicating, recovering, or reviewing?

### Question 2 — Is the threat still active?

If yes, actions that limit further damage usually become important.

### Question 3 — Do we understand the scope?

Search related hosts, accounts, indicators, network activity, and cloud activity.

### Question 4 — Is evidence important?

If forensic or legal investigation is involved, preserve evidence appropriately.

### Question 5 — Has the malicious presence been removed?

If not, the organization is not finished with eradication.

### Question 6 — Can the system be trusted again?

Recovery requires validation, not simply restarting the system.

### Question 7 — What prevents recurrence?

Address vulnerabilities, configuration weaknesses, identity problems, missing telemetry, or process failures identified during the investigation.

---

# 32. Practical SOC Incident Workflow

A practical SOC workflow can be represented as:

```text
Security Telemetry
       ↓
Detection / Alert
       ↓
Triage
       ↓
Validate
       ↓
Classify / Escalate
       ↓
Determine Scope
       ↓
Preserve Evidence
       ↓
Contain
       ↓
Investigate Root Cause
       ↓
Eradicate
       ↓
Recover
       ↓
Monitor
       ↓
Lessons Learned
       ↓
Improve Controls and Detections
```

The process is not always strictly linear. New evidence discovered during investigation can require responders to return to containment, expand the scope, or repeat earlier steps.

---

# 33. Final Mental Model

Think of incident response as answering a sequence of operational questions:

**Before the incident:**

> Are we prepared?

**When suspicious activity appears:**

> Is this actually malicious, and what happened?

**When compromise is confirmed:**

> How far has it spread, and how do we stop further damage?

**During eradication:**

> How did the attacker maintain access, and how do we remove the cause?

**During recovery:**

> Can we restore the environment to a trusted state?

**After recovery:**

> What failed, what evidence did we learn from, and what must change?

The strongest Security+ answers usually follow this logic rather than jumping directly to a technical action.

---

# 34. Key Takeaways

- Incident response is a structured lifecycle for handling security incidents.
- Preparation determines how effectively an organization can respond under pressure.
- An event is not automatically an alert, and an alert is not automatically an incident.
- Detection and analysis establish validity, scope, timeline, and impact.
- Containment limits ongoing damage and spread.
- Short-term containment prioritizes rapid risk reduction.
- Long-term containment establishes a more stable controlled state.
- Eradication removes malicious artifacts, persistence, compromised access, and root causes.
- Recovery restores systems to a trusted operational state and validates security controls.
- Evidence should be preserved when appropriate, especially when forensic or legal requirements exist.
- Chain of custody documents the controlled handling of evidence.
- Playbooks provide repeatable response guidance.
- Automation should be controlled with appropriate safeguards.
- Incident severity depends on context, asset criticality, scope, privilege, data sensitivity, and business impact.
- Incident response is different from vulnerability management, threat hunting, business continuity, and disaster recovery.
- Lessons learned should feed improvements into architecture, controls, detections, procedures, and training.

## Core Security+ Mental Model

**Detect → Validate → Scope → Contain → Preserve → Eradicate → Recover → Monitor → Learn → Improve**

That sequence provides a practical way to reason through most Security+ incident-response scenarios.