# IAM Monitoring, Audit & Compliance

## 1. Overview

Identity and Access Management controls are useful only if an organisation can verify that they operate correctly.

IAM monitoring, audit and compliance help answer questions such as:

```text
WHO accessed WHAT?

WHEN?

HOW?

WHY?

WHO approved it?

WHAT changed?

WAS the action allowed?

IS the access still appropriate?

CAN we prove it?
```

The basic lifecycle is:

```text
IAM Activity
     |
     v
Logging
     |
     v
Monitoring
     |
     v
Detection
     |
     v
Investigation
     |
     v
Remediation
     |
     v
Audit Evidence
```

---

# 2. Logging

Logging records events.

Examples:

- Successful login
- Failed login
- Account creation
- Account deletion
- Password change
- MFA registration
- Role assignment
- Group membership change
- Entitlement assignment
- Privileged role activation
- Access request
- Approval
- Access revocation
- Policy change

Example:

```text
2026-09-23 14:32
User: Alice
Action: ADD_GROUP_MEMBER
Group: Finance-Users
Result: SUCCESS
```

Logging provides raw evidence of activity.

---

# 3. Monitoring

Monitoring observes activity and looks for conditions requiring attention.

```text
EVENTS
  |
  v
MONITORING
  |
  +-- Normal
  |
  +-- Suspicious
  |
  +-- Policy Violation
  |
  +-- Operational Failure
```

Examples:

- Repeated authentication failures
- Unexpected privileged role activation
- Dormant account becomes active
- Privileged group membership change
- Provisioning failure
- Deprovisioning failure
- Break-glass account usage

---

# 4. Logging vs Monitoring

These concepts are related but different.

```text
LOGGING
=
Record events
```

```text
MONITORING
=
Observe events and detect conditions
```

Example:

```text
Log:
Alice activated Global Administrator
```

Monitoring may ask:

```text
Was this expected?

Was it approved?

Was it outside normal hours?

Should an alert be generated?
```

---

# 5. Audit

Audit evaluates whether IAM processes and controls operated as expected.

Audit may ask:

```text
Who had access?

Why did they have it?

Who approved it?

Was SoD checked?

Was access reviewed?

Was terminated-user access removed?

Can the organisation demonstrate this?
```

Audit depends heavily on reliable evidence.

---

# 6. Audit Trail

An audit trail records the history of an identity or access decision.

Example:

```text
Alice
 |
 +-- Access requested
 |
 +-- Manager approved
 |
 +-- SoD passed
 |
 +-- Access provisioned
 |
 +-- Access used
 |
 +-- Access recertified
 |
 +-- Access revoked
 |
 +-- Removal verified
```

The objective is traceability throughout the lifecycle.

---

# 7. Evidence

Evidence demonstrates that a control or process actually operated.

Examples include:

- Access request records
- Approval records
- Provisioning logs
- Authentication logs
- SoD evaluation results
- Certification decisions
- PAM session records
- Deprovisioning evidence
- Reconciliation results
- Change records

Important principle:

```text
Policy says control exists
```

is not the same as:

```text
Evidence proves control operated
```

---

# 8. Accountability

IAM systems should make it possible to determine:

```text
WHO
did
WHAT
to
WHICH OBJECT
WHEN
and
WHY?
```

Example:

```text
Actor:
Bob

Action:
Granted SAP-FI-APPROVE

Target:
Alice

Time:
14:32

Reason:
REQ-12345

Result:
SUCCESS
```

---

# 9. Authentication Monitoring

Authentication events are important security signals.

Examples:

```text
Successful login

Failed login

MFA challenge

MFA failure

Password reset

Account lockout

Token issuance

Authentication policy failure
```

Monitoring can detect unusual patterns.

Example:

```text
User
 |
 +-- Failed Login
 +-- Failed Login
 +-- Failed Login
 +-- Failed Login
 |
 v
Detection / Alert
```

---

# 10. Privileged Access Monitoring

Privileged activity deserves particular attention.

Examples:

- Domain Admin membership
- Entra privileged role activation
- root access
- Break-glass account use
- PAM credential checkout
- Privileged session
- Security policy modification

Example:

```text
Privileged Event
      |
      v
Log
      |
      v
Monitor
      |
      v
Alert if required
      |
      v
Investigate
```

---

# 11. Lifecycle Monitoring

JML processes should also be monitored.

Examples:

