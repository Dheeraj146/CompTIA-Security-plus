# Indicators of Malicious Activity

## Overview

Security analysts must recognize behavioral indicators that may suggest compromise. Individual indicators are not always proof of an incident; context and correlation are essential.

## Account Indicators

- Repeated authentication failures
- Successful login after many failures
- Impossible travel or unusual geographic access
- New privileged accounts
- Unexpected password resets
- Authentication from unfamiliar devices
- Unusual use of dormant accounts

## Endpoint Indicators

- Unexpected processes or services
- Suspicious persistence mechanisms
- Unusual outbound connections
- Security controls being disabled
- Unexpected administrative tools
- Abnormal file modifications
- Encryption of large numbers of files
- Unusual resource consumption

## Network Indicators

- Unexpected beaconing
- Large outbound transfers
- Connections to known malicious infrastructure
- Unusual DNS requests
- Unexpected remote administration traffic
- Sudden scanning behavior
- Abnormal protocols or ports

## Application Indicators

- Repeated authorization failures
- Unexpected administrative actions
- Unusual API activity
- Abnormal input patterns
- Sudden changes to application data
- Unexpected configuration modifications

## Correlation

A single event can be benign. Multiple related indicators can form a stronger detection. For example, a suspicious email attachment followed by a new process, an outbound connection, and a new persistence mechanism provides much stronger evidence than any one event alone.

## Security+ Exam Focus

Know the difference between an indicator and confirmed compromise. Indicators support detection and investigation; analysts must validate evidence before making conclusions.

## Key Takeaways

Use endpoint, identity, network, application, and cloud telemetry together. Good detection is based on context, baselines, correlation, and investigation.
