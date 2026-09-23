# Authoritative Sources, Identity Data, Correlation & Reconciliation

## 1. Overview

IAM depends on identity data.

Before deciding what access someone should receive, IAM needs reliable answers to questions such as:

```text
Who is this person?

Are they active?

What is their employee ID?

Who is their manager?

Which department are they in?

What is their job?

Where are they located?

When do they start?

When do they leave?
```

This information commonly originates from an authoritative source.

A simplified architecture is:

```text
Authoritative Source
        |
        v
       IGA
        |
   +----+----+------+
   |         |      |
   v         v      v
  AD       Entra   SAP
```

---

# 2. Authoritative Source

An authoritative source is a system trusted to provide particular identity attributes or lifecycle information.

For workforce identities, HR is commonly authoritative for attributes such as:

```text
Employee ID
Employment Status
Manager
Department
Job
Location
Start Date
End Date
```

Example:

```text
HR
 |
 | Authoritative Identity Data
 v
IGA
 |
 v
Identity Lifecycle
```

The authoritative source drives identity decisions.

---

# 3. Not Everything Has the Same Authoritative Source

An organisation can have different authoritative sources for different populations or attributes.

Example:

```text
Employees
    |
    v
HR System
```

```text
Contractors
    |
    v
Contractor Management System
```

```text
Customers
    |
    v
Customer Platform
```

Even attributes for one identity may originate from different systems.

Example:

```text
Employee Status -> HR

Email Address   -> Directory

Application Role -> IGA

Privileged Role -> PAM / IGA
```

The important question is:

> Which system is trusted for which information?

---

# 4. Source of Truth

The expression "source of truth" is frequently used alongside "authoritative source."

For a first mental model:

```text
AUTHORITATIVE SOURCE
=
System trusted to provide specific identity data
```

"Source of truth" is often used more loosely.

In IAM architecture, it is useful to be precise about which system is authoritative for each attribute or lifecycle event.

Example:

```text
HR is authoritative for:
- Employment status
- Department
- Manager
```

while:

```text
Active Directory may be authoritative for:
- Generated username
- Directory-specific attributes
```

depending on the architecture.

---

# 5. Identity Attributes

Identity records contain attributes.

Example:

```text
Identity: Alice Smith

employeeId = 12345
status     = ACTIVE
department = Finance
jobTitle   = Finance Analyst
manager    = Bob Jones
location   = Brussels
```

These attributes can drive IAM decisions.

Example:

```text
department = Finance
        |
        v
Finance Birthright Access
```

or:

```text
status = TERMINATED
       |
       v
Disable Access
```

---

# 6. Identity Data Quality

Bad identity data creates bad access decisions.

Example:

```text
HR says:

department = Finance
```

but Alice actually moved to Procurement.

IAM may continue granting Finance access.

Therefore:

```text
GOOD IDENTITY DATA
        |
        v
GOOD ACCESS DECISIONS
```

and:

```text
BAD IDENTITY DATA
        |
        v
BAD ACCESS DECISIONS
```

Data quality is therefore a security issue, not merely an administrative issue.

---

# 7. Identity Creation

An authoritative-source event may trigger creation of an identity.

Example:

```text
HR
 |
 | New employee
 v
IGA
 |
 v
Create Identity
 |
 v
Apply Joiner Rules
 |
 v
Provision Accounts
```

The IGA identity becomes the governance representation of the person.

---

# 8. Identity vs Account

This distinction is fundamental.

```text
IDENTITY
=
The person or entity
```

```text
ACCOUNT
=
Representation of that identity
inside a target system
```

Example:

```text
Alice Smith
   |
   +-- AD: ASMITH
   |
   +-- Entra: alice@company.com
   |
   +-- SAP: AS12345
   |
   +-- Database: alice_s
```

One identity can therefore own many accounts.

---

# 9. Target Systems

A target system is a system where accounts or access are managed.

Examples:

- Active Directory
- Microsoft Entra ID
- LDAP directories
- SAP
- Databases
- SaaS platforms
- Cloud platforms
- Business applications

Example:

```text
IGA
 |
 +-- AD
 |
 +-- Entra
 |
 +-- SAP
 |
 +-- Salesforce
 |
 +-- Database
```

---

# 10. Provisioning

Provisioning sends a desired identity or access change to a target system.

Example:

```text
IGA
 |
 | CREATE ACCOUNT
 v
Active Directory
```

or:

```text
IGA
 |
 | ADD GROUP MEMBERSHIP
 v
Active Directory
```

Provisioning is generally:

```text
IGA -> TARGET
```

Think:

```text
Provisioning
=
PUSH CHANGE
```

---

# 11. Deprovisioning

