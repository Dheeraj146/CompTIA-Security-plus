# Secure Protocols and Network Security Technologies

## 1. Introduction

Secure protocols and network security technologies are used to protect communications, control network access, enforce traffic policy, detect attacks, and prevent unauthorized activity. Security+ questions often describe a communication requirement or an architectural problem and expect you to identify the protocol or security technology that directly addresses it.

A secure architecture does not simply mean encrypting everything. The protocol or technology must provide the security properties required by the use case, such as confidentiality, integrity, authentication, authorization, non-repudiation, availability, or controlled access.

A useful way to reason about protocol selection is:

**Communication requirement → Security property → Protocol/technology → Deployment location → Operational trade-off**

For example, if administrators need encrypted remote command-line access, SSH is appropriate. If two networks need an encrypted connection across the public Internet, a site-to-site VPN using IPsec is a common architectural solution. If an organization needs to inspect and filter HTTP requests to a web application, a WAF is more directly relevant than a conventional network firewall.

---

# 2. Secure Protocol Fundamentals

## 2.1 Plaintext and Secure Communications

A plaintext protocol transmits information without providing cryptographic protection at the protocol layer. Anyone who can observe the traffic may potentially read sensitive information or manipulate it, depending on the protocol and surrounding controls.

Examples of traditionally insecure or plaintext-oriented protocols include:

- HTTP
- FTP
- Telnet
- SMTP without TLS
- POP3 without TLS
- IMAP without TLS
- LDAP without TLS
- SNMPv1/v2c
- TFTP

The security problem is not simply that these protocols are old. The important issue is what protection is missing. A protocol may lack confidentiality, integrity protection, strong authentication, or all three.

Modern security architecture generally replaces plaintext communications with encrypted and authenticated alternatives whenever sensitive information crosses an untrusted or insufficiently trusted network.

### Common replacements

| Insecure or weak protocol/use | More secure alternative |
|---|---|
| HTTP | HTTPS |
| Telnet | SSH |
| FTP | SFTP, FTPS, or another secure transfer mechanism |
| LDAP | LDAPS or LDAP protected with TLS |
| SNMPv1/v2c | SNMPv3 |
| Unprotected email transport | SMTP/POP3/IMAP with TLS |
| Unencrypted remote administration | SSH or another authenticated encrypted management protocol |

The exact replacement depends on the application and operational requirements.

---

# 3. TLS and HTTPS

## 3.1 TLS

Transport Layer Security (TLS) is a cryptographic protocol used to protect application-layer communications over networks. TLS can provide:

- Confidentiality through encryption
- Integrity through cryptographic authentication of transmitted data
- Server authentication through digital certificates
- Optional client authentication using client certificates

TLS is widely used to protect web traffic, APIs, email connections, and many other application protocols.

TLS normally relies on a certificate-based trust model for authenticating the server. During the TLS handshake, the communicating parties negotiate cryptographic parameters, authenticate the server when certificate validation is used, establish shared session keys, and then protect application data using symmetric encryption.

### Important concept

TLS does **not** mean that every part of a network connection is automatically protected. It protects the communication session where TLS is actually deployed. A secure design must consider every relevant segment and endpoint.

For example:

**Client → TLS → Web server**

may protect traffic between the client and web server, but if a reverse proxy terminates TLS and forwards traffic internally without encryption, the internal segment has different security properties.

## 3.2 HTTPS

HTTPS is HTTP carried over TLS. It protects web requests and responses from network-level interception and tampering when correctly configured.

HTTPS is especially important for:

- Login pages
- Payment transactions
- Web applications
- REST APIs
- Administrative portals
- Sensitive business applications

### Certificate validation

A browser or client normally validates the server certificate by checking factors such as:

1. The certificate is within its validity period.
2. The requested hostname matches the certificate identity.
3. The certificate chains to a trusted certificate authority.
4. The certificate has not been rejected because of relevant trust or revocation conditions.
5. The cryptographic parameters meet the client's security requirements.

A certificate warning can indicate that trust cannot be established. Simply ignoring certificate warnings defeats an important part of the authentication model.

---

# 4. SSH

Secure Shell (SSH) provides encrypted and authenticated remote access and command execution.

SSH is commonly used for:

- Linux administration
- Network-device administration
- Secure command execution
- Secure file transfer through SFTP or SCP
- Tunneling and port forwarding
- Automated administrative tasks

SSH provides confidentiality and integrity for the protected session and supports strong authentication mechanisms, including passwords and cryptographic keys.

## 4.1 SSH Keys

SSH commonly uses asymmetric cryptography for authentication. A user may possess a private key while the corresponding public key is stored or authorized on the remote system.

The private key should remain protected by the user. The server does not need the private key in order to authenticate the user through public-key authentication.

This is an important distinction from symmetric encryption, where the same secret key is used by communicating parties.

