# Identity and Access Management — Process Overview

This document provides a high-level overview of the principal processes,
controls, and capabilities involved in Identity and Access Management (IAM).

The individual topics are developed in more detail throughout this repository.

---

## 1. Identity Lifecycle — Joiner / Mover / Leaver (JML)

- **Joiner** — identity creation, onboarding, and initial access provisioning
- **Mover** — role, department, location, or responsibility change and access reassessment
- **Leaver** — controlled deprovisioning, account disablement, access revocation, and ownership transfer
- Rehire / returner lifecycle
- Contractor lifecycle
- Dormant account management
- Orphan account management

---

## 2. Access Request & Provisioning

- Access request workflow
- Approval workflow
  - Manager approval
  - Application owner approval
  - Data owner approval
- RBAC — Role-Based Access Control
- ABAC — Attribute-Based Access Control
- Birthright / baseline access
- Automated provisioning and deprovisioning
- SCIM / API / LDAP / connector-based provisioning
- Group and entitlement management

---

## 3. Access Governance / IGA

- Access recertification / access review campaigns
- Manager certification
- Application-owner certification
- Privileged-access certification
- Periodic access reviews
- Event-driven access reviews
- Removal and remediation of rejected access
- Evidence collection and audit trail

---

## 4. Segregation of Duties — SoD

- Toxic combinations
- Preventive SoD controls
  - Detect and block conflicting access during request or provisioning
- Detective SoD controls
  - Identify conflicts in existing access
- Risk acceptance
- Exception management
- Compensating controls

---

## 5. Authentication

- Password policies
- Multi-Factor Authentication (MFA)
- Passwordless authentication
- FIDO2 / passkeys
- Single Sign-On (SSO)
- Federation
  - SAML
  - OAuth 2.0
  - OpenID Connect (OIDC)
- Conditional authentication
- Risk-based authentication
- Authentication session management

---

## 6. Privileged Access Management — PAM

- Privileged account discovery
- Credential vaulting
- Credential rotation
- Just-in-Time (JIT) access
- Just-Enough-Access (JEA)
- Privileged session monitoring
- Session recording
- Emergency / break-glass access
- Administrative account management
- Service account management

---

## 7. Identity Data & Authoritative Sources

- HR systems as authoritative identity sources
- Identity correlation and reconciliation
- Identity matching
- Attribute synchronization
- Identity uniqueness
- Identity data quality
- Source-of-truth conflicts

---

## 8. Non-Human Identities — NHI

- Service accounts
- Application identities
- API identities
- Service principals
- Workload identities
- Certificates
- Keys
- Secrets
- Ownership and lifecycle
- Credential rotation

---

## 9. Role & Entitlement Governance

- Role engineering
- Role mining
- Business roles
- Technical roles
- Entitlement catalogue
- Role ownership
- Entitlement ownership
- Role review and cleanup
- Role explosion prevention

---

## 10. Monitoring, Audit & Compliance

- Authentication logging
- Access logging
- Provisioning and deprovisioning traceability
- Determining who has access to what
- Determining why access was granted
- Recording who approved access
- Recording when access was granted
- Recording when access was modified or removed
- SIEM integration
- Compliance evidence
- Regulatory and security frameworks
  - GDPR
  - ISO 27001
  - SOX and similar controls where applicable

---

## 11. Special Identity Lifecycle Processes

- Temporary access with automatic expiration
- External users
- Partners / B2B identities
- Contractors
- Guest accounts
- Emergency access
- Account inactivity management
- Account lock / unlock
- Access expiration
- Access renewal

---

## 12. IAM Operating & Governance Model

Typical IAM responsibilities and ownership include:

- Identity owner
- Manager
- Application owner
- Entitlement owner
- Role owner
- Data owner
- IAM operations
- Security
- Risk
- Compliance
- Exception management
- Escalation processes

---

## Core IAM Principles

The processes above should consistently implement several fundamental security principles:

- **Least privilege**
- **Need-to-know**
- **Separation of duties**
- **Default deny**
- **Accountability**
- **Traceability**
- **Time-bound access where appropriate**
- **Continuous reassessment of access**

---

## IAM Lifecycle Relationship

A simplified view of the relationship between the major IAM processes is:

```text
Authoritative Source
        |
        v
Identity Lifecycle (JML)
        |
        v
Provisioning / Deprovisioning
        |
        +----> Birthright Access
        |
        +----> Access Requests
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
            Access / Entitlements
                    |
          +---------+---------+
          |                   |
          v                   v
    Recertification          PAM
          |                   |
          +---------+---------+
                    |
                    v
             Audit / Monitoring
                    |
                    v
               Remediation
```

The lifecycle is continuous rather than linear. Changes to identity attributes,
employment status, roles, risk, or business requirements can trigger
re-evaluation of existing access.

---

## Example — Employee Moving from Finance to Procurement

A change from Finance to Procurement can trigger multiple IAM processes:

1. The authoritative source records the organizational change.
2. The IAM platform detects a **Mover** event.
3. Existing Finance access is reassessed.
4. Access no longer justified by the new role is removed.
5. Procurement birthright access may be automatically assigned.
6. Additional access may require an access request.
7. RBAC and/or ABAC policies determine applicable access.
8. SoD controls check for toxic combinations.
9. Required approvals are collected.
10. New entitlements are provisioned.
11. Changes are recorded in the audit trail.
12. Subsequent recertification verifies that the resulting access remains appropriate.

This illustrates how JML, provisioning, RBAC/ABAC, SoD, access requests,
recertification, and audit are interconnected rather than independent IAM
processes.
