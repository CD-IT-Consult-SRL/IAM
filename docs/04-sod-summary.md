# SoD & Toxic Combinations — Summary

## Core Idea

**Segregation of Duties (SoD)** prevents one person from having incompatible responsibilities that together create unacceptable risk.

The key idea:

```text
Access A = OK

Access B = OK

Access A + Access B = RISK
```

The combination is called a **toxic combination**.

---

## Classic Example

```text
CREATE PAYMENT
      +
APPROVE PAYMENT
      =
TOXIC COMBINATION
```

The two permissions are legitimate individually.

The problem is having both.

A safer model:

```text
Alice                    Bob
  |                       |
  v                       v
Create Payment      Approve Payment
       \                /
        \              /
         v            v
            Payment
```

No single person controls the complete transaction.

---

## SoD Rule

An SoD rule defines incompatible access.

Example:

```text
CREATE_PAYMENT
      X
APPROVE_PAYMENT
```

The rule may compare:

- Roles
- Entitlements
- Groups
- Permissions
- Privileges

---

## Preventive SoD

Checks for conflicts **before access is granted**.

```text
Existing Access
      +
Requested Access
      |
      v
   SoD Check
    /    \
   /      \
 SAFE    CONFLICT
  |         |
  v         v
GRANT    BLOCK/REVIEW
```

Remember:

```text
PREVENTIVE
=
BEFORE
```

---

## Detective SoD

Looks for conflicts that **already exist**.

```text
Existing Access
      |
      v
   SoD Scan
      |
      v
Conflict Found
      |
      v
Remediation
```

Remember:

```text
DETECTIVE
=
AFTER
```

Both preventive and detective controls are important.

---

## Exceptions

Sometimes a conflict cannot practically be avoided.

The conflict should not simply be ignored.

```text
Conflict
   |
   v
Risk Assessment
   |
   v
Approval
   |
   v
Documented Exception
   |
   v
Compensating Control
   |
   v
Expiration / Review
```

Exceptions should normally be:

- Justified
- Approved
- Documented
- Time-bound
- Reviewed

---

## Compensating Controls

A compensating control reduces the risk when an SoD conflict must temporarily or exceptionally exist.

Examples:

- Independent review
- Additional approval
- Transaction monitoring
- Enhanced logging
- Reconciliation
- Transaction limits
- Periodic review

Important:

```text
Compensating control
!=
Conflict removed
```

The conflict still exists.

The additional control reduces the risk.

---

## Relationship with Access Requests

```text
Access Request
      |
      v
Approval
      |
      v
SoD Check
      |
   +--+--+
   |     |
   v     v
 SAFE  CONFLICT
   |     |
   v     v
Grant  Review
```

The requested entitlement must be evaluated together with the user's **existing access**.

---

## Relationship with Movers

This is a classic source of SoD problems.

```text
Alice in Accounts Payable

CREATE_PAYMENT
```

Alice moves to another function:

```text
Payment Approval
```

New access:

```text
APPROVE_PAYMENT
```

If old access remains:

```text
CREATE_PAYMENT
      +
APPROVE_PAYMENT
      |
      v
TOXIC COMBINATION
```

Therefore:

```text
Mover
  |
  v
Access Reassessment
  |
  v
Remove Old Access
  |
  v
SoD Check
```

Otherwise:

```text
Mover
  |
  v
Old Access Remains
  |
  v
Privilege Creep
  |
  v
Possible SoD Conflict
```

---

## Relationship with Recertification

Recertification helps detect inappropriate access that already exists.

```text
Access Review
     |
     v
Existing Access
     |
     v
SoD Conflict?
   /      \
 NO       YES
 |         |
 v         v
KEEP    REMEDIATE
```

---

# Key Concepts

```text
SoD
=
Separate incompatible responsibilities
```

```text
Toxic Combination
=
Individually legitimate access
that becomes risky when combined
```

```text
Preventive SoD
=
Stop conflicts before granting access
```

```text
Detective SoD
=
Find conflicts that already exist
```

```text
Exception
=
Approved and documented acceptance
of an identified conflict
```

```text
Compensating Control
=
Additional control that reduces
the risk of an accepted conflict
```

---

# Mental Model

```text
              USER
                |
                v
        EXISTING ACCESS
                +
        REQUESTED ACCESS
                |
                v
            SoD CHECK
           /         \
          v           v
        SAFE       CONFLICT
          |           |
          v           v
        GRANT       REVIEW
                      |
               +------+------+
               |             |
               v             v
             DENY        EXCEPTION
                              |
                              v
                       COMPENSATING
                          CONTROL
                              |
                              v
                         REASSESS
```

## One Sentence to Remember

> Access can be legitimate individually but unacceptable when combined.
