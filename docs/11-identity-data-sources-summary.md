# Authoritative Sources & Identity Data — Summary

## Core Flow

```text
Authoritative Source
        |
        v
     Identity
        |
        v
       IGA
        |
        | Provision
        v
      Target
        |
        | Aggregate
        v
       IGA
        |
        v
    Correlate
        |
        v
    Reconcile
        |
        v
    Remediate
```

---

## Authoritative Source

```text
AUTHORITATIVE SOURCE
=
Trusted origin of identity data
```

Common workforce example:

```text
HR
```

Attributes may include:

- Employee ID
- Status
- Manager
- Department
- Job
- Location
- Start/end dates

---

## Identity vs Account

```text
IDENTITY
=
Alice
```

```text
ACCOUNT
=
Alice's representation
in a target system
```

One identity can own many accounts.

---

## Provisioning

```text
IGA -> TARGET
```

Think:

```text
PUSH CHANGE
```

---

## Aggregation

```text
TARGET -> IGA
```

Think:

```text
BRING BACK ACTUAL STATE
```

---

## Correlation

Question:

```text
WHO owns this account?
```

Mental model:

```text
ACCOUNT -> IDENTITY
```

---

## Reconciliation

Question:

```text
Does ACTUAL match EXPECTED?
```

Mental model:

```text
EXPECTED <-> ACTUAL
```

---

## Out-of-Band Change

```text
Admin
 |
 v
Target Change
 |
 v
Aggregation
 |
 v
Reconciliation
 |
 v
Unexpected Access
```

---

## Closed Loop

```text
REQUEST
   |
CHANGE
   |
VERIFY
```

Do not assume provisioning succeeded.

Verify it.

---

## Key Principle

> Provision outward, aggregate back, correlate ownership, reconcile state, and remediate discrepancies.
