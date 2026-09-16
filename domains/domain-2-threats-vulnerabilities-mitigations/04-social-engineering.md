# 04 — Social Engineering

## 1. Introduction to Social Engineering

**Social engineering** is the use of deception, manipulation, persuasion, or psychological influence to cause a person to disclose information, perform an action, grant access, transfer money, or weaken a security control.

A social engineering attack does not necessarily require the attacker to exploit a software vulnerability. Instead, the attacker exploits the **human decision-making process**.

This is important because organizations can have strong firewalls, endpoint protection, encryption, and access controls and still be compromised if an employee is persuaded to bypass those protections.

A useful model is:

**Information gathering → Establish trust → Create pressure → Request action → Exploit the result**

For example, an attacker may research an employee, impersonate the employee's manager, claim that an urgent payment is required, and persuade the employee to transfer money.

The technical system may function exactly as designed. The problem is that a legitimate user was manipulated into authorizing an unsafe action.

---

# 2. Why Social Engineering Works

Humans routinely make decisions using shortcuts. Attackers deliberately exploit those shortcuts.

Common psychological triggers include:

- **Authority** — pretending to be a manager, executive, administrator, police officer, or other authority figure.
- **Urgency** — creating a time limit so the victim does not stop to verify the request.
- **Fear** — threatening account suspension, legal consequences, financial loss, or other negative outcomes.
- **Curiosity** — offering information that the victim wants to investigate.
- **Trust** — impersonating a known person, organization, or service.
- **Familiarity** — using information that makes the attacker appear to know the victim or organization.
- **Scarcity** — claiming that an opportunity is available only briefly.
- **Reciprocity** — offering assistance or a benefit in exchange for information or action.
- **Social pressure** — making refusal appear rude, inconvenient, or harmful to the team.

### Example

A message says:

> "Your account will be disabled in 30 minutes. Click here immediately to verify your password."

The message is attempting to bypass careful reasoning by combining **urgency, fear, and authority**.

The important defensive response is to stop and independently verify the request rather than reacting to the emotional pressure.

---

# 3. Phishing

**Phishing** is a social engineering technique in which an attacker sends a fraudulent message designed to persuade a victim to perform an unsafe action.

The message may attempt to make the victim:

- Click a malicious link
- Open an attachment
- Enter credentials
- Approve an authentication request
- Transfer money
- Provide confidential information
- Install software
- Contact the attacker

Phishing can be delivered through email and other communication channels.

### Typical phishing flow

**Fraudulent message → Victim interaction → Credential/data theft or malicious execution → Attacker access**

### Common phishing indicators

- Unexpected request
- Urgent language
- Suspicious sender address
- Domain impersonation
- Unexpected attachment
- Mismatched links
- Requests for credentials
- Unusual payment instructions
- Poor grammar or unusual wording

Not every phishing message contains obvious spelling errors. Modern phishing campaigns can be professionally written and may use information gathered from public sources.

---

# 4. Spear Phishing

**Spear phishing** is a targeted form of phishing aimed at a specific person, group, or organization.

Instead of sending the same message to thousands of random recipients, the attacker customizes the communication.

Information may be gathered from:

- Company websites
- Social media
- Public documents
- Professional profiles
- Previous data breaches
- Organizational information

### Example

An attacker discovers that an employee works in the finance department and that the company's CFO is attending a conference. The attacker sends a carefully crafted email appearing to come from the CFO and requests an urgent invoice payment.

The attack is more convincing because it contains relevant organizational information.

### Key exam distinction

**Phishing = broad/fraudulent communication**

**Spear phishing = targeted/customized phishing**

---

# 5. Whaling

**Whaling** is a targeted social engineering attack directed at a high-value individual, commonly a senior executive or other decision maker.

Executives may have:

- Broad access
- Approval authority
- Financial authority
- Access to sensitive information
- Ability to authorize transactions

Therefore, successfully impersonating an executive can have significant consequences.

### Example

An attacker sends a carefully prepared message to a company's finance manager appearing to come from the CEO and requests a confidential acquisition payment.

The defining clue is the **high-value target**, not simply the use of email.

---

# 6. Business Email Compromise (BEC)

**Business Email Compromise (BEC)** involves the compromise or impersonation of a business email account or business identity to deceive employees into performing actions that benefit the attacker.

