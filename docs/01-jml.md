# Joiner / Mover / Leaver — JML

## 1. What is JML?

**Joiner / Mover / Leaver (JML)** is the process used to manage a person's identity and access throughout their relationship with an organisation.

The basic lifecycle is:

```text
JOINER  --------->  MOVER  --------->  LEAVER
   |                  |                  |
   v                  v                  v
Create             Modify              Disable
identity           access              / Remove
   |                  |                  |
   v                  v                  v
Provision          Reassess            Revoke
access             access              access
```

The objective is simple:

> Give the right person the right access at the right time — and remove it when it is no longer required.

---

# 2. Joiner

A **Joiner** is someone entering the organisation or beginning a new relationship with it.

Examples:

- New employee
- Contractor
- Consultant
- Temporary worker
- External partner

## Typical Joiner Flow

```text
HR / Authoritative Source
          |
          v
     Person created
          |
          v
    Identity created
          |
          v
    Account created
          |
          v
   Birthright access
          |
          v
Additional access if required
```

HR is often the **authoritative source** for employees.

Typical identity attributes include:

- Employee ID
- First name
- Last name
- Email address
- Department
- Job title
- Manager
- Location
- Employment type
- Start date
- End date

These attributes can drive IAM decisions.

## Birthright Access

**Birthright access** is access automatically granted because of who the person is or their position in the organisation.

For example:

```text
Employee
   |
   +-- Corporate account
   +-- Email
   +-- Intranet
   +-- Standard collaboration tools
```

A Finance employee might additionally receive access based on their role or department.

More sensitive access normally requires an explicit request and approval.

---

# 3. Mover

A **Mover** is someone whose position or relevant attributes change while they remain within the organisation.

Examples:

- Department change
- New job
- Promotion
- New manager
- Location change
- Employee becomes manager
- Contractor becomes employee

A Mover event is particularly important because access should not simply accumulate.

## Example

Alice moves from:

```text
Finance
```

to:

```text
Procurement
```

A bad implementation would simply add Procurement access:

```text
Finance access
      +
Procurement access
```

Alice could then retain unnecessary Finance privileges.

This is known as **access accumulation** or **privilege creep**.

A proper Mover process performs an access reassessment:

```text
             MOVER
               |
        Finance -> Procurement
               |
        +------+------+
        |             |
        v             v
Remove obsolete    Add required
Finance access     Procurement access
```

The IAM system should determine:

- What access must be removed?
- What access should be retained?
- What new access is automatically granted?
- What new access requires approval?
- Does the resulting access create an SoD conflict?

---

# 4. Leaver

A **Leaver** is someone whose relationship with the organisation ends.

Examples:

- Employee resignation
- End of contract
- Retirement
- Termination
- End of external collaboration

The main objective is:

> Remove access when the person no longer has a legitimate business reason to use it.

## Typical Leaver Flow

```text
HR / Authoritative Source
          |
          v
     Leaver event
          |
          v
   Disable identity
          |
          v
   Revoke sessions
          |
          v
   Remove access
          |
          v
 Handle ownership
          |
          v
 Retain / delete data
 according to policy
```

Actions can include:

- Disable user account
- Revoke application access
- Remove group memberships
- Revoke privileged access
- Revoke active sessions or tokens
- Disable VPN / remote access
- Revoke certificates or credentials
- Transfer ownership of files or resources
- Transfer application responsibilities
- Handle shared/service accounts owned by the person
- Retain or delete identity data according to policy

The timing depends on the situation.

For a normal departure, deprovisioning may occur at the agreed end date.

For an immediate termination, access may need to be revoked immediately.

---

# 5. Authoritative Source

JML normally begins with a trusted **authoritative source**.

For employees this is commonly an HR system.

```text
HR
 |
 | employee created
 | employee changed
 | employee terminated
 |
 v
IAM
 |
 +--> Directory
 +--> Email
 +--> Applications
 +--> Cloud platforms
 +--> Other target systems
```

The IAM system consumes identity information and translates lifecycle events into access actions.

This reduces dependence on manual account administration.

---

# 6. Provisioning and Deprovisioning

**Provisioning** creates or grants access.

Examples:

- Create an account
- Add a group membership
- Assign an application
- Assign a role

**Deprovisioning** removes or disables access.

Examples:

- Disable an account
- Remove a group membership
- Remove an application entitlement
- Revoke a privileged role

JML tells us **when identity changes occur**.

Provisioning and deprovisioning perform the resulting changes in target systems.

---

# 7. Important JML Risks

### Orphan Account

An account remains active even though the person no longer has a valid relationship with the organisation.

Example:

```text
Employee leaves
      |
      X  Leaver process fails
      |
      v
Account remains active
```

### Privilege Creep

A user accumulates access over time because old access is not removed after changes.

```text
Finance
   |
   v
Procurement
   |
   v
Operations

Result if poorly managed:

Finance + Procurement + Operations access
```

### Delayed Deprovisioning

A person has left but still has access.

This creates an obvious security risk.

### Incorrect Identity Data

If IAM decisions depend on attributes such as department, manager or employment status, incorrect source data can result in incorrect access.

---

# 8. Related Lifecycle Cases

JML also needs to handle situations such as:

- Rehire
- Return from extended absence
- Contractor extension
- Contractor becoming employee
- Temporary access
- External users
- Guest users
- Dormant accounts

These are variations of the same fundamental lifecycle principles.

---

# 9. Auditability

A good JML process should make it possible to determine:

- Who was created?
- When was the identity created?
- Why was access granted?
- What access was granted?
- What changed?
- What access was removed?
- When was it removed?
- Which source triggered the change?
- Who approved access when approval was required?

This provides **traceability** throughout the identity lifecycle.

---

# 10. Key Concepts to Remember

```text
JOINER
  -> Create identity
  -> Provision initial access
  -> Apply birthright access

MOVER
  -> Reassess existing access
  -> Remove obsolete access
  -> Add required access
  -> Avoid privilege creep
  -> Check for access conflicts

LEAVER
  -> Disable identity
  -> Revoke access
  -> Revoke sessions/credentials
  -> Handle ownership and retention
```

And the central principle:

> **Right person — right access — right time — right reason.**

JML is not only about creating and deleting accounts.

It is about maintaining appropriate access throughout the complete identity lifecycle.
