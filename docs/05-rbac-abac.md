# RBAC and ABAC

## 1. Overview

Two common ways to decide what access a user should receive are:

- **RBAC** — Role-Based Access Control
- **ABAC** — Attribute-Based Access Control

The simplest distinction is:

```text
RBAC
=
Access based on roles
```

```text
ABAC
=
Access based on attributes and rules
```

---

# 2. RBAC — Role-Based Access Control

With RBAC, permissions are grouped into roles.

Users receive access by being assigned to a role.

```text
USER
 |
 v
ROLE
 |
 v
PERMISSIONS
```

Example:

```text
Alice
 |
 v
Finance Analyst
 |
 +-- View invoices
 +-- Run finance reports
 +-- Access finance portal
```

Instead of assigning permissions one by one to Alice, the permissions are assigned to the role.

Alice receives those permissions because she has the role.

---

## 3. Why RBAC is Useful

RBAC simplifies access management.

Without RBAC:

```text
Alice -> Permission 1
Alice -> Permission 2
Alice -> Permission 3

Bob   -> Permission 1
Bob   -> Permission 2
Bob   -> Permission 3
```

With RBAC:

```text
          Finance Analyst
          /      |      \
         /       |       \
Permission1 Permission2 Permission3
     |
     +---- Alice
     +---- Bob
```

The role acts as an abstraction between users and permissions.

---

## 4. Business Roles and Technical Roles

Roles can exist at different levels.

### Business Role

Represents a business function.

Examples:

- Finance Analyst
- HR Manager
- Procurement Officer
- System Administrator

### Technical Role

Represents technical access in one or more systems.

Examples:

- AD-FINANCE-USERS
- SAP-FI-DISPLAY
- ENTRA-FINANCE-PORTAL

A business role may contain several technical roles or entitlements.

Example:

```text
Finance Analyst
       |
       +-- AD-FINANCE-USERS
       +-- SAP-FI-DISPLAY
       +-- ENTRA-FINANCE-PORTAL
```

---

# 5. ABAC — Attribute-Based Access Control

With ABAC, access decisions are based on attributes.

Typical attributes include:

### User attributes

- Department
- Job title
- Location
- Employment type
- Security clearance

### Resource attributes

- Application
- Data classification
- Resource owner
- Environment

### Context attributes

- Time
- Location
- Device
- Network
- Risk level

---

## 6. ABAC Example

Suppose access should only be granted when:

```text
Department = Finance
AND
Location = Belgium
AND
Device = Managed
```

Then the rule can be represented as:

```text
IF
    department == Finance
AND location == Belgium
AND device == Managed
THEN
    Allow access
```

The user does not necessarily need to be explicitly assigned to a static role.

The decision is made from attributes and policy.

---

# 7. RBAC vs ABAC

Simple comparison:

```text
RBAC
----
Who are you in the organisation?
Which role do you have?

ABAC
----
What attributes describe you,
the resource,
and the current context?
```

Example:

```text
RBAC:

Alice
  |
  v
Finance Analyst
  |
  v
Finance Application
```

Example:

```text
ABAC:

User.department = Finance
AND
User.location = Belgium
AND
Device.managed = True
        |
        v
Finance Application
```

---

# 8. RBAC and ABAC Can Work Together

RBAC and ABAC are not necessarily competing models.

They can be combined.

Example:

```text
ROLE = Finance Analyst

AND

Device = Managed

AND

Location = Belgium
```

The role grants eligibility for the application.

Attributes and contextual rules determine whether access is allowed at that moment.

---

# 9. Relationship with JML

RBAC and ABAC are closely related to the identity lifecycle.

Example:

```text
HR changes Alice:

Department:
Finance -> Procurement
```

This creates a Mover event.

The IAM system may then:

```text
Remove Finance role
        |
        v
Assign Procurement role
        |
        v
Recalculate access
```

With ABAC, the department attribute itself may change the access decision.

```text
department = Finance
      |
      X

department = Procurement
      |
      v
Different access policy
```

---

# 10. Risks

## Role Explosion

Too many highly specific roles are created.

Example:

```text
Finance-Belgium-Junior
Finance-Belgium-Senior
Finance-France-Junior
Finance-France-Senior
...
```

This makes RBAC difficult to manage.

---

## Incorrect Role Assignment

A user receives the wrong role and therefore receives incorrect access.

---

## Incorrect Attributes

ABAC depends heavily on accurate attributes.

If:

```text
department = Finance
```

is incorrect, access decisions may also be incorrect.

---

## Overly Complex Policies

ABAC policies can become difficult to understand if too many conditions are combined.

---

# 11. What to Remember

```text
RBAC
=
User -> Role -> Permissions
```

```text
ABAC
=
Attributes + Policy -> Access Decision
```

```text
Business Role
=
Business function
```

```text
Technical Role
=
Technical grouping of entitlements
```

```text
RBAC + ABAC
=
Roles for structure
+
Attributes/context for finer control
```

---

# Key Mental Model

```text
RBAC asks:

"What role does this person have?"
```

```text
ABAC asks:

"What attributes and conditions apply?"
```

And both depend on good identity data.

> Good access control depends on good identity information.