Common objectives include:

- Fraudulent payments
- Changing payment instructions
- Theft of credentials
- Sensitive information disclosure
- Payroll redirection
- Unauthorized purchases

BEC frequently combines technical compromise with social engineering.

### Example

An attacker compromises an executive's account and sends a message to the finance team requesting that a vendor payment be sent to a new bank account.

The finance employee may see a legitimate-looking account and follow the request.

### Important defense

High-risk requests should be verified through an **independent communication channel**.

For example, if a payment instruction arrives by email, the employee should confirm the request using a previously trusted phone number or another established communication method rather than replying to the suspicious email.

---

# 7. Vishing

**Vishing** means **voice phishing**.

The attacker uses a phone call, voicemail, or another voice-based interaction to manipulate the victim.

The attacker may impersonate:

- Bank employees
- IT support
- Government representatives
- Company executives
- Vendors
- Customers

### Example

A caller claims to be from the organization's IT department and says the employee's account has been compromised. The caller asks for a verification code.

The attack is attempting to obtain an authentication factor through social manipulation.

### Exam clue

If the primary delivery channel is **voice/phone**, think **vishing**.

---

# 8. Smishing

**Smishing** is phishing delivered through SMS or mobile messaging.

Common messages may impersonate:

- Banks
- Delivery companies
- Government services
- Employers
- Financial services
- Online accounts

The message may contain a malicious link or request sensitive information.

### Example

A victim receives an SMS stating that a package cannot be delivered and must be rescheduled through a provided link. The link leads to a fraudulent login page.

### Exam clue

**SMS/mobile message → Smishing**

---

# 9. Pharming

**Pharming** redirects users to a fraudulent destination even when the user believes they are accessing a legitimate service.

The user may enter the correct address but still be directed somewhere malicious because the underlying name-resolution or host environment has been manipulated.

Possible contributing mechanisms include:

- DNS manipulation
- Compromised hosts
- Modified local resolution information
- Compromised infrastructure

### Phishing vs pharming

**Phishing:** the attacker generally relies on a fraudulent message or lure to direct the victim.

**Pharming:** the attacker manipulates the destination or name-resolution path so the victim is redirected even though the victim may believe the requested destination is legitimate.

---

# 10. Pretexting

**Pretexting** involves creating a fabricated story, identity, or situation to persuade a victim to provide information or perform an action.

The attacker establishes a believable **pretext**.

### Example

An attacker calls an employee and claims to be a new member of the IT support team. The attacker says a security migration requires the employee's username and verification information.

The attacker is not simply sending a malicious link. The attacker is constructing a believable scenario.

### Key clue

If a question emphasizes a **fabricated identity or believable story**, consider **pretexting**.

---

# 11. Baiting

**Baiting** uses something tempting to persuade a victim to take an unsafe action.

The lure may be:

- Free software
- Interesting files
- A promised reward
- A supposedly useful document
- A removable storage device
- A tempting download

### Example

An attacker leaves a removable drive labeled with an interesting business-related name in an area where employees may find it. A curious employee connects it to a workstation.

The physical object is the **bait**.

### Security lesson

Baiting often exploits **curiosity or desire for a benefit** rather than authority or urgency.

---

# 12. Quid Pro Quo

**Quid pro quo** means an attacker offers a benefit, service, or assistance in exchange for information or access.

The attacker creates an apparent exchange:

**"I will give you something if you give me something."**

### Example

An attacker contacts an employee pretending to provide technical support and offers to fix a nonexistent problem in exchange for authentication information.

### Distinction from baiting

- **Baiting:** the lure itself attracts the victim.
- **Quid pro quo:** the attacker explicitly offers a benefit or service in exchange for something.

---

# 13. Tailgating

**Tailgating** is a physical social engineering technique in which an unauthorized person follows an authorized person into a restricted area without proper authorization.

### Example

An employee opens a secure office door using an access card. An unauthorized person follows immediately behind while pretending to be in a hurry.

The attacker is exploiting normal human politeness and the physical access-control process.

### Defenses

- Badge readers
- Security personnel
- Mantraps
- Visitor controls
- Access logs
- Security awareness
- Policies requiring individual authentication

---

# 14. Piggybacking

