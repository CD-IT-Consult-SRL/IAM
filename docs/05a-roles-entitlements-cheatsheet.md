# Roles & Entitlements — Cheat Sheet

## Mental Model

```text
WHO?
Identity

DOES WHAT?
Business Role

NEEDS WHAT?
Technical Role / Entitlement

WHERE?
Target System
```

## Key Definitions

```text
IDENTITY
=
WHO
```

```text
ROLE
=
WHAT FUNCTION
```

```text
ENTITLEMENT
=
WHAT ACCESS
```

```text
GROUP
=
Often a technical entitlement
```

## Example

```text
Alice
  |
  v
Finance Analyst
  |
  +-- AD-FINANCE
  +-- SAP-FI-DISPLAY
  +-- ENTRA-FINANCE
```

## Business vs Technical

```text
Business Role
=
Finance Analyst
```

```text
Technical Role
=
SAP / AD / Entra access needed
to perform that job
```

## Role Engineering

```text
Design roles
-> Add correct entitlements
```

## Role Mining

```text
Existing access
-> Find patterns
-> Candidate roles
```

## Role Explosion

```text
Too many roles
=
Hard to understand
Hard to maintain
Hard to govern
```

## 10-Second Memory

```text
Identity    = WHO

Role        = FUNCTION

Entitlement = ACCESS

Role Mining = discover patterns

Role Engineering = design roles

Role Explosion = too many roles
```

> Roles group access. Entitlements are the access.
