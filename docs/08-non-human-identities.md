# Non-Human Identities (NHI)

## 1. Overview

Identity and Access Management does not only concern people.

Applications, services, machines and automated processes also need identities in order to authenticate and access resources.

These are commonly called:

**Non-Human Identities (NHI)**.

Examples include:

- Service accounts
- Application identities
- Workload identities
- Managed identities
- API clients
- Automation accounts
- Machine identities
- Bots
- CI/CD identities

The basic model is:

```text
IDENTITY
   |
   +-- HUMAN
   |
   +-- NON-HUMAN
```

Both can authenticate and receive access.

---

# 2. Why Non-Human Identities Exist

Applications frequently need to communicate with other systems.

Example:

```text
Application
     |
     v
Database
```

The database must know:

```text
WHO is connecting?
```

and:

```text
WHAT is it allowed to do?
```

Therefore the application requires an identity.

Example:

```text
Application
     |
     v
Service Identity
     |
     v
Authentication
     |
     v
Database
     |
     v
Authorization
```

---

# 3. Service Accounts

A service account is an identity used by a service, application or automated process.

Example:

```text
Payroll Application
       |
       v
svc_payroll
       |
       v
Payroll Database
```

The service account might have permission to:

- Read employee records
- Write payroll transactions
- Execute database procedures

Service accounts should not simply be treated as normal employee accounts.

---

# 4. Application Identities

Applications may have their own identity.

Example:

```text
Application A
      |
      v
Application Identity
      |
      v
API
```

The application authenticates itself rather than authenticating as a human user.

Examples include application identities in:

- Microsoft Entra ID
- Cloud platforms
- Kubernetes
- API gateways
- SaaS platforms

---

# 5. Workload Identities

A workload identity represents a software workload.

Examples:

- Container
- Kubernetes workload
- Virtual machine
- Cloud function
- Automation process
- CI/CD pipeline

Example:

```text
Container
   |
   v
Workload Identity
   |
   v
Cloud API
```

The workload can authenticate without pretending to be a human user.

---

# 6. Managed Identities

Cloud platforms can provide identities whose credentials are managed by the platform.

Example:

```text
Virtual Machine
      |
      v
Managed Identity
      |
      v
Cloud Resource
```

This can avoid storing static credentials such as:

```text
username = svc_app
password = Secret123
```

inside application configuration.

Microsoft Entra managed identities are a common example.

---

# 7. Machine Identities

Machines and devices can also have identities.

Examples:

- Servers
- Workstations
- Network devices
- IoT devices

Authentication may use:

- Certificates
- Cryptographic keys
- Machine accounts
- Device identities

Example:

```text
Server
  |
  v
Certificate
  |
  v
Authenticate
  |
  v
Service
```

---

# 8. API Identities

Applications frequently authenticate to APIs.

Common mechanisms include:

- OAuth client credentials
- Certificates
- API keys
- Signed tokens
- Secrets

Example:

```text
Application
     |
     v
Client Identity
     |
     v
Authorization Server
     |
     v
Access Token
     |
     v
API
```

---

# 9. Secrets

A secret is credential material used to authenticate.

Examples include:

- Password
- API key
- Client secret
- Private key
- Token

Secrets require lifecycle management.

```text
CREATE
  |
  v
STORE
  |
  v
USE
  |
  v
ROTATE
  |
  v
REVOKE
```

Static secrets that never expire or rotate create significant risk.

---

# 10. Certificates

Certificates can be used to authenticate systems, applications or workloads.

Simplified:

```text
Application
     |
     v
Private Key
     |
     v
Certificate
     |
     v
Authentication
```

Certificates also have a lifecycle:

```text
Issue
  |
  v
Deploy
  |
  v
Use
  |
  v
Renew
  |
  v
Revoke / Expire
```

Certificate lifecycle management is therefore related to identity lifecycle management.

---

# 11. Human vs Non-Human Identity

A human identity may have:

```text
Alice
 |
 +-- Manager
 +-- Department
 +-- Job Title
 +-- Employment Status
```

A non-human identity may instead have:

```text
svc_payroll
 |
 +-- Owner
 +-- Application
 +-- Environment
 +-- Purpose
 +-- Criticality
```

The metadata is different, but governance is still required.

---

# 12. Ownership

Every non-human identity should have an accountable owner.

Example:

```text
svc_payroll
     |
     v
Owner
     |
     v
Payroll Application Team
```

Without ownership, it becomes difficult to answer:

```text
Who owns this identity?

Why does it exist?

What uses it?

What access does it have?

Is it still needed?
```

Ownership is one of the most important NHI governance concepts.

---

# 13. Purpose

A non-human identity should have a documented purpose.

Bad:

```text
svc123
```

No one knows why it exists.

Better:

```text
Identity:
svc_payroll_export

Purpose:
Export payroll reports

Owner:
Payroll Application Team

Target:
Reporting Database
```

---

# 14. Least Privilege

Non-human identities should receive only the access required for their purpose.

Bad:

```text
Application
     |
     v
Database Administrator
```

when the application only needs:

```text
SELECT
```

Better:

```text
Application
     |
     v
READ-ONLY DATABASE ROLE
```

The same least-privilege principle used for humans applies to NHIs.

---

# 15. Credential Storage

Credentials should not be embedded directly in:

- Source code
- Scripts
- Configuration files
- Container images
- Git repositories

Bad:

```text
DB_USER=svc_app
DB_PASSWORD=MySecretPassword
```

Better:

```text
Application
     |
     v
Secret Manager / Vault
     |
     v
Credential
```

or, where supported:

```text
Application
     |
     v
Managed / Workload Identity
     |
     v
Resource
```

without a long-lived stored password.

---

# 16. Credential Rotation

Credentials should have a lifecycle.

Example:

```text
Credential Created
       |
       v
Credential Used
       |
       v
Credential Rotated
       |
       v
Old Credential Revoked
```

Rotation reduces exposure from compromised credentials.

Automation is particularly important because manually rotating credentials across many applications can be difficult and error-prone.

---

# 17. Long-Lived vs Short-Lived Credentials

Long-lived credential:

```text
Password / Secret
      |
      v
Valid for months or years
```

Short-lived credential:

```text
Authentication
      |
      v
Temporary Token
      |
      v
Expires
```

Where practical, short-lived credentials reduce the period during which stolen credentials can be used.

---

# 18. NHI Lifecycle

Non-human identities require lifecycle management just like human identities.

A simplified lifecycle is:

```text
REQUEST
   |
   v
APPROVE
   |
   v
CREATE
   |
   v
ASSIGN OWNER
   |
   v
GRANT ACCESS
   |
   v
USE
   |
   v
REVIEW
   |
   v
ROTATE
   |
   v
REVOKE / DELETE
```

The triggers are different from human JML, but the lifecycle principle remains.

---

# 19. Human JML vs NHI Lifecycle

Human identity:

```text
JOINER
  |
MOVER
  |
LEAVER
```

Non-human identity:

```text
CREATE
  |
CHANGE
  |
RETIRE
```

Example:

```text
Application Created
      |
      v
Service Identity Created
```

Later:

```text
Application Retired
      |
      v
Service Identity Should Be Removed
```

If it is not removed, an orphaned identity remains.

---

# 20. Orphaned Non-Human Identities

An orphaned NHI has no valid owner or purpose.

Example:

```text
Application Retired
       |
       X
Service Account Remains
       |
       v
Orphaned Identity
```

This is dangerous because the account may still have active access.

Questions to ask:

```text
Who owns it?

Is it still used?

What can it access?

When was it last used?

Can it be removed?
```

---

# 21. NHI and PAM

Some non-human identities have privileged access.

Example:

```text
Backup Application
       |
       v
Privileged Service Account
       |
       v
Servers
```

PAM may help manage:

- Service credentials
- Password rotation
- Privileged secrets
- Vaulting
- Monitoring