**Piggybacking** is closely related to tailgating but generally implies that the authorized person knowingly permits the other individual to enter.

For example, an employee may intentionally hold a secure door open for someone who says they forgot their badge.

### Important terminology note

Security terminology can vary between sources. For exam questions, focus on the scenario's defining behavior rather than becoming overly dependent on a subtle wording distinction between tailgating and piggybacking.

---

# 15. Shoulder Surfing

**Shoulder surfing** occurs when an attacker obtains sensitive information by observing a victim directly.

Targets may include:

- Passwords
- PINs
- Authentication codes
- Confidential documents
- Screens

The attacker does not necessarily need malware or network access.

### Example

A person watches an employee enter a PIN at an ATM or observes a password being typed in a public location.

### Defenses

- Privacy screens
- Awareness training
- Physical positioning
- Secure handling of credentials
- Avoiding sensitive activities in exposed environments

---

# 16. Dumpster Diving

**Dumpster diving** is the process of examining discarded materials for information that can support an attack.

Potentially valuable material includes:

- Printed reports
- Employee lists
- Contact information
- System documentation
- Network diagrams
- Shipping labels
- Storage devices
- Discarded hardware

### Security lesson

Information does not stop being sensitive simply because an organization has discarded it.

Organizations should establish appropriate disposal procedures, including secure destruction or sanitization where required.

---

# 17. Watering-Hole Attack

A **watering-hole attack** compromises a website or online resource that members of a particular target group are likely to visit.

The attacker does not necessarily need to contact the target directly.

### Simplified flow

**Identify target group → Identify commonly visited resource → Compromise resource → Target visits → Malicious content delivered**

### Example

Attackers identify a specialized industry website frequently used by employees of a particular organization. The attackers compromise the website so that visitors encounter malicious content.

The term comes from the idea that attackers wait at a place their targets naturally visit.

---

# 18. Impersonation

**Impersonation** occurs when an attacker pretends to be another person or trusted entity.

The attacker may impersonate:

- An executive
- IT support
- A vendor
- A customer
- A bank representative
- A government official
- A coworker

Impersonation can occur through email, phone calls, messaging, or face-to-face interaction.

The defining concept is **pretending to be someone trusted**.

---

# 19. Influence Techniques in Social Engineering

Attackers often combine several psychological techniques.

### Authority

The attacker claims to represent someone with power or expertise.

### Urgency

The attacker creates a short deadline to prevent verification.

### Fear

The victim is threatened with loss, punishment, or account suspension.

### Curiosity

The attacker provides an interesting subject or mysterious file.

### Familiarity

The attacker uses known names, organizations, terminology, or previous interactions.

### Scarcity

The attacker claims that an opportunity is limited.

### Reciprocity

The attacker gives or promises something and expects cooperation in return.

### Social proof

The attacker claims that other employees have already completed the requested action.

### Commitment and consistency

The attacker gets the victim to agree to small requests and then escalates the request.

The key defensive principle is to recognize when a request is deliberately trying to influence the decision-making process rather than simply communicate information.

---

# 20. Information Gathering Before Social Engineering

Successful social engineering often begins before the victim is contacted.

Attackers may gather information from publicly available sources, organizational websites, social media, professional profiles, leaked information, or previously compromised data.

Useful information to an attacker may include:

- Employee names
- Job titles
- Reporting relationships
- Email formats
- Office locations
- Vendors
- Technologies used
- Business processes
- Public projects
- Travel information

This information can make a fraudulent message appear more legitimate.

### Defensive response

Organizations should understand what information is publicly exposed and determine whether unnecessary information should be removed or restricted.

---

# 21. Social Engineering Attack Chain

A social engineering campaign can be analyzed as a sequence:

**Reconnaissance → Target selection → Pretext/lure → Contact → Victim action → Initial access or information disclosure → Follow-on activity**

### Example

1. The attacker identifies a finance employee.
2. The attacker learns the organization's email naming convention.
3. The attacker identifies a senior executive.
4. The attacker creates a believable payment request.
5. The employee receives the message.
6. The employee follows the request.
7. The attacker gains financial or account-related benefit.

The social engineering step is not necessarily the final objective. It can be the mechanism used to obtain credentials, access, money, or another capability.

---

# 22. Detection of Social Engineering

Detection requires both technical and human controls.

### Email indicators