## 4.2 SSH Security Considerations

Secure SSH architecture should consider:

- Strong authentication
- Key protection
- Least privilege
- Disabling unnecessary accounts
- Restricting administrative access through management networks or jump hosts
- Logging authentication activity
- Limiting exposed SSH services
- Keeping the SSH implementation patched
- Using secure cryptographic algorithms

Changing the default SSH port is not a substitute for authentication, authorization, firewall policy, or vulnerability management. It may reduce some automated noise but does not provide meaningful security by itself.

---

# 5. Secure File Transfer

## 5.1 SFTP

SFTP, or SSH File Transfer Protocol, provides file transfer functionality through SSH. It is encrypted and authenticated using the SSH security model.

SFTP should not be confused with FTPS.

## 5.2 SCP

Secure Copy Protocol (SCP) provides secure file copying using SSH-based protection. It is useful for transferring files between systems in environments where SSH access is already established.

## 5.3 FTPS

FTPS is FTP protected using TLS. It is different from SFTP because SFTP is an SSH-based protocol rather than FTP protected by TLS.

### Security+ distinction

**SFTP = SSH-based file transfer**

**FTPS = FTP protected with TLS**

---

# 6. IPsec

Internet Protocol Security (IPsec) is a suite of protocols and standards used to protect IP communications. It is widely associated with VPN architectures.

IPsec can provide:

- Confidentiality
- Integrity
- Authentication
- Anti-replay protection

IPsec operates at the network layer and can protect IP traffic between endpoints, gateways, or other security peers depending on the architecture.

## 6.1 AH

Authentication Header (AH) provides authentication, integrity, and anti-replay protection for IP packets but does not provide confidentiality through encryption.

AH is therefore different from ESP when confidentiality is required.

## 6.2 ESP

Encapsulating Security Payload (ESP) can provide confidentiality, integrity, authentication, and anti-replay protection depending on the selected configuration and algorithms.

ESP is commonly used in modern IPsec VPN implementations.

### Security+ distinction

**AH:** integrity/authentication-related protection, no encryption-based confidentiality.

**ESP:** can provide encryption and integrity/authentication-related protection.

---

# 7. IPsec Transport Mode vs Tunnel Mode

## 7.1 Transport Mode

In transport mode, IPsec protects the payload of an IP packet while retaining the original IP header. It is generally associated with host-to-host communication.

## 7.2 Tunnel Mode

In tunnel mode, the original IP packet is encapsulated within another IP packet. This allows the original packet, including its addressing information, to be protected inside the tunnel.

Tunnel mode is commonly used for site-to-site VPNs, where security gateways establish protected communication between networks.

### Simple comparison

| Feature | Transport mode | Tunnel mode |
|---|---|---|
| Common use | Host-to-host | Network-to-network/VPN gateways |
| Original IP packet | Payload protected | Entire original IP packet encapsulated |
| New outer IP header | No | Yes |
| Common VPN association | Less common | Very common |

---

# 8. IKE and IPsec Key Management

Internet Key Exchange (IKE) is used with IPsec to negotiate security parameters and establish keys for protected communications.

A VPN cannot simply encrypt traffic without establishing cryptographic material and agreeing on how the communication will be protected. IKE helps peers negotiate these parameters and establish security associations.

A simplified process is:

1. VPN peers discover or initiate communication.
2. They authenticate each other.
3. They negotiate cryptographic and security parameters.
4. They establish shared keying material.
5. IPsec uses the negotiated security associations to protect traffic.
6. Keys and associations are periodically refreshed according to configuration.

The exact negotiation process depends on the IKE version and configuration.

---

# 9. VPN Technologies

A Virtual Private Network (VPN) creates a protected communication path across a network that may not be trusted, such as the public Internet.

The important security property is that the VPN provides protection for traffic traversing the untrusted path. A VPN does not automatically make the destination system trustworthy or secure.

## 9.1 Site-to-Site VPN

A site-to-site VPN connects networks rather than individual users.

Example:

**Head Office → encrypted VPN tunnel → Branch Office**

Users at each site can communicate across the protected connection according to routing and security policy.

Site-to-site VPNs are commonly implemented using security gateways or firewalls and IPsec.

## 9.2 Remote-Access VPN

A remote-access VPN connects an individual endpoint to an organizational network or protected service.

Example:

**Employee laptop → VPN → corporate network**

The user may authenticate using credentials, MFA, certificates, or another supported mechanism.

## 9.3 TLS/SSL VPN Concept

A TLS-based VPN uses TLS to protect remote-access or application-oriented VPN communication. These solutions can be useful for remote users and may operate through environments where traditional IPsec connectivity is less convenient.

The important Security+ concept is to distinguish the underlying security mechanism and use case rather than assuming all VPNs are identical.

---

# 10. DNS Security

