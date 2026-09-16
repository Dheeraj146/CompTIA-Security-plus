# Secure Baselines and Configuration Management

Secure configuration is the practice of configuring systems, applications, devices, and infrastructure so that their settings meet defined security requirements. **Configuration management** is the controlled process used to establish, maintain, monitor, document, and change those configurations throughout the asset lifecycle.

A **secure baseline** is the approved reference configuration against which a system can be evaluated.

The central idea is simple:

> **A system should have a known-good security state, and the organization should be able to detect when that state changes.**

This is important because systems do not remain static. Administrators make changes, software is installed, emergency troubleshooting occurs, applications are upgraded, vulnerabilities are discovered, and attackers may attempt to modify security settings. Configuration management provides the operational discipline required to keep systems aligned with approved security requirements.

---

## 1. What Is a Secure Baseline?

A secure baseline defines the minimum approved configuration and security settings for a particular class of system.

For example, a Windows workstation baseline might specify:

- Required security updates
- Host firewall enabled
- Endpoint protection enabled
- Screen lock configured
- Approved authentication settings
- Logging enabled
- Unnecessary services disabled
- Local administrator access restricted
- Approved applications only
- Secure protocol settings

A Linux server baseline could contain different requirements because the system has different functions and dependencies.

Therefore, there is usually **no single universal baseline for every system**. Baselines should reflect the system's purpose, operating system, risk, regulatory requirements, and operational dependencies.

---

## 2. Why Secure Baselines Matter

Without a baseline, administrators may know that systems have different configurations but may not know which configuration represents the organization's intended secure state.

A baseline provides a reference for:

- Secure deployment
- Configuration assessment
- Hardening
- Change detection
- Compliance verification
- Troubleshooting
- Incident investigation
- Vulnerability reduction
- Standardization

For example, if a server normally has only HTTPS exposed but later begins listening on an unexpected remote-management port, the baseline gives security operations something concrete against which to compare the current state.

---

## 3. Baseline vs. Current Configuration

Consider a server with an approved configuration:

```text
Approved baseline:
- SSH enabled
- HTTPS enabled
- Telnet disabled
- Host firewall enabled
- Root remote login disabled
- Security logging enabled
```

The current configuration later becomes:

```text
Current state:
- SSH enabled
- HTTPS enabled
- Telnet enabled
- Host firewall enabled
- Root remote login disabled
- Security logging enabled
```

The difference is a **configuration deviation**.

The security team must then determine whether the deviation is:

1. Authorized and documented.
2. Temporary and expected.
3. An accidental misconfiguration.
4. An outdated baseline.
5. An unauthorized change.
6. Potential evidence of compromise.

The deviation itself does not automatically prove an attack.

---

## 4. Configuration Drift

**Configuration drift** occurs when a system gradually deviates from its approved configuration.

Drift can occur because of:

- Manual administrator changes
- Emergency troubleshooting
- Temporary exceptions
- Software installation
- Application updates
- Configuration mistakes
- Unauthorized changes
- Different administrators using different settings
- Inconsistent deployment processes
- Incomplete change documentation

### Example

A server's firewall rule is temporarily changed to permit troubleshooting traffic. The administrator resolves the issue but forgets to remove the temporary rule.

The server is now more exposed than the approved baseline.

This is configuration drift.

Configuration drift can be gradual and difficult to notice without automated assessment.

---

## 5. Configuration Management Lifecycle

A practical configuration-management lifecycle is:

**Define → Build → Deploy → Monitor → Detect deviation → Assess → Approve/remediate → Validate → Document → Review**

### Define

Establish the desired configuration based on security and business requirements.

### Build

Create an image, template, configuration profile, or deployment definition representing the approved state.

### Deploy

Apply the configuration to systems.

### Monitor

Continuously or periodically assess systems against the approved state.

### Detect deviation

Identify configuration changes or drift.

### Assess

Determine whether the difference is legitimate, required, risky, or unauthorized.

### Approve or remediate

An authorized change may be documented and retained. An unnecessary or unauthorized change may need to be reversed.

### Validate

