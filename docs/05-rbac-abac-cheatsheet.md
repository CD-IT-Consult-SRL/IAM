# RBAC & ABAC — Cheat Sheet

## RBAC

```text
RBAC
=
ROLE decides access
```

```text
User -> Role -> Permissions
```

Example:

```text
Alice
  -> Finance Analyst
      -> SAP FI
      -> Reporting
```

## ABAC

```text
ABAC
=
ATTRIBUTES + RULES decide access
```

Example:

```text
Department = Finance
AND
Location = Belgium
AND
Device = Managed
```

## Difference

```text
RBAC asks:
"What role do you have?"
```

```text
ABAC asks:
"What attributes and conditions apply?"
```

## Together

```text
ROLE
 +
ATTRIBUTES
 +
CONTEXT
 =
ACCESS DECISION
```

## Important Terms

```text
Business Role
=
Business function
```

```text
Technical Role
=
Technical access grouping
```

```text
Role Explosion
=
Too many roles
```

## 10-Second Memory

```text
RBAC = roles

ABAC = attributes

RBAC = structure

ABAC = flexibility

Both depend on good identity data
```
