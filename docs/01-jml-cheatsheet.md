# JML — Cheat Sheet

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

## What to Remember

### JOINER

**Create -> Provision -> Birthright**

A new identity enters the organisation.

- Create identity/account
- Provision baseline access
- Grant birthright access
- Additional access may require approval

---

### MOVER

**Change -> Reassess -> Remove old + Add new**

Something relevant changes:

- Role
- Department
- Location
- Responsibilities
- Employment type

Do not simply add new access.

Remove access that is no longer justified to avoid **privilege creep**.

---

### LEAVER

**Leave -> Revoke -> Deprovision**

The relationship with the organisation ends.

- Disable account
- Revoke access
- Revoke sessions/tokens
- Remove entitlements
- Handle ownership/responsibilities

---

## Five Key Concepts

```text
Authoritative Source
        |
        v
      JOINER
        |
        v
  Birthright Access
        |
        v
    Provisioning
        |
        v
      MOVER
        |
        v
Avoid Privilege Creep
        |
        v
      LEAVER
        |
        v
  Deprovisioning
```

### Authoritative Source
Trusted source of identity information and lifecycle events.

**Typical example:** HR system.

### Birthright Access
Access automatically granted based on identity/status/role.

### Provisioning
Creating accounts or granting access.

### Deprovisioning
Disabling accounts or removing access.

### Privilege Creep
Accumulation of unnecessary access over time, especially after Mover events.

---

## The Mental Model

```text
JOINER = CREATE
MOVER  = REASSESS
LEAVER = REMOVE
```

And remember:

> **Right person — right access — right time — right reason.**