- Unexpected sender
- Domain impersonation
- Suspicious links
- Unexpected attachments
- Urgent requests
- Requests for credentials
- Unusual payment instructions
- Requests that bypass normal procedures

### Identity indicators

- Unexpected password-reset request
- Unusual MFA approval request
- Authentication from unexpected locations
- New account recovery information
- Suspicious privilege requests

### Business-process indicators

- Sudden payment-account changes
- Requests to bypass approval procedures
- Unusual wire transfers
- Urgent requests outside normal workflow
- Vendor banking changes without independent confirmation

### Physical indicators

- Unknown people in restricted areas
- Attempts to borrow badges
- Unauthorized visitors
- Unusual interest in sensitive screens or documents

---

# 23. Mitigation and Defense

Social engineering cannot be solved by technology alone. Effective defense combines **people, processes, and technology**.

## 23.1 Security Awareness Training

Employees should learn to identify suspicious requests, verify unusual instructions, report suspected attacks, and understand that attackers may impersonate trusted people.

Training should be reinforced rather than treated as a one-time event.

## 23.2 Independent Verification

High-risk requests should be verified using a communication channel independent of the suspicious request.

For example:

**Email payment change → call the known vendor contact using an established number.**

Do not simply reply to the suspicious message because the attacker may control the communication channel.

## 23.3 Strong Authentication

MFA reduces the consequences of password theft. Where practical, phishing-resistant authentication provides stronger protection against credential-phishing attacks than relying only on passwords or easily phished codes.

## 23.4 Email and Web Security

Controls can include:

- Spam filtering
- Phishing detection
- URL reputation checks
- Attachment analysis
- Malware scanning
- Domain protection
- Browser protections

## 23.5 Least Privilege

A manipulated account should have only the access necessary for its role.

Least privilege limits the damage that can result when an attacker successfully convinces a user to perform an unsafe action.

## 23.6 Physical Security

Organizations should use:

- Badge access
- Visitor management
- Security guards where appropriate
- Cameras
- Mantraps
- Access logs
- Clean-desk procedures

## 23.7 Financial Controls

Financial processes should include appropriate separation of duties, approval requirements, and independent verification for sensitive transactions.

This is particularly important for defending against BEC.

---

# 24. Scenario Analysis

### Scenario 1

An employee receives an email from an unknown sender containing a link that requests Microsoft 365 credentials.

**Likely technique:** Phishing.

The primary clues are a fraudulent message and a request for credentials.

---

### Scenario 2

The message is specifically customized for the company's CFO and references an upcoming acquisition.

**Likely technique:** Spear phishing.

If the target is specifically a senior executive, the scenario may additionally be described as **whaling**.

---

### Scenario 3

An attacker calls an employee and claims to be from IT support, requesting an authentication code.

**Likely technique:** Vishing, potentially combined with impersonation and pretexting.

---

### Scenario 4

An employee receives a text message claiming that a bank account will be locked unless a provided link is opened.

**Likely technique:** Smishing.

The defining clue is the SMS/mobile delivery channel.

---

### Scenario 5

A person claims to be a new IT employee and invents a system migration story to convince an employee to reveal information.

**Likely technique:** Pretexting.

The defining clue is the fabricated scenario or identity.

---

### Scenario 6

An attacker leaves an interesting USB device where employees can easily find it.

**Likely technique:** Baiting.

The device is the tempting lure.

---

### Scenario 7

An unauthorized individual follows an employee through a secured entrance without using an access badge.

**Likely technique:** Tailgating.

The defining feature is unauthorized physical entry by following an authorized person.

---

# 25. Social Engineering Comparison Table

| Technique | Defining characteristic | Typical channel |
|---|---|---|
| Phishing | Fraudulent message intended to manipulate a victim | Email/messaging |
| Spear phishing | Targeted phishing | Email/messaging |
| Whaling | Targeted at senior/high-value individuals | Email/messaging |
| Vishing | Voice-based phishing | Phone/voice |
| Smishing | SMS/mobile phishing | Text message |
| Pharming | Redirects victim to fraudulent destination | DNS/host/network |
| Pretexting | Fabricated story or identity | Any channel |
| Baiting | Tempting lure causes unsafe action | Physical/digital |
| Quid pro quo | Benefit/service offered in exchange for information or action | Any channel |
| Tailgating | Unauthorized person follows authorized person into restricted area | Physical |
| Piggybacking | Authorized person knowingly permits another person's entry | Physical |
| Shoulder surfing | Direct observation of sensitive information | Physical |
| Dumpster diving | Searching discarded material for useful information | Physical |
| Watering hole | Compromises a resource frequently visited by targets | Web |
| BEC | Business identity/account used for fraud or sensitive actions | Email/business communication |
| Impersonation | Pretending to be a trusted person/entity | Any channel |