Confirm that the system now satisfies the intended security state.

### Document

Record the change, reason, authorization, and resulting configuration where required.

### Review

Baselines themselves should be reviewed because security requirements, software versions, threats, and business requirements change.

---

## 6. System Hardening

**Hardening** reduces attack surface by removing unnecessary functionality and restricting what a system can do.

Common hardening actions include:

- Disable unnecessary services.
- Disable unused ports and protocols.
- Remove unnecessary applications.
- Remove or disable unnecessary accounts.
- Change default credentials.
- Restrict administrative interfaces.
- Apply security updates.
- Enable host-based firewalls.
- Enable endpoint protection.
- Restrict permissions.
- Enforce secure authentication.
- Disable insecure protocols.
- Enable appropriate auditing.
- Restrict remote access.

Hardening should always consider dependencies.

For example, disabling a service because it appears unnecessary can break an application if the service is actually required. Secure configuration therefore requires both security knowledge and understanding of the system's function.

---

## 7. Attack Surface Reduction Through Configuration

Every unnecessary service, application, interface, protocol, account, and permission can potentially increase attack surface.

Consider a server running:

```text
Web service
Database service
FTP service
Telnet service
Remote administration service
Unused development service
```

If the server only requires the web service and database service, unnecessary services increase exposure.

Hardening might involve removing or disabling services that are not required.

The security principle is:

> **Enable only what is required for the system's intended function.**

This supports least functionality and reduces opportunities for exploitation.

---

## 8. Secure Configuration Areas

A baseline can address many configuration categories.

### Authentication

Examples:

- Password policy
- MFA requirements
- Account lockout
- Authentication protocols
- Session controls

### Authorization

Examples:

- Administrative privileges
- File permissions
- Application permissions
- Service-account permissions

### Network

Examples:

- Firewall rules
- Listening ports
- Allowed protocols
- Network interfaces
- Proxy settings
- DNS configuration

### Services

Examples:

- Required services
- Disabled services
- Startup configuration
- Service accounts

### Logging

Examples:

- Audit categories
- Log destinations
- Log retention
- Centralized forwarding
- Security-event collection

### Endpoint protection

Examples:

- EDR/antimalware status
- Host firewall
- Application control
- Device-control settings

### Cryptography

Examples:

- Approved algorithms
- TLS versions
- Certificate configuration
- Encryption requirements

---

## 9. Secure Configuration Is Not the Same as Patching

Patching addresses vulnerabilities by updating software to versions that contain security fixes or other required changes.

Secure configuration addresses how software and systems are configured.

A system can be:

- Fully patched but insecurely configured.
- Securely configured but missing critical patches.
- Both securely configured and patched.
- Neither securely configured nor patched.

For example, a fully patched server with an unnecessarily exposed administrative interface may still have avoidable exposure.

Security operations therefore needs both **patch management and configuration management**.

---

## 10. Security Baselines and Compliance

Organizations may have configuration requirements originating from:

- Internal security policies
- Regulatory requirements
- Industry standards
- Vendor guidance
- Organizational risk decisions
- Contractual requirements

Configuration assessment can determine whether systems meet those requirements.

However, compliance with a baseline does not automatically mean a system is immune to compromise. A baseline is a defined security state, not a guarantee that no vulnerabilities exist.

---

## 11. Configuration Assessment

Configuration assessment compares actual system settings against approved requirements.

Tools that may assist include:

- Endpoint management platforms
- Configuration-management systems
- Vulnerability scanners
- Security-compliance scanners
- Cloud configuration tools
- Policy-enforcement systems
- Infrastructure-as-code validation tools

Assessment may identify:

- Disabled security controls
- Unexpected services
- Weak permissions
- Unauthorized software
- Insecure protocols
- Incorrect firewall settings
- Missing logging
- Weak authentication settings
- Configuration drift

Assessment can be periodic or continuous depending on the environment and risk.

---

## 12. Automated Configuration Enforcement

Some environments can automatically enforce desired settings.

For example, endpoint-management software may enforce:

