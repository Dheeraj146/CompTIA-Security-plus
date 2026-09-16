# Change and Configuration Management

Change and configuration management provides the operational discipline required to modify systems **without losing security, availability, accountability, or control**.

Modern environments change constantly. Administrators install software, security teams deploy new controls, developers release applications, cloud resources are modified, firewall rules are updated, and incidents sometimes require immediate containment changes.

If changes are made without control, an organization can introduce vulnerabilities, break security controls, create outages, lose auditability, or make incident investigation difficult.

Two related concepts must therefore be distinguished:

- **Configuration management** focuses on the desired and actual state of systems and infrastructure.
- **Change management** focuses on controlling modifications to that state.

A useful relationship is:

**Approved baseline → Change request → Risk assessment → Authorization → Implementation → Validation → Documentation → Configuration verification**

---

## 1. What Is Configuration Management?

Configuration management is the controlled process of establishing, maintaining, monitoring, and documenting the configuration of technology assets.

It answers questions such as:

- What configuration should this system have?
- What configuration does it currently have?
- When did it change?
- Who changed it?
- Was the change authorized?
- Does the current state still satisfy security requirements?

Configuration management can apply to:

- Servers
- Workstations
- Network devices
- Firewalls
- Applications
- Databases
- Cloud resources
- Containers
- Virtual machines
- IAM policies
- Security tools

---

## 2. What Is Change Management?

Change management is the structured process used to request, assess, authorize, implement, validate, document, and review changes.

The goal is not to prevent changes. Organizations must change systems to operate their businesses.

The goal is to ensure that changes are:

- Necessary
- Understood
- Authorized
- Tested when practical
- Implemented safely
- Reversible when possible
- Properly documented
- Validated after implementation

---

## 3. Why Change Management Is a Security Function

A configuration change can directly affect security.

For example, an administrator might:

- Open a firewall port.
- Disable endpoint protection.
- Modify an IAM policy.
- Change a logging configuration.
- Enable remote administration.
- Disable encryption.
- Install a new application.
- Change a database permission.

Each change can create security consequences.

Therefore, change management is not merely an IT service-management activity. It is also a security control that provides accountability and reduces uncontrolled configuration changes.

---

## 4. Standard Change Lifecycle

A typical change lifecycle is:

**Request → Analyze → Approve → Plan → Test → Schedule → Implement → Validate → Document → Review**

The exact workflow varies by organization, but the underlying objectives remain similar.

### Step 1 — Request

A person or team identifies a required change and records what needs to happen.

### Step 2 — Analyze

The team evaluates:

- Business purpose
- Security impact
- Technical impact
- Dependencies
- Availability impact
- Risk
- Required downtime
- Compatibility

### Step 3 — Approve

The appropriate authority determines whether the change should proceed.

### Step 4 — Plan

Implementation steps, responsibilities, testing, communication, and rollback procedures are prepared.

### Step 5 — Test

Where practical, the change is tested in a non-production environment or against representative systems.

### Step 6 — Schedule

The change is assigned an implementation window appropriate to the operational environment.

### Step 7 — Implement

Authorized personnel execute the planned change.

### Step 8 — Validate

The team verifies that the change produced the intended result and did not introduce unacceptable problems.

### Step 9 — Document

The final state and relevant implementation details are recorded.

### Step 10 — Review

The organization determines whether the change achieved its purpose and whether lessons should be incorporated into future procedures or baselines.

---

## 5. Change Request

A change request should contain enough information for reviewers to understand the proposed modification.

Typical information may include:

- Description of the change
- Business justification
- Systems affected
- Security impact
- Risk assessment
- Implementation plan
- Testing plan
- Maintenance window
- Responsible personnel
- Dependencies
- Rollback plan
- Validation criteria
- Communication requirements

The exact fields depend on organizational procedures.

---

## 6. Risk and Impact Assessment

Before approving a significant change, the organization should understand what could happen if the change succeeds or fails.

Questions include:

- Could the change expose a service to the internet?
- Could it disable a security control?
- Could it interrupt production?
- Could it modify sensitive data?
- Could it affect authentication?
- Could it affect dependent systems?
- Could it create compliance issues?
- What happens if the change fails halfway through?

### Example

Changing a firewall rule from:

```text
Source: Internal network
Destination: Application server
Port: TCP/443
```

to:

```text
Source: Any
Destination: Application server
Port: Any
```

is a major security change because it significantly expands network exposure.

The change should therefore be evaluated rather than treated as a routine configuration edit.

---

## 7. Testing Changes

Testing reduces the probability that a change will cause unexpected security or availability problems.

Testing may occur in:

