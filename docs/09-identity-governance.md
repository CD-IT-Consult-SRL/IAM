# Identity Governance & Administration (IGA)

## 1. Overview

Identity Governance & Administration (IGA) provides governance and lifecycle controls around identities and access.

IGA helps answer questions such as:

```text
WHO has access?

WHAT access do they have?

WHY do they have it?

WHO approved it?

HOW was it granted?

DOES it violate policy?

IS it still required?

WHEN should it be removed?
```

IGA brings together many IAM processes:

```text
JML
 |
 +-- Access Requests
 |
 +-- Roles / Entitlements
 |
 +-- Provisioning
 |
 +-- SoD
 |
 +-- Recertification
 |
 +-- Remediation
 |
 +-- Audit / Evidence
```

---

# 2. IAM vs IGA

IAM is a broad discipline covering identity and access.

IGA focuses particularly on governance and administration of identities and access.

A simplified mental model:

```text
IAM
=
Identity + Authentication + Authorization + Access
```

```text
IGA
=
Lifecycle + Governance + Policy + Review + Evidence
```

IGA is therefore part of the broader IAM landscape.

The boundaries can vary between products and organisations.

---

# 3. What IGA Tries to Achieve

The central objective is:

```text
RIGHT IDENTITY
      |
RIGHT ACCESS
      |
RIGHT REASON
      |
RIGHT APPROVAL
      |
RIGHT TIME
```

while maintaining:

```text
TRACEABILITY
+
ACCOUNTABILITY
+
POLICY COMPLIANCE
```

---

# 4. Identity Lifecycle

IGA commonly manages or orchestrates identity lifecycle processes.

```text
Authoritative Source
        |
        v
       JML
   /     |     \
  v      v      v
Joiner Mover  Leaver
```

Typical actions include:

### Joiner

```text
Create Identity
      |
      v
Create Accounts
      |
      v
Grant Birthright Access
```

### Mover

```text
Change Identity Attributes
        |
        v
Recalculate Access
        |
        +-- Remove Old
        |
        +-- Add New
```

### Leaver

```text
Terminate Identity
      |
      v
Disable Accounts
      |
      v
Remove Access
```

---

# 5. Authoritative Sources

IGA depends on reliable identity information.

A common authoritative source is:

```text
HR System
```

Example:

```text
HR
 |
 | Employee data
 v
IGA
 |
 +-- AD
 +-- Entra ID
 +-- SAP
 +-- SaaS
 +-- Applications
```

Important attributes may include:

- Employee ID
- Employment status
- Manager
- Department
- Job title
- Location
- Start date
- End date

Poor source data can produce incorrect access decisions.

---

# 6. Access Requests

IGA commonly provides access request workflows.

```text
User
 |
 v
Access Request
 |
 v
Approval
 |
 v
Policy Check
 |
 v
SoD Check
 |
 v
Provisioning
```

The workflow creates governance around the access decision.

---

# 7. Approval

Different access may require different approvers.

Examples:

```text
Manager
Application Owner
Role Owner
Entitlement Owner
Data Owner
Security
Compliance
```

The approval model should reflect the sensitivity and risk of the requested access.

---

# 8. Roles and Entitlements

IGA maintains relationships between:

```text
IDENTITY
   |
   v
ROLE
   |
   v
ENTITLEMENT
   |
   v
TARGET SYSTEM
```

Example:

```text
Alice
  |
  v
Finance Analyst
  |
  +-- AD-FINANCE
  +-- SAP-FI-DISPLAY
  +-- Finance Portal
```

Roles simplify access assignment and governance.

---

# 9. Birthright Access

IGA may automatically assign baseline access using identity attributes.

Example:

```text
Employee
AND
Department = Finance
       |
       v
Finance Birthright Access
```

Birthright access should still be governed.

Automatic does not mean uncontrolled.

---

# 10. Policy

IGA can enforce access policies.

Examples:

```text
Contractors cannot receive Role X
```

```text
Only Finance employees can receive Finance Role
```

```text
Privileged access requires additional approval
```

```text
Temporary access expires after 30 days
```

Policies transform business and security requirements into access controls.

