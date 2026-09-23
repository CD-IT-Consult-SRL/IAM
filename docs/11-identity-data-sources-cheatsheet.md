# Identity Data — Cheat Sheet

## Five Essential Terms

```text
AUTHORITATIVE SOURCE
=
TRUSTED ORIGIN
```

```text
PROVISIONING
=
IGA -> TARGET
```

```text
AGGREGATION
=
TARGET -> IGA
```

```text
CORRELATION
=
ACCOUNT -> IDENTITY
```

```text
RECONCILIATION
=
EXPECTED vs ACTUAL
```

---

## Identity vs Account

```text
Alice
=
IDENTITY
```

```text
asmith in AD
=
ACCOUNT
```

```text
Alice
 |
 +-- AD account
 +-- Entra account
 +-- SAP account
```

---

## Direction Trick

```text
       IGA
        |
        | PROVISION
        v
      TARGET
        |
        | AGGREGATE
        v
       IGA
```

Remember:

```text
PROVISION = OUT

AGGREGATE = IN
```

---

## Correlation

```text
asmith
   |
   v
Alice
```

Question:

```text
WHO OWNS THIS ACCOUNT?
```

---

## Reconciliation

```text
EXPECTED
   |
   X
   |
ACTUAL
```

Question:

```text
DO THEY MATCH?
```

---

## Orphan Account

```text
ACCOUNT
   |
   X
No valid owner
```

---

## Out-of-Band Change

```text
Admin -> Target
          |
          v
      Aggregation
          |
          v
     Reconciliation
          |
          v
        Detect
```

---

## Closed Loop

```text
PROVISION
    |
    v
TARGET
    |
    v
AGGREGATE
    |
    v
VERIFY
```

---

# 10-Second Memory

```text
Authoritative = TRUST

Provision      = OUT

Aggregate      = IN

Correlate      = WHO

Reconcile      = MATCH?

Remediate      = FIX
```

> Push the desired state out. Bring the actual state back. Compare them.
