# Secure Application Development and Deployment

## Secure-by-Design

Security should be incorporated throughout the software development lifecycle rather than added only during final testing. Requirements should identify confidentiality, integrity, availability, authentication, authorization, logging, privacy, and regulatory needs.

## Secure Development Practices

Use input validation, output encoding, parameterized queries, secure authentication, authorization checks, secrets management, dependency management, code review, security testing, and secure error handling.

## Deployment Models

Development, testing, staging, and production environments should be appropriately separated. Production credentials and sensitive data should not be casually copied into lower environments.

## CI/CD Security

Build pipelines should enforce access control, protect source code and secrets, validate dependencies, scan artifacts, and restrict who can modify deployment processes. Software provenance and artifact integrity should be considered.

## Infrastructure as Code

Infrastructure definitions can be version controlled and reviewed, improving consistency and auditability. Security checks can detect insecure configurations before deployment.

## Exam Focus

Security should be integrated throughout the lifecycle. Separation of environments, protected build pipelines, secure dependencies, and controlled deployment reduce supply-chain and configuration risk.
