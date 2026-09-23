# Access Recertification — Cheat Sheet

## The Whole Concept

```text
EXISTING ACCESS
      |
      v
REVIEW
   /      \
  v        v
KEEP     REVOKE
           |
           v
      REMOVE ACCESS
```

## Core Question

```text
"Does this person still need this access?"
```

## Reviewers

```text
Manager
Application Owner
Role Owner
Entitlement Owner
Data Owner
```

## Review Types

```text
Manager Certification
=
Review user's access
```

```text
Application Certification
=
Review everyone using an application
```

```text
Privileged Certification
=
Review high-risk access
```

## Timing

```text
Periodic
=
Scheduled
```

```text
Event-Driven
=
Triggered by change
```

## Decision

```text
KEEP
or
REVOKE
```

## Important

```text
REVOKE
without
DEPROVISION
=
FAILED CONTROL
```

## Main Risks

```text
Rubber stamping
Wrong reviewer
Too much data
Unclear entitlement names
Remediation failure
```

## Connections

```text
JML
 |
 v
Access
 |
 v
Recertification
 |
 v
Keep / Revoke
```

```text
SoD Conflict
 |
 v
Review
 |
 v
Remediate / Exception
```

## 10-Second Memory

```text
Recertification = review existing access

Question = still needed?

Decision = keep or revoke

Revoke = must actually deprovision

Privileged access = review more often
```

> Review is not complete until rejected access is actually removed.
