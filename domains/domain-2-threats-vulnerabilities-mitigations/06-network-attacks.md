# 06 — Network Attacks

## 1. Introduction to Network Attacks

**Network attacks** target network infrastructure, network protocols, communications, or the availability, confidentiality, integrity, and trust relationships of networked systems.

A network attack does not always mean that an attacker directly compromises a server. The attacker may instead manipulate a protocol, impersonate a device, exhaust a resource, intercept traffic, or abuse a weakness in network architecture.

A useful way to analyze a network attack is:

**Target → Network layer/protocol → Weakness → Attack technique → Security impact → Detection → Mitigation**

For example:

**DHCP service → DHCP protocol → Unauthorized DHCP server accepted → DHCP spoofing → Malicious network configuration → Rogue DHCP detection → DHCP snooping**

Understanding this chain is more useful than memorizing attack names independently.

---

# 2. Denial of Service (DoS)

A **Denial-of-Service (DoS)** attack attempts to make a system, application, or network service unavailable to legitimate users.

The attacker may exhaust:

- CPU
- Memory
- Bandwidth
- Network connections
- Application resources
- Connection tables
- Storage
- Processing capacity

The goal is generally to affect **availability**.

### Example

A web server can normally handle a certain number of simultaneous connections. An attacker sends enough requests or connection attempts to consume the server's available resources, preventing legitimate users from accessing the service.

---

# 3. Distributed Denial of Service (DDoS)

A **Distributed Denial-of-Service (DDoS)** attack uses multiple systems or sources to generate malicious traffic or requests toward a target.

The distributed nature makes the attack more difficult to block because there may be many apparent sources.

Compromised devices used for DDoS can include:

- Computers
- Servers
- IoT devices
- Network appliances
- Other internet-connected systems

A botnet is one common way attackers obtain a large number of systems capable of generating traffic.

### DoS vs DDoS

**DoS:** attack originates from a single source or relatively limited source set.

**DDoS:** attack is distributed across multiple sources.

The key exam clue is **distribution**.

---

# 4. Volumetric DDoS Attacks

A **volumetric attack** attempts to consume network bandwidth or infrastructure capacity with a large amount of traffic.

The objective is to overwhelm the network path or service with volume.

Common examples include:

- UDP floods
- ICMP floods
- Reflection attacks
- Amplification attacks

### Defensive controls

- Upstream DDoS protection
- Traffic filtering
- Rate limiting
- Load balancing
- Anycast or distributed architecture where appropriate
- Capacity planning
- Network monitoring

For large attacks, mitigation may need to occur upstream of the organization's own network because the organization's internet connection can become saturated before local controls can respond.

---

# 5. SYN Flood

A **SYN flood** abuses the TCP connection establishment process.

TCP normally establishes a connection through a handshake:

**Client → SYN → Server**

**Server → SYN/ACK → Client**

**Client → ACK → Server**

A SYN flood sends a large number of SYN requests while preventing the connection from completing normally.

The target may allocate resources for incomplete connections. If enough resources are consumed, legitimate connections can be delayed or rejected.

### Defensive controls

- SYN cookies
- Connection rate limiting
- Firewall filtering
- Load balancing
- DDoS protection
- Network capacity and monitoring

### Exam clue

If a question specifically mentions **TCP connection establishment and many incomplete SYN connections**, think **SYN flood**.

---

# 6. UDP Flood

A **UDP flood** sends a large amount of UDP traffic toward a target.

The target must process incoming traffic, and excessive traffic can consume network or system resources.

UDP does not use the same connection-oriented handshake as TCP, so the attack focuses on traffic volume and resource consumption rather than incomplete TCP connections.

### Exam clue

**Excessive UDP traffic → UDP flood.**

---

# 7. ICMP Flood

An **ICMP flood** generates excessive ICMP traffic toward a target.

ICMP is legitimately used for network diagnostics and error reporting, but excessive traffic can consume resources.

Defensive controls may include:

- Rate limiting
- Filtering where appropriate
- DDoS protection
- Network monitoring

The important point is that legitimate protocols can be abused when their traffic volume becomes malicious or excessive.

---

# 8. Reflection Attacks

A **reflection attack** causes third-party systems to send traffic toward the victim.

Instead of directly sending all traffic from the attacker's infrastructure, the attacker sends requests to other systems while manipulating the requests so that the responses are directed to the victim.

