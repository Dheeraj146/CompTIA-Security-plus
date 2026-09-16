# 07 — Application and Web Attacks

## 1. Introduction

**Application and web attacks** exploit weaknesses in software, application architecture, input handling, authentication, authorization, session management, memory handling, business logic, APIs, or third-party components.

Modern applications are rarely isolated programs. A typical web application may contain:

- Browser-based clients
- Web servers
- Application servers
- Databases
- APIs
- Authentication services
- Cloud services
- External integrations
- Third-party libraries
- Containerized components

A weakness in any of these layers can affect the overall security of the application.

A useful model is:

**User input → Application processing → Authentication/authorization → Business logic → Backend resource → Response**

Security+ questions often describe something happening at one point in this chain and ask you to identify the underlying vulnerability or the appropriate mitigation.

---

# 2. Trusting User Input

One of the most important principles in application security is:

> **Treat external input as untrusted until it has been safely processed.**

External input can come from:

- Form fields
- URL parameters
- HTTP headers
- Cookies
- API requests
- Uploaded files
- JSON/XML data
- Mobile applications
- Other services

The application must not assume that data supplied by a client is safe merely because the user interface normally restricts it.

### Client-side vs server-side validation

Client-side validation improves usability but cannot be treated as a security boundary because an attacker can send requests without using the normal interface.

Security-sensitive validation must therefore occur **server-side**.

---

# 3. SQL Injection

**SQL injection (SQLi)** occurs when untrusted input is incorporated into a database query in an unsafe way, allowing an attacker to alter the intended meaning of the query.

### Basic concept

Imagine an application constructs a database query using user-supplied input.

The application intends:

**User input → search for one record → return result**

If the input is inserted into the query structure unsafely, an attacker may cause the database to interpret part of the input as SQL syntax rather than ordinary data.

### Potential impact

Depending on the application and database configuration, SQL injection can lead to:

- Unauthorized data disclosure
- Data modification
- Data deletion
- Authentication bypass
- Administrative database actions

### Primary mitigation

**Parameterized queries / prepared statements** separate data from SQL instructions.

Other controls include:

- Secure database access libraries
- Server-side input validation
- Least-privileged database accounts
- Safe error handling
- Secure coding practices

### Important exam clue

If attacker-controlled input changes the meaning of a **database query**, think **SQL injection**.

---

# 4. SQL Injection Example Concept

Suppose a login application asks for:

- Username
- Password

The server constructs a database query from these values.

The security problem is not simply that the user can type arbitrary characters. The critical issue is that the application treats untrusted input as part of the **SQL command structure**.

A secure application instead uses a parameterized query so that the supplied username and password remain data rather than becoming executable SQL syntax.

### Security principle

**Do not attempt to make SQL injection safe by relying only on character filtering.**

The preferred design is to keep application data and database commands structurally separate.

---

# 5. Cross-Site Scripting (XSS)

**Cross-Site Scripting (XSS)** occurs when attacker-controlled script content executes in a victim's browser within the security context of a vulnerable web application.

XSS primarily targets the **client-side/browser execution environment**.

Potential consequences include:

- Reading accessible page data
- Performing actions as the victim
- Manipulating displayed content
- Stealing information accessible to scripts
- Session compromise in vulnerable designs
- Phishing within a trusted website context

The exact impact depends on browser protections, application design, cookie attributes, and what the victim can access.

---

# 6. Stored XSS

**Stored XSS** occurs when malicious content is stored by the application and later delivered to users.

Examples of storage locations can include:

- Database records
- Comments
- User profiles
- Forum posts
- Messages

### Simplified flow

**Attacker submits content → Application stores content → Victim views affected page → Browser executes unsafe content**

Because the malicious content is stored, multiple users may be affected.

### Exam clue

If the malicious script is **stored by the application and later served**, think **stored XSS**.

---

# 7. Reflected XSS

**Reflected XSS** occurs when malicious input is immediately returned in an application's response and executed by the victim's browser.

### Simplified flow