- Firewall enabled
- Encryption enabled
- Required security software running
- Screen lock enabled
- Approved applications installed

Automation reduces reliance on manual administration.

However, automatic enforcement must be designed carefully. A poorly defined policy can create widespread outages by changing many systems simultaneously.

---

## 13. Gold Images

A **gold image** is an approved system image containing a standardized operating system and configuration.

For example, an organization may maintain a hardened Windows workstation image containing:

- Approved OS version
- Required security updates
- Security software
- Standard configuration
- Required applications
- Security policies

New workstations can be deployed from the image instead of being configured manually from scratch.

### Benefits

- Consistency
- Faster deployment
- Reduced configuration errors
- Easier standardization
- Easier recovery

### Limitation

A gold image can become outdated.

If a security update released after the image was created is missing, every system deployed from that image may start with the same weakness.

Therefore:

> **A gold image is a standardized starting point, not a permanently secure artifact.**

---

## 14. Templates

Templates provide a similar concept for virtualized and cloud environments.

Examples include:

- VM templates
- Cloud machine images
- Infrastructure templates
- Container base images
- Configuration profiles

Templates allow organizations to deploy standardized environments repeatedly.

They should be version-controlled and maintained so that old insecure configurations do not continue to propagate.

---

## 15. Infrastructure as Code

**Infrastructure as Code (IaC)** represents infrastructure configuration in machine-readable definitions.

Examples include definitions for:

- Virtual networks
- Subnets
- Security groups
- Virtual machines
- Cloud storage
- Load balancers
- IAM policies
- Kubernetes resources

IaC can improve security because configurations can be:

- Version controlled
- Reviewed
- Tested
- Audited
- Reused
- Automatically deployed

### Important limitation

Automation does not automatically create security.

If an IaC template contains an insecure configuration, automation can reproduce that insecurity across hundreds of systems.

For example:

```text
Insecure template
       ↓
Automated deployment
       ↓
100 identical insecure resources
```

Therefore, IaC should be subjected to security review and automated validation.

---

## 16. Configuration Management in Cloud Environments

Cloud environments create additional configuration challenges because resources can be created quickly and configuration is often distributed across multiple services.

Important configuration areas include:

- IAM permissions
- Security groups
- Network ACLs
- Storage access policies
- Encryption settings
- Logging
- Public exposure
- API access
- Secrets
- Resource configurations

A cloud storage resource accidentally configured for public access can create significant data-exposure risk even if the underlying software is fully patched.

Cloud configuration-management tools can continuously evaluate resources against organizational policies.

---

## 17. Configuration Management and Containers

Container environments introduce configuration concerns such as:

- Container privileges
- Image provenance
- Open ports
- Secrets
- File permissions
- Runtime security
- Network policies
- Resource limits

A secure container baseline might specify that containers should:

- Avoid unnecessary privileges.
- Use approved images.
- Run as non-root where practical.
- Avoid unnecessary capabilities.
- Restrict network communication.
- Receive secrets through approved mechanisms.
- Have appropriate resource limits.

The same principle applies: establish a known-good state and continuously verify it.

---

## 18. Configuration Exceptions

Real environments sometimes require deviations from the standard baseline.

For example, a legacy application may require an older protocol that is normally prohibited.

Instead of silently ignoring the deviation, organizations should use a controlled exception process.

An exception may document:

- What baseline requirement is being bypassed
- Why the exception is necessary
- Which asset is affected
- Business justification
- Risk assessment
- Compensating controls
- Approval authority
- Expiration/review date

Exceptions should not become permanent undocumented weaknesses.

---

## 19. Configuration Management and Change Management

Configuration management and change management are closely related but are not identical.

**Configuration management** focuses on the desired and actual state of systems.

**Change management** focuses on controlling modifications to those systems.

For example:

> A firewall rule is changed to permit a new application.

Change management determines whether the modification is requested, reviewed, approved, tested, implemented, and documented.

Configuration management determines whether the firewall's resulting configuration matches the approved state.

Together they provide both **change accountability and configuration visibility**.

---

## 20. Emergency Changes

Security incidents sometimes require immediate configuration changes.

