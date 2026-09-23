# Identity Governance & Administration — Summary

## Core Idea

IGA governs identities and access throughout their lifecycle.

It answers:

```text
WHO has access?

WHAT do they have?

WHY do they have it?

WHO approved it?

DOES it violate policy?

IS it still needed?

WAS it actually removed?
```

---

## Main IGA Components

```text
                  IGA
                   |
       +-----------+-----------+
       |           |           |
      JML       Requests      Roles
       |           |           |
       +-----------+-----------+
                   |
                  SoD
                   |
             Provisioning
                   |
             Reconciliation
                   |
            Recertification
                   |
              Remediation
                   |
                 Audit
```

---

## IAM vs IGA

Simplified:

```text
IAM
=
Identity + Authentication
+ Authorization + Access
```

```text
IGA
=
Lifecycle + Governance
+ Policy + Review + Evidence
```

IGA is part of the broader IAM landscape.

---

## Authoritative Source

Often:

```text
HR
 |
 v
IGA
```

providing attributes such as:

```text
Employee ID
Manager
Department
Job
Location
Status
Start / End Date
```

Good governance depends on good identity data.

---

## Access Governance

The key question is not:

```text
CAN we give Alice access?
```

It is:

```text
SHOULD Alice have access?
```

---

## Access Request

```text
Request
   |
Approval
   |
Policy
   |
SoD
   |
Provision
```

---

## Recertification

```text
Existing Access
      |
      v
Review
   /      \
 KEEP    REVOKE
           |
           v
      Remediation
```

---

## Reconciliation

```text
EXPECTED
   |
   v
COMPARE
   ^
   |
ACTUAL
```

Reconciliation detects differences between IGA and target systems.

---

## Correlation

```text
Identity Alice
     |
     +-- AD account
     +-- Entra account
     +-- SAP account
     +-- Database account
```

Correlation links accounts to identities.

---

## IGA + PAM

```text
IGA
=
Who SHOULD have privileged access?
```

```text
PAM
=
How privileged access is controlled and used
```

---

## Key Principle

> IGA provides governance, lifecycle, policy, review, remediation and evidence around access.