The Domain Name System (DNS) translates names such as `example.com` into IP addresses and supports other types of service discovery and infrastructure functions.

Traditional DNS traffic is generally not encrypted by default. An attacker able to manipulate or observe DNS communication may attempt attacks such as:

- DNS spoofing
- DNS cache poisoning
- DNS hijacking
- Man-in-the-middle attacks
- Malicious domain resolution

## 10.1 DNSSEC

DNS Security Extensions (DNSSEC) provide cryptographic authentication and integrity for DNS data through digital signatures and a chain of trust.

DNSSEC helps a resolver verify that DNS responses originate from the authoritative DNS hierarchy and have not been modified in transit.

DNSSEC does **not** encrypt ordinary DNS queries and responses.

### Key distinction

**DNSSEC = authenticity/integrity of DNS data**

**DoH/DoT = encryption of DNS transport**

These technologies address related but different problems.

## 10.2 DNS over HTTPS (DoH)

DoH carries DNS queries through HTTPS, providing encryption for DNS communication between the client and the selected resolver.

## 10.3 DNS over TLS (DoT)

DoT carries DNS communication through TLS, providing encrypted transport between the client and resolver.

---

# 11. DHCP Security

Dynamic Host Configuration Protocol (DHCP) automatically provides network configuration such as IP addresses, gateways, and DNS server information.

DHCP is important to security architecture because a malicious or unauthorized DHCP server can provide incorrect network settings to clients.

Potential consequences include:

- Traffic redirection
- Malicious DNS configuration
- Gateway manipulation
- Man-in-the-middle opportunities
- Denial of service through address exhaustion

Network security controls such as DHCP snooping, trusted switch ports, network access control, and segmentation can reduce these risks.

---

# 12. Email Security Protocols

Email commonly involves SMTP for sending mail and POP3 or IMAP for retrieving mail.

## SMTP

Simple Mail Transfer Protocol (SMTP) is primarily used to send and relay email.

SMTP can be protected with TLS to encrypt communication between participating systems.

## POP3

Post Office Protocol version 3 (POP3) retrieves email, typically downloading messages to the client.

POP3 can be protected using TLS.

## IMAP

Internet Message Access Protocol (IMAP) allows clients to access and synchronize messages stored on a mail server.

IMAP can also be protected using TLS.

### Security+ distinction

Do not confuse the function of the protocol with the security mechanism:

- SMTP → sending/relaying email
- POP3 → retrieving email
- IMAP → accessing/synchronizing email
- TLS → protecting the communication channel

---

# 13. S/MIME and PGP/OpenPGP

TLS protects the communication channel between systems, but email may pass through multiple servers and intermediaries. End-to-end or message-level protection can therefore provide additional security.

## S/MIME

Secure/Multipurpose Internet Mail Extensions (S/MIME) uses certificates and public-key cryptography to provide email encryption and digital signatures.

S/MIME can provide:

- Confidentiality
- Integrity
- Authentication
- Digital signatures

## PGP/OpenPGP

Pretty Good Privacy (PGP) and OpenPGP use public-key cryptography and digital signatures to protect messages and files.

### Important distinction

**TLS protects the transport channel.**

**S/MIME or OpenPGP can protect the message itself.**

This distinction is useful in architecture questions involving email confidentiality across multiple mail servers.

---

# 14. LDAP and LDAPS

Lightweight Directory Access Protocol (LDAP) is commonly used to query and interact with directory services.

LDAP can carry sensitive information such as:

- Usernames
- Group membership
- Directory attributes
- Authentication-related information
- Organizational information

LDAPS refers to LDAP protected by TLS, commonly associated with secure directory communication.

LDAP can also be protected using StartTLS, where an existing connection is upgraded to TLS.

The architectural objective is to prevent sensitive directory communication from being exposed or modified over an untrusted network.

---

# 15. Kerberos

Kerberos is a network authentication protocol commonly associated with centralized identity environments such as Active Directory.

Kerberos uses tickets and a trusted authentication service rather than repeatedly sending a user's password to every service.

A simplified model involves:

1. The client authenticates to the authentication service.
2. The client receives a ticket-granting ticket (TGT).
3. The client requests a service ticket for a particular resource.
4. The client presents the service ticket to the target service.
5. The service validates the ticket and establishes the authenticated session.

Kerberos depends heavily on accurate time synchronization. Significant clock differences between systems can cause authentication failures.

### Security considerations

- Protect privileged accounts.
- Secure domain controllers/Kerberos infrastructure.
- Monitor abnormal ticket activity.
- Maintain accurate time synchronization.
- Use strong authentication and account controls.
- Protect service accounts and their credentials.

---

# 16. RADIUS and TACACS+

Both RADIUS and TACACS+ are commonly used for centralized authentication and authorization of network access or administrative access.

## RADIUS