---

# 11. Segregation of Duties

IGA can evaluate access against SoD policies.

Example:

```text
Existing:
CREATE_PAYMENT

Requested:
APPROVE_PAYMENT

       |
       v
    SoD Check
       |
       v
    CONFLICT
```

The system may:

- Block the request
- Require additional approval
- Create an exception workflow
- Require a compensating control

---

# 12. Access Certification / Recertification

IGA periodically reviews existing access.

```text
Existing Access
      |
      v
Certification Campaign
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

Typical reviewers include:

- Manager
- Application owner
- Role owner
- Entitlement owner

---

# 13. Remediation

Governance does not end with a decision.

Example:

```text
Reviewer
   |
   v
REVOKE
   |
   v
Remove Entitlement
   |
   v
Verify Removal
```

A governance process that identifies inappropriate access but fails to remove it is incomplete.

---

# 14. Provisioning

IGA may provision access directly or orchestrate another provisioning mechanism.

```text
IGA
 |
 +-- Active Directory
 |
 +-- Microsoft Entra ID
 |
 +-- LDAP Directory
 |
 +-- SAP
 |
 +-- SaaS
 |
 +-- Database
 |
 +-- Business Application
```

Provisioning mechanisms may include:

- Connectors
- APIs
- SCIM
- LDAP
- Scripts
- Manual fulfillment

---

# 15. Reconciliation

Provisioning answers:

```text
What SHOULD exist?
```

Reconciliation helps answer:

```text
What ACTUALLY exists?
```

Example:

```text
IGA Expected State
       |
       v
Compare
       ^
       |
Target System Actual State
```

This can identify discrepancies such as:

```text
Account exists in target
but not in IGA
```

or:

```text
IGA says entitlement removed
but target still has it
```

This is important because changes can occur outside the normal IAM process.

---

# 16. Identity Correlation

IGA may receive accounts from many systems and must determine which identity owns each account.

Example:

```text
Alice Smith

AD:
asmith

SAP:
AS12345

Database:
alice_s

Entra:
alice@company.com
```

IGA correlates these accounts to:

```text
Alice Smith
```

Incorrect correlation can result in serious governance problems.

---

# 17. Orphan Accounts

An orphan account exists without a valid identity or owner relationship.

Example:

```text
Target System

account = jsmith
     |
     X
No matching identity
```

Questions include:

```text
Who owns this?

Why does it exist?

Is it still required?

Should it be disabled?
```

Reconciliation and correlation help identify orphan accounts.

---

# 18. Access Model

IGA provides an access model describing relationships between:

```text
Identity
   |
   v
Business Role
   |
   v
Technical Role
   |
   v
Entitlement
   |
   v
Target System
```

This makes technical access understandable in business terms.

---

# 19. Access Governance

Access governance asks:

```text
Should this access exist?
```

not merely:

```text
Can we technically provision it?
```

This distinction is fundamental.

Example:

```text
Technical capability:
"We can add Alice to Domain Admins."
```

Governance question:

```text
"Should Alice have Domain Admin?"
```

---

# 20. Auditability

IGA should provide evidence explaining the lifecycle of access.

Example:

```text
Alice received SAP-FI-DISPLAY
        |
        +-- Requested: 10 March
        |
        +-- Approved by: Finance Manager
        |
        +-- SoD Check: Passed
        |
        +-- Provisioned: 10 March
        |
        +-- Recertified: 15 June
        |
        +-- Revoked: 20 September
```

This provides traceability.

---

# 21. Audit Questions

IGA should help answer:

```text
Who has access to application X?

Which privileged access does Alice have?

Who approved this entitlement?

When was the access granted?

Why was it granted?

When was it last reviewed?

Does it violate SoD?

Which accounts have no owner?

Which users left but still have accounts?

Was revoked access actually removed?
```

---

# 22. Non-Human Identities

IGA increasingly governs non-human identities as well.

Example:

```text
Service Account
      |
      +-- Owner
      +-- Purpose
      +-- Entitlements
      +-- Credential
      +-- Review
      +-- Expiration
