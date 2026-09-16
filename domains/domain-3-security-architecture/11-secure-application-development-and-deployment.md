# Secure Application Development and Deployment

Secure application development is the practice of designing, building, testing, deploying, and maintaining software with security requirements integrated throughout its lifecycle. Security is not a single testing activity performed immediately before release. A secure architecture considers threats, trust boundaries, data flows, authentication, authorization, dependencies, secrets, deployment infrastructure, logging, monitoring, and recovery from the beginning.

For Security+, the important idea is to understand **where security belongs in the software lifecycle and which control addresses a particular application-development or deployment risk**.

---

## 1. Secure-by-Design

**Secure-by-design** means security is deliberately incorporated into the architecture and design of a system instead of being treated as an afterthought.

A development team should consider questions such as:

- What data does the application process?
- Who is allowed to access it?
- Which systems does it trust?
- Where are trust boundaries located?
- What happens if a user supplies malicious input?
- What happens if an external dependency becomes compromised?
- How are credentials and secrets protected?
- What security events need to be logged?
- What happens when an authorization check fails?
- How can the application be recovered after compromise?

Security requirements should be established before implementation decisions become difficult or expensive to change.

### Security requirements may include

- Confidentiality
- Integrity
- Availability
- Authentication
- Authorization
- Accountability
- Non-repudiation where required
- Privacy
- Secure logging
- Data retention
- Regulatory requirements
- Cryptographic requirements

---

## 2. Secure Software Development Lifecycle

A **Secure Software Development Lifecycle (SSDLC)** integrates security activities into each stage of software development.

A simplified lifecycle is:

**Requirements → Design → Development → Testing → Deployment → Operations → Maintenance/Retirement**

Security activities should exist throughout this process.

### Requirements

Identify:

- Security requirements
- Data classification
- Compliance requirements
- Authentication requirements
- Authorization requirements
- Availability requirements
- Logging requirements
- Privacy requirements

### Design

Perform:

- Threat modeling
- Architecture review
- Trust-boundary analysis
- Attack-surface analysis
- Secure design review

### Development

Use:

- Secure coding practices
- Input validation
- Output encoding
- Parameterized queries
- Secure APIs
- Proper authentication and authorization
- Secure error handling
- Secrets management

### Testing

Perform security testing such as:

- Static application security testing (SAST)
- Dynamic application security testing (DAST)
- Software composition analysis (SCA)
- Fuzz testing
- Dependency scanning
- Penetration testing where appropriate

### Deployment

Control:

- Build pipelines
- Deployment credentials
- Configuration
- Artifacts
- Infrastructure
- Environment separation

### Operations

Monitor:

- Application logs
- Security events
- Vulnerability findings
- Dependency changes
- Authentication failures
- Authorization failures
- Application behavior

---

## 3. Shift Left Security

**Shift left** means moving security activities earlier in the development lifecycle.

Instead of discovering a serious vulnerability after production deployment, the organization attempts to identify it during requirements, design, coding, or automated testing.

For example:

**Late discovery:** A SQL injection vulnerability is found during a production penetration test.

**Shift-left approach:** Developers use secure query mechanisms and automated security testing during development so the vulnerability is identified earlier.

### Benefits

- Earlier detection
- Lower remediation cost
- Faster feedback
- Reduced production risk
- Greater developer security awareness

Shift left does not mean security testing should stop after development. Security remains necessary throughout operations.

---

## 4. Threat Modeling

**Threat modeling** is a structured process for identifying threats, attack paths, trust boundaries, and security requirements during system design.

A threat-modeling exercise may examine:

- Assets
- Actors
- Entry points
- Trust boundaries
- Data flows
- Dependencies
- Privileged operations
- Potential abuse cases

### Example

Consider a web application:

**Internet user → Web server → Application → Database**

Threat modeling asks:

- Can an unauthenticated user reach administrative functionality?
- Can application input reach the database without validation?
- Is the database directly reachable from the Internet?
- What happens if the application server is compromised?
- Which credentials allow database access?

The result can influence architecture before the software is deployed.

---

## 5. Attack Surface in Applications

An application's **attack surface** consists of the interfaces, components, services, and functionality through which an attacker may interact with or influence the system.

