# Privacy and Data Governance

## 1. Why Privacy and Data Governance Matter

Data is one of an organization's most valuable assets, but it can also create significant security, legal, regulatory, operational, and reputational risk.

Organizations collect and process information about:

- Customers
- Employees
- Contractors
- Suppliers
- Users
- Patients
- Students
- Business partners

This information may include:

- Names
- Contact information
- Identification information
- Financial information
- Health information
- Authentication information
- Location information
- Employment records
- Behavioral information

Security protects information against unauthorized access, alteration, disclosure, destruction, and interruption.

**Privacy** focuses on the appropriate handling of information about individuals.

**Data governance** establishes who is accountable for data, how data is classified, how it should be handled, how long it should be retained, and how decisions about it are made.

A useful mental model is:

**Data → Classification → Ownership → Handling → Access → Use/Sharing → Retention → Disposal**

Privacy and governance therefore affect the entire data lifecycle.

---

## 2. Privacy vs Security

Privacy and security are closely related but not identical.

### Security

Security asks:

> How do we protect information and systems from unauthorized access, alteration, disclosure, destruction, or disruption?

Security controls include:

- Encryption
- Access control
- MFA
- Network segmentation
- Logging
- EDR
- Backups

### Privacy

Privacy asks:

> Is information about individuals being collected, used, shared, retained, and disposed of appropriately?

Privacy considerations can include:

- Purpose of collection
- Transparency
- Consent or other lawful basis where applicable
- Data minimization
- Access
- Correction
- Retention
- Deletion
- Sharing
- Individual rights

A system can be technically secure while still creating a privacy problem.

For example:

> An application securely encrypts every customer record but collects far more personal information than is necessary for its stated purpose.

The encryption provides security, but unnecessary collection can still create a privacy concern.

---

## 3. Data Governance

**Data governance** is the organizational framework for managing data throughout its lifecycle.

It establishes:

- Ownership
- Accountability
- Classification
- Access rules
- Quality requirements
- Retention
- Protection
- Sharing
- Compliance
- Disposal
- Decision-making authority

Data governance answers questions such as:

- Who owns this data?
- How sensitive is it?
- Who may access it?
- Where may it be stored?
- How may it be shared?
- How long should it be retained?
- When should it be deleted?
- What requirements apply?

Without governance, data-handling decisions may be inconsistent across departments.

---

## 4. Data Ownership

A **data owner** is accountable for a particular dataset or category of information.

The data owner generally makes decisions about:

- Classification
- Access requirements
- Protection requirements
- Retention
- Sharing
- Risk acceptance related to the data

The owner is usually a business role rather than simply the person who technically stores the information.

### Example

The HR department may own employee records.

The IT team may operate the database storing those records.

Therefore:

**HR = data owner**

**IT/database team = data custodian**

The exact organizational structure can differ, but the distinction is important.

---

## 5. Data Custodian

A **data custodian** is responsible for the operational and technical handling of data according to the owner's requirements.

Responsibilities may include:

- Storage
- Backup
- Access implementation
- Encryption
- Technical security
- Availability
- Data transfer
- Recovery

The custodian generally does not independently decide the organization's business classification or access policy.

Example:

The data owner states:

> Only the payroll department may access payroll records.

The custodian implements the technical controls necessary to enforce that requirement.

---

## 6. Data Controller and Data Processor

Privacy programs may also use the concepts of **data controller** and **data processor**, particularly in privacy frameworks and laws.

The terminology and legal meaning depend on the applicable jurisdiction.

Generally:

### Controller

Determines important purposes and means of processing personal data.

### Processor

Processes personal data on behalf of the controller.

Example:

**Company → Cloud HR platform**

The company may determine why employee information is processed.

The HR platform may process the information on behalf of the company.

These terms should not automatically be treated as identical to data owner and data custodian.

They describe different governance relationships.

---

## 7. Data Classification

**Data classification** assigns a sensitivity or handling category to information.

Common organizational categories include:

- Public
- Internal
- Confidential
- Restricted

