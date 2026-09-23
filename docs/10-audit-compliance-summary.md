# IAM Monitoring, Audit & Compliance — Summary

## Core Model

```text
IAM Activity
     |
     v
Logging
     |
     v
Monitoring
     |
     v
Detection
     |
     v
Remediation
     |
     v
Evidence
     |
     v
Audit / Compliance
```

---

## Four Important Concepts

```text
LOGGING
=
Record what happened
```

```text
MONITORING
=
Observe and detect
```

```text
AUDIT
=
Verify and prove
```

```text
COMPLIANCE
=
Demonstrate requirements are satisfied
```

---

## Accountability

IAM should answer:

```text
WHO
did
WHAT
WHERE
WHEN
WHY?
```

---

## Evidence

Examples:

- Requests
- Approvals
- Authentication logs
- Provisioning results
- SoD results
- Certification decisions
- PAM sessions
- Deprovisioning results
- Reconciliation results

Remember:

```text
CONTROL
=
What should happen
```

```text
EVIDENCE
=
Proof that it happened
```

---

## Reconciliation

```text
EXPECTED
   |
   v
COMPARE
   ^
   |
ACTUAL
```

Useful for detecting:

- Manual changes
- Failed provisioning
- Failed deprovisioning
- Unmanaged access

---

## Control Types

```text
PREVENTIVE
=
STOP IT
```

```text
DETECTIVE
=
FIND IT
```

```text
CORRECTIVE
=
FIX IT
```

---

## Important Events

Monitor events such as:

- Account creation/deletion
- Authentication failures
- Role assignment
- Group changes
- Privileged activation
- MFA changes
- SoD conflicts
- Provisioning failures
- Deprovisioning failures
- Break-glass use

---

## SIEM

```text
AD -----+
Entra --+
IGA ----+---> SIEM
PAM ----+
Apps ---+
```

SIEM provides central correlation, detection and investigation.

---

## Key Principle

> A control should operate, be observable, be correctable, and produce evidence.
