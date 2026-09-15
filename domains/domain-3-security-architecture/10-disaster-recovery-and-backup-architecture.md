# Disaster Recovery and Backup Architecture

## Disaster Recovery

Disaster recovery restores technology services after disruptive events. Planning identifies critical services, dependencies, recovery priorities, alternate facilities, communication procedures, and restoration requirements.

## Recovery Metrics

**RTO (Recovery Time Objective)** is the maximum acceptable time to restore a service. **RPO (Recovery Point Objective)** is the maximum acceptable amount of data loss measured in time.

A low RTO requires rapid recovery. A low RPO requires frequent replication or backups so little recent data is lost.

## Backup Types

Full backups capture the selected data set. Incremental backups capture changes since the previous backup of any type. Differential backups capture changes since the last full backup.

## Backup Architecture

Maintain appropriate backup frequency, retention, encryption, access controls, geographic separation, integrity validation, and restoration testing. Protect backup systems from the same compromise affecting production systems.

## Recovery Sites

A hot site is highly prepared and can support rapid recovery. A warm site has partial infrastructure and requires additional preparation. A cold site provides facilities but requires substantial setup before operations can resume.

## Recovery Testing

Testing validates whether backups, procedures, dependencies, personnel, and technology actually support stated recovery objectives. Common exercises include tabletop, walkthrough, simulation, and technical recovery testing.

## Exam Focus

RTO concerns time; RPO concerns data loss. Backup existence does not guarantee recoverability—restoration must be tested.