### Simplified model

**Attacker → Reflector → Victim**

The reflector may be a legitimate internet service that has been abused for the attack.

### Why reflection is useful to attackers

It can:

- Hide the direct origin of some traffic
- Increase the number of traffic sources seen by the victim
- Support amplification

---

# 9. Amplification Attacks

An **amplification attack** occurs when a relatively small request causes a much larger response to be sent toward the victim.

The attacker seeks a favorable response-to-request ratio.

### Simplified example

**Small attacker request → large response → victim**

When combined with reflection, amplification can produce substantial traffic volumes.

### Reflection vs amplification

These concepts are related but not identical:

- **Reflection:** traffic is redirected through third-party systems toward the victim.
- **Amplification:** the response generated is substantially larger than the request.

A single attack can use both techniques.

---

# 10. Address Resolution Protocol (ARP)

**ARP** is used on IPv4 local networks to associate an IP address with a MAC address.

For example, if a host needs to communicate with `192.168.1.20` on the local network, it needs to know which MAC address corresponds to that IP address.

ARP provides this local mapping.

The protocol was designed for trusted local networks and does not inherently provide strong authentication of ARP responses.

This creates opportunities for attacks such as **ARP spoofing/poisoning**.

---

# 11. ARP Spoofing / ARP Poisoning

**ARP spoofing**, also called **ARP poisoning**, occurs when an attacker sends false ARP information so that devices associate an attacker's MAC address with another IP address.

### Example

Suppose:

- Gateway IP = `192.168.1.1`
- Gateway MAC = legitimate gateway MAC
- Attacker MAC = attacker's MAC

If the attacker successfully convinces a victim that the gateway IP corresponds to the attacker's MAC address, the victim may send local traffic toward the attacker.

### Possible consequences

- Traffic interception
- Man-in-the-middle attacks
- Traffic disruption
- Credential exposure when applications lack adequate encryption

### Defenses

- Dynamic ARP Inspection
- DHCP snooping
- Secure switch configuration
- Network segmentation
- Static ARP entries in limited appropriate cases
- TLS and other authenticated encryption
- VPNs where appropriate

Encryption at higher layers is particularly important because even if traffic is intercepted, properly protected TLS traffic should not expose its contents simply because the attacker can observe packets.

---

# 12. DHCP Fundamentals

**DHCP (Dynamic Host Configuration Protocol)** automatically provides network configuration to clients.

A DHCP server may provide:

- IP address
- Subnet mask
- Default gateway
- DNS server information
- Lease information

DHCP therefore plays an important role in how hosts join and operate on a network.

Because clients trust DHCP responses, unauthorized DHCP infrastructure can manipulate network configuration.

---

# 13. DHCP Spoofing / Rogue DHCP

**DHCP spoofing** occurs when an unauthorized DHCP server provides configuration information to clients.

The rogue server may attempt to provide malicious or incorrect values for:

- Default gateway
- DNS server
- IP configuration

### Example

A client joins a network and sends a DHCP request. Both the legitimate DHCP server and an attacker-controlled rogue DHCP server respond. If the client accepts the malicious response, its network configuration may be controlled by the attacker.

### Potential impact

A malicious gateway or DNS configuration can facilitate traffic interception, redirection, or other attacks.

### Defense

**DHCP snooping** on managed switches can identify trusted DHCP-server ports and block unauthorized DHCP server responses from untrusted ports.

---

# 14. DHCP Starvation

**DHCP starvation** attempts to consume the available DHCP address pool so legitimate clients cannot obtain addresses.

### Basic concept

**Exhaust available leases → legitimate clients cannot obtain addresses → network availability is affected**

This is different from DHCP spoofing.

- **DHCP spoofing:** attacker provides unauthorized configuration.
- **DHCP starvation:** attacker consumes available DHCP leases.

### Defensive controls

- DHCP snooping
- Switch port security
- Rate limiting
- MAC address controls
- Monitoring DHCP activity

---

# 15. MAC Flooding

A switch normally learns which MAC addresses are associated with its ports and uses that information to forward frames efficiently.

**MAC flooding** attempts to overwhelm the switch's MAC address table with a large number of source MAC addresses.

If the switch can no longer maintain useful forwarding information, behavior may become less selective, depending on the switch and configuration.

This can increase the opportunity for traffic observation on the local network.