This creates an overlap between:

```text
NHI
+
PAM
```

---

# 22. NHI and IGA

IGA can govern non-human identities by managing:

- Ownership
- Approval
- Access
- Entitlements
- Reviews
- Certification
- Lifecycle
- Policy

Example:

```text
Service Account
      |
      v
Owner
      |
      v
Entitlements
      |
      v
Periodic Review
```

---

# 23. NHI Recertification

Non-human identities should also be reviewed.

Questions include:

```text
Does this identity still exist for a valid reason?

Is the owner still correct?

Is the application still active?

Is the access still required?

Are the credentials properly managed?

Is the privilege level appropriate?
```

Possible outcome:

```text
Review
 /   \
v     v
KEEP RETIRE
       |
       v
Revoke Access
       |
       v
Remove Identity
```

---

# 24. NHI and SoD

Non-human identities can also create SoD problems.

Example:

```text
Automation Account
      |
      +-- CREATE_PAYMENT
      |
      +-- APPROVE_PAYMENT
```

The fact that the identity is non-human does not remove the risk.

SoD policies may therefore need to include both human and non-human identities.

---

# 25. Authentication Without Static Secrets

Modern architectures increasingly try to avoid long-lived static secrets.

Instead of:

```text
Application
     |
     v
Stored Password
     |
     v
Resource
```

prefer, where supported:

```text
Application / Workload
        |
        v
Workload Identity
        |
        v
Short-Lived Credential
        |
        v
Resource
```

This reduces secret-management risk.

---

# 26. Common Risks

## Unknown Owner

```text
Service Account
      |
      v
Owner = ???
```

Nobody is accountable.

---

## Excessive Privilege

The NHI has more access than required.

---

## Static Credentials

Credentials never change.

---

## Hard-Coded Secrets

Credentials exist in:

- Source code
- Scripts
- Configuration
- Git repositories

---

## Orphaned Identities

The application disappears but its identity remains.

---

## Shared Identities

Multiple applications use the same identity.

This makes accountability difficult.

---

## No Recertification

Access is granted once and never reviewed.

---

## Poor Inventory

The organisation does not know how many non-human identities exist.

Without inventory, governance is extremely difficult.

---

# 27. Good NHI Governance

A well-governed NHI should have:

```text
IDENTITY
   |
   +-- Unique identifier
   |
   +-- Owner
   |
   +-- Purpose
   |
   +-- Application / workload
   |
   +-- Environment
   |
   +-- Entitlements
   |
   +-- Credential type
   |
   +-- Credential lifecycle
   |
   +-- Review date
   |
   +-- Expiration / retirement process
```

---

# 28. What to Remember

```text
NHI
=
Identity used by something
other than a human
```

```text
SERVICE ACCOUNT
=
Identity used by a service
or application
```

```text
WORKLOAD IDENTITY
=
Identity of a software workload
```

```text
MANAGED IDENTITY
=
Identity whose credential lifecycle
is managed by the platform
```

```text
SECRET
=
Credential material
```

```text
OWNER
=
Human/team accountable for the NHI
```

```text
ROTATION
=
Replace credentials
```

```text
ORPHANED NHI
=
Identity without valid owner/purpose
```

---

# Key Mental Model

```text
               NON-HUMAN IDENTITY
                       |
          +------------+------------+
          |            |            |
          v            v            v
       Service     Application    Workload
       Account       Identity     Identity
          |            |            |
          +------------+------------+
                       |
                       v
                 AUTHENTICATE
                       |
                       v
                  ENTITLEMENTS
                       |
                       v
                    ACCESS
                       |
                       v
                   RESOURCE

Govern everything around it:

OWNER
  |
PURPOSE
  |
LEAST PRIVILEGE
  |
CREDENTIAL LIFECYCLE
  |
ROTATION
  |
RECERTIFICATION
  |
RETIREMENT
```

The central principle is:

> If something can authenticate and access a resource, its identity and access require governance.
