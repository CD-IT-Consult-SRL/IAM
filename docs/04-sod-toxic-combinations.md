# Segregation of Duties (SoD) & Toxic Combinations

## 1. Overview

**Segregation of Duties (SoD)** prevents one person from having a combination of access that would allow them to perform incompatible or excessively powerful activities alone.

The basic principle is:

> Critical activities should require more than one independent person.

A **toxic combination** is a combination of roles or entitlements that creates an unacceptable risk.

---

## 2. Simple Example

Consider a payment process.

```text
Create Payment
      +
Approve Payment
      =
TOXIC COMBINATION
```

Each entitlement is legitimate on its own.

The problem is having both.

```text
Alice
  |
  +-- CREATE_PAYMENT
  |
  +-- APPROVE_PAYMENT
           |
           v
       SoD Conflict
```

Alice could potentially create a fraudulent payment and approve it herself.

A safer model is:

```text
Alice                         Bob
  |                            |
  v                            v
Create Payment          Approve Payment
        \                  /
         \                /
          v              v
             Payment
```

---

# 3. Another Example — Supplier Management

Consider:

```text
CREATE_SUPPLIER
       +
APPROVE_SUPPLIER
       +
MAKE_PAYMENT
```

Giving all three capabilities to one person creates significant risk.

An organisation might define rules such as:

```text
CREATE_SUPPLIER
      X
APPROVE_SUPPLIER
```

and:

```text
MAINTAIN_SUPPLIER
      X
APPROVE_PAYMENT
```

The `X` represents an incompatible combination.

---

# 4. SoD Rules

An SoD rule defines combinations of access that should not normally exist together.

Example:

```text
Rule: SOD-FIN-001

Entitlement A:
CREATE_PAYMENT

conflicts with

Entitlement B:
APPROVE_PAYMENT
```

The rule can operate against:

- Roles
- Entitlements
- Privileges
- Groups
- Application permissions

---

# 5. Preventive SoD

**Preventive SoD** checks for conflicts before access is granted.

Example:

```text
Alice already has:
CREATE_PAYMENT

Alice requests:
APPROVE_PAYMENT

        |
        v
     SoD Check
        |
        v
 Conflict Detected
        |
        v
   BLOCK / REVIEW
```

This prevents the toxic combination from being created.

Think:

```text
Preventive SoD
=
Check BEFORE granting access
```

---

# 6. Detective SoD

**Detective SoD** searches for conflicts that already exist.

Example:

```text
Existing Access
      |
      v
   SoD Scan
      |
      v
Conflict Found

Alice:
CREATE_PAYMENT
+
APPROVE_PAYMENT
```

The conflict must then be investigated and remediated.

Think:

```text
Detective SoD
=
Find conflicts AFTER they exist
```

---

# 7. Why Both Are Needed

Preventive controls help stop new conflicts.

Detective controls identify conflicts that may already exist because of:

- Legacy access
- Manual changes
- Direct assignments
- Mover events
- Provisioning errors
- Changes made outside IAM
- Changes to SoD rules

Therefore:

```text
Preventive
    +
Detective
    =
Better SoD Control
```

---

# 8. SoD During an Access Request

SoD can be integrated directly into the access request workflow.

```text
Access Request
      |
      v
Requested Entitlement
      |
      v
Compare with Existing Access
      |
      v
    SoD Check
     /     \
    /       \
 No Conflict Conflict
    |          |
    v          v
Approval    Block / Exception
    |          |
    v          v
Provision   Risk Review
```

The important point is that the SoD check considers not only the requested access, but also the access the user already has.

---

# 9. SoD and Roles

Conflicts can also exist between roles.

Example:

```text
Role A
Accounts Payable Operator

Role B
Payment Approver
```

An SoD rule may specify:

```text
Accounts Payable Operator
           X
Payment Approver
```

But conflicts may also exist deeper inside the roles:

```text
Role A
  |
  +-- CREATE_PAYMENT

Role B
  |
  +-- APPROVE_PAYMENT
```

Therefore SoD analysis may need to examine the underlying entitlements.

---

# 10. Risk Acceptance and Exceptions

Sometimes the business cannot completely avoid an SoD conflict.

For example:

```text
Small remote office
Only one Finance employee
```

The organisation may decide to accept the risk temporarily.

This should not simply mean:

```text
SoD conflict -> Ignore
```

Instead:

```text
SoD Conflict
      |
      v
Risk Assessment
      |
      v
Business / Risk Approval
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

---

# 11. Compensating Controls

A **compensating control** reduces the risk when the preferred control cannot be fully implemented.

Examples:

- Independent transaction review
- Manager review
- Additional approval
- Enhanced logging
- Increased monitoring
- Daily reconciliation
- Transaction limits
- Periodic review

Example:

```text
Alice has conflicting access
          |
          v
Approved Exception
          |
          v
Every payment independently
reviewed by Finance Manager
```

The conflict still exists.

The compensating control reduces the associated risk.

---

# 12. SoD and Mover Events

Mover events are particularly important.

Example:

Alice previously worked in Accounts Payable:

```text
CREATE_PAYMENT
```

She moves to Payment Approval and receives:

```text
APPROVE_PAYMENT
```

If the old entitlement is not removed:

```text
CREATE_PAYMENT
      +
APPROVE_PAYMENT
      =
SoD Conflict
```

This connects:

```text
Mover
  |
  v
Privilege Creep
  |
  v
Toxic Combination
```

A good Mover process therefore includes access reassessment and SoD checking.

---

# 13. SoD and Recertification

Recertification can identify inappropriate access that already exists.

Example:

```text
Access Review
     |
     v
Alice's Access
     |
     +-- CREATE_PAYMENT
     +-- APPROVE_PAYMENT
              |
              v
         SoD Conflict
              |
              v
          Remediation
```

This is one reason access governance is continuous rather than a one-time activity.

---

# 14. Common Risks

## Conflict Not Detected

The IAM system grants access without checking existing entitlements.

## Conflict Hidden Inside Roles

Two apparently legitimate roles contain conflicting underlying permissions.

## Direct Access

An entitlement is assigned manually outside the normal IAM workflow.

## Permanent Exceptions

A temporary SoD exception is approved but never expires or gets reviewed.

## Stale Access

Old access remains after a Mover event and creates a new conflict.

---

# 15. What to Remember

```text
SoD
=
Separate incompatible responsibilities
```

```text
TOXIC COMBINATION
=
Two or more individually valid accesses
that become risky when combined
```

```text
PREVENTIVE SoD
=
Check before granting access
```

```text
DETECTIVE SoD
=
Find conflicts that already exist
```

```text
EXCEPTION
=
Documented acceptance of a conflict
```

```text
COMPENSATING CONTROL
=
Additional control used to reduce
the accepted risk
```

---

# Key Mental Model

```text
             EXISTING ACCESS
                    +
             REQUESTED ACCESS
                    |
                    v
                SoD CHECK
               /         \
              /           \
             v             v
           SAFE         CONFLICT
             |             |
             v             v
          GRANT       BLOCK / REVIEW
                           |
                           v
                       EXCEPTION?
                           |
                    +------+------+
                    |             |
                   NO            YES
                    |             |
                    v             v
                  DENY       COMPENSATING
                               CONTROL
```

The most important idea is:

> Access can be legitimate individually but unacceptable when combined.