### Defenses

- Port security
- MAC address limits
- Appropriate switch configuration
- Network segmentation
- Monitoring for abnormal MAC learning

---

# 16. VLAN Fundamentals

A **VLAN (Virtual Local Area Network)** logically separates network traffic at the switching layer.

VLANs can help isolate:

- Departments
- Server networks
- Guest networks
- Management systems
- Sensitive systems

Segmentation is a security control because it can reduce unnecessary communication between systems.

However, incorrect VLAN configuration can create opportunities for traffic to cross intended boundaries.

---

# 17. VLAN Hopping

**VLAN hopping** is an attack in which an attacker attempts to access traffic associated with another VLAN.

The attack generally relies on weaknesses or misconfigurations involving VLAN trunking or switch behavior.

### Security risks

Successful VLAN hopping can undermine segmentation and allow an attacker to reach traffic or systems that should be isolated.

### Defensive controls

- Disable unnecessary trunking
- Explicitly configure trunk ports
- Avoid unnecessary use of dynamic trunk negotiation
- Secure native VLAN configuration
- Use dedicated VLANs for appropriate purposes
- Apply proper switch hardening

### Exam clue

If a scenario says an attacker is attempting to **cross VLAN boundaries**, think **VLAN hopping**.

---

# 18. IP Spoofing

**IP spoofing** occurs when a packet is sent with a forged source IP address.

The source address in the packet may therefore not represent the actual origin of the traffic.

### Why attackers use spoofing

It may be used to:

- Obscure the apparent source
- Abuse trust relationships
- Support reflection attacks
- Bypass poorly designed source-based controls

IP spoofing does not automatically provide authentication or access. It is a technique that may support other attacks.

### Defense

**Ingress filtering** can reject packets entering a network when their source addresses should not legitimately originate from that interface.

**Egress filtering** can reduce the ability of internal systems to send packets with forged source addresses to external networks.

---

# 19. Man-in-the-Middle (MITM)

A **Man-in-the-Middle (MITM)** attack occurs when an attacker positions themselves between communicating parties and can potentially observe, relay, or modify communication.

### Basic model

**Client ↔ Attacker ↔ Server**

Without strong authentication and encryption, the attacker may be able to:

- Observe sensitive data
- Modify communications
- Inject content
- Capture authentication material
- Redirect traffic

### Important point

Simply being physically or logically between two systems does not automatically mean that a successful MITM attack has occurred. The attacker must also overcome the relevant authentication or encryption protections to meaningfully read or manipulate protected traffic.

### Defenses

- TLS
- Proper certificate validation
- Secure VPNs
- Strong authentication
- Network segmentation
- Secure wireless configuration
- Authenticated protocols

---

# 20. Session Hijacking

A **session hijacking** attack occurs when an attacker obtains control of a valid authenticated session.

Instead of stealing the user's password directly, the attacker may target the session itself.

A session can be represented by a token, cookie, or another server-recognized identifier.

### Potential impact

If a valid session is compromised, the attacker may be able to act as the authenticated user until the session expires or is invalidated.

### Defenses

- TLS
- Secure session cookies
- Short session lifetimes where appropriate
- Session invalidation
- Reauthentication for sensitive operations
- Protection against token exposure

---

# 21. Replay Attacks

A **replay attack** occurs when an attacker captures valid authentication or transaction information and later retransmits it to attempt to gain access or cause an action to occur again.

The attacker may not need to understand the entire original message if the system accepts the captured data again.

### Defense concepts

- Nonces
- Timestamps
- Sequence numbers
- Short-lived tokens
- Challenge-response authentication
- Replay detection

The goal is to ensure that previously captured valid communication cannot simply be reused as though it were new.

---

# 22. DNS Fundamentals

**DNS (Domain Name System)** translates names such as `example.com` into information such as IP addresses.

DNS is critical because users and applications frequently depend on name resolution to locate services.

A simplified process is:

**Application → Resolver → DNS infrastructure → Response → Application connects to destination**

Because clients trust DNS responses, manipulation of DNS information can redirect users or applications.

---

# 23. DNS Spoofing and Poisoning

**DNS spoofing** involves providing false DNS information so that a hostname resolves to an incorrect destination.

**DNS cache poisoning** is a specific form in which false DNS information is inserted into a DNS cache, causing subsequent queries to receive incorrect results.