Examples include:

- Web pages
- APIs
- File-upload functionality
- Authentication endpoints
- Administrative interfaces
- Network ports
- Third-party integrations
- Mobile interfaces
- Cloud APIs
- Management interfaces
- Dependencies

Reducing unnecessary attack surface can reduce exposure.

Examples:

- Disable unused services
- Remove unused endpoints
- Restrict administrative interfaces
- Apply least privilege
- Reduce unnecessary dependencies
- Restrict network access

---

## 6. Input Validation

**Input validation** verifies that supplied data conforms to expected rules before the application processes it.

Examples include validating:

- Data type
- Length
- Range
- Format
- Allowed characters
- Expected values

If an application expects an integer representing an account number, accepting arbitrary commands or unexpected structures creates unnecessary risk.

Input validation helps reduce risks associated with malicious or malformed input.

### Important distinction

Validation determines whether input is acceptable.

Encoding determines how output should be safely represented in a particular context.

Both may be required.

---

## 7. Output Encoding

**Output encoding** converts data into a representation that is safe for the context in which it is displayed or interpreted.

It is particularly important for preventing injection into contexts such as:

- HTML
- JavaScript
- URLs
- SQL-related contexts when appropriate mechanisms are used
- Operating-system commands

For example, user-controlled text displayed in a web page should not be interpreted by the browser as executable HTML or JavaScript.

---

## 8. Parameterized Queries

Applications that construct SQL statements by directly concatenating untrusted user input can become vulnerable to SQL injection.

Parameterized queries separate SQL instructions from data values.

Conceptually:

**Unsafe:**

```text
SQL statement + raw user input
```

**Safer approach:**

```text
SQL statement with parameter + separately supplied value
```

The database driver then treats the supplied value as data rather than as part of the SQL command structure.

This is an important example of using a secure design mechanism instead of attempting to solve injection solely through ad-hoc filtering.

---

## 9. Authentication and Authorization

Applications must distinguish between:

**Authentication:** Who are you?

**Authorization:** What are you allowed to do?

A secure application should not assume that successful authentication automatically grants access to every function.

### Authorization controls may include

- Role-based access control (RBAC)
- Attribute-based access control (ABAC)
- Resource-based permissions
- Least privilege
- Separation of duties

Authorization checks should be performed server-side for sensitive operations.

Client-side controls alone should not be trusted because users can potentially manipulate client applications or requests.

---

## 10. Session Security

Web applications often maintain authenticated sessions using cookies, tokens, or other mechanisms.

Security considerations include:

- Secure session identifiers
- Appropriate expiration
- Session invalidation after logout
- Protection against session fixation
- Protection against session theft
- Secure cookie attributes
- Appropriate token validation

Sensitive session information should not be exposed unnecessarily.

---

## 11. Secrets Management

Secrets include:

- Passwords
- API keys
- Access tokens
- Private keys
- Database credentials
- Service credentials

Secrets should not be hard-coded into source code or committed to public repositories.

### Insecure pattern

```text
username = "admin"
password = "SuperSecretPassword"
```

### Better architecture

Applications retrieve secrets from an appropriate secure secrets-management mechanism at runtime.

Security controls can include:

- Secret vaults
- Access policies
- Rotation
- Short-lived credentials
- Encryption
- Audit logging

The application should receive only the secrets it actually requires.

---

## 12. Cryptography in Application Architecture

Applications may require encryption for:

- Data in transit
- Data at rest
- Sensitive application secrets
- Authentication credentials where applicable
- Tokens and sensitive communications

Developers should generally use established cryptographic libraries and protocols rather than creating custom cryptographic algorithms.

Important considerations include:

- Key management
- Certificate validation
- Key rotation
- Algorithm selection
- Secure random number generation
- Protection of private keys

Cryptography is only as strong as its implementation and key-management process.

---

## 13. Dependency Management

Modern applications frequently depend on external:

- Libraries
- Frameworks
- Packages
- Container images
- Operating-system components
- APIs
- Build tools

A vulnerability in a dependency can become a vulnerability in the application.

Organizations should therefore maintain visibility into dependencies and monitor them for vulnerabilities.

Useful practices include:

