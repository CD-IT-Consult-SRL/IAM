# Access Recertification — Summary

## Core Idea

Recertification reviews existing access and asks:

> Does this person still need this access?

Basic flow:

```text
Existing Access
      |
      v
Review Campaign
      |
      v
Reviewer
   /      \
  v        v
KEEP     REVOKE
           |
           v
      Remediation
```

## What Can Be Reviewed?

- Roles
- Entitlements
- Groups
- Application access
- Privileged access
- Accounts
- Temporary access
- External users

## Typical Reviewers

- Manager
- Application owner
- Role owner
- Entitlement owner
- Data owner
- Security / Compliance

## Review Types

### Manager Review

```text
Manager
  |
  v
Review access of team members
```

### Application Review

```text
Application Owner
      |
      v
Review everyone with access
```

### Privileged Access Review

Usually more frequent because of higher risk.

## Periodic vs Event-Driven

```text
Periodic
=
Quarterly / 6-monthly / Annual
```

```text
Event-Driven
=
Triggered by change
```

Examples:

- Mover
- Manager change
- Department change
- Security incident

## Decision

Usually:

```text
KEEP
```

or:

```text
REVOKE
```

## Remediation

A revoke decision must result in actual removal.

```text
REVOKE
   |
   v
Deprovision
   |
   v
Verify Removal
```

## Risks

- Rubber stamping
- Wrong reviewer
- Reviewer does not understand entitlement
- Review fatigue
- Remediation failure
- Stale ownership

## Relationship with JML

```text
Mover
  |
  v
Old Access Remains
  |
  v
Privilege Creep
  |
  v
Recertification Detects It
```

But recertification should not replace a good Mover process.

## Relationship with SoD

Reviews can identify existing toxic combinations.

## Key Principle

> Recertification confirms that existing access is still justified.
