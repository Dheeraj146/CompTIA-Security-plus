# Resilience, Redundancy, and High Availability

## Resilience

Resilience is the ability of an environment to continue operating or recover effectively after disruption. It combines preventive design, redundancy, recovery capability, and adaptability.

## Redundancy

Redundancy provides additional components so a single failure does not necessarily stop service. Examples include redundant power supplies, network links, servers, storage devices, and geographic facilities.

## High Availability

High availability minimizes service interruption through architectures such as clustering, failover, load balancing, redundant infrastructure, and automated recovery.

### Active-Active
Multiple systems actively serve workloads. Failure of one can shift traffic to others.

### Active-Passive
A primary system handles service while a standby system becomes active after failure.

## Fault Tolerance

Fault-tolerant designs continue operating through certain component failures with minimal interruption. They are generally more expensive and complex than ordinary redundancy.

## Capacity and Resilience

Redundancy must account for capacity. A backup server that cannot handle production load does not provide meaningful availability.

## Exam Focus

Availability architecture must match business requirements. Redundancy reduces single points of failure; high availability reduces downtime; fault tolerance aims to continue operation despite component failure.
