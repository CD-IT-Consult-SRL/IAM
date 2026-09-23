# PAM — Cheat Sheet

## PAM

```text
PAM
=
Privileged Access Management
```

Think:

```text
HIGH-RISK ACCESS
```

Examples:

```text
root
Domain Admin
Entra Admin
DBA
Cloud Admin
```

---

## Main Concepts

```text
VAULT
=
Protect credentials
```

```text
ROTATION
=
Change credentials
```

```text
JIT
=
Access only when needed
```

```text
STANDING PRIVILEGE
=
Permanent privileged access
```

```text
SESSION RECORDING
=
Trace admin activity
```

```text
BREAK GLASS
=
Emergency access
```

---

## PAM Flow

```text
Admin
  |
  v
MFA
  |
  v
PAM
  |
  v
Request
  |
  v
Approve
  |
  v
JIT
  |
  v
Privileged Session
  |
  v
Record / Monitor
  |
  v
Remove Privilege
```

---

## Standard vs Privileged

```text
Alice
 |
 +-- alice
 |    NORMAL
 |
 +-- adm-alice
      ADMIN
```

Don't use privileged accounts for ordinary work.

---

## PAM vs PIM

For the first mental model:

```text
PAM
=
Accounts + Credentials + Sessions
```

```text
PIM
=
Role Eligibility + Activation
```

Terminology varies between products.

---

## JIT

```text
Permanent Admin
      X

Temporary Admin
      |
      v
    Better
```

Goal:

```text
REDUCE STANDING PRIVILEGE
```

---

## Accountability

```text
WHO
did
WHAT
WHERE
WHEN
WHY?
```

---

## JML Connection

```text
JOINER
-> Grant only if needed

MOVER
-> Reassess privilege

LEAVER
-> Revoke immediately
```

---

## SoD Connection

```text
REQUESTER
    !=
APPROVER
```

where independent approval is required.

---

## Recertification

```text
Still need admin?
   /       \
 YES       NO
  |         |
 KEEP     REVOKE
```

---

# 10-Second Memory

```text
PAM   = control privileged access

Vault = protect credentials

Rotate = change credentials

JIT   = temporary privilege

PIM   = privileged role activation

Record = accountability

Break Glass = emergency access

Goal = reduce standing privilege
```

> Privileged access should be exceptional, controlled, limited, and traceable.