Remote Authentication Dial-In User Service (RADIUS) is widely used for:

- Network access authentication
- VPN authentication
- Wireless Enterprise authentication
- 802.1X environments

RADIUS commonly separates authentication from the network access device and centralizes identity decisions.

## TACACS+

TACACS+ is commonly used for centralized administrative access to network devices.

A key Security+ distinction is:

**RADIUS → commonly associated with network access such as VPN and enterprise Wi-Fi**

**TACACS+ → commonly associated with centralized administrative access to network devices**

TACACS+ also provides more granular separation of authentication, authorization, and accounting functions than traditional RADIUS deployments.

---

# 17. SNMP

Simple Network Management Protocol (SNMP) is used for monitoring and managing network devices.

## SNMPv1 and SNMPv2c

Older SNMP versions commonly use community strings as a basic form of access control. Community strings should not be treated as equivalent to modern strong authentication and encryption.

## SNMPv3

SNMPv3 provides stronger security capabilities, including authentication and privacy features.

### Security+ distinction

**SNMPv1/v2c → weak security model based heavily on community strings**

**SNMPv3 → supports authentication and encryption/privacy**

When sensitive management traffic is involved, SNMPv3 is generally the preferred secure architecture.

---

# 18. NTP and Secure Time

Network Time Protocol (NTP) synchronizes clocks across systems.

Accurate time is critical for:

- Kerberos authentication
- Log correlation
- Incident investigation
- Certificate validation
- Scheduled security operations
- Distributed systems

An attacker who manipulates time can complicate authentication, disrupt log analysis, or interfere with security controls.

Secure NTP designs should use trusted time sources and appropriate authentication or network restrictions where supported.

### SOC relevance

When investigating an incident, analysts frequently correlate events from multiple systems. If one system's clock is incorrect, the apparent order of events may become misleading.

---

# 19. Syslog

Syslog is a common mechanism for transmitting event and log messages from devices and systems to centralized logging infrastructure.

Traditional syslog transmission may be unencrypted depending on the implementation and transport configuration.

Secure logging architecture should consider:

- Authentication of log sources
- Integrity of log messages
- Confidentiality where sensitive information is transmitted
- Centralized storage
- Access control
- Retention
- Time synchronization
- Protection against log tampering

Transport protection such as TLS can be used where supported.

---

# 20. HTTP and HTTPS

HTTP is an application-layer protocol used for web communication. HTTP itself does not provide encryption.

HTTPS combines HTTP with TLS.

A simplified flow is:

**Client → HTTPS/TLS → Web server or reverse proxy → Application**

Security architecture should consider where TLS terminates. TLS may terminate at:

- The web server
- A reverse proxy
- A load balancer
- A web application firewall

If traffic is decrypted at an intermediary, the internal architecture must still protect the subsequent connection when required.

---

# 21. API Security

Modern applications frequently communicate through APIs. API security requires more than simply using HTTPS.

A secure API architecture can include:

- HTTPS/TLS
- Strong authentication
- Authorization
- API keys where appropriate
- OAuth 2.0 for delegated authorization use cases
- OpenID Connect for identity/authentication scenarios built on OAuth 2.0
- Input validation
- Rate limiting
- WAF/API gateway controls
- Logging and monitoring
- Token expiration and secure token handling

### Important distinction

**TLS protects the communication channel.**

**Authentication identifies the caller.**

**Authorization determines what the caller is allowed to do.**

Using HTTPS does not automatically authorize a user to access every API function.

---

# 22. Wireless Security Protocols

Wireless networks expose communication to radio-based interception, making strong wireless security particularly important.

## WEP

Wired Equivalent Privacy (WEP) is an obsolete and insecure wireless security protocol. It should not be used in modern secure deployments.

## WPA

Wi-Fi Protected Access (WPA) was introduced as an improvement over WEP but is now outdated compared with modern standards.

## WPA2

WPA2 commonly uses AES-based CCMP for strong wireless encryption and supports both Personal and Enterprise deployment models.

## WPA3

WPA3 provides improved wireless security and stronger protection mechanisms compared with older standards. It supports modern authentication approaches and improves protection against certain password-guessing attacks in Personal mode.

## Personal vs Enterprise

### Personal

Uses a pre-shared key or password-based model. It is common in homes and small environments.

### Enterprise

Uses centralized authentication, commonly through 802.1X and an authentication server such as RADIUS.

Enterprise wireless is better suited to organizations requiring individual identities, centralized access control, and account-level management.

---

# 23. 802.1X and EAP

802.1X provides port-based network access control. It can require a device or user to authenticate before allowing access to the protected network.

A simplified architecture includes:

- **Supplicant:** endpoint requesting access
- **Authenticator:** switch or wireless access point enforcing access
- **Authentication server:** commonly RADIUS

