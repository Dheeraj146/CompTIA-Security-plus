# Asset Management

## 1. What Is Asset Management?

Asset management is the process of identifying, documenting, tracking, classifying, maintaining, and eventually retiring technology assets throughout their lifecycle.

Security teams cannot protect assets they do not know exist. A reliable inventory supports vulnerability management, secure configuration, access control, monitoring, incident response, and recovery.

## 2. Types of Assets

An organization's asset inventory can include:

- Desktops and laptops
- Servers
- Network switches and routers
- Firewalls and wireless access points
- Virtual machines
- Cloud workloads
- Containers
- Mobile devices
- Applications
- Databases
- SaaS services
- IoT devices
- Industrial systems
- Storage systems
- Security appliances
- Accounts and identities
- Data repositories

The inventory should not be limited to physical hardware.

## 3. Asset Inventory

An asset inventory records information needed to identify and manage each asset. Useful attributes include:

- Asset identifier
- Hostname
- IP address or network location
- MAC address where applicable
- Operating system
- Software and versions
- Owner or responsible team
- Business purpose
- Physical or logical location
- Data classification
- Criticality
- Security controls
- Lifecycle status
- Warranty or support status

## 4. Asset Classification

Not every asset has the same security importance. Classification allows organizations to prioritize effort.

For example, a public-facing web server and an employee test workstation may require different levels of monitoring, patching priority, recovery objectives, and access restrictions.

Criticality can be based on:

- Business impact
- Data sensitivity
- Availability requirements
- Regulatory requirements
- Dependency relationships
- Exposure to untrusted networks

## 5. Asset Lifecycle

A typical lifecycle is:

**Planning → Acquisition → Deployment → Operation → Maintenance → Transfer/Retirement → Secure Disposal**

### Planning

Security requirements are identified before acquisition.

### Acquisition

The organization obtains approved hardware, software, cloud services, or other resources.

### Deployment

Assets are securely configured, documented, and placed into service.

### Operation

The asset is monitored, patched, backed up, and maintained.

### Retirement

Assets are removed from production when they are obsolete, replaced, unsupported, or no longer required.

### Secure Disposal

Data must be securely removed before equipment or storage media leaves organizational control. Depending on the medium and sensitivity, appropriate techniques may include secure erasure, cryptographic erasure, or physical destruction.

## 6. Shadow IT

Shadow IT occurs when employees or departments use hardware, applications, cloud services, or other technology without going through approved organizational processes.

Security risks include:

- Unknown attack surface
- Unmanaged accounts
- Missing patches
- Weak configurations
- Unapproved data storage
- Lack of logging
- Unclear ownership
- Regulatory exposure

The correct response is not simply to assume every unauthorized service is malicious. Security teams should identify the technology, understand the business requirement, assess risk, and either bring it under management or formally remove it.

## 7. Asset Discovery

Organizations can discover assets using multiple sources:

- Network discovery
- DHCP records
- DNS records
- Directory services
- Vulnerability scanners
- EDR platforms
- Cloud inventories
- Mobile device management
- Procurement records
- Configuration management databases

No single source is guaranteed to provide complete visibility.

## 8. Hardware and Software Inventories

Hardware inventory answers **what devices exist**. Software inventory answers **what software is installed or running**.

Software inventory is particularly important for vulnerability management because a vulnerability may affect a specific product and version rather than an entire operating system.

## 9. Unsupported and End-of-Life Assets

End-of-life systems no longer receive normal vendor security updates. Such systems create increasing risk because known vulnerabilities may remain permanently unpatched.

Possible responses include:

1. Upgrade or replace the system.
2. Migrate the workload.
3. Isolate the system through segmentation.
4. Restrict access.
5. Apply compensating controls.
6. Monitor closely.
7. Retire the asset when possible.

Compensating controls reduce risk but do not make an unsupported product equivalent to a fully supported one.

## 10. Example Scenario

A vulnerability scanner reports a critical vulnerability affecting a particular web server version. The security team searches the asset inventory to determine which systems run that version, identifies their owners and business criticality, and prioritizes remediation.

Without an accurate software and asset inventory, the organization may not even know which systems are affected.

## 11. Security+ Exam Focus

Understand:

- Why asset inventory is foundational to security
- Hardware versus software inventory
- Asset ownership and accountability
- Asset criticality
- Asset lifecycle management
- Shadow IT
- End-of-life and unsupported systems
- Secure disposal
- Why unknown assets represent security risk

## 12. Key Takeaways

- Asset management provides visibility into the environment.
- Inventory should include physical, virtual, cloud, software, and specialized assets.
- Asset owners should be identifiable.
- Critical assets deserve appropriately prioritized protection.
- Shadow IT expands attack surface outside normal security controls.
- Retirement and disposal are security activities, not merely administrative tasks.
