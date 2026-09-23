# Non-Human Identities — Cheat Sheet

## NHI

```text
NHI
=
Identity not representing
a human user
```

Examples:

```text
Service Account
Application Identity
Workload Identity
Managed Identity
API Client
Machine Identity
Automation Account
```

---

## Basic Model

```text
APP / SERVICE / MACHINE
          |
          v
       IDENTITY
          |
          v
    AUTHENTICATE
          |
          v
     ENTITLEMENT
          |
          v
       RESOURCE
```

---

## Service Account

```text
Service
   |
   v
svc_account
   |
   v
Resource
```

---

## Managed / Workload Identity

Prefer where appropriate:

```text
Workload
   |
   v
Identity
   |
   v
Short-Lived Credential
   |
   v
Resource
```

instead of:

```text
Application
   |
   v
Hard-Coded Password
```

---

## Secrets

```text
Password
API Key
Client Secret
Private Key
Token
```

Remember:

```text
CREATE
STORE
USE
ROTATE
REVOKE
```

---

## Most Important Attribute

```text
NHI
 |
 v
OWNER
```

Ask:

```text
Who owns it?

Why does it exist?

What uses it?

What can it access?

Is it still needed?
```

---

## Lifecycle

```text
CREATE
  |
  v
USE
  |
  v
REVIEW
  |
  v
ROTATE
  |
  v
RETIRE
```

---

## Biggest Risks

```text
No owner

Hard-coded secret

Static credential

Excessive privilege

Shared identity

Orphaned identity

No review
```

---

## PAM Connection

```text
Privileged NHI
     |
     v
    PAM
     |
     +-- Vault
     +-- Rotate
     +-- Monitor
```

---

## IGA Connection

```text
NHI
 |
 +-- Owner
 +-- Entitlements
 +-- Approval
 +-- Review
 +-- Lifecycle
```

---

# 10-Second Memory

```text
NHI = non-human identity

Service account = service/application identity

Workload identity = software workload identity

Managed identity = platform-managed identity

Secret = credential

Owner = accountability

Rotate = replace credentials

Orphan = no valid owner/purpose

Goal = no unmanaged identities or secrets
```

> Machine does not mean unmanaged.
