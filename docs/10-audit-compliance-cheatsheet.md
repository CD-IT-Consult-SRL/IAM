# IAM Monitoring, Audit & Compliance — Cheat Sheet

## Four Words

```text
LOG
=
RECORD
```

```text
MONITOR
=
WATCH
```

```text
AUDIT
=
PROVE
```

```text
COMPLIANCE
=
MEET REQUIREMENTS
```

---

## Control Lifecycle

```text
PREVENT
   |
   v
DETECT
   |
   v
CORRECT
   |
   v
VERIFY
```

Remember:

```text
Preventive = STOP

Detective = FIND

Corrective = FIX
```

---

## Accountability

```text
WHO
WHAT
WHERE
WHEN
WHY
```

---

## Control vs Evidence

```text
CONTROL
=
Should happen
```

```text
EVIDENCE
=
Proof it happened
```

---

## Reconciliation

```text
EXPECTED
   !=
ACTUAL
```

means:

```text
INVESTIGATE
```

---

## Critical IAM Events

```text
Account Created

Account Disabled

Role Granted

Role Revoked

MFA Changed

Privileged Access Activated

SoD Conflict

Provisioning Failed

Deprovisioning Failed

Break Glass Used
```

---

## Dangerous Example

```text
IGA:
REVOKED
```

but:

```text
TARGET:
STILL ACTIVE
```

This is why we need:

```text
RECONCILIATION
+
MONITORING
```

---

## SIEM

```text
IAM Sources
    |
    v
   SIEM
    |
    +-- Correlate
    +-- Detect
    +-- Alert
    +-- Investigate
```

---

## Audit Questions

```text
Who has access?

Why?

Who approved?

When granted?

Still required?

Any SoD conflict?

Was revoke actually executed?

Can we prove it?
```

---

# 10-Second Memory

```text
Logging        = RECORD

Monitoring     = DETECT

Audit          = PROVE

Compliance     = REQUIREMENTS

Reconciliation = EXPECTED vs ACTUAL

Preventive     = STOP

Detective      = FIND

Corrective     = FIX

Evidence       = PROOF
```

> If you cannot demonstrate that a control operated, you have an evidence problem even if the control was designed correctly.