- Dependency inventories
- Version pinning where appropriate
- Vulnerability scanning
- Patch management
- Software composition analysis
- Reviewing package provenance
- Removing unnecessary dependencies

---

## 14. Software Composition Analysis (SCA)

**Software Composition Analysis (SCA)** identifies and analyzes third-party and open-source components used by an application.

SCA can help identify:

- Known vulnerabilities
- Outdated packages
- License issues
- Dependency relationships
- Transitive dependencies

A transitive dependency is a dependency brought into the application indirectly through another package.

For example:

**Application → Library A → Library B**

Even if the development team explicitly selected Library A, Library B may still become part of the software supply chain.

---

## 15. Static Application Security Testing (SAST)

**SAST** analyzes source code or compiled representations without executing the application in the normal way.

It can identify patterns associated with vulnerabilities such as:

- Unsafe input handling
- Hard-coded secrets
- Insecure API usage
- Certain injection patterns
- Weak coding practices

SAST is useful earlier in the development process because developers can receive feedback while code is being written.

### Limitation

SAST may produce false positives and may not understand all runtime behavior.

It should therefore be combined with other testing techniques.

---

## 16. Dynamic Application Security Testing (DAST)

**DAST** evaluates a running application from an external perspective.

It can identify issues such as:

- Web application vulnerabilities
- Authentication weaknesses
- Session problems
- Input-handling issues
- Configuration problems

DAST more closely resembles interaction with the deployed application.

### SAST vs DAST

| Technique | Main Target | Execution |
|---|---|---|
| SAST | Source/code representation | Generally without normal application execution |
| DAST | Running application | Tests runtime behavior |

They are complementary rather than interchangeable.

---

## 17. Fuzz Testing

**Fuzz testing** supplies unexpected, malformed, random, or unusual input to an application to identify crashes, unexpected behavior, or security weaknesses.

Examples include:

- Oversized input
- Unexpected characters
- Invalid file structures
- Malformed protocol messages
- Randomized values

Fuzzing can be especially useful for parsers, file-processing components, APIs, and protocol implementations.

---

## 18. Code Review

Code review involves examining source code to identify defects, security weaknesses, and violations of development standards.

Review may be:

- Manual
- Automated
- Peer-based
- Security-focused

Reviewers can examine:

- Authentication logic
- Authorization checks
- Input validation
- Error handling
- Secrets
- Cryptography
- Logging
- Dependency usage

Automated analysis improves scale, while human review can identify contextual design problems that tools may miss.

---

## 19. Error Handling

Applications should fail safely.

Error messages should provide developers with useful diagnostic information without unnecessarily exposing sensitive internal details to users.

### Dangerous information disclosure

An error response might reveal:

- Database credentials
- Internal file paths
- Stack traces
- SQL statements
- Server configuration
- Internal hostnames

Production applications should generally avoid exposing unnecessary internal implementation details to untrusted users.

Detailed diagnostic information should be securely logged for authorized personnel.

---

## 20. Logging and Application Security

Applications should generate useful security telemetry.

Events may include:

- Successful authentication
- Failed authentication
- Privilege changes
- Administrative actions
- Authorization failures
- Account changes
- Configuration changes
- Sensitive data access
- Application errors
- Security-control failures

Logs should be:

- Protected from unauthorized modification
- Time synchronized
- Centrally collected where appropriate
- Monitored
- Retained according to requirements

Logging should also avoid unnecessarily recording sensitive information such as plaintext passwords.

---

## 21. Development, Testing, Staging, and Production Environments

Application environments should be appropriately separated.

A common structure is:

**Development → Testing → Staging → Production**

Each environment serves a different purpose.

### Development

Used by developers to build and modify software.

### Testing

Used to validate functionality and security before release.

### Staging

Designed to closely resemble production so release candidates can be validated under realistic conditions.

### Production

The live environment serving actual users or business operations.

---

## 22. Environment Separation

Environment separation reduces the risk that development activity will directly affect production.

Controls can include:

- Separate networks
- Separate accounts
- Separate credentials
- Separate databases
- Access restrictions
- Deployment approvals
- Environment-specific secrets

Production credentials should not be reused casually in development environments.

---

## 23. Test Data and Sensitive Data

