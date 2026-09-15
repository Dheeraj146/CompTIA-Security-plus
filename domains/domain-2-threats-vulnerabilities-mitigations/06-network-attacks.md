# Network Attacks

## 1. Overview

Network attacks target the availability, confidentiality, integrity, or trust relationships of network communications and infrastructure.

## 2. Denial-of-Service Attacks

A DoS attack attempts to make a service unavailable by exhausting processing capacity, memory, bandwidth, connections, or another resource. A DDoS attack distributes the traffic or requests across many systems, making the attack larger and more difficult to block at a single source.

### Common Patterns

- **SYN flood:** abuses the TCP connection-establishment process by creating large numbers of incomplete connections.
- **UDP flood:** overwhelms a target with UDP traffic.
- **ICMP flood:** generates excessive ICMP traffic.
- **Reflection:** causes third-party systems to send responses toward the victim.
- **Amplification:** a small request results in a much larger response, increasing attack volume.

Mitigation can include rate limiting, filtering, load balancing, upstream DDoS protection, resilient architecture, and sufficient capacity.

## 3. Address Resolution and Local Network Attacks

### ARP Spoofing/Poisoning
False ARP information causes systems to associate an attacker's MAC address with another IP address. This can facilitate interception or disruption of local traffic.

Defenses include dynamic ARP inspection, DHCP snooping, segmentation, secure switch configuration, and encryption at higher layers.

### DHCP Spoofing
A rogue DHCP server provides malicious or incorrect network configuration to clients. DHCP snooping and trusted-port configuration help prevent unauthorized DHCP responses.

### DHCP Starvation
An attacker consumes available DHCP leases, potentially preventing legitimate clients from receiving addresses. Switch controls and DHCP infrastructure protections can reduce the risk.

### MAC Flooding
Excessive MAC addresses are presented to a switch, potentially causing the switch to behave less selectively with traffic. Port security and MAC limits can mitigate this attack.

## 4. VLAN Attacks

VLAN hopping attempts to access traffic belonging to another VLAN. Secure switch configuration, disabling unnecessary trunking, explicitly configuring trunk ports, and using appropriate native-VLAN practices reduce exposure.

## 5. Spoofing

IP spoofing uses a forged source IP address. It can support reflection attacks, bypass poorly designed trust relationships, or obscure the apparent source of traffic. Ingress and egress filtering can reduce spoofed traffic.

## 6. Man-in-the-Middle Attacks

A MITM attack places an attacker between communicating parties so traffic can potentially be observed or manipulated. TLS, certificate validation, secure VPNs, network segmentation, and authenticated protocols help prevent successful interception.

## 7. Session Hijacking and Replay

Session hijacking occurs when an attacker obtains or takes control of a valid session. Replay attacks reuse previously captured authentication or transaction data. Short-lived tokens, secure session handling, TLS, nonce mechanisms, and reauthentication help reduce risk.

## 8. DNS Attacks

DNS poisoning or spoofing causes users to receive incorrect name-resolution results. DNSSEC can provide authenticity for DNS data, while secure resolver configuration, monitoring, and encrypted application protocols provide additional protection.

## 9. Rogue Devices

Unauthorized access points, switches, routers, or other network devices can create unmonitored paths into the environment. Network access control, asset inventory, wireless monitoring, and switch security help identify and prevent rogue infrastructure.

## 10. Security+ Exam Focus

Recognize the layer and mechanism involved. ARP attacks concern local address resolution; DHCP attacks concern network configuration assignment; DNS attacks concern name resolution; VLAN hopping concerns segmentation boundaries; SYN floods exploit TCP connection handling; DDoS uses distributed sources.

## 11. Key Takeaways

Network defense is strongest when layered: secure protocols protect data, segmentation limits movement, infrastructure controls prevent unauthorized connections, monitoring identifies anomalies, and resilient architecture limits availability impact.