- Development environments
- Test environments
- Staging environments
- Lab environments
- Pilot deployments

Testing can verify:

- Functionality
- Compatibility
- Security controls
- Performance
- Authentication
- Logging
- Network connectivity
- Application behavior

Testing should reflect the risk and nature of the change. Not every emergency security action can be fully tested before implementation.

---

## 8. Maintenance Windows

A maintenance window is a planned period during which changes can be implemented with acceptable operational impact.

The appropriate window depends on:

- Business operating hours
- Customer activity
- System criticality
- Geographic distribution
- Dependencies
- Expected downtime
- Staffing

A maintenance window does not eliminate risk. It simply provides a controlled period for implementation.

---

## 9. Rollback and Backout Plans

A **rollback plan** defines how to return a system to a previous known-good state if a change fails.

For example, before changing a firewall configuration, an administrator might preserve the previous configuration so it can be restored if the new policy causes unexpected traffic disruption.

Rollback may involve:

- Restoring a configuration
- Reverting a software version
- Restoring a database backup
- Re-deploying a previous application version
- Reverting an IaC commit
- Restoring a VM snapshot where appropriate

A rollback plan should be realistic. It should not assume that every change can be reversed instantly or without data consequences.

---

## 10. Validation After a Change

Implementation does not mean success.

After a change, validation should confirm that:

1. The intended functionality works.
2. Security controls remain active.
3. Logging continues to function.
4. Access is correct.
5. No unexpected exposure was introduced.
6. Dependent services continue operating.
7. The system matches the approved configuration.

For example, after deploying a new firewall rule, validation should include both the intended allowed traffic and traffic that should remain blocked.

---

## 11. Configuration Drift and Unauthorized Changes

A system can deviate from its approved baseline because of:

- Authorized changes
- Emergency changes
- Manual administration
- Software updates
- Configuration errors
- Unauthorized changes
- Malware or attacker activity

Configuration monitoring can detect the deviation, but additional investigation is required to determine its cause.

A configuration difference is therefore an **indicator requiring context**, not automatically proof of malicious activity.

---

## 12. Change Records and Auditability

Change records provide evidence of what was intentionally modified.

During an investigation, security personnel may discover a suspicious firewall rule.

The change-management system can help answer:

- Was this rule intentionally created?
- Who requested it?
- Who approved it?
- When was it implemented?
- What was the business justification?
- When should it have been removed?

Without change records, analysts may have difficulty distinguishing legitimate administration from unauthorized modification.

---

## 13. Standard, Normal, and Emergency Changes

Organizations often categorize changes according to their predictability and urgency.

### Standard changes

Standard changes are well-understood, repeatable, low-risk activities that have an established procedure.

Examples might include a routine approved maintenance task performed according to a documented process.

### Normal changes

Normal changes require assessment and authorization because their impact or risk is not sufficiently routine to use a standard procedure.

### Emergency changes

Emergency changes address urgent situations such as:

- Active exploitation
- Major security incidents
- Critical vulnerabilities
- Severe service failures
- Immediate containment requirements

Emergency changes may use an expedited approval process.

They are **not exempt from accountability**.

The organization should still record what happened and perform appropriate review afterward.

---

## 14. Emergency Change Example

Suppose an actively exploited vulnerability is discovered in an internet-facing service.

The security team determines that the service must be temporarily blocked immediately.

Waiting several days for the normal change window could increase exposure.

An emergency process may allow:

1. Rapid authorization by the designated authority.
2. Immediate firewall or access-control change.
3. Verification that the exploit path is blocked.
4. Documentation of the emergency change.
5. Follow-up remediation of the vulnerable service.
6. Post-implementation review.

The key distinction is:

**Emergency means expedited; it does not mean undocumented or unauthorized.**

---

## 15. Separation of Duties

Separation of duties reduces the risk that one person can initiate and complete a sensitive action without oversight.

For example:

- One person requests a high-risk change.
- Another authorized person approves it.
- A designated administrator implements it.
- A separate monitoring or audit function may verify the result.

The exact separation depends on organizational size and risk.

In small environments, complete separation may be difficult. Compensating oversight can be used where appropriate.

---

## 16. Least Privilege and Change Management

Only authorized personnel should have the permissions required to implement changes.

For example, an analyst who only needs to review firewall events should not automatically receive permission to modify firewall policies.

Restricting change privileges reduces the likelihood that:

- A compromised account can alter security controls.
- An accidental action causes an outage.
- An unauthorized administrator makes undocumented changes.

Privileged actions should also be logged where practical.

---

## 17. Version Control

Version control allows organizations to maintain historical versions of configuration and infrastructure definitions.

It is especially valuable for:

- Firewall configurations
- IaC definitions
- Application source code
- Configuration files
- Security policies implemented as code
- Deployment templates

Version history helps determine:

- What changed?
- When did it change?
- Who made the change?
- What was the previous state?

It also supports rollback when the previous version represents a known-good state.

---

## 18. Infrastructure as Code and Change Management

IaC changes should still follow change-management principles.

For example:

```text
Developer/admin proposes IaC change
          ↓
Version control commit
          ↓
Peer review
          ↓
Security validation
          ↓
Testing
          ↓
Approval
          ↓
Automated deployment
          ↓
Validation
```

This creates a traceable relationship between the requested infrastructure state and the deployed state.

Automation can improve consistency, but it does not remove the need for authorization and security review.

---

## 19. Configuration Management Database and Change Management

A CMDB can provide information about configuration items and their relationships.

Change management can use that information to understand impact.

For example, before changing a database server, the organization can determine which applications depend on it.

This helps prevent a situation where a seemingly simple change causes multiple services to fail.

The combination is:

**Configuration information + dependency information + change control = better impact analysis**

---

## 20. Change Management and Security Baselines

A baseline defines the intended state.

A change process controls how the organization moves from one approved state to another.

For example:

```text
Baseline A
    ↓
Approved Change
    ↓
Baseline/Configuration B
```

If a change occurs without authorization, the current state may no longer be trustworthy.

Configuration monitoring can identify the difference, while change records help determine whether it was legitimate.

---

## 21. Security Tool Changes

Security tools themselves require change management.

Examples include:

- SIEM detection-rule changes
- EDR policy changes
- Firewall-rule changes
- IDS/IPS signature changes
- DLP policy changes
- WAF-rule changes
- IAM policy changes
- Email security policy changes

Changing a detection rule can affect security visibility just as changing a firewall rule can affect network exposure.

For example, disabling a noisy SIEM rule may reduce false positives but could also remove detection coverage. Such changes should be evaluated, documented, and monitored.

---

## 22. Change Freeze

A **change freeze** is a period during which nonessential changes are restricted or prohibited.

Organizations may use change freezes during:

- Major business events
- Peak transaction periods
- Critical operational windows
- Large migrations
- High-risk periods

A change freeze reduces unnecessary operational risk, but emergency security changes may still need to occur.

---

## 23. Configuration Standardization

Standardization reduces unnecessary variation between similar systems.

For example, if an organization operates 500 workstations, standardizing their security configuration makes it easier to:

- Patch them
- Monitor them
- Investigate them
- Apply security policies
- Detect deviations
- Troubleshoot problems

However, standardization should not ignore legitimate system differences.

A database server and a user workstation should not necessarily have identical configurations simply because consistency is desirable.

---

## 24. Secure Deployment Practices

Secure deployment can use:

- Hardened images
- Standard templates
- IaC
- Version control
- Configuration profiles
- Automated security checks
- Peer review
- Separation of duties
- Deployment pipelines
- Post-deployment validation

The objective is to reduce manual error and make the intended security state reproducible.

---

## 25. Security Operations Scenario: Firewall Rule Change

An application team requests that a firewall allow inbound traffic from a new partner.

A structured process would include:

1. Identify the business requirement.
2. Identify source and destination systems.
3. Determine the required protocol and port.
4. Assess exposure and risk.
5. Confirm the partner's expected source addresses where applicable.
6. Create the least-permissive rule that satisfies the requirement.
7. Obtain appropriate approval.
8. Implement during an appropriate window.
9. Validate allowed and denied traffic.
10. Document the final rule.
11. Review the rule periodically.

This demonstrates that change management and least privilege can apply directly to network security.

---

## 26. Security Operations Scenario: Emergency Account Disablement

A privileged account is believed to be compromised.

Immediate containment may require disabling the account and terminating active sessions.

Because this is an urgent security action, it may follow an emergency change procedure.

After containment, the organization should:

- Document the action.
- Investigate the compromise.
- Determine whether additional accounts are affected.
- Rotate credentials as appropriate.
- Review related changes.
- Restore required access through controlled procedures.
- Perform a post-incident review.

The incident-response need does not eliminate change accountability.

---

## 27. Security Operations Scenario: Configuration Drift

A server baseline requires a host firewall to be enabled.

Configuration monitoring reports that the firewall is disabled.

The analyst should determine:

- When it was disabled.
- Which account performed the change.
- Whether a change request exists.
- Whether troubleshooting was occurring.
- Whether the change was approved.
- What security exposure resulted.

If the change was unauthorized, the team should remediate the configuration and investigate whether it is related to a security incident.

---

## 28. Security Operations Scenario: Failed Deployment

