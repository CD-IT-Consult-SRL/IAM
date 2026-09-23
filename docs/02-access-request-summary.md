# Access Request & Provisioning — Summary

## Core Idea

Access generally comes from two sources:

```text
ACCESS
  |
  +-- Birthright Access
  |
  +-- Requested Access
```

## Birthright Access

Automatically granted based on identity attributes such as:

- Department
- Role
- Location
- Employment type
- Business unit

Example:

```text
Employee
  |
  +-- Email
  +-- Collaboration tools
  +-- Intranet
```

## Requested Access

Access that requires an explicit request and usually approval.

```text
Request
   |
   v
Approval
   |
   v
Policy / SoD Check
   |
   v
Provisioning
   |
   v
Access Granted
```

## Identity, Account, Entitlement

```text
IDENTITY
   |
   v
ACCOUNT
   |
   v
ENTITLEMENT
```

### Identity

Who the person or entity is.

### Account

How the identity exists in a particular target system.

### Entitlement

The actual access granted.

Examples:

- Group membership
- Application role
- Permission
- Privilege
- License

## Provisioning

Provisioning means actually creating or granting access.

Examples:

- Create account
- Add group membership
- Assign role
- Assign application
- Grant entitlement

Targets and mechanisms may include:

- Active Directory
- Microsoft Entra ID
- LDAP directories
- SCIM
- APIs
- SaaS applications
- Business applications

## Deprovisioning

Removing or disabling access.

Typical triggers:

- Mover
- Leaver
- Access expiration
- Recertification
- Policy violation

## Approval

Depending on the access, approval may involve:

- Manager
- Application owner
- Data owner
- Role owner
- Security
- Compliance

## Key Principle

> Requesting access does not mean being entitled to access.

The request starts the decision process.

## Mental Model

```text
WHO?
Identity

WHERE?
Account

WHAT ACCESS?
Entitlement

HOW GRANTED?
Provisioning
```