Using real production data in development or testing can expose sensitive information.

Where possible, organizations should use:

- Synthetic data
- Masked data
- Anonymized data
- Sanitized test datasets

If production data must be used, appropriate security and privacy controls are required.

---

## 24. Version Control

Version-control systems maintain a history of code changes.

Security benefits include:

- Change tracking
- Accountability
- Code review
- Rollback capability
- Branch management
- Auditability

Access to repositories should be controlled using least privilege and strong authentication.

Sensitive secrets should not be committed to source control.

---

## 25. Branch Protection and Code Integrity

Organizations can protect important branches by requiring controls such as:

- Peer review
- Automated testing
- Security checks
- Approved changes
- Protected branch policies

The objective is to prevent unauthorized or insufficiently reviewed code from reaching critical branches.

---

## 26. Continuous Integration and Continuous Delivery/Deployment

### Continuous Integration (CI)

CI automatically integrates code changes and performs automated validation.

Security checks can include:

- Unit tests
- SAST
- SCA
- Secret scanning
- Dependency scanning
- Configuration checks

### Continuous Delivery

Continuous delivery keeps software in a deployable state, while release to production may require an explicit approval.

### Continuous Deployment

Continuous deployment automatically releases qualifying changes into production according to the configured pipeline.

The exact implementation varies by organization.

---

## 27. CI/CD Pipeline Security

The CI/CD pipeline itself is a high-value target because compromise of the pipeline can result in malicious software being distributed to users.

Protect:

- Source repositories
- Build servers
- Pipeline definitions
- Build credentials
- Signing keys
- Artifact repositories
- Deployment credentials
- Secrets

### Pipeline principle

**Code integrity → Build integrity → Artifact integrity → Deployment integrity**

An attacker who compromises any major stage may be able to influence the final software.

---

## 28. Build Pipeline Threats

Potential threats include:

- Compromised developer account
- Malicious code commit
- Stolen CI credentials
- Malicious dependency
- Compromised build server
- Pipeline configuration modification
- Artifact replacement
- Signing-key compromise

Security controls may include:

- MFA
- Least privilege
- Protected branches
- Peer review
- Secret management
- Isolated build environments
- Dependency verification
- Artifact signing
- Pipeline monitoring

---

## 29. Software Artifacts

A **software artifact** is a generated output of the build process, such as:

- Executable
- Package
- Container image
- Library
- Installer
- Deployment bundle

Artifacts should be protected against unauthorized modification.

An attacker who replaces a legitimate artifact with a malicious one can compromise downstream systems even when the original source code appears legitimate.

---

## 30. Artifact Integrity and Signing

Digital signatures can help verify the integrity and authenticity of software artifacts.

A signing process can provide assurance that:

- The artifact was signed using the expected signing key
- The artifact has not been modified after signing

Signing keys themselves must be strongly protected.

If an attacker obtains the private signing key, they may be able to create apparently legitimate signed artifacts.

Therefore:

**Artifact signing + secure key management** are both required.

---

## 31. Software Bill of Materials (SBOM)

A **Software Bill of Materials (SBOM)** is an inventory describing software components and dependencies contained in a software product.

An SBOM can help organizations:

- Understand dependencies
- Identify affected components during vulnerability disclosures
- Improve supply-chain visibility
- Support software inventory and risk management

For example, if a critical vulnerability is discovered in a commonly used library, an organization with accurate component inventories can determine which applications contain that dependency more efficiently.

---

## 32. Software Supply Chain Security

The software supply chain includes the people, processes, code, dependencies, tools, build systems, and distribution mechanisms involved in producing software.

Supply-chain risks can originate from:

- Compromised dependencies
- Malicious packages
- Compromised repositories
- Build-server compromise
- Stolen signing keys
- Malicious insiders
- Vendor compromise

Security architecture should therefore protect the entire development and deployment chain rather than only the application source code.

---

## 33. Infrastructure as Code (IaC)

**Infrastructure as Code** represents infrastructure configuration in machine-readable definitions.

Examples include definitions for:

- Networks
- Virtual machines
- Cloud resources
- Security groups
- Load balancers
- Storage
- IAM resources

### Security benefits

IaC enables:

