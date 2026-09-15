# Segmentation and Isolation

## Purpose

Segmentation limits communication between systems so compromise of one area does not automatically provide access to everything else. It is a major defense-in-depth mechanism.

## Core Designs

### VLAN Segmentation
Separates Layer 2 broadcast domains logically. VLANs should be protected by appropriate routing and access controls rather than treated as a complete security boundary by themselves.

### DMZ
A DMZ places internet-facing services in a controlled network separated from internal systems. Typical examples include public web, mail, and DNS services.

### Microsegmentation
Applies granular policy between workloads, users, applications, or services. It is especially useful in virtualized and cloud environments.

### Air Gap
A highly isolated system has no normal network connectivity to other environments. An air gap reduces remote attack paths but does not eliminate risks involving removable media, maintenance personnel, or supply chains.

### Jump Server
A hardened intermediary system provides controlled administrative access to protected networks. Administrative activity can be centralized, monitored, and restricted.

## Security Principles

Segment based on trust, data sensitivity, administrative function, and business requirements. Separate user, server, management, guest, development, production, and security infrastructure where appropriate.

## Exam Focus

Segmentation reduces lateral movement. Isolation is stronger than ordinary logical separation but can introduce operational complexity. A DMZ is designed for services that require controlled exposure to less-trusted networks.
