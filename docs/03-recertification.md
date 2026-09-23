# Access Recertification & Access Review Campaigns

## 1. Overview

Access recertification is the process of periodically or event-driven reviewing existing access to confirm that it is still appropriate.

The key question is:

> Does this person still need this access?

Access can become inappropriate over time because of:

- Role changes
- Department changes
- Temporary assignments
- Project completion
- Privilege creep
- Manual provisioning
- Legacy access
- Incorrect ownership
- Forgotten exceptions

Recertification provides a formal process to review and either keep or remove existing access.

---

## 2. Basic Flow

```text
Existing Access
      |
      v
Access Review Campaign
      |
      v
Reviewer
      |
   +--+--+
   |     |
   v     v
 KEEP   REVOKE
   |       |
   v       v
Remain   Remediation
```

The reviewer confirms whether the current access remains justified.

---

## 3. What Can Be Reviewed?

A campaign can review:

- User accounts
- Group memberships
- Roles
- Entitlements
- Application access
- Privileged access
- Service accounts
- External users
- Temporary access
- SoD exceptions

Example:

```text
Alice
  |
  +-- Finance Analyst Role
  +-- SAP FI Display
  +-- Reporting Access
  +-- VPN Access
```

A review may ask whether Alice still requires each item.

---

## 4. Typical Reviewers

Different types of access may have different reviewers.

Common reviewers include:

- Manager
- Application owner
- Role owner
- Entitlement owner
- Data owner
- Privileged access owner
- Security
- Compliance

Example:

```text
Alice's Manager
      |
      v
Review Alice's Access
```

or:

```text
Application Owner
      |
      v
Review All Users
of Payment Application
```

---

## 5. Manager Certification

A manager reviews the access held by people reporting to them.

Example:

```text
Manager
  |
  +-- Alice
  |    +-- Finance Portal
  |    +-- SAP FI
  |
  +-- Bob
       +-- Reporting
       +-- VPN
```

The manager decides whether each access item should remain.

This approach gives the reviewer business context about the user.

---

## 6. Application-Owner Certification

The application owner reviews who has access to a particular application.

Example:

```text
Payment Application
        |
        v
Application Owner
        |
        +-- Alice
        +-- Bob
        +-- Carol
```

The owner checks whether each user still requires access.

This gives the reviewer strong context about the application and its sensitivity.

---

## 7. Privileged-Access Certification

Privileged access generally deserves stricter and more frequent review.

Examples:

- Domain administrator
- Entra privileged role
- Root access
- Database administrator
- CyberArk privileged account
- Production administration

Example:

```text
Privileged Access
      |
      v
Frequent Review
      |
      v
Still Required?
   /       \
 YES       NO
  |         |
  v         v
KEEP      REVOKE
```

---

## 8. Periodic Reviews

Reviews can be scheduled regularly.

Examples:

```text
Quarterly
Every 6 months
Annually
```

Higher-risk access is usually reviewed more frequently.

Example:

```text
Standard application access
=
Annual review
```

```text
Privileged access
=
Quarterly review
```

The exact frequency depends on risk, policy, and regulatory requirements.

---

## 9. Event-Driven Reviews

A review does not always have to wait for a scheduled campaign.

Events can trigger reassessment.

Examples:

- Mover event
- Manager change
- Department change
- Contract extension
- Return from leave
- SoD conflict
- Security incident
- Application ownership change

Example:

```text
Finance -> Procurement
        |
        v
Mover Event
        |
        v
Access Reassessment
```

This connects recertification closely with JML.

---

## 10. Review Decisions

Typical decisions include:

```text
KEEP
```

Access remains justified.

```text
REVOKE
```

Access is no longer justified and should be removed.

Some systems may also support:

```text
MODIFY
```

or:

```text
DELEGATE / REASSIGN
```

depending on the review process.

---

## 11. Remediation

A review is only useful if rejected access is actually removed.