- Version control
- Peer review
- Repeatable deployments
- Configuration consistency
- Automated security validation
- Auditability

### Security risk

An insecure IaC template can repeatedly deploy insecure infrastructure.

Therefore IaC should itself undergo security review and testing.

---

## 34. Configuration and Secrets in IaC

Sensitive values should not be embedded directly in infrastructure definitions.

Instead, use secure mechanisms for retrieving secrets at deployment or runtime.

IaC security should check for:

- Public storage
- Excessive IAM permissions
- Open firewall rules
- Unencrypted storage
- Hard-coded secrets
- Insecure network configurations

---

## 35. Containers and Application Deployment

Containers provide application isolation through operating-system-level mechanisms rather than requiring a complete guest operating system for each application.

Security considerations include:

- Trusted base images
- Image scanning
- Minimal images
- Non-root execution
- Resource limits
- Network segmentation
- Secret management
- Registry security
- Runtime monitoring

Container security is part of the application deployment supply chain.

---

## 36. Secure Container Images

Container images should be obtained from trusted sources and scanned for vulnerabilities.

Important practices include:

- Use minimal base images
- Remove unnecessary packages
- Keep dependencies updated
- Scan images before deployment
- Verify image provenance
- Protect registries
- Avoid running unnecessary processes as root

An insecure base image can introduce vulnerabilities into every application built from it.

---

## 37. Serverless Application Security

Serverless architectures move some infrastructure-management responsibilities to the cloud provider, but application security remains necessary.

Security considerations include:

- Function permissions
- API authentication
- Input validation
- Dependency security
- Secrets management
- Logging
- Event-source validation
- Least privilege

A serverless function should receive only the permissions required to perform its task.

---

## 38. API Security

APIs expose programmatic interfaces to applications and services.

Security controls may include:

- Authentication
- Authorization
- TLS
- Input validation
- Rate limiting
- Schema validation
- Logging
- API gateways
- Token validation

APIs should not assume that requests originating from another internal service are automatically trustworthy.

---

## 39. Deployment Strategies

Different deployment strategies can reduce deployment risk.

### Blue-green deployment

Two environments are maintained:

- Blue: current production
- Green: new version

Traffic can be switched to the new environment after validation.

If serious problems occur, traffic can potentially be returned to the previous environment.

### Canary deployment

A new version is released to a small portion of users or infrastructure first.

The organization observes behavior before expanding deployment.

### Rolling deployment

The new version is gradually deployed across systems rather than replacing all instances simultaneously.

These approaches can reduce the blast radius of deployment failures.

---

## 40. Rollback

A rollback returns an application or infrastructure deployment to a previously known state.

Rollback capability is important when a deployment causes:

- Application failure
- Security regression
- Configuration problems
- Compatibility issues
- Performance problems

Rollback should be planned and tested rather than improvised during an incident.

---

## 41. Change Approval and Separation of Duties

Sensitive production changes may require:

- Change requests
- Peer review
- Testing
- Approval
- Scheduled deployment windows
- Audit logging

Separation of duties reduces the possibility that one individual can independently introduce and deploy an unauthorized change without oversight.

---

## 42. Secure Configuration Management

Application deployment should use controlled configuration rather than manual undocumented changes.

Configuration may include:

- Database endpoints
- Authentication settings
- Security headers
- Logging levels
- Network settings
- Feature flags
- API endpoints

Configuration should be versioned, reviewed, and protected from unauthorized modification.

---

## 43. Security Headers and Application Gateway Controls

Web applications can use security-related HTTP headers to influence browser behavior.

Examples include controls associated with:

- Content Security Policy (CSP)
- Strict Transport Security (HSTS)
- Clickjacking protection
- MIME-type handling

A WAF or reverse proxy may also provide additional filtering and policy enforcement at the application boundary.

These controls complement secure application code rather than replacing it.

---

## 44. Secure Deployment Architecture

A typical secure application architecture might look conceptually like:

**Internet → Firewall/Load Balancer → WAF/Reverse Proxy → Web Tier → Application Tier → Database Tier**

Additional controls may include:

- IAM
- Secrets management
- Network segmentation
- Logging
- IDS/IPS
- EDR
- Monitoring

The database should generally not be directly exposed to untrusted networks merely because the application needs database connectivity.