Extensible Authentication Protocol (EAP) provides a framework for authentication methods used with 802.1X.

This architecture is particularly important for enterprise wired and wireless networks.

---

# 24. Network Security Technologies

Secure protocols protect communications, while network security technologies enforce policy, mediate traffic, control access, detect attacks, or prevent malicious activity.

The major technologies tested by Security+ include:

- Firewalls
- Next-generation firewalls
- Unified threat management
- Proxies
- Reverse proxies
- Web application firewalls
- IDS
- IPS
- Network access control
- VPN gateways
- Secure web/email gateways
- Load balancers
- Network monitoring and security analytics

The correct technology depends on the layer and requirement described in the scenario.

---

# 25. Firewalls

A firewall controls network traffic according to defined security policy.

A firewall may make decisions based on characteristics such as:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Connection state
- Application identity
- User identity
- Other contextual information depending on the firewall

## 25.1 Stateless Firewall

A stateless firewall evaluates each packet independently against configured rules.

It does not maintain the same type of connection-state table used by a stateful firewall.

## 25.2 Stateful Firewall

A stateful firewall tracks the state of network connections. It can determine whether a packet belongs to an established connection or represents a new connection attempt.

Stateful inspection generally provides more contextual traffic control than simple stateless filtering.

## 25.3 Next-Generation Firewall

A Next-Generation Firewall (NGFW) can provide capabilities beyond traditional port and IP filtering, such as:

- Application awareness
- User-aware policy
- Integrated intrusion prevention
- Advanced traffic inspection
- URL/content controls
- Threat intelligence integration

Exact capabilities vary by vendor and product.

### Security+ reasoning

If the requirement is primarily **network traffic policy**, think firewall.

If the requirement is specifically **web application request inspection**, think WAF.

---

# 26. Unified Threat Management

Unified Threat Management (UTM) combines multiple security functions into one platform.

Depending on the product, a UTM may integrate:

- Firewall
- VPN
- IDS/IPS
- Web filtering
- Malware protection
- Email security
- Other gateway controls

The main architectural benefit is centralized functionality and management. The trade-off may include platform dependency, performance constraints, or the impact of a failure affecting multiple security functions.

---

# 27. Forward Proxy

A forward proxy acts on behalf of clients when they access external resources.

Example:

**Internal client → Forward proxy → Internet**

A forward proxy can provide:

- URL filtering
- Content inspection
- Access control
- User-based policies
- Malware scanning
- Logging
- Data-loss controls in some architectures

The destination server may see the proxy as the immediate client rather than the original internal host, depending on configuration.

---

# 28. Reverse Proxy

A reverse proxy acts on behalf of servers.

Example:

**Internet client → Reverse proxy → Internal application server**

Reverse proxies can provide:

- TLS termination
- Load balancing
- Request routing
- Application protection
- Backend concealment
- Authentication integration
- Caching

A reverse proxy is often placed in front of public-facing applications.

### Forward vs reverse proxy

**Forward proxy → represents clients.**

**Reverse proxy → represents servers.**

This is a common Security+ scenario distinction.

---

# 29. Web Application Firewall

A Web Application Firewall (WAF) protects web applications by inspecting HTTP/HTTPS requests and responses according to application-layer security rules.

A WAF can help detect or block attacks such as:

- SQL injection
- Cross-site scripting
- Malicious HTTP requests
- Certain path traversal attempts
- Application-layer protocol abuse

A WAF is not a replacement for secure application development. Vulnerable code should still be fixed.

### Security+ reasoning

If a scenario says:

> “The organization wants to inspect incoming HTTP requests and protect a web application from SQL injection.”

The relevant technology is a **WAF**.

A conventional firewall may allow or block the network connection, but it is not primarily designed to understand application-specific HTTP attack patterns at the same depth as a WAF.

---

# 30. IDS and IPS

## 30.1 IDS

An Intrusion Detection System (IDS) monitors activity and identifies potentially malicious or suspicious behavior.

Its primary function is **detection and alerting**.

An IDS may use:

- Signature detection
- Anomaly detection
- Behavioral analysis
- Protocol analysis

## 30.2 IPS

An Intrusion Prevention System (IPS) can detect suspicious activity and actively block or prevent malicious traffic.

The main distinction is the ability to take preventive action inline or through another enforcement mechanism.

### Security+ distinction

**IDS = detect/alert**

**IPS = detect and prevent/block**

An IDS can be useful where passive monitoring is required. An IPS is useful where the architecture permits active enforcement.

---

# 31. Network Access Control

Network Access Control (NAC) controls whether a device is allowed to access the network and under what conditions.

NAC decisions may consider:

- User identity
- Device identity
- Device health
- Operating system
- Security software status
- Certificate status
- Network location
- Authentication result

NAC can place a noncompliant device into a restricted or remediation network.

Example:

**Corporate laptop → authentication → posture check → permitted VLAN**

or

**Unknown/unhealthy device → authentication/posture failure → quarantine VLAN**

### Security+ reasoning

If the scenario is about **controlling who or what is admitted to the network**, NAC is a strong candidate.

---

# 32. Load Balancers

A load balancer distributes network or application traffic across multiple backend systems.

Security and availability benefits can include:

- Reduced dependency on a single server
- Health checking
- Traffic distribution
- TLS termination in some architectures
- Integration with reverse-proxy functionality

A load balancer is primarily an availability and traffic-distribution technology, although it can participate in a broader security architecture.

---

# 33. Secure Gateways

Security gateways sit at controlled boundaries and inspect or mediate traffic between environments.

Examples include:

- Secure web gateways
- Secure email gateways
- VPN gateways
- Firewall gateways
- API gateways

## Secure Web Gateway

A secure web gateway can enforce organizational web-access policy and inspect web traffic. Depending on the implementation, it may provide URL filtering, malware detection, content inspection, and user-based policy.

## Secure Email Gateway

A secure email gateway can inspect inbound and outbound mail for:

- Malware
- Spam
- Phishing indicators
- Malicious attachments
- Suspicious URLs
- Policy violations

---

# 34. Network Security Technology Placement

Technology placement matters because the same security product can provide different protection depending on where it is deployed.

A simplified architecture might look like:

```text
                         Internet
                            |
                     [Edge Firewall]
                            |
                  [IDS/IPS / Gateway]
                            |
                         [DMZ]
                       /       \
                [WAF/Proxy]  [Public Service]
                       |
                [Internal Firewall]
                       |
                Internal Network
                  /           \
           User Network     Server Network
                              |
                        Database Network
```

The architecture should create appropriate trust boundaries and limit unnecessary communication between zones.

---

# 35. Encrypted Traffic Inspection

Encryption protects confidentiality but can also make network inspection more difficult.

For example, an IDS cannot necessarily inspect the contents of encrypted application traffic unless the architecture provides a controlled decryption or inspection point.

Organizations may use:

- TLS inspection
- Secure web gateways
- Reverse proxies
- Endpoint telemetry
- Application-layer logging

However, decryption introduces important considerations:

- Privacy
- Certificate management
- Performance
- Key protection
- Application compatibility
- Legal or regulatory requirements
- Sensitive categories of traffic that should not be inspected

Security architecture must balance visibility with confidentiality and privacy requirements.

---

# 36. PKI and Secure Protocols

Public Key Infrastructure (PKI) provides the trust infrastructure used by many secure protocols.

PKI can support:

- Digital certificates
- Certificate authorities
- Identity binding
- Digital signatures
- Certificate validation
- Key lifecycle management

TLS, S/MIME, 802.1X certificate-based authentication, and other technologies can depend on certificate-based trust.

A secure protocol is therefore not isolated from the rest of the architecture. Certificate issuance, validation, renewal, revocation, private-key protection, and trust-anchor management are operational security requirements.

---

# 37. Protocol Selection Criteria

When selecting a protocol, consider more than whether it is labeled “secure.” Evaluate:

## Confidentiality

Does the protocol prevent unauthorized parties from reading the data?

## Integrity

Can the recipient detect unauthorized modification of the data?

## Authentication

Can the parties verify who they are communicating with?

## Authorization

Does the surrounding architecture control what authenticated identities can do?

## Replay Protection

Can an attacker capture valid traffic and successfully reuse it later?

## Performance

Does encryption or inspection introduce acceptable overhead?

## Compatibility

Does the protocol work with existing clients, servers, applications, and infrastructure?

## Manageability

Can the organization centrally configure, monitor, patch, and audit the technology?

## Availability

Does the technology introduce a single point of failure?

## Compliance and Privacy

Does traffic inspection, data storage, or cryptographic processing satisfy applicable organizational and regulatory requirements?

---

# 38. Common Insecure Protocols and Their Security Problems

| Protocol | Primary concern | Common secure approach |
|---|---|---|
| Telnet | Plaintext remote administration | SSH |
| FTP | Plaintext credentials/data | SFTP or FTPS |
| HTTP | No transport encryption | HTTPS |
| LDAP without TLS | Directory traffic exposure | LDAPS/StartTLS |
| SNMPv1/v2c | Weak security/community strings | SNMPv3 |
| Unprotected SMTP | Email transport exposure | SMTP with TLS |
| Unprotected POP3 | Mail retrieval exposure | POP3 over TLS |
| Unprotected IMAP | Mail access exposure | IMAP over TLS |
| TFTP | Minimal security/no encryption | Secure file-transfer mechanism |
| WEP | Cryptographically broken | WPA2/WPA3 |

The secure alternative must always be selected according to the actual use case and environment.

---

# 39. Common Security+ Technology Distinctions