Organizations may use different names.

The purpose is to determine how data should be protected.

For example:

### Public

Information intentionally available to the public.

Examples:

- Public website content
- Published marketing material

### Internal

Information intended for organizational use.

Examples:

- Internal procedures
- Internal communications

### Confidential

Information that could cause significant harm if disclosed.

Examples:

- Business plans
- Customer information
- Internal financial information

### Restricted

Highly sensitive information requiring stronger controls.

Examples:

- Authentication secrets
- Highly sensitive personal information
- Certain regulated information
- Cryptographic keys

The exact categories must be defined by the organization.

---

## 8. Classification vs Ownership

These concepts are frequently confused.

### Classification

Answers:

> How sensitive is this information and how must it be handled?

### Ownership

Answers:

> Who is accountable for decisions about this information?

Example:

> Payroll records are classified as Restricted.

This describes sensitivity.

> The HR director is the data owner.

This identifies accountability.

A data owner may determine the appropriate classification and handling requirements.

---

## 9. Data Handling Requirements

Classification should translate into practical handling requirements.

For sensitive data, requirements may include:

- Encryption
- MFA
- Restricted access
- Network segmentation
- Approved storage locations
- Secure transmission
- DLP
- Logging
- Retention limits
- Secure disposal

For example:

**Restricted data**
→ Encrypt at rest
→ Encrypt in transit
→ Restrict access
→ Log access
→ Retain only as required
→ Securely destroy when no longer needed

Classification is therefore useful only when it drives actual controls.

---

## 10. Data Lifecycle

A common data lifecycle is:

**Create/Collect**
↓
**Store**
↓
**Use**
↓
**Share/Process**
↓
**Archive/Retain**
↓
**Securely Dispose**

Security and privacy controls should apply throughout the lifecycle.

The risk changes at each stage.

For example:

- Collection creates initial privacy exposure.
- Storage creates unauthorized-access risk.
- Sharing creates third-party risk.
- Retention creates long-term exposure.
- Disposal creates residual-data risk.

---

## 11. Data Collection

Organizations should understand:

- What information is being collected?
- Why is it needed?
- Who is collecting it?
- How is it collected?
- Where will it be stored?
- What legal or organizational requirements apply?

Collection should have a defined business or legal purpose.

Collecting information simply because it might be useful later can increase:

- Breach impact
- Storage costs
- Compliance obligations
- Privacy risk

This leads directly to **data minimization**.

---

## 12. Data Minimization

**Data minimization** means collecting, processing, and retaining only the information necessary for an identified legitimate purpose.

Example:

An application needs to verify whether a customer is over a certain age.

If the application only needs an eligibility result, storing the customer's complete identity document indefinitely may create unnecessary risk.

Data minimization reduces:

- Attack surface
- Breach impact
- Storage requirements
- Privacy exposure
- Unnecessary processing

It is both a privacy and security principle.

---

## 13. Purpose Limitation

Data should be used consistently with the defined purpose and applicable requirements.

Example:

An organization collects an employee's contact information to administer employment.

Using that information for an unrelated purpose without appropriate authority or legal basis may create a privacy concern.

Purpose limitation helps prevent organizations from treating collected data as unrestricted organizational property.

The exact legal requirements depend on the applicable jurisdiction and context.

---

## 14. Transparency

Individuals may need to understand how their information is handled.

Depending on applicable requirements, organizations may provide information about:

- What data is collected
- Why it is collected
- How it is used
- Who receives it
- How long it is retained
- How individuals can exercise applicable rights

Transparency helps individuals understand the organization's data practices.

---

## 15. Consent and Other Legal Bases

Some privacy regimes use **consent** as one possible legal basis for processing personal information.

However, consent is not universally required for every processing activity.

Other legal bases may exist depending on the applicable law, such as:

- Contractual necessity
- Legal obligations
- Legitimate interests
- Vital interests
- Public-interest grounds

Security+ questions may use simplified examples, but real-world privacy decisions should be evaluated against the applicable jurisdiction and legal requirements.