**Attacker-controlled request → Vulnerable application response → Victim's browser processes response**

The malicious content is generally not permanently stored by the application.

### Exam clue

If the malicious input is **reflected immediately in the response**, think **reflected XSS**.

---

# 8. XSS Mitigation

Common defensive controls include:

- Context-appropriate output encoding
- Safe handling of user-generated content
- Content Security Policy (CSP)
- Secure cookie attributes
- Server-side input handling
- Framework security controls

### Output encoding

Output encoding ensures that data intended to be displayed as text is not interpreted as executable markup or script in the relevant context.

### Content Security Policy

A properly designed **Content Security Policy** can restrict where scripts and other resources may be loaded from and can reduce the impact of some XSS vulnerabilities.

CSP is a defense-in-depth control, not a substitute for fixing unsafe application code.

---

# 9. Cross-Site Request Forgery (CSRF)

**Cross-Site Request Forgery (CSRF)** causes a user's browser to send an unwanted request to a website where the user is already authenticated.

The key idea is that the browser may automatically include authentication information associated with the target site.

### Example concept

A user is logged into an online service. The user visits another malicious page. That page causes the browser to send a request to the authenticated service.

If the target application does not properly verify that the request was intentionally initiated by the user, an unwanted action may occur.

### Potential impact

- Changing account settings
- Performing transactions
- Modifying data
- Changing email addresses
- Other state-changing actions

### Mitigations

- Anti-CSRF tokens
- SameSite cookie settings
- Origin/Referer validation where appropriate
- Reauthentication for sensitive operations

### XSS vs CSRF

**XSS:** attacker-controlled script executes in the victim's browser.

**CSRF:** victim's authenticated browser is tricked into making an unwanted request.

---

# 10. Command Injection

**Command injection** occurs when untrusted input reaches an operating-system command interpreter and changes the intended command execution.

### Example concept

An application legitimately needs to invoke a system utility. If user-controlled input is concatenated into a shell command without safe handling, an attacker may cause additional unintended commands or arguments to be interpreted.

### Potential impact

Depending on application privileges, command injection can result in:

- Unauthorized system commands
- Data access
- File manipulation
- Malware execution
- Privilege escalation through subsequent activity

### Mitigation

- Avoid shell invocation when a safe API exists
- Use parameterized process APIs
- Strictly validate input
- Use allowlists for expected values
- Run services with least privilege

### SQL injection vs command injection

**SQL injection → database command/query**

**Command injection → operating-system command interpreter**

---

# 11. Path Traversal

**Path traversal** occurs when an attacker manipulates a file path so that an application accesses a file outside its intended directory.

The vulnerability commonly occurs when an application constructs file paths from untrusted input without safely resolving and restricting the final path.

### Potential impact

- Reading sensitive files
- Accessing configuration files
- Exposing credentials or secrets
- Modifying files in vulnerable applications

### Mitigation

- Use safe file APIs
- Canonicalize paths correctly
- Enforce an approved base directory
- Use allowlists where practical
- Apply filesystem permissions
- Avoid constructing filesystem paths directly from untrusted input

### Exam clue

If the scenario involves manipulating a filename/path to access **outside the intended directory**, think **path traversal**.

---

# 12. File Inclusion

**File inclusion** vulnerabilities occur when an application dynamically loads files based on attacker-influenced input.

Two terms are commonly encountered:

### Local File Inclusion (LFI)

The attacker attempts to cause the application to include a file located on the local system.

### Remote File Inclusion (RFI)

The application may be tricked into loading content from a remote location when its architecture and configuration permit this behavior.

### Mitigation

- Strict allowlists
- Fixed resource mappings
- Safe application architecture
- Avoid directly using user input as a file/resource selector
- Appropriate filesystem permissions

---

# 13. Server-Side Request Forgery (SSRF)

**Server-Side Request Forgery (SSRF)** occurs when an attacker causes a server to make a network request to a destination chosen or influenced by the attacker.

The important distinction is that the **server** makes the request.

