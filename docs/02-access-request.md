# Access Request & Provisioning

## 1. Overview

Access can generally come from two main sources:

```text
                 ACCESS
                    |
          +---------+---------+
          |                   |
          v                   v
     BIRTHRIGHT           REQUESTED
       ACCESS               ACCESS
          |                   |
          |                   v
          |                Request
          |                   |
          |                   v
          |                Approval
          |                   |
          |                   v
          |               SoD Check
          |                   |
          +---------+---------+
                    |
                    v
               Provision
                    |
                    v
               Entitlement
```

The key difference is:

- **Birthright access** is granted automatically.
- **Requested access** requires an explicit request and usually one or more approvals.

---

## 2. Birthright Access

Birthright access is automatically granted because of who the person is or because of attributes associated with the identity.

Typical attributes include:

- Department
- Job role
- Location
- Employment type
- Business unit
- Manager
- Employee status

Example:

```text
Department = Finance
Location   = Brussels
Type       = Employee
```

This could automatically result in:

```text
Corporate account
Email
Collaboration tools
Finance portal
```

Birthright access should normally represent the standard minimum access required for the person's role.

---

## 3. Requested Access

Some access is too sensitive or too specific to be automatically granted.

In that case, an access request is required.

Typical flow:

```text
User / Manager
      |
      v
Access Request
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

---

## 4. Approval Workflow

Depending on the type of access, approval can involve:

- Manager
- Application owner
- Data owner
- Role owner
- Security
- Compliance
- Privileged access owner

Example:

```text
Alice requests access to Payment Application
                |
                v
         Manager Approval
                |
                v
      Application Owner Approval
                |
                v
             SoD Check
                |
                v
            Provision
```

Not every access request requires multiple approvals.

The approval workflow should be proportional to the sensitivity and risk of the requested access.

---

## 5. Identity, Account and Entitlement

These three concepts are important to distinguish.

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

Represents the person or non-human entity.

Example:

```text
Alice Smith
```

### Account

Represents the identity inside a specific system.

Examples:

```text
alice.smith
asmith
alice@company.com
```

### Entitlement

Represents what the account is allowed to access or do.

Examples:

- Group membership
- Application role
- Permission
- Privilege
- License
- Resource access

Example:

```text
Alice Smith                         Identity

      |
      +-- alice@company.com         Account
      |       |
      |       +-- Finance-Users     Entitlement
      |       +-- VPN-Users         Entitlement
      |
      +-- ASMITH (SAP)              Account
              |
              +-- FI_DISPLAY        Entitlement
              +-- FI_REPORTING      Entitlement
```

---

## 6. Provisioning

Provisioning is the technical process of actually creating or granting access.

Examples:

- Create an account
- Add a group membership
- Assign a role
- Assign an application
- Assign a license
- Grant an entitlement

Provisioning can be:

- Manual
- Automated
- Connector-based
- API-based
- SCIM-based
- LDAP-based

---

## 7. Deprovisioning

Deprovisioning removes or disables access.

Examples:

- Disable an account
- Remove a group membership
- Remove a role
- Remove an entitlement
- Revoke privileged access
- Remove an application assignment

Deprovisioning is especially important during:

- Mover events
- Leaver events
- Access review remediation
- Access expiration
- Policy violations

---

## 8. Example

Alice works in Finance.

She automatically receives:

```text
Email
Teams
Finance portal
```

This is birthright access.

Alice then needs access to a payment application.

```text
Alice
  |
  v
Request Payment Application
  |
  v
Manager Approval
  |
  v
Application Owner Approval
  |
  v
SoD Check
  |
  v
Provision Entitlement
```

The requested entitlement is only granted after the appropriate checks and approvals.

---

## 9. Key Risks

### Excessive Access

Users receive more access than necessary.

### Inappropriate Approval

The wrong person approves access.

### Missing SoD Check

Access is granted even though it creates a toxic combination.

### Manual Provisioning Error

The requested access and the actual provisioned access do not match.

### Access Not Removed

Temporary or obsolete access remains active.

---

## 10. What to Remember

```text
BIRTHRIGHT
    =
Automatic baseline access
```

```text
ACCESS REQUEST
    =
Request -> Approval -> Controls -> Provisioning
```

```text
PROVISIONING
    =
Actually create or grant the access
```

```text
ENTITLEMENT
    =
The permission, role, group or access being granted
```

```text
IDENTITY
    =
Who the person is
```

```text
ACCOUNT
    =
How that identity exists in a target system
```

---

## Core Principle

> Requesting access does not mean being entitled to access.

The request starts the decision process.

Access should only be granted when it is justified, approved, compliant with policy, and properly provisioned.