### Potential impact

Users may be redirected to:

- Phishing websites
- Malicious servers
- Fake login pages
- Attacker-controlled infrastructure

### Defenses

- DNSSEC where supported and appropriately deployed
- Secure resolver configuration
- Monitoring for unexpected DNS changes
- Protected DNS infrastructure
- TLS and certificate validation at the application layer

DNSSEC provides authenticity and integrity protection for DNS data, but it does not encrypt ordinary DNS queries.

---

# 24. Rogue Devices

A **rogue device** is an unauthorized device connected to an organization's network or infrastructure.

Examples include:

- Unauthorized access point
- Rogue switch
- Unauthorized router
- Personal device
- Unauthorized server

### Why rogue devices are dangerous

A rogue device may create an unmonitored path into the environment and bypass normal network security controls.

### Defenses

- Network Access Control (NAC)
- Asset inventory
- Port security
- Wireless monitoring
- Switch monitoring
- Device authentication
- Physical security

---

# 25. Rogue Access Point

A **rogue access point** is an unauthorized wireless access point connected to or operating near an organization's network.

An attacker may attempt to create an access point that resembles a legitimate corporate network, encouraging users to connect to it.

A rogue AP can potentially enable traffic interception, credential collection, or unauthorized network access depending on how the environment is configured.

### Defenses

- Wireless intrusion detection/prevention
- NAC
- Access-point inventory
- Strong wireless authentication
- Monitoring for unauthorized SSIDs
- Physical security

---

# 26. Evil Twin

An **evil twin** is a fraudulent wireless access point designed to imitate a legitimate wireless network.

### Example

A legitimate organization provides Wi-Fi named `Company-WiFi`. An attacker creates another wireless network with a confusingly similar name and attempts to convince users to connect.

### Potential consequences

The attacker may attempt to:

- Intercept traffic
- Capture credentials through fraudulent portals
- Observe unencrypted communications
- Manipulate the user's network path

### Defense

Users and organizations should rely on strong wireless authentication and certificate validation rather than trusting an SSID name alone.

---

# 27. Network Attack Relationships

Many attacks can be combined.

For example:

**Rogue DHCP → malicious gateway/DNS → traffic redirection → MITM attempt → credential theft**

Another chain could be:

**Compromised botnet → DDoS traffic → reflection/amplification → service outage**

Another could be:

**ARP poisoning → traffic interception → session or credential exposure → account compromise**

This demonstrates why network attacks should be understood as mechanisms that can support broader attack chains.

---

# 28. Network Attack Detection

Network attacks can produce different telemetry depending on the technique.

### DDoS indicators

- Sudden traffic spikes
- Large numbers of connection attempts
- Unusual source distribution
- Bandwidth saturation
- Service latency
- Increased packet rates

### ARP attack indicators

- Unexpected ARP changes
- Multiple IP addresses associated with one MAC address
- Frequent ARP replies
- Gateway MAC address changes

### DHCP attack indicators

- Unexpected DHCP servers
- Multiple DHCP responses
- Abnormal DHCP request rates
- Rapid lease consumption

### DNS attack indicators

- Unexpected DNS changes
- Suspicious domains
- Unusual resolver behavior
- Inconsistent DNS responses

### Rogue device indicators

- Unknown MAC addresses
- New network interfaces
- Unexpected switch-port activity
- Unknown wireless access points

Detection should use context rather than treating every anomaly as malicious.

---

# 29. Network Attack Mitigation Strategy

A layered network-defense strategy can include:

### Layer 1 — Secure protocols

Use authenticated and encrypted protocols such as TLS and appropriately secured VPN technologies.

### Layer 2 — Infrastructure security

Harden switches, routers, wireless infrastructure, DHCP services, and DNS infrastructure.

### Layer 3 — Segmentation

Separate systems according to trust, business function, and sensitivity.

### Layer 4 — Access control

Use NAC, port security, firewall policies, and appropriate identity-based controls.

### Layer 5 — Monitoring

Collect network telemetry and analyze anomalies.

### Layer 6 — Resilience

Design services to tolerate traffic spikes and failures through redundancy, capacity, load balancing, and upstream DDoS protection where appropriate.

---

# 30. Network Attack Comparison