### Why SSRF is dangerous

A server may have network access that the attacker does not have directly.

For example, an application may be able to access:

- Internal services
- Management interfaces
- Private network addresses
- Cloud metadata services
- Internal APIs

The attacker can potentially abuse the server as a proxy into these locations.

### Potential impact

- Internal service discovery
- Access to sensitive internal resources
- Cloud metadata exposure
- Credential or token exposure
- Network pivoting

### Mitigation

- Restrict outbound server requests
- Validate and allowlist destinations
- Block access to unnecessary internal address ranges
- Segment sensitive services
- Protect cloud metadata services
- Revalidate redirects and resolved destinations where appropriate

### Exam clue

**Attacker controls/influences a request, but the server sends it → SSRF.**

---

# 14. Insecure Deserialization

**Serialization** converts an object or structured data into a representation that can be stored or transmitted.

**Deserialization** converts that representation back into an object or data structure.

**Insecure deserialization** occurs when an application processes untrusted serialized data in a way that allows unintended object creation, manipulation, or potentially code execution.

### Why it is dangerous

Some serialization mechanisms contain instructions or object metadata that influence how data is reconstructed.

If an application trusts attacker-controlled serialized data, an attacker may abuse the deserialization process.

### Mitigation

- Avoid unsafe native object deserialization
- Prefer safer data formats where appropriate
- Authenticate serialized data where needed
- Validate expected structure and types
- Restrict classes/types that can be reconstructed
- Keep frameworks and libraries patched

---

# 15. Buffer Overflow

A **buffer overflow** occurs when software writes more data into a memory buffer than the buffer was designed to hold.

The excess data may overwrite adjacent memory.

### Potential consequences

Depending on the vulnerability and platform, a buffer overflow may cause:

- Application crashes
- Data corruption
- Memory corruption
- Unexpected program behavior
- Potential code execution

### Defensive controls

- Memory-safe programming languages where appropriate
- Bounds checking
- Compiler protections
- Address Space Layout Randomization (ASLR)
- Data Execution Prevention (DEP) / non-executable memory protections
- Secure coding
- Patch management

### Important concept

A buffer overflow is a **memory-management vulnerability**, not a specific malware type.

---

# 16. Race Conditions

A **race condition** occurs when the security or correctness of a program depends on the timing or ordering of concurrent operations.

A common example is **Time-of-Check to Time-of-Use (TOCTOU)**.

### TOCTOU concept

An application may:

1. Check whether a resource is safe.
2. Assume the resource remains unchanged.
3. Use the resource.

If another process changes the resource between the check and the use, the security assumption can become invalid.

### Mitigation

- Atomic operations
- Proper locking
- Transaction design
- Avoiding unsafe check-then-use patterns
- Synchronization mechanisms

### Exam clue

If the vulnerability depends on **timing or concurrent actions**, consider a race condition.

---

# 17. API Attacks

Modern applications commonly expose **APIs (Application Programming Interfaces)** to mobile applications, web frontends, integrations, and other services.

An API can expose vulnerabilities when it has weaknesses in:

- Authentication
- Authorization
- Input validation
- Rate limiting
- Object-level access control
- Function-level access control
- Data exposure
- Token handling
- Error handling

### Broken authorization example

A user is authorized to view their own record. The application accepts an object identifier supplied by the client but fails to verify that the authenticated user is authorized to access that particular object.

The problem is not necessarily authentication. The user is authenticated. The problem is **authorization**.

### API defenses

- Strong authentication
- Server-side authorization
- Object-level access checks
- Function-level access checks
- Input validation
- Rate limiting
- Secure token handling
- Logging and monitoring
- Minimize returned data

---

# 18. Authentication vs Authorization in Application Security

These concepts are frequently confused.

### Authentication

**Who are you?**

It verifies identity.

### Authorization

**What are you allowed to do?**

It determines permitted actions or resources.

### Example

A user successfully logs into an application. Authentication has succeeded.

If the application then allows that user to access another customer's records, the problem is an **authorization failure**.