A software update causes an application to stop communicating with its database.

The change team should use the documented rollback or recovery procedure if appropriate.

After service restoration, the organization should determine:

- Why testing did not detect the problem.
- Whether dependencies were misunderstood.
- Whether the rollback procedure worked.
- Whether the deployment process should change.
- Whether monitoring should be improved.

The objective is not merely to restore service but to reduce recurrence.

---

## 29. Common Change Management Failures

### Failure 1 — Unauthorized changes

Changes occur without approval or documentation.

### Failure 2 — No impact assessment

Teams modify systems without understanding dependencies or security consequences.

### Failure 3 — No testing

Changes are deployed directly to production when testing could reasonably have been performed.

### Failure 4 — No rollback plan

A failed change becomes difficult to reverse.

### Failure 5 — No validation

Teams assume that successful implementation means successful outcome.

### Failure 6 — Emergency changes remain undocumented

Urgent actions are performed but never entered into the change record.

### Failure 7 — Excessive permissions

Too many personnel can make sensitive changes.

### Failure 8 — Configuration and change records disagree

The documented state does not match the actual environment.

### Failure 9 — Stale exceptions

Temporary deviations become permanent without review.

### Failure 10 — Security-tool changes are ignored

Detection rules and security policies can lose effectiveness when modified without proper review.

---

## 30. Security+ Exam Focus

Understand the difference between:

- Configuration management and change management
- Baseline and configuration drift
- Standard, normal, and emergency changes
- Change request and change implementation
- Testing and validation
- Rollback and recovery
- Authorization and authentication
- Separation of duties and least privilege
- Version control and configuration history
- IaC and manual configuration

Remember:

> **Change management controls how changes are introduced; configuration management verifies and maintains the resulting state.**

---

## 31. Common Security+ Distinctions

| Concept | Meaning |
|---|---|
| Configuration management | Management of the desired and actual configuration state |
| Change management | Controlled process for modifying systems or configurations |
| Baseline | Approved reference configuration |
| Configuration drift | Deviation from the approved baseline |
| Change request | Formal record proposing a modification |
| Risk assessment | Evaluation of potential security and business consequences |
| Maintenance window | Planned period for implementing changes |
| Rollback plan | Procedure for returning to a previous state when a change fails |
| Validation | Confirmation that the implemented change achieved its intended result |
| Standard change | Predefined, repeatable, low-risk change with an established procedure |
| Normal change | Change requiring assessment and authorization |
| Emergency change | Expedited change required to address urgent conditions |
| Change freeze | Period during which nonessential changes are restricted |
| Version control | Management of historical versions of configurations or code |

---

## 32. Change Management Decision Framework

For Security+ scenario questions, use this process:

### Step 1 — Identify the requested change

What exactly will be modified?

### Step 2 — Determine the business and security purpose

Why is the change required?

### Step 3 — Assess risk and dependencies

What systems, users, security controls, or data could be affected?

### Step 4 — Determine the change category

Is it standard, normal, or emergency?

### Step 5 — Obtain appropriate authorization

Follow the organization's change-control process.

### Step 6 — Plan implementation

Define implementation, testing, communication, and rollback procedures.

### Step 7 — Implement with least privilege

Only authorized personnel should perform the change.

### Step 8 — Validate

Confirm both functionality and security.

### Step 9 — Document

Record the final state and relevant evidence.

### Step 10 — Monitor and review

Verify that the configuration remains secure and determine whether lessons should update the baseline or process.

---

## 33. Key Takeaways

- Configuration management maintains visibility and control over system states.
- Change management controls how modifications are introduced.
- A secure baseline defines the expected state.
- Configuration drift identifies a difference between actual and approved state.
- Changes should be assessed for security, business, availability, and dependency impact.
- Testing reduces deployment risk when practical.
- Rollback plans provide a controlled path back to a known-good state.
- Validation confirms that the intended result was actually achieved.
- Change records provide accountability and investigation evidence.
- Emergency changes are expedited but remain accountable and should receive appropriate post-change review.
- Separation of duties and least privilege reduce the risk of unauthorized or harmful modifications.
- Version control provides historical configuration visibility and supports controlled rollback.
- IaC can improve consistency and auditability but still requires security review and change control.
- Security tools and detection rules require change management too.
- Change freezes reduce unnecessary risk but do not eliminate the need for emergency security actions.
- Standardization reduces configuration inconsistency while legitimate system differences must still be respected.
- The objective is not to eliminate change; it is to make change **controlled, authorized, secure, traceable, and verifiable**.

**Core principle:**

> **Know the current state → define the desired state → control the transition → validate the result → document and monitor the new state.**
