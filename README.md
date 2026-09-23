# Identity and Access Management (IAM)

A structured knowledge base covering **Identity and Access Management (IAM)** concepts, processes, architectures, technologies, security controls, and operational practices.

The objective of this repository is to provide practical and technology-neutral IAM documentation while also covering common implementations and platforms where relevant.

---

## Scope

Identity and Access Management answers several fundamental questions:

- **Who are you?**
- **How is your identity established and maintained?**
- **How do you prove who you are?**
- **What are you allowed to access?**
- **Why do you have that access?**
- **Who approved it?**
- **Is that access still required?**
- **When should it be removed?**
- **Can the complete lifecycle be audited?**

IAM therefore extends well beyond authentication. It covers the complete lifecycle of identities, accounts, roles, entitlements, credentials, privileges, and access decisions.

---

## Core IAM Principles

The material in this repository is based around several fundamental security principles:

- **Least privilege**
- **Need-to-know**
- **Default deny**
- **Separation of Duties (SoD)**
- **Accountability**
- **Traceability**
- **Time-bound access where appropriate**
- **Continuous reassessment of access**
- **Automation where reliable and controlled**
- **Explicit ownership of identities, roles and entitlements**

---

## IAM Domains

The repository covers the following major areas.

### 1. Identity Lifecycle — Joiner / Mover / Leaver

Management of identities throughout their lifecycle:

- Joiner
- Mover
- Leaver
- Rehire / returner
- Contractors
- External identities
- Dormant accounts
- Orphan accounts

### 2. Access Request & Provisioning

Processes used to request, approve, provision, modify and revoke access:

- Access requests
- Approval workflows
- Birthright access
- Automated provisioning
- Deprovisioning
- Group and entitlement management
- SCIM
- APIs
- LDAP
- IAM connectors

### 3. Identity Governance & Administration — IGA

Governance processes ensuring that access remains appropriate:

- Access reviews
- Recertification campaigns
- Manager certification
- Application-owner certification
- Privileged-access certification
- Remediation
- Evidence and audit trails

### 4. Segregation of Duties — SoD

Prevention and detection of conflicting privileges:

- Toxic combinations
- Preventive SoD
- Detective SoD
- Risk acceptance
- Exceptions
- Compensating controls

### 5. Authentication & Federation

Establishing and verifying identity:

- Password authentication
- MFA
- Passwordless authentication
- FIDO2
- Passkeys
- Single Sign-On (SSO)
- SAML
- OAuth 2.0
- OpenID Connect (OIDC)
- Conditional authentication
- Risk-based authentication

### 6. Privileged Access Management — PAM

Management and protection of privileged access:

- Privileged accounts
- Credential vaulting
- Credential rotation
- Just-in-Time (JIT) access
- Just-Enough-Access (JEA)
- Session monitoring
- Session recording
- Break-glass access

### 7. Identity Data & Authoritative Sources

Management of identity information and its sources:

- Authoritative identity sources
- HR-driven identity lifecycle
- Identity correlation
- Reconciliation
- Attribute synchronization
- Identity matching
- Data quality
- Source-of-truth management

### 8. Non-Human Identities — NHI

Lifecycle and governance of identities that do not represent human users:

- Service accounts
- Application identities
- Service principals
- API identities
- Workload identities
- Certificates
- Keys
- Secrets
- Credential rotation

### 9. Role & Entitlement Governance

Design and governance of access models:

- RBAC
- ABAC
- Role engineering
- Role mining
- Business roles
- Technical roles
- Entitlement catalogues
- Role ownership
- Entitlement ownership
- Role lifecycle

### 10. Monitoring, Audit & Compliance

Providing visibility and evidence across the IAM lifecycle:

- Authentication logging
- Authorization logging
- Provisioning traceability
- Access-change auditing
- SIEM integration
- Compliance evidence
- Security monitoring

---

## IAM Process Overview

The major IAM capabilities are interconnected.

```text
              Authoritative Sources
                      |
                      v
               Identity Lifecycle
              Joiner / Mover / Leaver
                      |
                      v
          Provisioning / Deprovisioning
                      |
             +--------+--------+
             |                 |
             v                 v
      Birthright Access   Access Requests
                               |
                               v
                         RBAC / ABAC
                               |
                               v
                           SoD Check
                               |
                               v
                           Approval
                               |
                               v
                         Provisioning
                               |
                               v
                    Accounts / Entitlements
                               |
                    +----------+----------+
                    |                     |
                    v                     v
             Recertification             PAM
                    |                     |
                    +----------+----------+
                               |
                               v
                       Audit / Monitoring
                               |
                               v
                          Remediation
```

IAM should be considered a **continuous lifecycle**, not a one-time provisioning process.

Changes to employment status, organizational structure, responsibilities, identity attributes, risk, policy, or business requirements may trigger reassessment of existing access.

---

## Repository Structure

```text
IAM/
├── README.md
├── IAM_PROCESS_OVERVIEW.md
├── docs/
│   ├── 01-jml.md
│   ├── 02-access-request.md
│   ├── 03-recertification.md
│   ├── 04-sod-toxic-combinations.md
│   ├── 05-rbac-abac.md
│   ├── 06-authentication-federation.md
│   ├── 07-pam.md
│   ├── 08-non-human-identities.md
│   ├── 09-identity-governance.md
│   └── 10-audit-compliance.md
├── diagrams/
└── notes/
```

The high-level process catalogue is maintained in:

**[IAM_PROCESS_OVERVIEW.md](IAM_PROCESS_OVERVIEW.md)**

Detailed documentation is maintained under:

**[docs/](docs/)**

---

## Technologies & Platforms

The repository is intended to remain conceptually technology-neutral while providing practical examples involving technologies and platforms such as:

- Microsoft Entra ID
- Active Directory
- Red Hat Identity Management / FreeIPA
- LDAP
- Kerberos
- SailPoint
- CyberArk
- Keycloak
- SCIM
- SAML
- OAuth 2.0
- OpenID Connect

Platform-specific material should illustrate IAM concepts rather than make the overall documentation dependent on a particular vendor.

---

## Documentation Approach

Topics are developed from both governance and technical perspectives.

Where applicable, documentation covers:

1. Purpose
2. Terminology
3. Actors and ownership
4. Triggers
5. Process flow
6. Business rules
7. Security controls
8. Technical implementation
9. Automation
10. Auditability
11. Failure scenarios
12. Risks and common mistakes
13. Practical examples

---

## Status

This repository is under active development.

The initial documentation focuses on the fundamental IAM lifecycle and governance processes before expanding into protocols, architectures, platform implementations, operational controls, and advanced IAM topics.

---

## License

See the repository's [LICENSE](LICENSE) file for licensing information.
