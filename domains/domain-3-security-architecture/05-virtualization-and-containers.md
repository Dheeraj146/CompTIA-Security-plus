# Virtualization and Containers

## Virtualization

Virtualization allows multiple logical systems to share physical computing resources through a hypervisor. It improves utilization and supports isolation, testing, scalability, and recovery.

### Hypervisors

Type 1 hypervisors run directly on hardware. Type 2 hypervisors run on a host operating system. The security model differs because the hypervisor and management plane become critical components.

### Virtualization Risks

Risks include hypervisor vulnerabilities, insecure management interfaces, VM escape, snapshot exposure, virtual-network misconfiguration, resource exhaustion, and excessive administrative privileges.

## Containers

Containers package applications and dependencies while sharing the host operating system kernel. They are generally lighter than full virtual machines but should not be treated as automatically secure isolation boundaries.

### Container Security

Use trusted images, scan images and dependencies, minimize container privileges, protect registries, restrict network access, manage secrets securely, keep hosts patched, and monitor runtime behavior.

## Orchestration

Container orchestration platforms manage deployment, networking, scaling, and lifecycle. Their control planes and service accounts are highly sensitive and require strong authentication, authorization, logging, and segmentation.

## Exam Focus

VMs provide stronger isolation than ordinary processes, while containers share the host kernel. Protect both the workload and the management plane.