```text
Reviewer
   |
   v
REVOKE
   |
   v
Remediation Task
   |
   v
Deprovision
   |
   v
Verify Removal
```

This is important:

> A review decision without remediation is incomplete.

---

## 12. Evidence and Audit Trail

A good recertification process records:

- What was reviewed
- Who reviewed it
- When it was reviewed
- What decision was made
- Why the decision was made
- When revoked access was removed
- Whether remediation succeeded

Example:

```text
User: Alice
Entitlement: SAP-FI-DISPLAY
Reviewer: Finance Manager
Decision: KEEP
Date: 2026-09-23
```

This provides compliance evidence.

---

## 13. Campaign Scope

A campaign should clearly define what is being reviewed.

Examples:

```text
All Finance access
```

```text
All privileged accounts
```

```text
All users of SAP
```

```text
All contractors
```

```text
All access not reviewed in 12 months
```

Large campaigns may be divided into smaller targeted campaigns.

---

## 14. Risk-Based Recertification

Not all access has the same level of risk.

A risk-based approach may prioritize:

```text
Privileged Access
        |
        v
Most Frequent Review
```

```text
Sensitive Financial Access
        |
        v
Frequent Review
```

```text
Standard Low-Risk Access
        |
        v
Less Frequent Review
```

This helps focus effort where it provides the most value.

---

## 15. Common Problems

### Rubber Stamping

Reviewers approve everything without actually reviewing it.

```text
SELECT ALL
   |
   v
APPROVE
```

This defeats the purpose of recertification.

---

### Reviewer Does Not Understand Access

Example:

```text
Manager sees:

SAP_Z_FI_X127
```

but does not know what it means.

Good entitlement descriptions and ownership are important.

---

### Too Much Information

A reviewer receives hundreds or thousands of access items at once.

This creates review fatigue.

---

### Wrong Reviewer

The assigned reviewer may not have enough knowledge to make the decision.

---

### Revoked Access Is Not Removed

```text
Decision = REVOKE

but

Access remains active
```

The remediation process must be monitored.

---

### Stale Ownership

The owner of a role, entitlement, or application has changed but IAM still points to the old owner.

---

## 16. Relationship with JML

Mover events can create inappropriate access.

```text
Finance
   |
   v
Procurement
```

If Finance access remains:

```text
Old Access
   +
New Access
   |
   v
Privilege Creep
```

Recertification can detect this later.

However:

> Recertification should not replace a good Mover process.

The correct approach is to remove inappropriate access during the lifecycle event and use recertification as an additional control.

---

## 17. Relationship with SoD

Access reviews can identify toxic combinations.

Example:

```text
Alice

CREATE_PAYMENT
      +
APPROVE_PAYMENT
```

During review:

```text
Access Review
      |
      v
SoD Conflict Identified
      |
      v
Revoke / Exception / Compensating Control
```

---

## 18. Relationship with Least Privilege

Recertification supports least privilege by removing access that is no longer required.

```text
Existing Access
      |
      v
Review
      |
      +-- Required ----> KEEP
      |
      +-- Not Required -> REVOKE
```

---

## 19. What to Remember

```text
RECERTIFICATION
=
Review existing access
```

```text
CORE QUESTION
=
"Does this person still need this access?"
```

```text
REVIEWER
=
Manager / Application Owner / Role Owner / Data Owner
```

```text
DECISION
=
KEEP or REVOKE
```

```text
REMEDIATION
=
Actually remove rejected access
```

```text
EVIDENCE
=
Record who reviewed what, when, and what happened
```

---

# Key Mental Model

```text
EXISTING ACCESS
      |
      v
REVIEW CAMPAIGN
      |
      v
REVIEWER
   /      \
  v        v
KEEP     REVOKE
 |          |
 v          v
Remain   Remediate
             |
             v
         Verify
             |
             v
          Audit
```

The most important idea is:

> Recertification verifies that existing access is still justified.