---

## 45. Production Deployment Security

Before production release, organizations should verify:

- Security requirements are satisfied
- Vulnerabilities are reviewed
- Dependencies are approved
- Secrets are protected
- Configurations are secure
- Logging is enabled
- Monitoring is operational
- Access controls are correct
- Backup/recovery exists
- Rollback is possible

Security should be part of the release criteria.

---

## 46. Secure Application Retirement

Security responsibilities continue when an application reaches end of life.

Retirement should address:

- Data retention
- Data destruction
- Credential revocation
- API key revocation
- Certificate revocation where applicable
- DNS records
- Network rules
- Cloud resources
- Repository access
- Backup retention
- Third-party integrations

Simply shutting down the application does not guarantee that all associated access and data have been removed.

---

## 47. DevSecOps

**DevSecOps** integrates development, security, and operations into a collaborative lifecycle.

The objective is not to create a final security gate that blocks developers after everything has been built. Instead, security controls are integrated into development and operational workflows.

A DevSecOps pipeline may include:

**Commit → Build → SAST → SCA → Test → Container Scan → Artifact Signing → Deploy → Monitor**

Security becomes continuous rather than a single phase.

---

## 48. Common Application Security Failures

### Failure 1 — Security added only before production

**Problem:** Vulnerabilities are discovered late.

**Lesson:** Integrate security throughout the lifecycle.

### Failure 2 — Production credentials copied into development

**Problem:** A lower-security environment now has access to production resources.

**Lesson:** Separate credentials and environments.

### Failure 3 — Secrets committed to Git

**Problem:** Credentials may remain in repository history even after deletion from the latest version.

**Lesson:** Use secure secret management and rotate exposed credentials.

### Failure 4 — CI/CD pipeline has excessive privileges

**Problem:** Pipeline compromise can affect production.

**Lesson:** Apply least privilege and separate deployment permissions.

### Failure 5 — Untrusted dependencies

**Problem:** Vulnerabilities or malicious code enter through the software supply chain.

**Lesson:** Use dependency management, SCA, provenance controls, and approved sources.

### Failure 6 — Only client-side authorization

**Problem:** Attackers can potentially bypass client controls by sending requests directly to backend APIs.

**Lesson:** Enforce authorization server-side.

---

## 49. Security+ Scenario Reasoning

### Scenario 1 — Vulnerability should be detected during coding

A company wants to automatically inspect source code for security weaknesses before the application runs.

**Technology:** SAST

Why? SAST analyzes source/code representation without requiring normal runtime execution.

---

### Scenario 2 — Test a running web application

A security team wants to evaluate a deployed web application from an external perspective.

**Technology:** DAST

Why? DAST interacts with the running application.

---

### Scenario 3 — Identify vulnerable open-source packages

A company needs to identify vulnerable third-party libraries and dependencies.

**Technology:** SCA

Why? Software composition analysis focuses on software components and dependencies.

---

### Scenario 4 — Prevent database injection

A developer constructs SQL queries using untrusted user input.

**Security control:** Parameterized queries/prepared statements.

Why? They separate query structure from supplied data.

---

### Scenario 5 — Protect production from development

Developers require access to development infrastructure but should not automatically obtain production credentials.

**Architecture:** Environment separation with separate access controls and credentials.

---

### Scenario 6 — Protect the software pipeline

An attacker compromises a build server and replaces a legitimate application package before deployment.

**Security focus:** Build integrity and artifact integrity.

Controls may include isolated builds, artifact signing, protected repositories, least privilege, and pipeline monitoring.

---

### Scenario 7 — Gradually release a risky application change

A company wants to release a new version to a small percentage of users before deploying it everywhere.

**Deployment strategy:** Canary deployment.

Why? Canary deployment limits the initial blast radius and allows observation before wider release.

---

### Scenario 8 — Maintain the previous production version

An organization wants to switch between two complete environments so it can rapidly return to the previous version if necessary.

**Deployment strategy:** Blue-green deployment.

---

## 50. Common Security+ Exam Traps

### Authentication vs authorization

- Authentication → identity
- Authorization → permissions

### SAST vs DAST

- SAST → analyzes code
- DAST → tests running application

