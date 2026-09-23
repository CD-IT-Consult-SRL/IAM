# SoD & Toxic Combinations — Cheat Sheet

## The Whole Concept

```text
A = OK
B = OK

A + B = NOT OK

       =
TOXIC COMBINATION
```

Example:

```text
CREATE_PAYMENT
      +
APPROVE_PAYMENT
      =
SoD CONFLICT
```

---

## SoD

```text
Segregation of Duties
=
Separate incompatible responsibilities
```

Goal:

```text
No single person should control
an entire sensitive process.
```

---

## Preventive vs Detective

```text
PREVENTIVE
=
BEFORE
=
Stop conflict before access is granted
```

```text
DETECTIVE
=
AFTER
=
Find conflicts already present
```

---

## Access Request

```text
Existing Access
      +
Requested Access
      |
      v
   SoD CHECK
    /    \
   v      v
 SAFE   CONFLICT
   |      |
   v      v
GRANT   REVIEW
```

---

## Exception

```text
CONFLICT
   |
   v
Risk Assessment
   |
   v
Approval
   |
   v
Exception
   |
   v
Compensating Control
   |
   v
Expiration / Review
```

Never think:

```text
Exception = Ignore
```

Think:

```text
Exception
=
Accept + Document + Control + Review
```

---

## Compensating Control

Examples:

```text
Independent review
Additional approval
Monitoring
Logging
Reconciliation
Transaction limits
```

---

## Mover Danger

```text
OLD ACCESS
    +
NEW ACCESS
    |
    v
PRIVILEGE CREEP
    |
    v
SoD CONFLICT
```

Therefore:

```text
MOVER
  =
REASSESS ACCESS
  +
REMOVE OLD ACCESS
  +
CHECK SoD
```

---

## Connection to IAM

```text
JML
 |
 v
Access
 |
 v
Roles / Entitlements
 |
 v
SoD
 |
 v
Recertification
 |
 v
Remediation
```

---

# 10-Second Memory

```text
SoD        = separate duties

Toxic      = A OK + B OK -> together NOT OK

Preventive = BEFORE

Detective  = AFTER

Exception  = approved + documented + time-bound

Compensate = reduce the remaining risk
```

## One Sentence

> Individually valid access can become dangerous when combined.
