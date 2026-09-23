# Access Request & Provisioning — Cheat Sheet

## Two Types of Access

```text
BIRTHRIGHT
=
Automatic baseline access
```

```text
REQUESTED
=
Request -> Approval -> Control -> Provision
```

## Key Terms

```text
Identity
=
WHO
```

```text
Account
=
Identity inside a target system
```

```text
Entitlement
=
WHAT ACCESS
```

```text
Provisioning
=
GRANT / CREATE
```

```text
Deprovisioning
=
REMOVE / DISABLE
```

## Example

```text
Alice
  |
  v
Requests SAP access
  |
  v
Manager Approval
  |
  v
Application Owner
  |
  v
SoD Check
  |
  v
Provision
```

## Typical Targets

```text
AD
Entra ID
LDAP
SCIM
APIs
Applications
Cloud platforms
```

## 10-Second Memory

```text
Birthright = automatic

Request = ask

Approval = authorize

SoD = check conflict

Provision = grant

Entitlement = access itself
```

> A request is not an authorization.
