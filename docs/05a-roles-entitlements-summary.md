# Roles & Entitlements — Summary

## Core Model

```text
IDENTITY
   |
   v
BUSINESS ROLE
   |
   v
TECHNICAL ROLE
   |
   v
ENTITLEMENT
   |
   v
TARGET SYSTEM
```

## Entitlement

An entitlement is a specific access right.

Examples:

- AD group
- Entra ID group
- SAP role
- Application permission
- Database role
- File share permission

Example:

```text
SAP-FI-DISPLAY
```

## Role

A role groups access together.

Example:

```text
Finance Analyst
      |
      +-- AD Finance Group
      +-- SAP FI Display
      +-- Finance Portal
```

## Business Role

Represents what someone does.

Examples:

- Finance Analyst
- HR Manager
- Procurement Officer

## Technical Role

Represents technical access needed to perform that function.

Examples:

```text
AD-FINANCE
SAP-FI-READ
ENTRA-FINANCE
```

## Group vs Role

A group is often a technical object.

A role represents a business or technical access concept.

A group can therefore be an entitlement inside a role.

## Direct Assignment

Access can also be granted directly:

```text
Alice
  |
  +-- Finance Analyst Role
  |
  +-- SPECIAL_REPORT_ACCESS
```

Too many direct assignments make governance harder.

## Role Engineering

Designing roles and deciding which entitlements belong to them.

```text
Business Need
     |
     v
Design Role
     |
     v
Assign Entitlements
```

## Role Mining

Discovering role candidates from existing access patterns.

```text
Existing Access
      |
      v
Find Patterns
      |
      v
Candidate Roles
```

## Role Explosion

Too many highly specific roles make the model difficult to manage.

## JML Relationship

Mover events should trigger role reassessment.

```text
Finance Role
     |
   MOVER
     |
     v
Procurement Role
```

Old roles should be removed when no longer required.

## SoD Relationship

Roles or entitlements may conflict.

```text
CREATE_PAYMENT
      +
APPROVE_PAYMENT
      =
TOXIC COMBINATION
```

## Key Principle

> Roles simplify access management; entitlements represent the actual access.
