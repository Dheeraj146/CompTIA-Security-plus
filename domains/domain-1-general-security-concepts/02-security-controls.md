# 2. Security Controls

Security controls are safeguards implemented to reduce security risk. A control can prevent an unwanted event, detect it, correct its effects, discourage an attacker, compensate for another weakness, or direct people toward expected behavior.

## 2.1 Why Security Controls Exist

Organizations have finite budgets, personnel, and technical resources. Security controls are therefore selected according to risk. A control should address a meaningful threat or vulnerability and provide an appropriate reduction in risk without creating unacceptable operational problems.

A control can protect confidentiality, integrity, availability, accountability, privacy, or several objectives simultaneously.

For example, MFA primarily strengthens authentication and reduces account-compromise risk. Network segmentation limits lateral movement. Backups support availability and recovery. Audit logging supports accountability and investigation.

## 2.2 Control Categories

Security+ distinguishes broad categories describing where a control is implemented.

### Technical Controls

Technical controls are implemented through technology.

Examples:

- Firewalls
- Intrusion detection and prevention systems
- Encryption
- MFA systems
- Endpoint detection and response
- Access-control mechanisms
- Network segmentation
- Security monitoring platforms

Technical controls can operate automatically and consistently, although they still depend on correct configuration and maintenance.

### Managerial Controls

Managerial controls are controls based on management decisions, risk management, and organizational direction.

Examples include:

- Risk assessments
- Security policies
- Security governance
- Vendor risk assessments
- Security strategy
- Risk acceptance decisions

They establish the organization's security direction rather than directly filtering packets or scanning files.

### Operational Controls

Operational controls are implemented primarily through people and processes.

Examples include:

- Security awareness training
- Incident response procedures
- Personnel security
- Change-management processes
- Backup procedures
- User onboarding and offboarding
- Security guard operations

Operational controls frequently depend on consistent execution by personnel.

### Physical Controls

Physical controls protect facilities, hardware, and physical access.

Examples include:

- Locks
- Fences
- Security guards
- CCTV
- Mantraps
- Badge readers
- Lighting
- Bollards
- Fire suppression systems

Physical security is part of cybersecurity because an attacker who gains physical access may bypass logical controls or directly manipulate systems.

## 2.3 Control Types

Control types describe the purpose or function of a control.

### Preventive Controls

Preventive controls are designed to stop an unwanted event before it occurs.

Examples:

- Firewall rules blocking unauthorized traffic.
- MFA preventing password-only access.
- File permissions preventing unauthorized modification.
- Door locks preventing unauthorized physical entry.

### Deterrent Controls

Deterrent controls discourage an actor from attempting an unwanted action by increasing perceived risk or consequences.

Examples include warning banners, visible security cameras, security guards, and legal notices. A deterrent does not necessarily prevent an action technically; instead, it is intended to influence behavior.

### Detective Controls

Detective controls identify or record an event after it occurs or while it is occurring.

Examples:

- IDS alerts
- SIEM detections
- CCTV monitoring
- File-integrity monitoring
- Security audit logs

Detection does not necessarily stop the activity. It provides visibility so that defenders can investigate and respond.

### Corrective Controls

Corrective controls reduce the effects of an incident or restore a system after a security event.

Examples include malware removal, restoring a compromised system, patching a vulnerability after discovery, and recovering systems from a known-good backup.

### Compensating Controls

A compensating control provides an alternative safeguard when the preferred control cannot be implemented or does not fully address a requirement.

For example, if an old system cannot support a required authentication mechanism, the organization might isolate it on a restricted network, add stronger monitoring, and limit administrative access. These controls do not make the old system equivalent to a modern system automatically; they reduce the associated risk through additional safeguards.

### Directive Controls

Directive controls tell users or personnel what they are expected or required to do.

Examples include security policies, procedures, standards, acceptable-use requirements, and mandatory security training.

## 2.4 Controls Can Have Multiple Characteristics

A single control can belong to more than one conceptual category. For example, a firewall is a technical control and may perform preventive functions. A SIEM is a technical control and generally performs detective functions. A security policy is managerial or administrative in nature and can be directive.

The important distinction is whether the question asks about **where/how the control is implemented** or **what the control is intended to accomplish**.

## 2.5 Control Selection

Control selection should consider:

- Asset value
- Threat likelihood
- Potential impact
- Vulnerability severity
- Regulatory requirements
- Business requirements
- Implementation cost
- Operational impact
- Existing controls
- Recovery requirements

Security teams should avoid selecting controls solely because they are popular or technically impressive. The correct control is the one that addresses the organization's actual risk and requirements.

## 2.6 Example: Protecting a Critical Database

Suppose an organization operates a database containing customer information.

A layered control strategy could include:

1. **Preventive technical:** firewall rules restrict network access.
2. **Preventive technical:** database permissions enforce least privilege.
3. **Preventive technical:** encryption protects stored data.
4. **Detective technical:** database activity is logged and forwarded to a SIEM.
5. **Operational:** administrators follow change-management procedures.
6. **Managerial:** policy defines acceptable access and retention requirements.
7. **Physical:** server-room access is restricted using badge controls.
8. **Corrective:** backups allow recovery after corruption or ransomware.

This demonstrates how multiple control categories and control types work together.

## Security+ Exam Focus

Be able to distinguish:

- Technical vs managerial vs operational vs physical.
- Preventive vs deterrent vs detective vs corrective vs compensating vs directive.
- A control's implementation category from its functional purpose.

When analyzing a scenario, identify what the control actually does rather than relying only on the technology name.

## Key Takeaways

- Controls reduce risk; they do not eliminate risk completely.
- Technical controls use technology.
- Managerial controls establish direction and risk decisions.
- Operational controls depend on processes and people.
- Physical controls protect physical environments and assets.
- Preventive controls try to stop incidents.
- Detective controls provide visibility.
- Corrective controls restore or remediate.
- Deterrent controls discourage behavior.
- Compensating controls provide alternative risk reduction.
- Directive controls establish expected behavior.
