# Logging, Monitoring, and SIEM

## Logging

Logs record security-relevant and operational activity. Useful sources include operating systems, authentication services, applications, firewalls, DNS, VPNs, cloud platforms, endpoints, and network devices.

## Important Log Properties

Accurate timestamps, synchronized clocks, source identification, event context, severity, and integrity protection improve investigation quality.

## SIEM

A Security Information and Event Management platform centralizes and correlates logs and security telemetry. It can normalize data, apply detection rules, correlate events, generate alerts, support investigations, and provide dashboards and reports.

## Detection Workflow

**Collect → Normalize → Correlate → Detect → Alert → Investigate → Respond → Document.**

A single failed login may be routine. A sequence of hundreds of failures followed by a successful login from an unusual location may represent a credential attack.

## Monitoring

Effective monitoring requires useful telemetry, meaningful detection logic, tuned thresholds, time synchronization, adequate retention, and analysts who understand the environment.

## Alert Triage

Analysts should determine whether an alert is benign, suspicious, or an actual incident. Priority should consider asset criticality, confidence, potential impact, and evidence of compromise.

## Exam Focus

SIEM is primarily for centralized security event collection, correlation, analysis, and alerting. Logging without appropriate collection, retention, and analysis provides limited security value.