A common mistake is assuming:

> "Every collection of personal data requires consent."

That is not universally correct.

---

## 16. Data Subject Rights

Applicable privacy laws may provide individuals with rights concerning their personal information.

Depending on the jurisdiction, these may include rights related to:

- Access
- Correction
- Deletion
- Portability
- Restriction
- Objection
- Automated decision-making

The exact rights, exceptions, and procedures vary.

Organizations therefore need processes for identifying applicable rights and responding within required timeframes.

---

## 17. Data Retention

**Data retention** defines how long information should be kept.

Retention requirements may depend on:

- Legal obligations
- Business requirements
- Contracts
- Litigation holds
- Regulatory requirements
- Operational needs
- Security considerations

Keeping data forever is not automatically safer.

Long retention can increase:

- Breach impact
- Storage cost
- Privacy exposure
- Discovery burden

Retention should therefore be intentional.

---

## 18. Data Disposal

When information is no longer required, it should be disposed of according to applicable requirements.

Methods can include:

- Secure deletion
- Cryptographic erasure
- Media sanitization
- Physical destruction
- Secure shredding

The method depends on the medium and sensitivity.

For example, deleting a file from a normal filesystem may not guarantee that all recoverable remnants are eliminated.

Sensitive data may require stronger sanitization.

---

## 19. Data Lifecycle and Backup Copies

A common mistake is assuming that deleting production data means all copies have been deleted.

Data may exist in:

- Primary databases
- Backups
- Snapshots
- Archives
- Replicas
- Logs
- Caches
- Cloud storage
- Vendor systems

Retention and deletion policies should consider the complete lifecycle and relevant copies.

Legal and operational requirements may also affect when backup data can be deleted.

---

## 20. Data Residency

**Data residency** refers to where data is physically or logically stored, depending on the context.

Organizations may need to understand:

- Country
- Region
- Cloud location
- Backup location
- Disaster-recovery location
- Vendor processing locations

Residency can matter because different jurisdictions may impose different requirements.

An organization should not assume that:

> "The application is hosted in our country, so all data must be there."

Backups, support systems, subprocessors, and analytics services may operate elsewhere.

---

## 21. Data Sovereignty

**Data sovereignty** generally concerns the legal authority and jurisdiction applicable to data based on where it is located or processed and the applicable laws.

Data may be subject to laws of the jurisdiction where it resides or is processed.

This creates considerations for:

- Cloud services
- Global organizations
- Cross-border transfers
- International vendors

Residency and sovereignty are related but should not be treated as exactly identical concepts.

---

## 22. Cross-Border Data Transfers

Organizations operating internationally may transfer personal information across jurisdictions.

Security and privacy teams may need to evaluate:

- Applicable transfer requirements
- Contractual safeguards
- Data location
- Vendor processing
- Encryption
- Access controls
- Government-access considerations

The appropriate legal mechanism depends on the jurisdictions involved.

Security+ reasoning should focus on recognizing that **cross-border processing can introduce additional privacy and compliance considerations**.

---

## 23. Privacy by Design

**Privacy by design** means incorporating privacy considerations into systems and processes from the beginning rather than attempting to add them after deployment.

Design decisions can include:

- Data minimization
- Purpose limitation
- Access restrictions
- Encryption
- Retention controls
- Deletion mechanisms
- Transparency
- Privacy-preserving defaults

Example:

Instead of building an application that collects every possible customer attribute and later asking how to protect it, the development team first determines which information is actually necessary.

---

## 24. Privacy by Default

Privacy by default means that systems should use appropriately protective settings without requiring users to manually enable every protection.

Examples:

- Minimal default data collection
- Restricted sharing defaults
- Limited visibility
- Shorter default retention where appropriate
- Privacy-preserving configuration

This reduces dependence on users remembering complex privacy settings.

---

## 25. Privacy Impact Assessment

A **Privacy Impact Assessment (PIA)** or similar privacy assessment evaluates potential privacy risks associated with a system, process, product, or data use.

