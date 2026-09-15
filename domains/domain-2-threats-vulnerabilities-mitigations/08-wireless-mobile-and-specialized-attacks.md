# Wireless, Mobile, and Specialized Attacks

## 1. Wireless Attacks

Wireless networks extend the attack surface beyond physically connected ports. Attackers may target authentication, encryption, access points, management frames, or users.

### Evil Twin
A fraudulent wireless access point imitates a legitimate network. Victims may connect to it and expose traffic or credentials.

### Rogue Access Point
An unauthorized access point is connected to or operated within an organization's environment. It creates an unmanaged network path.

### Deauthentication/Disassociation Attacks
Management frames can be abused to disrupt wireless connections. Protected management frames in modern wireless standards reduce this risk.

### Wi-Fi Security
WPA2 and WPA3 provide stronger protections than obsolete protocols such as WEP. Enterprise wireless deployments can use centralized authentication such as 802.1X/EAP.

## 2. Bluetooth Attacks

Bluetooth-enabled systems can be exposed through pairing weaknesses, unauthorized connections, malicious devices, or vulnerable implementations. Keep Bluetooth disabled when unnecessary, use current device firmware, use secure pairing, and restrict discoverability where appropriate.

## 3. Mobile Device Attacks

Mobile devices contain credentials, applications, communications, sensors, and organizational data. Risks include malicious applications, outdated operating systems, insecure configurations, phishing, lost devices, SIM-related attacks, and unauthorized profiles.

### SIM Swapping
An attacker convinces a telecommunications provider to transfer a victim's mobile number to another SIM. This can allow interception of SMS-based authentication and account-recovery messages.

Use stronger authentication methods that do not depend solely on SMS and protect carrier-account changes.

### Malicious Applications
Untrusted applications may steal information, abuse permissions, or perform unwanted actions. Use managed application sources, mobile device management, application allowlisting where appropriate, and permission controls.

## 4. NFC and Proximity Technologies

Near-field communication can support payments, identification, and device interactions. Risks include unauthorized transactions, malicious tags, relay scenarios, and misuse of device permissions. Use transaction confirmation, secure application design, and platform security controls.

## 5. IoT and Specialized Devices

IoT devices often have limited processing capacity, long lifecycles, default credentials, weak management interfaces, and inconsistent patching. Security measures include unique credentials, network segmentation, secure firmware, asset inventory, restricted management access, and replacement of unsupported devices.

## 6. Security+ Exam Focus

Know the distinction between an evil twin and a rogue AP: an evil twin impersonates a legitimate wireless network to deceive clients, while a rogue AP is an unauthorized access point in the environment. Understand that mobile security requires both technical controls and lifecycle management.

## 7. Key Takeaways

Wireless, mobile, and specialized technologies should be treated as part of the enterprise attack surface. Secure authentication, encryption, segmentation, device management, patching, and continuous inventory reduce risk.