Examples include:

- Blocking malicious IP addresses
- Disabling a compromised account
- Isolating an endpoint
- Disabling an exploited service
- Restricting network communication

Normal change procedures may be accelerated during an emergency, but the organization should still record what was changed, why it was changed, who authorized it where practical, and what happened afterward.

Emergency changes should be reviewed after the immediate threat is addressed.

---

## 21. Configuration Monitoring and Unauthorized Changes

A configuration-monitoring system may detect that a sensitive file, registry setting, firewall rule, service, or security control has changed.

The detection should trigger investigation when appropriate.

An analyst should ask:

- Was the change authorized?
- Who made it?
- When did it occur?
- What account was used?
- What process made the change?
- Was a change ticket created?
- Does the change correspond to maintenance activity?
- Did other suspicious activity occur?

An unauthorized configuration change can be an operational error, an insider action, or a sign of compromise. Context is required.

---

## 22. Baseline Review and Maintenance

Security baselines themselves require lifecycle management.

A baseline may become inappropriate when:

- The operating system changes.
- Applications are replaced.
- New vulnerabilities are discovered.
- Business requirements change.
- New compliance requirements apply.
- Security architecture changes.
- Legacy technology is retired.

A stale baseline can create problems in two directions:

1. It may permit configurations that are no longer secure.
2. It may prohibit legitimate configurations required by newer systems.

Therefore, baseline review should be part of normal configuration governance.

---

## 23. Configuration Drift Detection Workflow

Consider a production server whose firewall configuration changes unexpectedly.

A structured response can be:

1. Detect the deviation.
2. Identify the affected asset.
3. Compare the current state with the approved baseline.
4. Determine what changed.
5. Identify the account or administrator responsible.
6. Check change-management records.
7. Determine whether the change was authorized.
8. Assess security impact.
9. Reverse or approve the change as appropriate.
10. Validate the final configuration.
11. Document the outcome.
12. Investigate further if evidence suggests compromise.

This demonstrates that configuration monitoring is not simply about finding differences. It is about determining whether differences are expected and secure.

---

## 24. Security Operations Scenario: Remote Administration Service

An administrator temporarily enables a remote administration service to troubleshoot a server.

The troubleshooting is completed, but the service remains enabled.

Later, configuration monitoring reports that the server no longer matches its baseline.

The analyst should:

- Verify the deviation.
- Check the change record.
- Determine whether the service is still required.
- Assess exposure.
- Disable the service if unnecessary.
- Validate the configuration.
- Document the result.

The key concept is **configuration drift caused by an operational change**.

---

## 25. Security Operations Scenario: Gold Image

An organization deploys hundreds of workstations from a gold image created six months earlier.

Security discovers that the image does not contain several important security updates.

The correct lesson is not that gold images are insecure. The issue is that the image lifecycle was not maintained.

The organization should:

1. Update the image.
2. Apply current security requirements.
3. Validate the new image.
4. Version the image.
5. Retire the outdated image.
6. Assess already deployed systems.

This demonstrates why standardized deployment must be combined with continuous maintenance.

---

## 26. Security Operations Scenario: IaC Misconfiguration

An infrastructure template accidentally permits unrestricted inbound access to a cloud service.

Because the template is automated, the same configuration is deployed repeatedly.

The correct response should include:

- Identify the insecure definition.
- Prevent further deployment where appropriate.
- Correct the template.
- Validate the corrected configuration.
- Assess already deployed resources.
- Redeploy or remediate affected resources.
- Review why security validation did not detect the problem.

The key principle is:

> **Fix the source of repeatable misconfiguration, not only the individual instances.**

---

## 27. Common Configuration Management Failures

### Failure 1 — No approved baseline

Without a reference state, teams may disagree about what configuration is secure or authorized.

### Failure 2 — Manual configuration everywhere

Manual configuration increases inconsistency and human error.

### Failure 3 — Stale baselines

Old baselines can preserve outdated security requirements.

### Failure 4 — No drift detection

Unauthorized or accidental changes can remain unnoticed.