| Attack | Primary target/mechanism | Defining clue | Typical impact |
|---|---|---|---|
| DoS | System/service resources | Service made unavailable | Availability |
| DDoS | Distributed traffic sources | Many attacking sources | Availability |
| SYN flood | TCP connection establishment | Many incomplete SYN connections | Availability |
| UDP flood | UDP traffic | Excessive UDP traffic | Availability |
| ICMP flood | ICMP traffic | Excessive ICMP traffic | Availability |
| Reflection | Third-party systems | Reflectors send traffic to victim | Availability/obfuscation |
| Amplification | Protocol response size | Small request produces large response | Availability |
| ARP poisoning | Local address resolution | False IP-to-MAC mapping | Interception/disruption |
| DHCP spoofing | DHCP configuration | Rogue DHCP response | Redirection/interception |
| DHCP starvation | DHCP lease pool | Addresses exhausted | Availability |
| MAC flooding | Switch MAC table | Excessive source MAC addresses | Traffic exposure |
| VLAN hopping | VLAN boundaries | Attempts to cross VLANs | Segmentation bypass |
| IP spoofing | Source IP address | Forged source address | Trust abuse/reflection |
| MITM | Communication path | Attacker positioned between parties | Confidentiality/integrity |
| Session hijacking | Active session | Valid session controlled by attacker | Unauthorized access |
| Replay | Captured valid communication | Previously captured data reused | Authentication/transaction abuse |
| DNS poisoning | DNS resolution | False DNS information | Redirection |
| Rogue device | Network infrastructure | Unauthorized device | Unauthorized access |
| Evil twin | Wireless users | Fake AP impersonates legitimate network | Interception/credential theft |

---

# 31. Important Security+ Distinctions

### DoS vs DDoS

**DoS:** limited source of attack traffic.

**DDoS:** distributed sources.

### Reflection vs Amplification

**Reflection:** third-party systems send traffic toward the victim.

**Amplification:** the response is larger than the request.

They can occur together.

### ARP Poisoning vs DNS Poisoning

**ARP poisoning:** manipulates local IP-to-MAC mapping.

**DNS poisoning:** manipulates name-resolution information.

### DHCP Spoofing vs DHCP Starvation

**Spoofing:** unauthorized DHCP server provides malicious configuration.

**Starvation:** attacker consumes available DHCP leases.

### IP Spoofing vs MITM

**IP spoofing:** falsifies the source IP address.

**MITM:** attacker positions themselves in the communication path and attempts to observe or manipulate communication.

IP spoofing may support other attacks but is not itself synonymous with MITM.

### Session Hijacking vs Replay

**Session hijacking:** attacker obtains control of an active session.

**Replay:** attacker retransmits captured valid communication.

### Rogue AP vs Evil Twin

A **rogue AP** is an unauthorized access point.

An **evil twin** specifically imitates a legitimate wireless network to deceive users.

---

# 32. Detailed Security+ Scenario — ARP Poisoning

### Scenario

Users on an internal network report that traffic is intermittently passing through an unknown device. The network team observes that the MAC address associated with the default gateway IP has unexpectedly changed to a workstation's MAC address.

### Analysis

The important clue is the false relationship between the gateway IP and another MAC address.

This points toward **ARP spoofing/poisoning**.

### Potential impact

An attacker may attempt to position themselves between users and the gateway.

### Appropriate controls

- Dynamic ARP Inspection
- DHCP snooping
- Network segmentation
- Secure switch configuration
- TLS
- Monitoring

---

# 33. Detailed Security+ Scenario — DHCP

### Scenario

Several workstations suddenly receive a default gateway and DNS server that do not match the organization's approved network configuration.

### Analysis

DHCP provides network configuration. An unauthorized DHCP server may be supplying the clients with malicious settings.

This indicates **DHCP spoofing/rogue DHCP**.

### Appropriate control

A switch configured with **DHCP snooping** can identify trusted DHCP-server ports and restrict unauthorized DHCP responses.

---

# 34. Detailed Security+ Scenario — DDoS

### Scenario

A public web service becomes unavailable. Network monitoring shows enormous amounts of traffic arriving from thousands of geographically distributed source systems.

### Analysis

The defining clue is the **distributed sources**.

This indicates a **DDoS attack**.

If the organization cannot absorb the traffic at its internet connection, local firewall rules may not be sufficient. Upstream DDoS mitigation may be necessary.

---

# 35. Detailed Security+ Scenario — VLAN Hopping

