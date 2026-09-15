# Secure Baselines and Configuration Management

## 1. What Is a Secure Baseline?

A secure baseline is an approved minimum configuration that defines how a system should be configured to meet the organization's security requirements.

Instead of allowing every administrator to configure systems differently, an organization establishes a known-good state. Systems can then be compared against that state to identify configuration drift.

Examples of baseline requirements include:

- Disable unnecessary services
- Remove or disable unnecessary accounts
- Enforce strong authentication
- Apply approved password and lockout policies
- Enable appropriate logging
- Configure host firewalls
- Restrict administrative access
- Apply approved encryption settings
- Remove unnecessary software
- Configure secure network protocols
- Apply required security updates

## 2. Why Baselines Matter

A baseline provides a reference point for secure configuration. Without one, an organization may know that two servers are different without knowing which configuration is correct.

Baselines improve:

- Consistency
- Security
- Troubleshooting
- Auditability
- Compliance
- Incident investigation
- Change detection

## 3. Configuration Drift

Configuration drift occurs when a system gradually moves away from its approved baseline.

Drift can happen because of:

- Manual administrator changes
- Emergency troubleshooting
- Software installation
- Application updates
- Temporary firewall rules
- Unauthorized modifications
- Misconfiguration
- Changes that were never documented

Regular assessment is required because a system that was secure when deployed may become insecure later.

## 4. Configuration Management

Configuration management is the controlled process of establishing, maintaining, documenting, and reviewing system configurations.

A simplified lifecycle is:

**Define baseline → Deploy → Monitor → Detect deviation → Assess change → Approve/remediate → Validate → Document**

The goal is not to prevent every change. Organizations must be able to change systems safely while maintaining security and accountability.

## 5. Hardening

Hardening reduces the attack surface by removing or restricting unnecessary functionality.

Common hardening actions include:

- Disable unused ports and services
- Remove unnecessary applications
- Restrict administrative interfaces
- Enforce secure protocols
- Apply patches
- Configure endpoint protection
- Restrict permissions
- Enable logging
- Remove default accounts or change default credentials
- Apply secure configuration templates

Hardening should be appropriate to the system's function. Disabling a service without understanding its dependencies can cause an outage.

## 6. Configuration Assessment

Security teams can compare systems against approved configurations using configuration assessment tools, vulnerability scanners, endpoint management platforms, policy enforcement tools, and automated compliance checks.

Assessment may identify:

- Missing security settings
- Unauthorized software
- Weak permissions
- Insecure services
- Disabled security controls
- Unexpected configuration changes

## 7. Change Management

Security operations must coordinate with change management. A change should generally have a documented reason, appropriate authorization, testing where feasible, implementation steps, rollback procedures, and validation.

### Emergency Changes

Security incidents may require immediate changes, such as blocking a malicious IP address or disabling a compromised account. Emergency procedures allow rapid action while still requiring documentation and subsequent review.

## 8. Gold Images and Templates

A gold image is an approved system image containing the organization's desired operating system and configuration. Templates serve a similar purpose for virtual machines and cloud environments.

They improve consistency and reduce manual configuration errors.

However, an image can become outdated. Gold images must therefore be maintained and updated rather than treated as permanently secure.

## 9. Infrastructure as Code

Infrastructure as Code (IaC) represents infrastructure configuration in machine-readable definitions. This enables repeatable deployment, version control, review, testing, and automated enforcement.

Security benefits include:

- Consistent deployments
- Reduced manual error
- Auditable changes
- Repeatability
- Easier rollback
- Security checks before deployment

IaC does not automatically mean secure infrastructure. Insecure definitions can reproduce insecure configurations at scale.

## 10. Example Scenario

An administrator manually enables a remote management service for troubleshooting and forgets to disable it afterward. The service remains exposed after the maintenance activity.

A configuration monitoring system detects that the server no longer matches its approved baseline. Security operations investigates the deviation, determines whether the change was authorized, removes the unnecessary exposure, and documents the event.

## 11. Security+ Exam Focus

Know the relationships between:

- Baseline and configuration drift
- Hardening and attack-surface reduction
- Configuration management and change management
- Gold images and standardization
- IaC and repeatable deployments
- Secure configuration and vulnerability management

Remember that **a vulnerability is not always caused by missing software patches; insecure configuration can itself create a vulnerability**.

## 12. Key Takeaways

- A secure baseline defines an approved known-good configuration.
- Configuration drift creates security and operational risk.
- Hardening reduces unnecessary attack surface.
- Changes should be controlled, tested when practical, authorized, and documented.
- Standard images and templates improve consistency.
- Automated configuration management can detect and reduce drift.
- Security configurations must be continuously reviewed rather than assumed to remain secure forever.