| Requirement | Technology most directly associated |
|---|---|
| Protect web traffic in transit | TLS/HTTPS |
| Secure remote command-line administration | SSH |
| Secure file transfer over SSH | SFTP/SCP |
| Secure FTP using TLS | FTPS |
| Network-layer encrypted tunnel | IPsec/VPN |
| Authenticate and protect DNS data | DNSSEC |
| Encrypt DNS transport | DoH/DoT |
| Centralized network-access authentication | RADIUS |
| Centralized network-device administration | TACACS+ |
| Secure enterprise wireless authentication | 802.1X/EAP/RADIUS |
| Secure network management | SNMPv3 |
| Web application attack filtering | WAF |
| Network traffic policy enforcement | Firewall |
| Detect suspicious network activity | IDS |
| Detect and actively block suspicious traffic | IPS |
| Control endpoint network admission | NAC |
| Represent internal clients to external resources | Forward proxy |
| Represent internal servers to external clients | Reverse proxy |
| Distribute traffic across servers | Load balancer |
| Protect multiple gateway functions in one platform | UTM |
| Secure message-level email content | S/MIME/OpenPGP |

---

# 40. Detailed Security+ Scenarios

## Scenario 1 — Secure Remote Administration

**Requirement:** Administrators need to remotely manage Linux servers over an untrusted network.

**Reasoning:** Remote command-line administration requires confidentiality, integrity, and authentication.

**Appropriate technology:** SSH.

---

## Scenario 2 — Branch Connectivity

**Requirement:** Two corporate offices need encrypted communication over the public Internet.

**Reasoning:** This is a network-to-network communication requirement.

**Appropriate architecture:** Site-to-site VPN, commonly using IPsec.

---

## Scenario 3 — Remote Employee

**Requirement:** Employees working from home need secure access to internal resources.

**Reasoning:** An individual endpoint needs a protected connection to the organization's network.

**Appropriate architecture:** Remote-access VPN, subject to the organization's authentication and access-control design.

---

## Scenario 4 — Web Application Attack

**Requirement:** A company wants to block malicious HTTP requests targeting a public web application.

**Reasoning:** The requirement is application-layer web traffic inspection.

**Appropriate technology:** WAF.

---

## Scenario 5 — Unknown Endpoint

**Requirement:** The organization wants to prevent unmanaged laptops from joining the internal network.

**Reasoning:** The problem is network admission and endpoint identity/posture.

**Appropriate technology:** NAC, often integrated with 802.1X and RADIUS.

---

## Scenario 6 — Detect Only

**Requirement:** Security staff want visibility into suspicious network traffic without placing an enforcement device inline.

**Reasoning:** The requirement is detection and alerting rather than automatic blocking.

**Appropriate technology:** IDS.

---

## Scenario 7 — Automatic Blocking

**Requirement:** The organization wants suspicious network traffic to be automatically blocked.

**Reasoning:** The requirement includes active prevention.

**Appropriate technology:** IPS.

---

## Scenario 8 — DNS Integrity

**Requirement:** DNS resolvers must verify that DNS records have not been modified and originate from the legitimate DNS hierarchy.

**Reasoning:** The requirement is DNS data authenticity and integrity.

**Appropriate technology:** DNSSEC.

---

## Scenario 9 — DNS Confidentiality

**Requirement:** Users' DNS queries should be encrypted between the endpoint and DNS resolver.

**Reasoning:** The requirement is transport confidentiality for DNS.

**Appropriate technology:** DoH or DoT.

---

## Scenario 10 — Enterprise Wi-Fi

**Requirement:** Each employee should authenticate individually to corporate Wi-Fi using centralized credentials rather than sharing one wireless password.

**Reasoning:** Individual enterprise authentication is required.

**Appropriate architecture:** WPA2/WPA3 Enterprise with 802.1X/EAP and commonly RADIUS.

---

# 41. Common Exam Traps

## Trap 1 — IDS vs IPS

If the requirement says **detect and alert**, IDS is the direct match.

If it says **detect and block/prevent**, IPS is the direct match.

## Trap 2 — Firewall vs WAF

A firewall controls network traffic. A WAF specializes in web application traffic and HTTP/HTTPS attacks.

## Trap 3 — NAC vs Firewall

NAC answers the question:

> “Should this endpoint be admitted to the network?”

A firewall answers questions about whether particular traffic should be allowed between network zones or destinations.

## Trap 4 — Forward vs Reverse Proxy

Forward proxy = client side.

Reverse proxy = server side.

## Trap 5 — DNSSEC vs DoH/DoT

DNSSEC validates DNS data through cryptographic signatures.

DoH/DoT encrypt DNS transport.

They are not interchangeable.

## Trap 6 — SFTP vs FTPS

SFTP uses SSH.

FTPS uses FTP with TLS.