It may examine:

- What personal data is collected
- Why it is collected
- Who can access it
- Where it goes
- Third parties
- Retention
- Security controls
- Individual impact
- Privacy risks
- Mitigation measures

A privacy assessment can be especially useful before introducing a new system that processes sensitive personal information.

---

## 26. Privacy Risk Assessment

Privacy risk can involve more than unauthorized access.

Potential privacy harms may include:

- Unnecessary collection
- Unexpected use
- Excessive disclosure
- Inaccurate information
- Excessive retention
- Unauthorized profiling
- Inappropriate sharing

Therefore, a privacy assessment should examine how information is used, not only whether it is encrypted.

---

## 27. Data Quality

Data governance includes data quality.

Organizations should consider:

- Accuracy
- Completeness
- Consistency
- Timeliness
- Validity

Incorrect personal information can cause harm even if the data is securely protected.

For example:

> An employee's emergency contact information is securely stored but incorrect.

The security controls may be functioning, but data quality is poor.

---

## 28. Data Integrity and Privacy

Integrity is important to both security and privacy.

Unauthorized modification can cause:

- Incorrect decisions
- Incorrect records
- Financial harm
- Operational problems
- Privacy impacts

Controls can include:

- Access control
- Change management
- Validation
- Audit trails
- Integrity checks
- Version control

---

## 29. Access Control for Personal Data

Access should follow:

- Least privilege
- Need-to-know
- Role-based access
- Strong authentication
- Periodic access reviews
- Privileged access controls

Not every employee who works for an organization needs access to every dataset.

For example:

> A payroll employee may need payroll records but not unrestricted access to all customer databases.

Data governance should define access requirements, while technical systems enforce them.

---

## 30. Data Masking

**Data masking** obscures sensitive information while preserving enough structure for a legitimate purpose.

Example:

Instead of displaying:

> 4111 1111 1111 1111

a system may display:

> **** **** **** 1111

Masking can reduce exposure during:

- Support operations
- Development
- Testing
- Reporting

It is important to distinguish masking from encryption.

**Encryption** transforms data using cryptographic methods and is intended to allow authorized recovery with appropriate keys.

**Masking** displays or substitutes data so that sensitive values are not exposed unnecessarily.

---

## 31. Tokenization

**Tokenization** replaces sensitive data with a token that can be mapped back to the original value by an appropriate system.

Example:

**Original payment value → Token**

The token may be used by systems that do not need direct access to the original sensitive value.

Tokenization can reduce exposure of sensitive information, although the security of the tokenization system itself remains important.

---

## 32. Pseudonymization

**Pseudonymization** replaces identifying information with pseudonyms or identifiers so that direct identification is reduced.

However, if additional information can reconnect the pseudonym to an individual, the information may still be considered personal data under applicable privacy requirements.

This is different from true irreversible anonymization.

---

## 33. Anonymization

**Anonymization** attempts to transform information so that individuals cannot reasonably be identified, taking applicable technical and contextual factors into account.

Anonymization can reduce privacy risk, but organizations should evaluate whether re-identification remains possible.

Removing only a name does not automatically make a dataset anonymous.

For example:

> Age + ZIP code + rare occupation + location history

may still identify a person when combined with other information.

---

## 34. Encryption and Privacy

Encryption is an important security control for protecting personal data.

It can protect:

- Data at rest
- Data in transit
- Backup data
- Portable devices
- Cloud storage

However:

> **Encryption does not automatically make all privacy requirements disappear.**

An organization can still violate privacy requirements through:

- Excessive collection
- Unnecessary retention
- Improper sharing
- Lack of transparency

Encryption is one layer of privacy protection, not the complete privacy program.

---

## 35. Data Loss Prevention

**Data Loss Prevention (DLP)** tools can help identify and prevent unauthorized movement of sensitive information.

DLP may monitor:

- Email
- Endpoints
- Cloud storage
- Web uploads
- Removable media
- Network traffic

Policies can detect patterns associated with:

- Payment information
- Personal information
- Confidential documents
- Source code

DLP should be aligned with data classification and organizational policies.

---

## 36. Privacy and Logging

Logging creates an interesting privacy/security balance.

Logs may contain:

- Usernames
- IP addresses
- Email addresses
- URLs
- File names
- Authentication information
- Application data

Therefore, logging should collect sufficient information for security monitoring without unnecessarily exposing sensitive personal information.

Organizations should consider:

- Log access
- Retention
- Masking
- Redaction
- Encryption
- Least privilege

Security logs themselves can become sensitive data.

---

## 37. Privacy and Monitoring

Monitoring may involve employee or customer activity.

Organizations should consider:

- Purpose
- Proportionality
- Authorization
- Applicable laws
- Transparency
- Retention
- Access

The objective is not to avoid monitoring entirely.

The objective is to conduct legitimate monitoring with appropriate governance and controls.

---

## 38. Privacy and Incident Response

A security incident involving personal data can create privacy obligations.

Example:

A database containing customer information is compromised.

The response may require:

- Containment
- Investigation
- Evidence preservation
- Determining affected data
- Identifying affected individuals
- Legal/privacy assessment
- Regulatory notification where required
- Customer communication where required
- Remediation

Security teams should involve privacy and legal personnel according to the incident-response plan.

---

## 39. Data Breach vs Privacy Incident

A privacy incident does not always require a successful external breach.

Examples:

- Employee sends personal data to the wrong recipient
- Sensitive information is exposed internally
- Data is retained longer than permitted
- Personal data is collected without appropriate authorization
- A vendor uses information outside approved purposes

A security incident may involve confidentiality, integrity, or availability without involving personal information.

The two categories can overlap.

---

## 40. Data Governance Roles

Different organizations use different role names, but responsibilities commonly include:

### Data Owner

Accountable for data decisions.

### Data Custodian

Performs technical/operational data handling.

### Data Steward

May manage data quality, classification implementation, metadata, and governance processes.

### Privacy Officer / Privacy Function

Helps oversee privacy requirements and privacy risk.

### Security Team

Implements and monitors security controls.

### Legal/Compliance

Interprets applicable legal and regulatory obligations.

These roles should work together rather than assuming one team owns every data-related decision.

---

## 41. Data Stewardship

A **data steward** helps ensure that governance requirements are applied consistently.

Responsibilities may include:

- Data quality
- Metadata
- Classification
- Data definitions
- Access coordination
- Lifecycle processes
- Governance standards

The exact distinction between data owner and data steward varies between organizations.

The key principle is clear accountability.

---

## 42. Data Inventory

An organization should know what important data it has and where it exists.

A data inventory may include:

- Dataset
- Owner
- Classification
- Location
- System
- Processing purpose
- Retention period
- Access groups
- Third parties
- Backup locations

Without data visibility, privacy and governance decisions become difficult.

---

## 43. Data Discovery

Data discovery identifies where sensitive or regulated information exists.

Techniques may include:

- Database scanning
- File-system scanning
- Cloud discovery
- DLP discovery
- Metadata analysis
- Application inventory
- Data-flow mapping

Discovery can identify **shadow data** that exists outside approved repositories.

---

## 44. Shadow Data

Shadow data is information stored or processed outside approved organizational governance.

Examples:

- Personal cloud storage
- Unapproved SaaS
- Local spreadsheets
- USB drives
- Personal email
- Unmanaged databases

Shadow data creates risks because:

- Security controls may be missing
- Retention may be unknown
- Access may be uncontrolled
- Deletion may be difficult
- Compliance scope may be unclear

Data governance should therefore include discovery and lifecycle controls.

---

## 45. Third-Party Data Processing

When a vendor processes personal or sensitive data, the organization should understand:

- What data is shared
- Why it is shared
- Where it is processed
- Who can access it
- Subprocessors
- Retention
- Security controls
- Incident notification
- Return/deletion requirements

Contracts should define appropriate responsibilities.

