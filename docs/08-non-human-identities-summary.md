# Non-Human Identities — Summary

## Core Idea

IAM is not only about people.

```text
IDENTITY
   |
   +-- HUMAN
   |
   +-- NON-HUMAN
```

Examples of NHI:

- Service accounts
- Application identities
- Workload identities
- Managed identities
- API clients
- Automation accounts
- Machine identities

---

## Service Account

```text
Application
     |
     v
Service Account
     |
     v
Resource
```

Used by an application, service or automated process.

---

## Workload Identity

```text
Container / VM / Process
          |
          v
    Workload Identity
          |
          v
       Resource
```

---

## Managed Identity

The platform manages the identity and credential lifecycle.

```text
Workload
   |
   v
Managed Identity
   |
   v
Resource
```

This can avoid storing static passwords or secrets.

---

## Secrets

Examples:

```text
Password
API Key
Client Secret
Private Key
Token
```

Lifecycle:

```text
Create
  |
Store
  |
Use
  |
Rotate
  |
Revoke
```

---

## Ownership

Every NHI should have an accountable owner.

```text
NHI
 |
 +-- Owner
 +-- Purpose
 +-- Application
 +-- Access
 +-- Credential
 +-- Review
```

Without ownership, governance becomes difficult.

---

## Least Privilege

```text
Application needs READ

Give:
READ

Not:
ADMIN
```

The same least-privilege principle applies to humans and NHIs.

---

## NHI Lifecycle

```text
Request
   |
Approve
   |
Create
   |
Grant Access
   |
Use
   |
Review
   |
Rotate
   |
Retire
```

---

## Orphaned NHI

```text
Application Retired
       |
       X
Identity Remains
       |
       v
ORPHANED NHI
```

Orphaned identities can retain active access.

---

## NHI + PAM

Privileged service accounts may require:

- Vaulting
- Rotation
- Monitoring
- Privileged access controls

---

## NHI + IGA

IGA can govern:

- Ownership
- Entitlements
- Reviews
- Approval
- Lifecycle
- Recertification

---

## Key Principle

> If something can authenticate and access a resource, its identity and access require governance.
