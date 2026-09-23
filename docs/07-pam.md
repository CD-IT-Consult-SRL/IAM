# Privileged Access Management (PAM)

## 1. Overview

Privileged Access Management (PAM) controls and monitors access to powerful accounts, roles, credentials, and administrative functions.

Examples include:

- root
- Domain Administrator
- Entra privileged roles
- Database administrator
- Network administrator
- Application administrator
- Cloud administrator
- Service accounts
- Emergency accounts

The basic idea is:

```text
STANDARD ACCESS
=
Normal business activity
```

```text
PRIVILEGED ACCESS
=
Administrative / high-impact activity
```

Privileged access requires stronger controls because misuse or compromise can have a much greater impact.

---

# 2. What is a Privileged Account?

A privileged account has elevated permissions.

Examples:

```text
Linux
-> root
```

```text
Active Directory
-> Domain Admin
```

```text
Microsoft Entra ID
-> Global Administrator
```

```text
Database
-> DBA
```

```text
Application
-> Application Administrator
```

These accounts may be able to:

- Create users
- Delete users
- Change permissions
- Access sensitive data
- Modify systems
- Install software
- Change security configuration
- Disable security controls

---

# 3. Standard vs Privileged Identity

Administrators should generally not use privileged access for ordinary daily activity.

Example:

```text
Alice
 |
 +-- alice@company.com
 |       |
 |       v
 |   Standard Account
 |
 +-- adm-alice
         |
         v
    Privileged Account
```

The standard account can be used for:

- Email
- Browsing
- Collaboration
- Normal business applications

The privileged account is used only when administrative privileges are required.

This reduces exposure.

---

# 4. PAM Core Functions

A PAM solution commonly provides several controls:

```text
PAM
 |
 +-- Credential Vaulting
 |
 +-- Credential Rotation
 |
 +-- Privileged Access Request
 |
 +-- Approval
 |
 +-- Just-In-Time Access
 |
 +-- Session Management
 |
 +-- Session Recording
 |
 +-- Monitoring
 |
 +-- Audit
```

Not every PAM implementation uses every feature, but these are common capabilities.

---

# 5. Credential Vaulting

Privileged credentials can be stored securely in a vault.

Instead of:

```text
Administrator
     |
     v
Knows root password
```

we can have:

```text
Administrator
     |
     v
PAM
     |
     v
Credential Vault
     |
     v
Target System
```

The user may not need to know the privileged password.

---

# 6. Credential Rotation

Privileged passwords should not remain static indefinitely.

PAM systems can automatically rotate credentials.

```text
Old Password
     |
     v
PAM Rotation
     |
     v
New Random Password
     |
     v
Vault Updated
```

Rotation can occur:

- Periodically
- After use
- After credential checkout
- After an incident
- According to policy

---

# 7. Privileged Access Request

Privileged access should normally have a clear reason.

Example:

```text
Administrator
      |
      v
Request Privileged Access
      |
      v
Provide Justification
      |
      v
Approval / Policy Check
      |
      v
Access Granted
```

The request may include:

- Target system
- Required privilege
- Business reason
- Duration
- Ticket/change number

---

# 8. Just-In-Time Access — JIT

Just-In-Time access means privileged access is granted only when needed and for a limited period.

Instead of:

```text
Alice
 |
 v
Permanent Administrator
```

use:

```text
Alice
 |
 v
Request Admin Access
 |
 v
Approved
 |
 v
Admin Access
 |
 | 1 hour
 |
 v
Automatic Removal
```

Think:

```text
JIT
=
Right privilege
+
Right time
+
Limited duration
```

This reduces standing privilege.

---

# 9. Standing Privilege

Standing privilege means privileged access is permanently assigned.

Example:

```text
Alice
 |
 v
Domain Admin
24 hours/day
365 days/year
```

Even if Alice only needs the privilege occasionally, the account remains powerful continuously.

This increases risk.

A common PAM objective is therefore:

```text
Reduce Standing Privilege
        |
        v
Use JIT Where Appropriate
```

---

# 10. Privileged Identity Management — PIM

PIM commonly refers to managing privileged role assignments and activation.

A typical model is:

```text
User
 |
 v
Eligible for Privileged Role
 |
 v
Request / Activate
 |
 v
MFA / Approval / Justification
 |
 v
Temporary Privilege
 |
 v
Automatic Expiration
```

Microsoft Entra Privileged Identity Management is a common example.

Terminology can vary between vendors and organisations, but a useful first-pass distinction is:

```text
PAM
=
Broader control of privileged access,
accounts, credentials and sessions
```

```text
PIM
=
Privileged identity / role assignment
and activation
```

---

# 11. Session Management

PAM can broker privileged sessions.

Instead of connecting directly:

```text
Administrator
      |
      v
Server
```

the connection may pass through PAM:

```text
Administrator
      |
      v
     PAM
      |
      v
Target Server
```

This provides additional control over the privileged session.

---

# 12. Session Recording

Privileged sessions may be recorded.

Example:

```text
Administrator
      |
      v
PAM Session
      |
      +-- Commands
      +-- Activity
      +-- Time
      +-- Target
      |
      v
Audit Evidence
```

This improves accountability and supports investigation.

The exact recording mechanism depends on the PAM platform and protocol.

---

# 13. Accountability

A major PAM objective is answering:

```text
WHO
did
WHAT
on
WHICH SYSTEM
WHEN
and
WHY?
```

Example:

```text
User: Alice
Target: production-db01
Privilege: DBA
Start: 14:00
End: 14:42
Reason: INC-12345
Approval: Bob
Session: Recorded
```

This creates traceability.

---

# 14. Shared Privileged Accounts

