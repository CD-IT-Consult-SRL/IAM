# RBAC & ABAC — Summary

## RBAC

**Role-Based Access Control**

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
  +-- Finance Portal
  +-- Reporting
  +-- SAP FI Display
```

RBAC answers:

> What role does this person have?

## ABAC

**Attribute-Based Access Control**

Access is determined using attributes and policies.

Example:

```text
department = Finance
AND
location = Belgium
AND
device = Managed
        |
        v
Allow Access
```

ABAC can use:

### User Attributes

- Department
- Job title
- Location
- Employment type

### Resource Attributes

- Application
- Classification
- Owner

### Context Attributes

- Time
- Device
- Network
- Risk

ABAC answers:

> What attributes and conditions apply?

## RBAC + ABAC

They can be combined.

```text
Role = Finance Analyst
AND
Device = Managed
AND
Location = Belgium
```

RBAC provides structure.

ABAC adds contextual or dynamic control.

## Business vs Technical Roles

```text
Business Role
Finance Analyst
      |
      +-- AD group
      +-- SAP role
      +-- Entra group
```

## Risks

### RBAC

- Wrong role assignment
- Role explosion
- Excessive role membership

### ABAC

- Incorrect attributes
- Complex policies
- Poor source data

## JML Relationship

A Mover event may change:

```text
Finance -> Procurement
```

which can trigger:

```text
Remove Finance Role
Add Procurement Role
Recalculate Access
```

or change ABAC decisions directly through identity attributes.

## Key Principle

> Good access control depends on good identity data.