```text
JOINER
-> Was identity created on time?
```

```text
MOVER
-> Was old access removed?
```

```text
LEAVER
-> Were accounts disabled promptly?
```

A particularly important control is:

```text
Leaver
   |
   v
Account Disabled?
   |
   +-- YES -> OK
   |
   +-- NO --> Alert / Remediate
```

---

# 12. Provisioning Monitoring

Provisioning can fail.

Example:

```text
IGA
 |
 | Provision entitlement
 v
Target System
 |
 X
FAILED
```

Without monitoring, the governance system may believe access was granted or removed when the target system is in a different state.

Therefore provisioning results should be tracked.

---

# 13. Deprovisioning Monitoring

Deprovisioning failures can be particularly dangerous.

Example:

```text
IGA
 |
 | REVOKE
 v
Target System
 |
 X
Removal Failed
```

The governance decision says:

```text
NO ACCESS
```

but the actual system says:

```text
ACCESS STILL EXISTS
```

This should be detected and remediated.

---

# 14. Reconciliation

Reconciliation compares expected access with actual access.

```text
IGA
Expected State
      |
      v
   COMPARE
      ^
      |
Target System
Actual State
```

Possible discrepancy:

```text
Expected:
Alice NOT member of Finance-Admin

Actual:
Alice IS member of Finance-Admin
```

This can indicate:

- Failed deprovisioning
- Manual change
- Provisioning error
- Synchronisation problem
- Unmanaged access

---

# 15. Direct Changes

Administrators may sometimes modify target systems directly.

Example:

```text
Administrator
      |
      v
Active Directory
      |
      v
Add Alice to Group
```

The change bypasses the normal IGA workflow.

Reconciliation can detect:

```text
IGA expected state
       !=
Target actual state
```

Depending on policy, the organisation may:

- Import the change
- Request certification
- Generate an alert
- Automatically remove it
- Investigate it

---

# 16. Access Review Evidence

Recertification produces important audit evidence.

Example:

```text
User:
Alice

Entitlement:
SAP-FI-DISPLAY

Reviewer:
Finance Manager

Decision:
KEEP

Date:
2026-09-23
```

For revoked access:

```text
Decision:
REVOKE

Removal:
SUCCESS

Verified:
YES
```

The second part is essential.

A revoke decision alone does not prove that access was removed.

---

# 17. SoD Evidence

SoD controls should also produce evidence.

Example:

```text
Requested:
APPROVE_PAYMENT

Existing:
CREATE_PAYMENT

SoD Rule:
PAYMENT_CREATOR_VS_APPROVER

Result:
CONFLICT
```

If an exception is approved:

```text
Exception Owner
        |
        v
Justification
        |
        v
Compensating Control
        |
        v
Expiration Date
        |
        v
Periodic Review
```

---

# 18. PAM Evidence

PAM can provide detailed privileged-access evidence.

Example:

```text
Human:
Alice

Privileged Account:
root

Target:
server01

Reason:
INC-12345

Start:
14:00

End:
14:42

Session:
Recorded
```

This connects a human identity to privileged activity.

---

# 19. Compliance

Compliance means satisfying applicable requirements.

Requirements may come from:

- Laws
- Regulations
- Industry standards
- Security frameworks
- Contracts
- Internal policies

IAM controls frequently support requirements around:

- Least privilege
- Access approval
- Segregation of Duties
- Strong authentication
- Privileged access
- Access reviews
- Timely termination
- Accountability
- Traceability

---

# 20. Control vs Evidence

This distinction is fundamental.

```text
CONTROL
=
What should happen
```

```text
EVIDENCE
=
Proof that it happened
```

Example:

```text
CONTROL:

Leaver accounts must be disabled
within the required timeframe.
```

Evidence might include:

```text
Termination timestamp
+
Account disable timestamp
+
Provisioning result
```

---

# 21. Preventive vs Detective Controls

## Preventive

Prevent the undesirable event.

Examples:

```text
MFA
SoD blocking
Approval workflow
RBAC
Conditional Access
PAM
```

## Detective

Identify that something happened.

Examples:

```text
Log monitoring
Reconciliation
Access review
Anomaly detection
Audit
```

Simple mental model:

```text
PREVENTIVE
=
STOP IT
```

```text
DETECTIVE
=
FIND IT
```

Both are necessary.

---

# 22. Corrective Controls

A third category is useful:

```text
CORRECTIVE
=
FIX IT
```

Example:

```text
Detect excessive access
        |
        v
Revoke entitlement
```

So:

```text
PREVENT
   |
DETECT
   |
CORRECT
```

forms a useful control lifecycle.

---

# 23. SIEM

IAM logs are often forwarded to a Security Information and Event Management platform.

Simplified:

```text
AD --------+
           |
Entra -----+
           |
IGA -------+----> SIEM
           |
PAM -------+
           |
Apps ------+
```

The SIEM can:

- Aggregate events
- Correlate events
- Detect patterns
- Generate alerts
- Support investigation
- Retain security evidence

IAM systems remain responsible for producing useful identity-related events.

---

# 24. Useful IAM Events

Examples of events worth monitoring include:

```text
Identity created

Identity disabled

Account created

Account deleted

Role granted

Role revoked

Group membership changed

Privileged role activated

MFA changed

Password reset

Access request approved

Access request rejected

SoD conflict detected

Certification completed

Provisioning failed

Deprovisioning failed

Break-glass account used
```

---

# 25. Identity Context

Raw technical events become more useful when enriched with identity context.

Raw event:

```text
asmith added to GG-FIN-ADMIN
```

Enriched event:

```text
User:
Alice Smith

Department:
Finance

Manager:
Bob

Group:
GG-FIN-ADMIN

Risk:
High

Change Source:
Manual

Approved Request:
NONE
```

Identity context makes monitoring and investigation more effective.

---

# 26. Metrics

IAM programmes may track metrics such as:

```text
Number of orphan accounts

Number of dormant accounts

Number of SoD conflicts

Number of privileged accounts

Number of failed provisioning operations

Number of failed deprovisioning operations

Certification completion rate

Average access approval time

Leaver deprovisioning time

Number of unmanaged accounts

Number of overdue access reviews
```

Metrics should help identify risk and process problems rather than exist only for reporting.

---

# 27. Common Audit Findings

Typical problems include:

## Orphan Accounts

```text
Account exists
but
Owner does not
```

## Excessive Access

Users have more access than required.

## Privilege Creep

Old access remains after role changes.

## Dormant Accounts

Accounts remain enabled despite long periods of inactivity.

## Failed Deprovisioning

Access should have been removed but remains active.

## Missing Approval

Access exists without evidence of authorization.

## Missing Review

Sensitive access has never been recertified.

## Shared Accounts

Actions cannot easily be attributed to an individual.

## Missing Logs

Important IAM activity is not recorded.

---

# 28. Audit Questions

A strong IAM environment should be able to answer:

```text
Who has access to system X?

Why does Alice have entitlement Y?

Who approved it?

When was it granted?

When was it last reviewed?

Does it create an SoD conflict?

Which users have privileged access?

Which accounts have no owner?

Which leavers still have active accounts?

Which provisioning operations failed?

Which privileged accounts were used yesterday?

Was revoked access actually removed?
```

---

# 29. End-to-End Example

Alice requests access to a financial application.

```text
Alice
  |
  v
Access Request
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
  |
  v
Access Granted
  |
  v
LOG EVERYTHING
  |
  v
Monitor
  |
  v
Recertify
  |
  v
REVOKE
  |
  v
Deprovision
  |
  v
Reconcile
  |
  v
Verify Removal
  |
  v
Retain Evidence
```

An auditor should be able to reconstruct this lifecycle.

---

# 30. What to Remember

```text
LOGGING
=
Record
```

```text
MONITORING
=
Observe / Detect
```

```text
AUDIT
=
Verify / Prove
```

```text
COMPLIANCE
=
Meet requirements
```

```text
RECONCILIATION
=
Expected vs Actual
```

```text
PREVENTIVE
=
Stop
```

```text
DETECTIVE
=
Find
```

```text
CORRECTIVE
=
Fix
```

---

# Key Mental Model

```text
                    IAM ACTIVITY
                         |
                         v
                       LOG
                         |
                         v
                     MONITOR
                         |
                         v
                      DETECT
                         |
                         v
                    INVESTIGATE
                         |
                         v
                     CORRECT
                         |
                         v
                      VERIFY
                         |
                         v
                    EVIDENCE
                         |
                         v
                 AUDIT / COMPLIANCE
```

The central principle is:

> An IAM control is not complete merely because it is designed. It must operate, be monitored, be correctable, and produce evidence that it worked.