Deprovisioning removes or disables access.

Example:

```text
IGA
 |
 | REMOVE ENTITLEMENT
 v
Target System
```

or:

```text
IGA
 |
 | DISABLE ACCOUNT
 v
Active Directory
```

Typical triggers include:

- Leaver
- Mover
- Revoked access request
- Recertification decision
- Expired temporary access

---

# 12. Aggregation

Aggregation brings identity/account/access information from target systems into the governance platform.

Example:

```text
Active Directory
       |
       |
       v
      IGA
```

The IGA platform may retrieve:

- Accounts
- Groups
- Memberships
- Roles
- Entitlements
- Account status

Think:

```text
PROVISIONING
=
IGA -> TARGET
```

```text
AGGREGATION
=
TARGET -> IGA
```

---

# 13. Why Aggregation Matters

IGA cannot govern what it cannot see.

Example:

```text
Administrator manually creates:

AD account = asmith2
```

If IGA only knows what it provisioned itself, it may never discover the account.

Aggregation allows IGA to discover actual target-system state.

```text
TARGET
   |
   v
AGGREGATE
   |
   v
IGA discovers account
```

---

# 14. Correlation

After accounts are aggregated, IGA needs to determine:

> Which identity owns this account?

This is correlation.

Example:

```text
Identity:
Alice Smith

employeeId:
12345
```

Target account:

```text
AD account:
asmith

employeeId:
12345
```

Correlation rule:

```text
Identity.employeeId
=
Account.employeeId
```

Result:

```text
Alice Smith
    |
    v
asmith
```

---

# 15. Correlation Example

Before correlation:

```text
IDENTITIES              ACCOUNTS

Alice                    asmith
Bob                      bjones
Carol                    cwilliams
```

After correlation:

```text
Alice ------> asmith

Bob --------> bjones

Carol ------> cwilliams
```

IGA can now understand which accounts belong to which identities.

---

# 16. Correlation Rules

Correlation may use attributes such as:

- Employee ID
- Unique HR identifier
- Username
- Email address
- External identifier

A stable unique identifier is generally preferable.

Example:

```text
employeeId = 12345
```

is usually safer than matching only:

```text
firstName = Alice
lastName  = Smith
```

because names are not necessarily unique and can change.

---

# 17. Incorrect Correlation

Bad correlation can be dangerous.

Example:

```text
Account
 |
 v
Linked to WRONG identity
```

IGA may then:

- Display incorrect access
- Certify access under the wrong person
- Remove the wrong account
- Grant incorrect access
- Produce incorrect audit evidence

Correlation rules therefore require careful design.

---

# 18. Uncorrelated Accounts

Sometimes IGA discovers an account but cannot associate it with an identity.

```text
Target Account
     |
     v
Aggregation
     |
     v
IGA
     |
     X
No Identity Match
```

This is an:

```text
UNCORRELATED ACCOUNT
```

It requires investigation.

---

# 19. Orphan Accounts

An orphan account generally refers to an account without a valid corresponding owner/identity.

Example:

```text
jsmith
   |
   X
No valid identity
```

Possible reasons include:

- Employee left
- Account manually created
- Correlation failed
- Identity deleted
- Service account has no owner
- Legacy account

Orphan accounts represent an important IAM risk.

---

# 20. Reconciliation

Reconciliation compares what IAM believes should exist with what actually exists in the target system.

Think:

```text
EXPECTED
   |
   v
COMPARE
   ^
   |
ACTUAL
```

Example:

```text
IGA EXPECTS:

Alice NOT member of Finance-Admin
```

but:

```text
AD ACTUAL:

Alice IS member of Finance-Admin
```

Result:

```text
DISCREPANCY
```

---

# 21. Aggregation vs Reconciliation

These concepts are closely related but different.

```text
AGGREGATION
=
Bring target data into IGA
```

```text
RECONCILIATION
=
Compare target reality
with expected state
```

A simplified flow:

```text
TARGET
   |
   v
AGGREGATION
   |
   v
IGA
   |
   v
RECONCILIATION
   |
   v
DISCREPANCIES
```

---

# 22. Correlation vs Reconciliation

This distinction is extremely important.

```text
CORRELATION
=
WHO owns this account?
```

```text
RECONCILIATION
=
Does actual access match expected access?
```

Remember:

```text
CORRELATION
=
ACCOUNT -> IDENTITY
```

```text
RECONCILIATION
=
EXPECTED <-> ACTUAL
```

---

# 23. Provisioning vs Aggregation

These are opposite directions.

```text
                IGA
              /     \
             /       \
            v         ^
      Provision     Aggregate
           /           \
          v             \
       TARGET <----------+
```

Simplified:

```text
PROVISION
=
OUT
```

```text
AGGREGATE
=
IN
```

---

# 24. Detecting Out-of-Band Changes

An out-of-band change is made directly in a target system outside the normal governance process.

Example:

```text
Administrator
      |
      v
Active Directory
      |
      v
Add Alice to Domain Admins
```

IGA did not request the change.

Later:

```text
AD
 |
 v
Aggregation
 |
 v
IGA
 |
 v
Reconciliation
 |
 v
Unexpected Access Detected
```

The organisation can then:

- Alert
- Investigate
- Certify
- Import
- Remove
- Remediate automatically

depending on policy.

---

# 25. Closed-Loop Provisioning

A strong IAM process does not simply send a provisioning request and assume success.

Instead:

```text
IGA
 |
 | Provision
 v
Target
 |
 | Result
 v
IGA
 |
 | Aggregate / Verify
 v
Confirmed State
```

This creates a closed loop.

Think:

```text
REQUEST
   |
   v
CHANGE
   |
   v
VERIFY
```

---

# 26. Example: Joiner

Alice joins Finance.

```text
HR
 |
 | Alice starts
 v
IGA
 |
 | Create identity
 v
Alice
 |
 | Birthright rules
 v
Finance Access
 |
 | Provision
 v
AD / Entra / Applications
```

Later:

```text
Targets
   |
   v
Aggregation
   |
   v
Correlation
   |
   v
Reconciliation
```

IGA verifies that the expected accounts and access exist.

---

# 27. Example: Mover

Alice moves:

```text
Finance
   |
   v
Procurement
```

HR changes:

```text
department = Procurement
```

IGA receives the change:

```text
HR
 |
 v
IGA
 |
 +-- Remove Finance Access
 |
 +-- Add Procurement Access
```

Later reconciliation verifies:

```text
Finance Access = REMOVED

Procurement Access = PRESENT
```

This helps prevent privilege creep.

---

# 28. Example: Leaver

HR marks Alice terminated.

```text
HR
 |
 | status = TERMINATED
 v
IGA
 |
 +-- Disable AD
 +-- Disable Entra
 +-- Remove SAP access
 +-- Revoke application access
```

Then:

```text
Target Systems
      |
      v
Aggregation
      |
      v
Reconciliation
```

Question:

```text
Does Alice still have active access anywhere?
```

That is a critical leaver control.

---

# 29. Identity Data Flow

A complete simplified flow is:

```text
               HR
               |
               | Authoritative Data
               v
              IGA
               |
       Identity Created
               |
       Rules / Governance
               |
               v
           Provision
               |
       +-------+-------+
       |       |       |
       v       v       v
      AD     Entra    SAP
       |       |       |
       +-------+-------+
               |
               v
           Aggregate
               |
               v
           Correlate
               |
               v
           Reconcile
               |
               v
          Remediate
```

---

# 30. Common Risks

## Bad Source Data

Incorrect identity attributes produce incorrect access.

---

## Duplicate Identities

The same person exists more than once in the identity repository.

---

## Incorrect Correlation

An account is linked to the wrong identity.

---

## Uncorrelated Accounts

Accounts exist but cannot be linked to identities.

---

## Orphan Accounts

Accounts remain without valid owners.

---

## Failed Provisioning

IGA requests a change but the target does not implement it.

---

## Failed Deprovisioning

IGA requests removal but access remains.

---

## Out-of-Band Changes

Access is modified directly in the target system.

---

## Stale Aggregation

IGA has outdated target-system information.

---

# 31. What to Remember

```text
AUTHORITATIVE SOURCE
=
Where trusted identity data originates
```

```text
IDENTITY
=
Person / entity being governed
```

```text
ACCOUNT
=
Representation in a target system
```

```text
PROVISIONING
=
IGA -> Target
```

```text
AGGREGATION
=
Target -> IGA
```

```text
CORRELATION
=
Account -> Identity
```

```text
RECONCILIATION
=
Expected vs Actual
```

```text
REMEDIATION
=
Correct the discrepancy
```

---

# Key Mental Model

```text
              AUTHORITATIVE SOURCE
                       |
                       v
                    IDENTITY
                       |
                       v
                      IGA
                       |
                       | PROVISION
                       v
                 TARGET SYSTEM
                       |
                       | AGGREGATE
                       v
                      IGA
                       |
                       v
                  CORRELATE
                       |
                       v
                  RECONCILE
                       |
                       v
                 DISCREPANCY?
                    /     \
                  NO       YES
                  |         |
                  v         v
                 OK     REMEDIATE
```

The central principle is:

> IAM needs both directions: push governed changes to target systems and bring actual target state back so that identity ownership and access can be verified.