### Failure 5 — Treating every deviation as malicious

Legitimate approved changes also create configuration differences.

### Failure 6 — Ignoring exceptions

Unmanaged exceptions can become permanent security weaknesses.

### Failure 7 — Insecure automation

Automation can reproduce bad configurations at scale.

### Failure 8 — No validation after changes

A configuration change should be verified rather than assumed to have worked correctly.

### Failure 9 — No rollback capability

Changes that cause outages or security problems may be difficult to reverse.

---

## 28. Security+ Exam Focus

Be able to explain:

- What a secure baseline is
- Why baselines are needed
- Configuration drift
- System hardening
- Attack-surface reduction
- Configuration assessment
- Gold images
- Templates
- Infrastructure as Code
- Configuration exceptions
- Configuration management vs. change management
- Emergency changes
- Cloud configuration management
- Container configuration management
- Continuous configuration monitoring
- Why validation is required after changes

Remember:

> **A secure baseline defines the desired state; configuration management keeps the actual environment aligned with that state.**

---

## 29. Common Security+ Distinctions

| Concept | Meaning |
|---|---|
| Secure baseline | Approved reference configuration for a system or system class |
| Hardening | Reducing attack surface by removing or restricting unnecessary functionality |
| Configuration drift | Deviation from the approved configuration |
| Configuration assessment | Comparing actual settings against defined requirements |
| Configuration management | Lifecycle process for establishing, maintaining, monitoring, and controlling configurations |
| Change management | Controlled process for modifying systems or configurations |
| Gold image | Approved standardized system image |
| Template | Reusable definition for deploying standardized infrastructure or systems |
| IaC | Machine-readable infrastructure definitions used for repeatable deployment and management |
| Configuration exception | Authorized deviation from a standard requirement |
| Compensating control | Alternative control that reduces risk when the preferred control cannot be implemented directly |

---

## 30. Configuration Management Decision Framework

For Security+ scenario questions, work through the following sequence:

### Step 1 — Identify the system

Determine which asset and configuration are involved.

### Step 2 — Identify the intended state

Find the approved baseline, policy, standard, or template.

### Step 3 — Compare actual vs. expected

Determine exactly what differs.

### Step 4 — Determine why the difference exists

Was it authorized, accidental, required, temporary, outdated, or suspicious?

### Step 5 — Assess security and business impact

Consider exposure, criticality, availability, dependencies, and risk.

### Step 6 — Select the appropriate action

Possible actions include:

- Approve and document
- Remediate
- Revert
- Create a controlled exception
- Apply a compensating control
- Investigate as a potential security event

### Step 7 — Validate

Confirm that the resulting system matches the intended secure state.

### Step 8 — Document and improve

Update records, baselines, templates, detection rules, or procedures when necessary.

---

## 31. Key Takeaways

- A secure baseline establishes an approved known-good configuration.
- Baselines provide the reference required to identify configuration drift.
- Hardening reduces unnecessary attack surface.
- Secure configuration is different from patching; both are necessary.
- Configuration management controls and monitors the lifecycle of system configurations.
- Configuration assessment identifies deviations from defined requirements.
- Gold images and templates improve standardization but must be maintained.
- IaC enables repeatable infrastructure deployment but can reproduce insecure configurations if the definitions are wrong.
- Configuration exceptions should be documented, approved, risk-assessed, and reviewed.
- Configuration management and change management are complementary processes.
- Emergency changes may require accelerated procedures but should still be documented and reviewed.
- Cloud and container environments require configuration management just as traditional systems do.
- Configuration monitoring helps identify unauthorized, accidental, or unexpected changes.
- A configuration difference is not automatically evidence of malicious activity; context is required.
- Baselines themselves must be reviewed and updated as technology, threats, and business requirements change.
- Validation is essential after configuration changes and remediation.
- The goal is not to prevent all change; the goal is to ensure that change is **controlled, understood, authorized, secure, and verifiable**.

**Core principle:**

> **Define the secure state → deploy it consistently → continuously compare reality with the baseline → investigate deviations → remediate or authorize them → validate the result.**