Third-party processing should align with the organization's data governance and privacy requirements.

---

## 46. Data Retention vs Legal Hold

Normally, an organization may delete data after the defined retention period.

However, a **legal hold** may require preservation of information relevant to legal proceedings.

This can temporarily override normal deletion practices for affected information.

Therefore:

> Retention policy + legal requirements + legal holds

must be considered together.

---

## 47. Privacy and Data Classification Example

Consider three datasets.

### Dataset A

Public product documentation.

Classification:

**Public**

Controls may be relatively limited because the information is intended for public disclosure.

### Dataset B

Internal business procedures.

Classification:

**Internal**

Access should generally be limited to authorized personnel.

### Dataset C

Customer financial information.

Classification:

**Confidential/Restricted**, depending on organizational policy.

It may require:

- Strong access control
- MFA
- Encryption
- Monitoring
- Retention limits
- Secure disposal

The controls should be proportional to sensitivity.

---

## 48. Privacy and Data Lifecycle Example

Consider customer information.

### Collection

Collect only necessary information.

### Storage

Encrypt and restrict access.

### Use

Use it for approved purposes.

### Sharing

Share only with authorized parties.

### Retention

Keep it only as long as required.

### Disposal

Securely delete or destroy it when no longer needed.

This lifecycle approach prevents privacy from being treated as a single point-in-time control.

---

## 49. Common Privacy and Governance Failures

### Failure 1: Collecting Everything

Organizations collect unnecessary information "just in case."

**Better approach:** apply data minimization.

### Failure 2: No Data Owner

Nobody is accountable for classification and access decisions.

**Better approach:** assign ownership.

### Failure 3: Confusing Owner and Custodian

The technical administrator is assumed to own the business decision.

**Better approach:** separate accountability from operational handling.

### Failure 4: Encryption as the Entire Privacy Strategy

The organization encrypts everything but retains excessive personal data indefinitely.

**Better approach:** combine encryption with minimization, retention, access, and disposal controls.

### Failure 5: Ignoring Backups

Production data is deleted, but copies remain in backups indefinitely.

**Better approach:** define lifecycle requirements for copies and backups.

### Failure 6: Ignoring Shadow Data

Sensitive spreadsheets exist in personal cloud accounts.

**Better approach:** data discovery, DLP, policy, and approved storage.

### Failure 7: Treating Vendors as Outside the Privacy Program

A processor handles personal data but is not assessed.

**Better approach:** include third-party processing in governance.

### Failure 8: No Data Flow Visibility

The organization does not know where information goes.

**Better approach:** map collection, processing, storage, sharing, and deletion.

### Failure 9: No Privacy Review for New Systems

A new application begins collecting personal information without assessing privacy implications.

**Better approach:** integrate privacy by design and privacy assessments into system development.

---

## 50. Detailed Security+ Scenario 1 — Data Owner vs Custodian

HR owns employee records.

The database administrator maintains the storage platform.

Who decides classification and access requirements?

**Data owner.**

Who implements technical storage and backup controls?

**Data custodian.**

The exact titles may vary, but accountability and operational responsibilities should remain clear.

---

## 51. Detailed Security+ Scenario 2 — Data Minimization

An application needs to determine whether a customer qualifies for a service.

The application collects:

- Full identity document
- Home address
- Exact location history
- Employment history
- Eligibility information

If only eligibility information is necessary, collecting all other information creates unnecessary exposure.

The privacy principle is:

**Data minimization.**

---

## 52. Detailed Security+ Scenario 3 — Retention

An organization has a policy requiring customer records to be retained for a defined period.

A department wants to keep every record indefinitely "just in case."

This may create unnecessary privacy and security exposure.

The organization should follow the applicable retention requirements and consider legal holds and legitimate business needs.

---

## 53. Detailed Security+ Scenario 4 — Data Disposal

A company deletes sensitive files from a workstation before disposing of the device.

Because the device contains storage media, the organization should consider whether normal deletion is sufficient.

For sensitive information, appropriate:

