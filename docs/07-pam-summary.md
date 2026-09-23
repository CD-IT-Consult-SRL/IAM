# PAM — Summary

## Core Idea

Privileged Access Management controls high-risk administrative access.

```text
Normal Access
     |
     v
IAM / IGA

Privileged Access
     |
     v
PAM
```

Examples:

- root
- Domain Admin
- Entra privileged roles
- DBA
- Application administrator
- Service accounts

---

## Separate Standard and Admin Access

```text
Alice
 |
 +-- alice
 |    Standard
 |
 +-- adm-alice
      Privileged
```

Privileged accounts should only be used when elevated access is required.

---

## Core PAM Capabilities

```text
PAM
 |
 +-- Vault
 +-- Credential Rotation
 +-- Access Request
 +-- Approval
 +-- JIT
 +-- Session Management
 +-- Session Recording
 +-- Monitoring
 +-- Audit
```

---

## Vaulting

```text
Administrator
     |
     v
PAM Vault
     |
     v
Privileged Credential
```

The administrator may not need to know the password.

---

## JIT — Just In Time

```text
Request
   |
   v
Approve
   |
   v
Temporary Privilege
   |
   v
Work
   |
   v
Automatic Removal
```

JIT reduces **standing privilege**.

---

## PIM

Simplified distinction:

```text
PAM
=
Privileged accounts,
credentials and sessions
```

```text
PIM
=
Privileged role eligibility
and activation
```

---

## Session Recording

```text
Human
  |
  v
PAM
  |
  v
Privileged Account
  |
  v
Target
```

PAM can record who performed the privileged activity.

---

## Break Glass

Emergency access when normal mechanisms fail.

```text
Normal Access FAILS
       |
       v
Break Glass
       |
       v
Emergency Access
```

Use should be monitored, logged and reviewed.

---

## Service Accounts

Non-human identities can also hold privileged access.

They require:

- Ownership
- Least privilege
- Credential protection
- Rotation
- Monitoring
- Review

---

## Accountability

PAM should help answer:

```text
WHO?
WHAT?
WHERE?
WHEN?
WHY?
```

---

## Key Principle

> Privileged access should be exceptional, controlled, limited, and traceable.