Security controls must therefore enforce authorization on the server rather than trusting identifiers or permissions supplied by the client.

---

# 19. Business Logic Vulnerabilities

A **business logic vulnerability** occurs when an application correctly executes its programmed rules but those rules allow an attacker to manipulate the intended business process.

Examples conceptually include:

- Performing an action in an unintended sequence
- Bypassing a required approval step
- Repeating a transaction that should occur once
- Manipulating quantities or prices
- Abusing refund workflows
- Circumventing process restrictions

These vulnerabilities can be difficult to detect because the requests may look technically valid.

### Defense

Security testing should evaluate not only technical input validation but also whether the **business workflow itself can be abused**.

---

# 20. Session Attacks

Web applications commonly maintain sessions so users do not need to authenticate on every request.

Session-related weaknesses can include:

- Predictable session identifiers
- Session fixation
- Session theft
- Insecure cookie configuration
- Failure to invalidate sessions
- Excessively long session lifetimes

### Defensive controls

- TLS
- Secure and HttpOnly cookies where appropriate
- SameSite cookie settings
- Strong unpredictable session identifiers
- Session expiration
- Session invalidation after logout
- Reauthentication for sensitive operations

---

# 21. Session Fixation

**Session fixation** occurs when an attacker causes a victim to use a session identifier known to the attacker and then benefits after the victim authenticates.

The key issue is that the application's session identifier is not properly regenerated after authentication.

### Mitigation

Regenerate the session identifier when authentication state changes and invalidate inappropriate prior sessions.

### Distinction

**Session fixation:** attacker influences or knows the session identifier before authentication.

**Session hijacking:** attacker obtains or takes control of a valid session.

---

# 22. Directory and Information Exposure

Applications can unintentionally expose information through:

- Directory listings
- Debug pages
- Verbose error messages
- Source maps
- Backup files
- Configuration files
- Metadata
- Stack traces

This information can help attackers understand the application and identify further weaknesses.

### Defense

- Disable unnecessary directory listing
- Use safe error messages
- Remove development artifacts from production
- Protect configuration and secret files
- Minimize information disclosure

---

# 23. Error Handling and Information Disclosure

Detailed errors can be useful during development but dangerous in production.

A production application should avoid exposing unnecessary information such as:

- Database details
- Internal file paths
- Stack traces
- Framework versions
- Internal hostnames
- Credentials or secrets

### Security principle

Return enough information for legitimate users and administrators to understand the problem without unnecessarily revealing internal implementation details to an attacker.

---

# 24. Dependency and Supply-Chain Risk

Applications depend on third-party components such as:

- Libraries
- Frameworks
- Packages
- Container images
- Build tools
- Plugins
- Software development kits

A vulnerability in a dependency can introduce risk even when the organization's own application code is written securely.

A malicious dependency can also introduce intentional malicious behavior.

### Defensive controls

- Software inventory
- Dependency scanning
- Version tracking
- Vulnerability monitoring
- Trusted package sources
- Software composition analysis
- Controlled update processes
- Software Bill of Materials (SBOM) where appropriate

---

# 25. Input Validation vs Output Encoding

These controls solve different problems.

### Input validation

Determines whether incoming data conforms to expected rules.

Example:

A field expecting an integer should reject values that do not match the application's expected format.

### Output encoding

Ensures data is represented safely when placed into a particular output context, such as HTML.

### Important principle

Neither should automatically be treated as a universal replacement for the other.

Security architecture often uses multiple layers of validation, encoding, parameterization, and access control.

---

# 26. Secure Application Design Principles

Application security should be built into the architecture rather than added only after development.

Important principles include:

### Least privilege

Applications, service accounts, and database accounts should receive only the permissions they require.

### Defense in depth

Use multiple controls so that failure of one layer does not automatically result in compromise.

### Secure defaults

Applications should start in a secure configuration rather than requiring administrators to discover and disable unsafe options.

### Fail securely