- Sanitization
- Cryptographic erasure
- Physical destruction

may be required depending on the medium and policy.

---

## 54. Detailed Security+ Scenario 5 — Privacy Incident

An employee accidentally emails a spreadsheet containing personal information to the wrong external recipient.

No attacker exploited a vulnerability.

Nevertheless, this may constitute a:

**Privacy incident / data-handling incident**

and should be reported according to organizational procedures.

---

## 55. Detailed Security+ Scenario 6 — Cloud Privacy

An organization stores personal information in a cloud service.

The organization should determine:

- Where data is stored
- Where backups are stored
- Who processes it
- What subprocessors are involved
- Which privacy requirements apply
- How data is encrypted
- How access is controlled
- How data is deleted

Cloud adoption does not remove privacy obligations.

---

## 56. Detailed Security+ Scenario 7 — Pseudonymization

A dataset replaces customer names with randomly generated identifiers.

However, a separate database can map those identifiers back to individuals.

This is generally **pseudonymization**, not automatically anonymization.

The re-identification mechanism remains important to the privacy analysis.

---

## 57. Detailed Security+ Scenario 8 — Privacy by Design

A development team is creating a new customer application.

Instead of collecting all possible information and adding privacy controls later, the team:

- Collects only necessary fields
- Uses restricted defaults
- Defines retention
- Builds deletion mechanisms
- Limits access
- Encrypts sensitive data

This demonstrates:

**Privacy by design.**

---

## 58. Security+ Exam Distinctions

### Privacy vs Security

**Privacy:** appropriate handling of information about individuals.

**Security:** protection of information and systems from threats and unauthorized activity.

### Data Owner vs Data Custodian

**Owner:** accountable for decisions.

**Custodian:** performs technical/operational handling.

### Data Classification vs Ownership

**Classification:** sensitivity and handling requirements.

**Ownership:** accountability and decision authority.

### Data Minimization vs Data Retention

**Minimization:** limit what is collected/processed.

**Retention:** limit how long it is kept.

Both reduce unnecessary exposure.

### Encryption vs Masking

**Encryption:** cryptographic transformation intended for authorized recovery.

**Masking:** obscures sensitive values from view.

### Tokenization vs Encryption

**Tokenization:** replaces data with a token mapped to the original value.

**Encryption:** transforms data cryptographically.

### Pseudonymization vs Anonymization

**Pseudonymization:** direct identification is reduced but re-identification may remain possible.

**Anonymization:** intended to prevent reasonable identification.

### Data Residency vs Data Sovereignty

**Residency:** where data is stored/processed.

**Sovereignty:** which jurisdiction's legal authority applies.

### Privacy Assessment vs Security Assessment

Privacy assessment examines privacy risks and data practices.

Security assessment examines security controls and threats.

They overlap but are not identical.

---

## 59. Security+ Decision Framework

When analyzing a privacy or data-governance scenario, use this sequence.

### Step 1 — Identify the Data

What information is being collected or processed?

### Step 2 — Determine Sensitivity

What classification applies?

### Step 3 — Identify Ownership

Who is accountable for the data?

### Step 4 — Identify Purpose

Why is the data needed?

### Step 5 — Apply Minimization

Is every collected field actually necessary?

### Step 6 — Map the Lifecycle

Where is the data:

- Collected?
- Stored?
- Used?
- Shared?
- Archived?
- Deleted?

### Step 7 — Identify Access

Who needs access and why?

### Step 8 — Identify Third Parties

Who else processes the information?

### Step 9 — Determine Retention

How long must it be retained?

### Step 10 — Determine Disposal

How should it be securely destroyed?

### Step 11 — Identify Applicable Requirements

Which legal, regulatory, contractual, and organizational requirements apply?

### Step 12 — Validate Controls

Verify that technical and procedural controls enforce the intended governance requirements.

---

## 60. Complete Data Governance Workflow

