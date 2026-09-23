# JML — Quick Reference

## Joiner / Mover / Leaver

```text
JOINER                  MOVER                   LEAVER
  |                       |                        |
Create                  Change                   Leave
  |                       |                        |
Provision              Reassess                 Revoke
  |                       |                        |
Birthright        Remove old + add new       Deprovision
                          |
                    Avoid privilege
                        creep
```

## Joiner

A person enters the organisation.

**Main actions:**

- Create the identity
- Create required accounts
- Provision initial access
- Assign birthright access
- Request/approve additional access when required

**Think:** `Create -> Provision`

---

## Mover

A person's role, department, location, responsibilities, or other relevant attributes change.

**Main actions:**

- Reassess existing access
- Remove access that is no longer required
- Retain access that is still justified
- Add newly required access
- Check for SoD conflicts / toxic combinations
- Prevent privilege creep

**Think:** `Reassess -> Remove old -> Add new`

A Mover should **not simply add more access**.

---

## Leaver

A person's relationship with the organisation ends.

**Main actions:**

- Disable identity/accounts
- Revoke access
- Revoke active sessions/tokens
- Revoke privileged access
- Remove group memberships and entitlements
- Revoke credentials where applicable
- Transfer ownership/responsibilities
- Retain or delete data according to policy

**Think:** `Disable -> Revoke -> Deprovision`

---

## Five Key JML Concepts

### 1. Authoritative Source

The trusted source providing identity lifecycle information.

Typically:

```text
HR -> IAM -> Target Systems
```

HR may tell IAM that a person:

- joined
- changed role
- changed department
- changed manager
- changed employment status
- left

---

### 2. Birthright Access

Access automatically granted because of the person's identity, status, role, department, location, or other attributes.

Examples:

- Corporate account
- Email
- Intranet
- Standard collaboration tools

More sensitive access normally requires explicit request and approval.

---

### 3. Provisioning

Creating or granting access.

Examples:

- Create account
- Assign application
- Add group membership
- Assign role or entitlement

```text
Identity -> Provision -> Access
```

---

### 4. Deprovisioning

Removing or disabling access.

Examples:

- Disable account
- Remove group membership
- Remove entitlement
- Revoke privileged role
- Revoke credentials

```text
Identity change -> Deprovision -> Access removed
```

---

### 5. Privilege Creep

Access accumulates because obsolete access is not removed when a person's responsibilities change.

Example:

```text
Finance
   |
   v
Procurement
   |
   v
Operations

BAD RESULT:

Finance + Procurement + Operations
```

A proper Mover process prevents this by reassessing existing access.

---

## Important Risks

### Orphan Account

An account remains active without a valid owner or after the person has left.

### Delayed Deprovisioning

Access remains active after it should have been removed.

### Incorrect Identity Data

Incorrect information from an authoritative source can result in incorrect access decisions.

### Privilege Creep

Users accumulate unnecessary access over time.

---

## JML in One Flow

```text
Authoritative Source
        |
        v
       JML
        |
        +---- JOINER ----> Create + Provision
        |
        +---- MOVER -----> Reassess + Modify
        |
        +---- LEAVER ----> Revoke + Deprovision
        |
        v
   Target Systems
```

## Core Principle

> **Right person — right access — right time — right reason.**

JML is not simply account creation and deletion.

It is the continuous management of appropriate identity and access throughout the complete identity lifecycle.