When an error occurs, the application should not accidentally grant access or expose sensitive information.

### Server-side enforcement

Security decisions must be enforced by trusted server-side components rather than relying on the client.

### Minimize attack surface

Remove unnecessary endpoints, features, services, permissions, and dependencies.

---

# 27. Application Attack Detection

Application attacks can be detected through multiple telemetry sources.

### Web server logs

Look for:

- Unusual requests
- Repeated errors
- Suspicious parameters
- Unexpected HTTP methods
- Abnormal request rates

### Application logs

Look for:

- Authentication failures
- Authorization failures
- Unexpected application errors
- Abnormal transactions
- Suspicious object access

### Database logs

Look for:

- Unexpected queries
- Privilege changes
- Unusual data access
- Large exports

### Network telemetry

Look for:

- Unexpected outbound connections
- Abnormal request patterns
- Connections to unusual destinations

Detection is stronger when these sources are correlated.

---

# 28. Application Attack Mitigation Matrix

| Vulnerability/Attack | Primary mitigation |
|---|---|
| SQL injection | Parameterized queries/prepared statements |
| XSS | Context-appropriate output encoding and secure application design |
| CSRF | Anti-CSRF tokens and appropriate cookie/origin controls |
| Command injection | Safe APIs; avoid shell execution with untrusted input |
| Path traversal | Safe path handling, canonicalization, allowlists |
| File inclusion | Strict resource allowlists and safe design |
| SSRF | Destination allowlisting and outbound network restrictions |
| Insecure deserialization | Avoid unsafe deserialization and validate data |
| Buffer overflow | Memory-safe design, bounds checking, compiler/runtime protections |
| Race condition | Atomic operations, locking, synchronization |
| API authorization flaws | Server-side object/function authorization |
| Session fixation | Regenerate session IDs after authentication |
| Information disclosure | Safe error handling and removal of unnecessary exposed data |
| Dependency vulnerabilities | Dependency inventory, scanning, patching |

---

# 29. Detailed Security+ Scenario — SQL Injection

### Scenario

A web application's search function accepts a product identifier. The development team reports that attackers have been able to alter database queries by manipulating the identifier.

### Analysis

The defining clue is that attacker-controlled input is changing the behavior of a **database query**.

This is **SQL injection**.

### Primary mitigation

Use **parameterized queries/prepared statements**.

Additional defense should include a least-privileged database account and safe error handling.

---

# 30. Detailed Security+ Scenario — XSS

### Scenario

An online forum stores user comments. When another user views a page containing a malicious comment, browser-executed script runs in the context of the forum.

### Analysis

The content is stored and later delivered to another user's browser.

This is **stored XSS**.

### Primary defenses

- Context-appropriate output encoding
- Safe handling of user-generated content
- CSP as defense in depth
- Secure cookie configuration

---

# 31. Detailed Security+ Scenario — CSRF

### Scenario

A user is authenticated to an online banking application. The user visits an unrelated malicious website, which causes the browser to send a state-changing request to the banking application.

### Analysis

The attacker is abusing the victim's authenticated browser session to cause an unwanted request.

This is **CSRF**.

### Defenses

- Anti-CSRF tokens
- SameSite cookies
- Appropriate origin validation
- Reauthentication for sensitive actions

---

# 32. Detailed Security+ Scenario — SSRF

### Scenario

A public web application contains a feature that retrieves a URL supplied by the user. An attacker manipulates the URL so that the application requests an internal service that is not directly accessible from the internet.

### Analysis

The key clue is that the **server is being induced to make the request**.

This is **SSRF**.

### Defenses

- Destination allowlisting
- Outbound network restrictions
- Network segmentation
- Protection of internal management services
- Cloud metadata protection

---

# 33. Detailed Security+ Scenario — API Authorization

### Scenario

A user is authenticated to an application. By changing an object identifier in an API request, the user can access another customer's record.

### Analysis

Authentication succeeded. The application failed to verify whether the authenticated user was authorized to access the requested object.

The primary issue is **broken authorization / insecure direct object access behavior**.