**Identify data**
↓
**Assign owner**
↓
**Classify data**
↓
**Define purpose**
↓
**Apply minimization**
↓
**Map data flows**
↓
**Define access**
↓
**Define security controls**
↓
**Define sharing requirements**
↓
**Define retention**
↓
**Monitor use**
↓
**Review third-party processing**
↓
**Archive where required**
↓
**Securely dispose**
↓
**Validate compliance**
↓
**Improve governance**

This creates lifecycle-based governance rather than treating data protection as a storage-only problem.

---

## 61. Practical Privacy Governance Example

Consider an organization developing a mobile banking application.

### Step 1 — Identify Data

The application may process:

- Customer identity
- Account information
- Transaction information
- Device information
- Authentication information

### Step 2 — Classify

Sensitive financial and authentication information receives stronger protection.

### Step 3 — Define Purpose

Each category of information should have a defined business or legal purpose.

### Step 4 — Minimize

The application should avoid collecting unnecessary information.

### Step 5 — Protect

Controls may include:

- MFA
- Encryption
- Tokenization
- Strong access control
- Secure APIs
- Logging

### Step 6 — Control Sharing

Third-party processors should receive only the information required for their services.

### Step 7 — Retain

Retention should follow applicable requirements.

### Step 8 — Dispose

Information that is no longer required should be securely disposed of according to policy and legal requirements.

### Step 9 — Monitor

The organization monitors:

- Access
- Data movement
- Third-party processing
- Policy violations
- Privacy incidents

This demonstrates privacy and data governance across the entire lifecycle.

---

## 62. Final Mental Model

Remember:

**Data**
→ What information do we have?

**Purpose**
→ Why do we need it?

**Classification**
→ How sensitive is it?

**Owner**
→ Who is accountable?

**Custodian**
→ Who technically manages it?

**Access**
→ Who needs it?

**Minimization**
→ Are we collecting more than necessary?

**Sharing**
→ Who else receives it?

**Protection**
→ How is it secured?

**Retention**
→ How long should we keep it?

**Disposal**
→ How do we securely remove it?

**Privacy**
→ Are we handling information about individuals appropriately?

**Governance**
→ Who makes and enforces the data decisions?

The central Security+ principle is:

> **Data should be governed and protected throughout its entire lifecycle, with accountability, classification, minimization, access control, appropriate sharing, retention, and secure disposal aligned to the sensitivity and purpose of the information.**

## Key Takeaways

- Privacy and security overlap but are not the same discipline.
- **Privacy** focuses on appropriate handling of information about individuals.
- **Security** protects information and systems from unauthorized activity and disruption.
- Data governance establishes ownership, accountability, classification, lifecycle, handling, quality, and decision-making.
- **Data owners are accountable for data decisions; data custodians perform technical/operational handling.**
- Data classification determines sensitivity and handling requirements.
- Classification should drive actual controls rather than exist only as a label.
- Data should be governed throughout its lifecycle: **collect → store → use → share → retain → dispose**.
- Data minimization reduces unnecessary privacy and security exposure.
- Purpose limitation helps prevent inappropriate secondary use.
- Retention should be intentional and aligned with applicable requirements.
- Deleting production data does not necessarily remove copies from backups, archives, replicas, or vendor systems.
- Data residency and sovereignty can create additional considerations for cloud and international processing.
- Privacy by design incorporates privacy requirements before systems are deployed.
- Privacy assessments help identify risks associated with new data-processing activities.
- Data masking, tokenization, and pseudonymization reduce exposure in different ways and should not be treated as interchangeable.
- Encryption is an important privacy-supporting security control but does not replace privacy governance.
- DLP, access control, logging, and monitoring can support data governance.
- Third-party processing must be included in privacy and data-governance analysis.
- Privacy incidents can occur without an external attacker.
- Shadow data creates governance and security gaps.
- Data quality and integrity are important because inaccurate information can also cause harm.
- Legal holds can affect normal retention and disposal processes.
- The objective is not simply to protect data after it exists; it is to **govern what data is collected, why it is used, who can access it, where it goes, how long it remains, and how it is ultimately disposed of**.