### Scenario

An attacker connected to a user-facing switch port attempts to gain access to traffic belonging to a server VLAN. The investigation finds that unnecessary trunking and insecure switch configuration are present.

### Analysis

The attacker is attempting to cross a VLAN boundary.

This is consistent with **VLAN hopping**.

### Mitigation

- Disable unnecessary trunking
- Explicitly configure trunk ports
- Harden native VLAN configuration
- Disable unnecessary dynamic trunk negotiation
- Apply switch security controls

---

# 36. Common Exam Mistakes

### Mistake 1: Calling every availability attack a DDoS

A service outage does not automatically mean DDoS. The question may describe a SYN flood, UDP flood, resource exhaustion, or another DoS technique.

### Mistake 2: Confusing reflection and amplification

Reflection concerns **where the traffic comes from**. Amplification concerns **how much larger the response becomes**.

### Mistake 3: Confusing ARP and DNS

ARP operates in local network address resolution. DNS resolves names into network information.

### Mistake 4: Assuming IP spoofing means the attacker can automatically receive replies

A forged source address does not automatically create bidirectional communication. Spoofing is often useful for reflection or abusing poorly designed trust relationships.

### Mistake 5: Assuming TLS prevents all network attacks

TLS protects application communication when correctly implemented and validated. It does not prevent DDoS, DHCP starvation, ARP manipulation, or physical network attacks.

### Mistake 6: Confusing rogue AP and evil twin

A rogue AP is unauthorized. An evil twin specifically imitates a legitimate wireless network.

### Mistake 7: Assuming segmentation is automatically secure

Segmentation only provides security when correctly configured and enforced. Misconfigured trunks, firewall rules, routing, or access controls can undermine it.

---

# 37. Security+ Scenario Reasoning Framework

When you encounter a network-attack scenario, use this process.

### Step 1: Identify the affected resource

Is the attack targeting:

- Availability?
- Local network traffic?
- DNS?
- DHCP?
- VLAN boundaries?
- Wireless access?
- Active sessions?

### Step 2: Identify the protocol or infrastructure component

Look for terms such as:

- TCP → SYN flood
- ARP → ARP poisoning
- DHCP → DHCP spoofing/starvation
- DNS → DNS poisoning
- VLAN → VLAN hopping
- Wireless AP → rogue AP/evil twin

### Step 3: Identify the attack behavior

Ask whether the attacker is:

- Flooding
- Spoofing
- Intercepting
- Redirecting
- Replaying
- Hijacking
- Crossing a segmentation boundary
- Introducing unauthorized infrastructure

### Step 4: Determine the security impact

Classify the main effect:

- Confidentiality
- Integrity
- Availability
- Authentication/trust

### Step 5: Select the control

Match the control to the mechanism.

Examples:

**ARP poisoning → Dynamic ARP Inspection**

**DHCP spoofing → DHCP snooping**

**VLAN hopping → secure switch/trunk configuration**

**DDoS → upstream DDoS protection**

**MITM → authenticated encryption/TLS and certificate validation**

---

# 38. Key Takeaways

1. Network attacks exploit protocols, infrastructure, trust relationships, or resource limitations.
2. DoS attacks target availability; DDoS attacks use distributed sources.
3. SYN floods abuse TCP connection establishment.
4. UDP and ICMP floods use excessive protocol traffic to consume resources.
5. Reflection uses third-party systems to send traffic toward a victim.
6. Amplification causes a relatively small request to produce a much larger response.
7. ARP poisoning manipulates local IP-to-MAC mappings.
8. DHCP spoofing uses unauthorized DHCP responses to provide malicious configuration.
9. DHCP starvation consumes available address leases.
10. MAC flooding targets switch MAC-address learning.
11. VLAN hopping attempts to cross VLAN boundaries.
12. IP spoofing forges the apparent source IP address.
13. MITM attacks place an attacker between communicating parties.
14. Session hijacking targets valid authenticated sessions.
15. Replay attacks reuse captured valid communication.
16. DNS poisoning provides false name-resolution information.
17. Rogue devices create unauthorized network paths.
18. Evil twins imitate legitimate wireless networks.
19. Strong encryption and authentication protect communication, while infrastructure controls and segmentation address different attack classes.
20. Security+ questions are often solved by identifying the **protocol, attack behavior, affected layer, security impact, and matching mitigation**.
