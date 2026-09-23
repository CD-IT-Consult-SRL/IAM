# Roles & Entitlements

## 1. Overview

An **entitlement** represents a specific access right or capability.

A **role** groups access together so that it can be assigned and managed more easily.

The basic mental model is:

```text
IDENTITY
   |
   v
 ROLE
   |
   v
ENTITLEMENTS
   |
   v
RESOURCES
```

Example:

```text
Alice
  |
  v
Finance Analyst
  |
  +-- Finance Portal access
  +-- SAP FI display
  +-- Finance AD group
```

---

# 2. What is an Entitlement?

An entitlement is something that grants or represents access in a target system.

Examples include:

- Group membership
- Application role
- Permission
- Privilege
- Database access
- File share access
- Application access
- Cloud role

Examples:

```text
AD group:
GG-FINANCE-USERS

Entra ID group:
Finance-Portal-Users

SAP role:
FI_DISPLAY

Database role:
REPORTING_READ
```

From an IAM/IGA perspective, these can all be treated as **entitlements**.

---

# 3. What is a Role?

A role groups access that is required for a particular function or purpose.

Instead of assigning many individual entitlements:

```text
Alice
 |
 +-- Entitlement A
 +-- Entitlement B
 +-- Entitlement C
 +-- Entitlement D
```

we can assign:

```text
Alice
 |
 v
Finance Analyst
 |
 +-- Entitlement A
 +-- Entitlement B
 +-- Entitlement C
 +-- Entitlement D
```

This makes access easier to understand and manage.

---

# 4. Business Role

A **business role** represents what someone does in the organisation.

Examples:

```text
Finance Analyst
Procurement Officer
HR Manager
Helpdesk Operator
```

A business role should make sense to the business.

Example:

```text
Alice
  |
  v
Finance Analyst
```

---

# 5. Technical Role

A **technical role** groups technical permissions or entitlements.

Example:

```text
Finance Analyst
      |
      +-- FINANCE-AD
      |
      +-- SAP-FI-READ
      |
      +-- FINANCE-REPORTING
```

The business understands:

```text
Finance Analyst
```

The IAM platform translates that into the technical access required across target systems.

---

# 6. Role Hierarchy

A simplified model can look like:

```text
IDENTITY
   |
   v
BUSINESS ROLE
   |
   v
TECHNICAL ROLES
   |
   v
ENTITLEMENTS
   |
   v
TARGET SYSTEMS
```

Example:

```text
Alice
  |
  v
Finance Analyst
  |
  +-- AD Finance Role
  |       |
  |       +-- GG-FINANCE-USERS
  |
  +-- SAP Finance Role
  |       |
  |       +-- FI_DISPLAY
  |       +-- FI_REPORTING
  |
  +-- Entra Finance Role
          |
          +-- Finance-Portal-Users
```

---

# 7. Groups vs Roles

A group and a role are related concepts, but they are not necessarily the same thing.

A group is often a technical object used by a target system.

Examples:

```text
Active Directory Group
Entra ID Group
LDAP Group
```

A role generally represents a collection of access associated with a function or purpose.

For example:

```text
Business Role
Finance Analyst
      |
      +-- AD group
      +-- Entra ID group
      +-- SAP role
      +-- Application permission
```

A group can therefore be an **entitlement contained within a role**.

---

# 8. Direct Entitlement Assignment

Access does not always come through a role.

For example:

```text
Alice
  |
  +-- Finance Analyst Role
  |
  +-- SPECIAL_REPORT_ACCESS
```

`SPECIAL_REPORT_ACCESS` may have been individually requested and approved.

This is a **direct entitlement assignment**.

Too many direct assignments can make access difficult to understand and govern.

---

# 9. Role Engineering

**Role engineering** is the process of designing roles and determining which entitlements belong to them.

A simple example:

```text
Finance Analysts require:

- Finance Portal
- SAP FI display
- Reporting access
```

These can be grouped into:

```text
Finance Analyst Role
```

Role engineering can involve both business requirements and technical analysis.

---

# 10. Role Mining

**Role mining** works in the other direction.

Existing access is analysed to discover common patterns.

Example:

```text
Alice -> A B C
Bob   -> A B C
Carol -> A B C
David -> A B C
```

This may suggest that:

```text
A + B + C
```

could form a reusable role.

```text
Existing Access
      |
      v
Find Patterns
      |
      v
Candidate Roles
```

---

# 11. Role Explosion

Roles are useful, but creating too many roles creates another problem.

Example:

```text
Finance-Belgium-Junior
Finance-Belgium-Senior
Finance-France-Junior
Finance-France-Senior
Finance-Belgium-Manager
...
```

This is commonly called **role explosion**.

The role model becomes difficult to:

- Understand
- Maintain
- Review
- Govern

This is one reason organisations may combine RBAC with attribute-based controls.

---

# 12. Role Ownership

Roles and entitlements should have clear ownership.

Typical owners include:

```text
Business Role
    |
    v
Business / Role Owner

Application Entitlement
    |
    v
Application Owner

Data Permission
    |
    v
Data Owner
```

Ownership matters because someone must be responsible for deciding:

- Who should receive the access?
- What does the access allow?
- Is the access still required?
- Should it be approved?
- Should it be removed?

---

# 13. Relationship with JML

Roles are frequently affected by lifecycle events.

Example:

```text
Alice

Finance
   |
   v
Finance Analyst Role
```

Alice moves to Procurement:

```text
MOVER EVENT
     |
     +-- Remove Finance Analyst Role
     |
     +-- Add Procurement Role
     |
     v
Recalculate Entitlements
```

This prevents old access from simply accumulating.

---

# 14. Relationship with Recertification

Roles and entitlements must periodically be reviewed.

The organisation may ask:

```text
Does Alice still need Finance Analyst?
```

or:

```text
Does Alice still need FI_DISPLAY?
```

The answer may be:

```text
KEEP
```

or:

```text
REVOKE
```

This is part of **access recertification**.

---

# 15. Relationship with SoD

Individual roles may be acceptable on their own but dangerous when combined.

Example:

```text
Create Supplier
      +
Approve Supplier Payment
```

Each entitlement may be legitimate.

Together they may create a **toxic combination**.

This is where Segregation of Duties (SoD) controls become important.

---

# 16. What to Remember

```text
ENTITLEMENT
=
A specific access right
```

```text
ROLE
=
A collection of access associated
with a function or purpose
```

```text
BUSINESS ROLE
=
What someone does
```

```text
TECHNICAL ROLE
=
Technical access required to support it
```

```text
GROUP
=
Often a technical object that can
represent an entitlement
```

```text
ROLE MINING
=
Existing access -> discover role patterns
```

```text
ROLE ENGINEERING
=
Design roles -> assign appropriate entitlements
```

```text
ROLE EXPLOSION
=
Too many roles -> difficult governance
```

---

# Key Mental Model

```text
WHO?
 |
 v
Identity

DOES WHAT?
 |
 v
Business Role

NEEDS WHAT?
 |
 v
Technical Roles / Entitlements

WHERE?
 |
 v
AD / Entra ID / SAP / Applications / Databases / ...
```

> Roles simplify access management; entitlements represent the actual access.