### Defense

The server must perform an authorization check for every protected object rather than trusting the identifier supplied by the client.

---

# 34. Common Exam Traps

### Trap 1: SQL injection vs command injection

Ask where the malicious input is interpreted:

- Database → SQL injection
- OS command interpreter → command injection

### Trap 2: XSS vs CSRF

- XSS → attacker-controlled script executes in the browser.
- CSRF → authenticated browser is tricked into making an unwanted request.

### Trap 3: Stored vs reflected XSS

- Stored → application saves malicious content.
- Reflected → malicious input is returned in the immediate response.

### Trap 4: SSRF vs CSRF

- SSRF → server makes the attacker-influenced request.
- CSRF → victim's browser makes the unwanted request.

### Trap 5: Authentication vs authorization

A user can be successfully authenticated and still be unauthorized to access a particular resource.

### Trap 6: Input validation as the only SQLi defense

Parameterized queries are the primary control for preventing SQL injection. Input validation is useful defense in depth but should not replace safe query construction.

### Trap 7: Client-side security controls

Client-side validation and restrictions can be bypassed. Security decisions must be enforced server-side.

### Trap 8: Patching everything as the answer

Patching is important, but the question may ask for a control that directly addresses the vulnerability mechanism.

---

# 35. Security+ Scenario Reasoning Framework

When a Security+ question describes an application attack, work through the following process.

### Step 1: Identify where the input goes

Does it reach:

- Database?
- Browser?
- OS command interpreter?
- Filesystem?
- Network request function?
- Deserialization process?
- Memory buffer?

### Step 2: Identify what the attacker controls

Is the attacker controlling:

- Input
- File path
- Object identifier
- URL
- Serialized object
- Session token
- API request

### Step 3: Identify who makes the dangerous action

- Browser executes script → XSS
- Browser sends unwanted authenticated request → CSRF
- Server makes attacker-influenced request → SSRF
- Database interprets input as query syntax → SQL injection
- OS command interpreter processes attacker-controlled input → command injection

### Step 4: Identify the security property affected

Consider:

- Confidentiality
- Integrity
- Availability
- Authentication
- Authorization

### Step 5: Select the mitigation closest to the root cause

Examples:

**SQL injection → parameterized queries**

**XSS → output encoding**

**CSRF → anti-CSRF controls**

**SSRF → destination restrictions/outbound filtering**

**Path traversal → safe path handling and allowlisting**

**Buffer overflow → bounds checking and memory-safety protections**

---

# 36. Key Takeaways

1. Application attacks exploit weaknesses in code, architecture, input processing, authentication, authorization, sessions, memory, or dependencies.
2. External input should be treated as untrusted.
3. SQL injection targets unsafe database query construction.
4. Parameterized queries are a primary SQL injection defense.
5. XSS causes attacker-controlled script content to execute in a victim's browser.
6. Stored XSS is persisted by the application; reflected XSS is returned through the immediate response.
7. CSRF abuses an authenticated browser session to cause an unwanted action.
8. Command injection reaches an operating-system command interpreter.
9. Path traversal manipulates file paths to access outside the intended directory.
10. File inclusion occurs when attacker-influenced input controls which files/resources an application loads.
11. SSRF causes the server to make an attacker-influenced network request.
12. Insecure deserialization can cause unsafe object reconstruction and potentially more severe consequences.
13. Buffer overflows are memory-management vulnerabilities.
14. Race conditions depend on timing or ordering of concurrent operations.
15. APIs require strong authentication, authorization, input validation, rate limiting, and careful data exposure controls.
16. Authentication answers **who are you?** while authorization answers **what are you allowed to access or do?**
17. Business logic vulnerabilities abuse valid application workflows in unintended ways.
18. Secure session management is essential for protecting authenticated users.
19. Third-party dependencies are part of the application's attack surface.
20. Security+ questions are often solved by identifying **where attacker-controlled input is interpreted, who performs the action, and which control directly addresses the weakness**.