Shared administrative accounts create an accountability problem.

Example:

```text
root
```

If five administrators know the password:

```text
root performed action X
```

does not automatically tell us which human performed it.

PAM can improve accountability:

```text
Alice
  |
  v
PAM
  |
  v
root
```

The target may see:

```text
root
```

while PAM records that the actual user was Alice.

---

# 15. Service Accounts

Service accounts are non-human identities used by:

- Applications
- Services
- Scheduled jobs
- Automation
- Integration processes

Example:

```text
Application
    |
    v
Service Account
    |
    v
Database
```

Service accounts can become highly privileged and are often difficult to manage.

Controls may include:

- Credential vaulting
- Credential rotation
- Ownership
- Least privilege
- Usage monitoring
- Regular review

Modern architectures may also use managed identities, workload identities, certificates, or short-lived credentials instead of static passwords.

---

# 16. Break-Glass Accounts

A break-glass account provides emergency access when normal access mechanisms fail.

Example:

```text
Normal Administration
       |
       X
   Unavailable
       |
       v
Break-Glass Account
       |
       v
Emergency Access
```

Break-glass access should be highly controlled.

Typical controls include:

- Very restricted use
- Strong authentication
- Secure credential storage
- Monitoring
- Immediate alerting
- Logging
- Post-use review
- Credential rotation after use

Break-glass accounts should not become ordinary administrator accounts.

---

# 17. PAM and MFA

Privileged access should generally use stronger authentication controls.

Example:

```text
Administrator
      |
      v
Authentication
      |
      v
MFA
      |
      v
PAM
      |
      v
Privileged Session
```

A stolen password alone should ideally not be sufficient to obtain privileged access.

---

# 18. PAM and SoD

Privileged access may also be subject to Segregation of Duties.

Example:

```text
Request Privilege
      |
      v
Approval by Independent Person
      |
      v
Privilege Activated
```

The requester should not necessarily be able to approve their own privileged access.

Another example:

```text
Create privileged account
          +
Approve privileged account
```

may represent an SoD conflict.

---

# 19. PAM and Recertification

Privileged access should be reviewed regularly.

```text
Privileged Accounts
       |
       v
Access Review
       |
   +---+---+
   |       |
   v       v
 KEEP    REVOKE
```

Questions include:

- Does the user still need privileged access?
- Is the account still used?
- Is the owner still valid?
- Is permanent access really necessary?
- Could JIT replace standing privilege?

---

# 20. PAM and JML

Privileged access must follow the identity lifecycle.

## Joiner

Do not automatically give unnecessary privileged access.

## Mover

Reassess privileged roles.

```text
Old Job
  |
  v
Privileged Access
  |
  v
Mover
  |
  v
Reassess / Remove
```

## Leaver

Privileged access should be revoked promptly.

```text
LEAVER
  |
  +-- Disable standard account
  |
  +-- Remove privileged roles
  |
  +-- Disable privileged accounts
  |
  +-- Revoke sessions/tokens
  |
  +-- Rotate shared credentials if necessary
```

---

# 21. Common PAM Risks

## Permanent Privileged Access

```text
Admin Forever
```

creates unnecessary standing privilege.

---

## Shared Passwords

Multiple people know the same administrative password.

This weakens accountability.

---

## Static Credentials

Passwords or secrets remain unchanged for long periods.

---

## Privileged Accounts Outside PAM

Some administrator accounts bypass PAM controls.

This creates unmanaged privileged access.

---

## Excessive Privilege

An administrator receives more privilege than required.

---

## Orphaned Privileged Accounts

The owner leaves but the privileged account remains active.

---

## Unmanaged Service Accounts

Service credentials are embedded in:

- Scripts
- Configuration files
- Source code
- Scheduled jobs

and are never rotated.

---

# 22. Typical PAM Flow

```text
Administrator
      |
      v
Authentication + MFA
      |
      v
PAM
      |
      v
Request Privilege
      |
      v
Justification
      |
      v
Policy / Approval
      |
      v
JIT Privilege
      |
      v
Privileged Session
      |
      +-- Monitor
      +-- Record
      +-- Audit
      |
      v
Session Ends
      |
      v
Privilege Removed
```

---

# 23. Example Technologies

Examples of technologies associated with privileged access management include:

- CyberArk
- Delinea
- BeyondTrust
- One Identity
- Microsoft Entra PIM
- Cloud-provider privileged access mechanisms

Different products cover different parts of the PAM/PIM landscape.

---

# 24. What to Remember

```text
PAM
=
Control privileged access
```

```text
VAULT
=
Protect privileged credentials
```

```text
ROTATION
=
Change credentials
```

```text
JIT
=
Privilege only when needed
and for limited time
```

```text
STANDING PRIVILEGE
=
Permanent privileged access
```

```text
SESSION RECORDING
=
Trace privileged activity
```

```text
PIM
=
Manage privileged role eligibility
and activation
```

```text
BREAK GLASS
=
Emergency privileged access
```

---

# Key Mental Model

```text
                 ADMINISTRATOR
                       |
                       v
               Authentication
                     + MFA
                       |
                       v
                      PAM
                       |
            +----------+----------+
            |          |          |
            v          v          v
         Request    Approval   Justification
            \          |          /
             \         |         /
              +--------+--------+
                       |
                       v
                  JIT ACCESS
                       |
                       v
              PRIVILEGED SESSION
                       |
              +--------+--------+
              |                 |
              v                 v
           Monitor            Record
              |                 |
              +--------+--------+
                       |
                       v
                  Session Ends
                       |
                       v
               Remove Privilege
                       |
                       v
                     Audit
```

The central principle is:

> Privileged access should be exceptional, controlled, limited, and traceable.