```

The lifecycle differs from human JML, but governance principles remain similar.

---

# 23. PAM and IGA

IGA and PAM solve related but different problems.

Simplified:

```text
IGA
=
Who SHOULD have access?
```

```text
PAM
=
How is PRIVILEGED access controlled and used?
```

Example:

```text
IGA
 |
 | User approved for privileged role
 v
PAM
 |
 | JIT activation / controlled session
 v
Privileged Resource
```

The two systems can work together.

---

# 24. IGA and Authentication

IGA generally governs whether access should exist.

Authentication establishes identity when access is used.

```text
IGA
 |
 | Governance
 v
Entitlement

User
 |
 v
Authentication
 |
 v
Authorization
 |
 v
Use Entitlement
```

These are related but separate IAM concerns.

---

# 25. Common IGA Risks

## Bad Identity Data

Incorrect HR attributes produce incorrect access.

---

## Privilege Creep

Old access accumulates after changes.

---

## Rubber-Stamp Certification

Reviewers approve everything without meaningful review.

---

## Poor Entitlement Descriptions

Reviewers cannot understand what they are approving.

---

## Orphan Accounts

Accounts remain without valid owners.

---

## Direct Changes

Administrators modify target systems outside IGA.

---

## Failed Remediation

Access is marked revoked but remains active.

---

## Role Explosion

Too many roles make governance difficult.

---

## Missing Ownership

Roles, entitlements, applications or NHIs have no accountable owner.

---

# 26. Example End-to-End IGA Flow

```text
                  HR
                  |
                  v
            Identity Created
                  |
                  v
            Birthright Access
                  |
                  v
             Employee Works
                  |
          +-------+-------+
          |               |
          v               v
    Access Request     Mover Event
          |               |
          v               v
      Approval       Recalculate Access
          |
          v
      SoD Check
          |
          v
     Provisioning
          |
          v
      Entitlement
          |
          v
    Reconciliation
          |
          v
    Recertification
          |
       +--+--+
       |     |
       v     v
      KEEP REVOKE
              |
              v
         Remediation
              |
              v
            Audit
```

---

# 27. Example IGA Technologies

Examples of products associated with IGA include:

- SailPoint
- Saviynt
- One Identity
- Omada
- Microsoft Entra ID Governance

Different platforms provide different combinations of:

- Lifecycle management
- Access requests
- Provisioning
- Role management
- SoD
- Certification
- Analytics
- Governance

---

# 28. What to Remember

```text
IGA
=
Identity Governance & Administration
```

```text
JML
=
Manage identity lifecycle
```

```text
ACCESS REQUEST
=
Govern new access
```

```text
ROLE / ENTITLEMENT
=
Model access
```

```text
SoD
=
Prevent incompatible access
```

```text
RECERTIFICATION
=
Verify existing access
```

```text
RECONCILIATION
=
Compare expected vs actual access
```

```text
CORRELATION
=
Connect accounts to identities
```

```text
REMEDIATION
=
Actually correct inappropriate access
```

```text
AUDIT
=
Prove what happened
```

---

# Key Mental Model

```text
               AUTHORITATIVE SOURCE
                       |
                       v
                      JML
                       |
                       v
                   IDENTITY
                       |
            +----------+----------+
            |                     |
            v                     v
       BIRTHRIGHT            ACCESS REQUEST
                                  |
                                  v
                              APPROVAL
                                  |
                                  v
                             POLICY / SoD
                                  |
                 +----------------+----------------+
                 |                                 |
                 v                                 v
               DENY                            PROVISION
                                                   |
                                                   v
                                              ENTITLEMENT
                                                   |
                                                   v
                                             TARGET SYSTEM
                                                   |
                                                   v
                                            RECONCILIATION
                                                   |
                                                   v
                                            RECERTIFICATION
                                                   |
                                              +----+----+
                                              |         |
                                              v         v
                                             KEEP     REVOKE
                                                         |
                                                         v
                                                    REMEDIATION
                                                         |
                                                         v
                                                       AUDIT
```

The central principle is:

> IGA governs who should have access, why they should have it, how it was approved, whether it remains appropriate, and whether the complete lifecycle is auditable.
