# Application and Web Attacks

## 1. Overview

Application attacks exploit weaknesses in software, application logic, input handling, authentication, session management, or dependencies.

## 2. SQL Injection

SQL injection occurs when untrusted input is incorporated into a database query in an unsafe way. An attacker may alter the intended meaning of a query, potentially exposing or modifying data.

**Mitigation:** parameterized queries/prepared statements, safe database access libraries, input validation as a secondary control, least-privileged database accounts, and secure error handling.

## 3. Cross-Site Scripting

XSS causes attacker-controlled script content to execute in a victim's browser in the security context of the vulnerable application.

- **Stored XSS:** malicious content is stored by the application and later served to users.
- **Reflected XSS:** malicious content is returned immediately as part of a response.

Output encoding, appropriate content-security policies, input handling, and secure session cookies reduce risk.

## 4. Cross-Site Request Forgery

CSRF abuses an authenticated user's browser session to cause an unwanted action. Anti-CSRF tokens, SameSite cookie settings, origin validation, and appropriate reauthentication can mitigate the attack.

## 5. Command Injection

Command injection occurs when untrusted input reaches an operating-system command interpreter and changes the intended command execution. Avoid invoking shell commands with untrusted input; use safe APIs and strict input validation.

## 6. Path Traversal

Path traversal attempts to access files outside an application's intended directory by manipulating path input. Canonicalization, allowlisting, safe file APIs, and correct access controls reduce risk.

## 7. File Inclusion

Applications that dynamically load files can be vulnerable when attacker-controlled input influences which file is loaded. Strict allowlists and safe application design are preferred.

## 8. Server-Side Request Forgery

SSRF causes a server to make a request selected or influenced by an attacker. The impact can be significant when the server can access internal services that are unavailable from the public network. Restrict outbound access, validate destinations, segment sensitive services, and protect cloud metadata services.

## 9. Insecure Deserialization

Applications that deserialize untrusted data may unintentionally create or execute attacker-controlled objects. Avoid unsafe deserialization, authenticate data sources, use safe formats, and validate serialized data.

## 10. Buffer Overflow

A buffer overflow occurs when software writes beyond the memory allocated for a buffer. Modern mitigations include memory-safe languages, bounds checking, compiler protections, address-space layout randomization, non-executable memory, patching, and secure development practices.

## 11. Race Conditions

A race condition occurs when the security outcome depends on the timing or ordering of concurrent operations. A time-of-check/time-of-use issue is a common example. Atomic operations, locking, and secure transaction design help prevent these weaknesses.

## 12. API and Authentication Attacks

APIs can expose excessive data, weak authorization, predictable tokens, missing rate limits, or improperly validated input. Secure API design requires strong authentication, authorization at the object and function level, input validation, rate limiting, logging, and secure secret handling.

## 13. Dependency and Supply-Chain Risk

Applications depend on libraries, frameworks, packages, containers, and build components. A vulnerable or malicious dependency can introduce risk into an otherwise secure application. Maintain a software inventory, track versions, scan dependencies, verify sources, and update components through controlled processes.

## 14. Security+ Exam Focus

Focus on recognizing the weakness from the scenario. SQL injection targets database query construction; XSS targets browser-side script execution; CSRF abuses an authenticated browser session; SSRF causes the server to make attacker-influenced requests; path traversal manipulates file paths; command injection reaches an OS command interpreter.

## 15. Key Takeaways

Secure applications should treat all external input as untrusted, enforce authorization server-side, minimize privileges, protect sessions, validate dependencies, and log security-relevant activity.