## Trap 7 — IPsec AH vs ESP

AH does not provide encryption-based confidentiality.

ESP can provide confidentiality and integrity/authentication-related protection.

## Trap 8 — TLS vs Authentication

TLS can authenticate a server and protect the channel, but HTTPS alone does not determine what an authenticated application user is authorized to do.

## Trap 9 — VPN vs Firewall

A VPN creates a protected communication channel.

A firewall enforces traffic policy.

A VPN does not automatically replace firewall policy.

## Trap 10 — Encryption vs Integrity

Encryption primarily protects confidentiality. Integrity requires appropriate cryptographic integrity protection such as authenticated encryption or a secure MAC/signature mechanism.

---

# 42. Secure Protocol Architecture Checklist

When reviewing a protocol or network security design, ask:

### Communication

- What systems communicate?
- Is the network trusted or untrusted?
- Is the communication local, remote, site-to-site, or Internet-facing?

### Security properties

- Is confidentiality required?
- Is integrity required?
- Is authentication required?
- Is authorization handled separately?
- Is replay protection required?

### Protocol

- Is the protocol encrypted?
- Does it use modern cryptographic mechanisms?
- Is certificate validation required?
- How are keys established and protected?

### Network control

- Which firewall rules permit the traffic?
- Is segmentation required?
- Is NAC required?
- Is a proxy or gateway appropriate?
- Should IDS/IPS monitor the traffic?

### Operations

- Is logging enabled?
- Are events time synchronized?
- Can administrators monitor failures?
- Are certificates and keys rotated?
- Are vulnerable protocols disabled?

### Resilience

- Is there a single point of failure?
- Are redundant gateways required?
- What happens if the security technology fails?
- Does fail-open or fail-closed behavior match the risk?

---

# 43. Scenario Reasoning Framework

For Security+ questions involving protocols and network security technologies, use this process:

### Step 1 — Identify what is being protected

Is it:

- A web application?
- A network connection?
- A remote administrator?
- A wireless network?
- An endpoint joining the network?
- DNS data?
- Email?
- Directory services?

### Step 2 — Identify the security requirement

Is the question asking for:

- Encryption?
- Authentication?
- Integrity?
- Network admission?
- Detection?
- Prevention?
- Application-layer filtering?
- Traffic distribution?

### Step 3 — Identify the layer

Determine whether the problem is primarily:

- Application layer
- Transport/session security
- Network layer
- Network access layer
- Identity/authentication layer

### Step 4 — Identify the enforcement point

Ask where the control should operate:

- Endpoint
- Switch
- Wireless access point
- Firewall
- Proxy
- WAF
- VPN gateway
- Authentication server
- Application gateway

### Step 5 — Consider trade-offs

Finally consider:

- Performance
- Availability
- Compatibility
- Visibility
- Privacy
- Management overhead
- Failure behavior

This approach is more reliable than memorizing isolated protocol names.

---

# 44. Key Takeaways

1. **TLS/HTTPS** protects application communication in transit and commonly provides certificate-based server authentication.
2. **SSH** provides secure remote administration and supports secure file transfer through SFTP/SCP.
3. **IPsec** protects IP communication and is widely used for VPNs.
4. **AH** provides integrity/authentication-related protection but not encryption-based confidentiality; **ESP** can provide confidentiality and integrity/authentication-related protection.
5. **Transport mode** protects the IP payload while retaining the original IP header; **tunnel mode** encapsulates the original IP packet and is widely used for VPN gateways.
6. **Site-to-site VPNs** connect networks; **remote-access VPNs** connect individual users or endpoints.
7. **DNSSEC** protects DNS data authenticity and integrity; **DoH/DoT** protect DNS transport with encryption.
8. **S/MIME and OpenPGP** can provide message-level email protection, while TLS protects the communication channel.
9. **Kerberos** uses tickets for network authentication and depends on accurate time synchronization.
10. **RADIUS** is commonly used for centralized network-access authentication, while **TACACS+** is commonly associated with administrative access to network devices.
11. **SNMPv3** provides stronger security than older SNMP versions.
12. **802.1X/EAP/RADIUS** supports enterprise network-access authentication.
13. **Firewall** = traffic policy enforcement.
14. **IDS** = detection and alerting.
15. **IPS** = detection plus active prevention/blocking.
16. **WAF** = web application traffic protection.
17. **NAC** = endpoint/network admission control.
18. **Forward proxy** represents clients; **reverse proxy** represents servers.
19. **Load balancers** distribute traffic and can contribute to availability and TLS termination.
20. Encryption is only one part of secure architecture; authentication, authorization, integrity, segmentation, logging, monitoring, resilience, and key management also matter.

The central Security+ skill is not memorizing protocol names. It is recognizing **what the scenario requires, where the control belongs, what security property it provides, and what limitations or dependencies it introduces**.