---

# 26. Common Exam Traps

### Trap 1: Phishing vs spear phishing

Do not focus only on the presence of an email.

Ask whether the attack is **generic or specifically targeted**.

### Trap 2: Spear phishing vs whaling

Whaling is a targeted form of phishing directed at a high-value individual, commonly an executive.

### Trap 3: Vishing vs smishing

Look at the communication channel:

- Voice → vishing
- SMS → smishing

### Trap 4: Baiting vs quid pro quo

- Baiting → tempting lure
- Quid pro quo → promised benefit/service in exchange for cooperation

### Trap 5: Tailgating vs shoulder surfing

- Tailgating → unauthorized physical entry
- Shoulder surfing → observing sensitive information

### Trap 6: Phishing vs pharming

- Phishing → fraudulent lure/message
- Pharming → fraudulent redirection/destination

### Trap 7: Training as the only defense

Security awareness is important, but it should be combined with technical and procedural controls.

---

# 27. Security+ Scenario Reasoning Framework

When a question presents a social engineering scenario, ask these questions in order:

### Question 1: What is being manipulated?

Is the attacker targeting:

- Credentials?
- Money?
- Information?
- Physical access?
- Software execution?
- Trust?

### Question 2: What communication channel is used?

- Email → phishing family
- Voice → vishing
- SMS → smishing
- Physical interaction → physical social engineering

### Question 3: Is the attack targeted?

- Broad audience → phishing
- Specific individual/group → spear phishing
- Senior executive/high-value person → whaling

### Question 4: What psychological mechanism is being used?

Look for authority, urgency, fear, curiosity, scarcity, familiarity, or reciprocity.

### Question 5: What action is the attacker trying to cause?

Examples:

- Enter credentials
- Approve authentication
- Transfer money
- Open an attachment
- Install software
- Reveal information
- Allow physical access

### Question 6: What is the appropriate control?

Choose the control that directly addresses the scenario.

For example:

- Suspicious payment request → independent verification
- Phishing email → email filtering and awareness
- Stolen credentials → MFA
- Tailgating → physical access controls
- Excessive user privileges → least privilege

---

# 28. Practical Defensive Mindset

A useful organizational rule is:

> **Trust should be verified when the requested action is unusual, sensitive, or high impact.**

Employees should not be trained simply to identify suspicious-looking emails. They should understand **when to stop and verify**.

For example, even if a message appears to come from a legitimate executive, a request to change payment details should still follow the organization's verification process.

This approach is stronger than relying on visual inspection alone because attackers can make fraudulent communications increasingly convincing.

---

# 29. Key Takeaways

1. Social engineering attacks exploit human behavior rather than relying exclusively on technical vulnerabilities.
2. Phishing uses fraudulent communications to manipulate victims.
3. Spear phishing is targeted and customized.
4. Whaling targets high-value individuals, commonly executives.
5. Vishing uses voice communication.
6. Smishing uses SMS or mobile messaging.
7. Pharming involves redirection to a fraudulent destination.
8. Pretexting uses a fabricated story or identity.
9. Baiting uses a tempting lure.
10. Quid pro quo offers a benefit or service in exchange for cooperation.
11. Tailgating and piggybacking concern unauthorized physical access.
12. Shoulder surfing relies on direct observation.
13. Dumpster diving searches discarded material for useful information.
14. Watering-hole attacks compromise resources frequently visited by the target group.
15. BEC commonly targets business processes such as payments, credentials, or sensitive information.
16. Social engineering defenses require people, processes, and technology.
17. Independent verification is especially important for high-risk requests.
18. Strong authentication can reduce the consequences of credential theft but does not eliminate social engineering.
19. Security+ questions often depend on identifying the **channel, target, psychological technique, and requested action**.