### SCA vs SAST

- SCA → third-party/open-source components and dependencies
- SAST → application code/code representation

### Validation vs encoding

- Validation → determine whether input conforms to requirements
- Encoding → safely represent data for its output context

### Backup vs version control

Version control tracks code changes; it should not automatically be treated as a complete disaster-recovery backup strategy for all application data.

### Blue-green vs canary

- Blue-green → two environments and controlled traffic switching
- Canary → gradual release to a small subset before wider deployment

### CI vs CD

- CI → integrate and validate changes
- Continuous delivery → keep changes deployable, often with controlled release
- Continuous deployment → automatically release qualifying changes

### Secure-by-design vs final security testing

Secure-by-design incorporates security from architecture and requirements onward. Final testing is only one part of the overall process.

---

## 51. Secure Application Architecture Checklist

When reviewing an application architecture, ask:

### Identity

- How are users authenticated?
- How are services authenticated?
- Is MFA used where appropriate?

### Authorization

- Is least privilege enforced?
- Are sensitive actions authorized server-side?
- Are administrative functions restricted?

### Data

- Is sensitive data encrypted appropriately?
- Are keys securely managed?
- Is sensitive data minimized?

### Input and output

- Is input validated?
- Is output encoded appropriately?
- Are injection risks addressed?

### Dependencies

- Are dependencies inventoried?
- Are vulnerable packages identified?
- Are package sources trusted?

### Development

- Is code reviewed?
- Is SAST used?
- Is SCA used?
- Are secrets scanned?

### Deployment

- Are environments separated?
- Are CI/CD pipelines protected?
- Are artifacts verified?
- Is deployment access restricted?

### Operations

- Is security logging enabled?
- Is monitoring available?
- Can the application be rolled back?
- Are backups and recovery procedures available?

---

## 52. Application Security Decision Framework

When solving a Security+ application-security scenario, use this sequence:

**Requirement → Threat → Attack surface → Trust boundary → Secure design → Development control → Testing control → Deployment control → Monitoring → Recovery**

For example:

**Requirement:** Prevent malicious database input.

**Threat:** SQL injection.

**Design/development control:** Parameterized queries and input validation.

**Testing:** SAST/DAST and security testing.

**Operations:** Logging and monitoring for suspicious activity.

This approach is more reliable than memorizing individual technologies without understanding where they apply.

---

## 53. Key Takeaways

1. **Secure application development integrates security throughout the software lifecycle.**
2. **Secure-by-design begins with security requirements and architecture.**
3. **Threat modeling identifies threats, trust boundaries, attack paths, and security requirements before deployment.**
4. **Shift-left security moves security activities earlier in development.**
5. **Input validation verifies that data conforms to expected requirements.**
6. **Output encoding helps prevent data from being interpreted as executable content in the wrong context.**
7. **Parameterized queries are a key defense against SQL injection.**
8. **Authentication establishes identity; authorization determines permissions.**
9. **Secrets should be stored and managed securely rather than hard-coded into applications or repositories.**
10. **SAST analyzes application code; DAST tests a running application.**
11. **SCA analyzes third-party and open-source dependencies.**
12. **Fuzzing tests applications with unexpected or malformed input.**
13. **Development, testing, staging, and production environments should be appropriately separated.**
14. **Production credentials should not be casually reused in lower environments.**
15. **CI/CD pipelines are part of the application's attack surface and supply chain.**
16. **Build and artifact integrity are critical because pipeline compromise can distribute malicious software.**
17. **SBOMs improve visibility into software components and dependencies.**
18. **Infrastructure as Code improves consistency and auditability but can also automate insecure configurations if poorly designed.**
19. **Blue-green deployment maintains two environments and supports controlled traffic switching.**
20. **Canary deployment releases a new version to a limited population before wider deployment.**
21. **Rollback capability helps recover from failed or insecure deployments.**
22. **Container and serverless deployments still require least privilege, dependency security, secrets management, and monitoring.**
23. **Security controls should continue through application operation and retirement.**
24. **DevSecOps integrates security with development and operations rather than treating security as a final gate.**
25. **Application security is strongest when architecture, development, testing, deployment, and operations are treated as one continuous security lifecycle.**
