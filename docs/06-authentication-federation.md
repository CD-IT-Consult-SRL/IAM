# Authentication, SSO & Federation

## 1. Overview

Authentication answers:

```text
WHO ARE YOU?

and

HOW DO YOU PROVE IT?
```

Once identity has been established, another question follows:

```text
WHAT ARE YOU ALLOWED TO DO?
```

These are different concepts:

```text
Authentication
=
Who are you?
```

```text
Authorization
=
What are you allowed to do?
```

This distinction is fundamental in IAM.

---

# 2. Authentication Factors

Authentication factors are commonly divided into categories.

## Something You Know

Examples:

- Password
- PIN

```text
KNOWLEDGE FACTOR
```

## Something You Have

Examples:

- Smartphone
- Hardware token
- Smart card
- Security key

```text
POSSESSION FACTOR
```

## Something You Are

Examples:

- Fingerprint
- Face recognition

```text
INHERENCE FACTOR
```

---

# 3. Multi-Factor Authentication — MFA

MFA requires authentication using more than one independent factor.

Example:

```text
Password
   +
Security Key
   =
MFA
```

or:

```text
Password
   +
Authenticator App
   =
MFA
```

The important point is that the factors should come from different categories.

For example:

```text
Password + PIN
```

uses two knowledge factors and is therefore not normally considered true MFA.

---

# 4. Passwordless Authentication

Passwordless authentication removes the traditional password from the authentication process.

Examples include:

- Passkeys
- FIDO2 security keys
- Platform authenticators
- Smart cards
- Certificate-based authentication

Example:

```text
User
 |
 v
Device / Security Key
 |
 v
Cryptographic Authentication
 |
 v
Identity Verified
```

---

# 5. Passkeys and FIDO2

Passkeys use public-key cryptography.

Simplified model:

```text
Device
 |
 +-- Private Key
 |
 |   NEVER leaves device
 |
 v
Authentication

Service
 |
 +-- Public Key
```

The private key is not sent to the remote service.

This provides strong resistance to traditional password theft and phishing attacks when correctly implemented.

---

# 6. Single Sign-On — SSO

Single Sign-On allows a user to authenticate once and then access multiple applications without repeatedly entering credentials.

```text
             +--> Application A
             |
User -> IdP -+--> Application B
             |
             +--> Application C
```

The Identity Provider performs authentication.

Applications trust the Identity Provider.

Important:

```text
SSO
!=
One password copied everywhere
```

SSO is based on trust between systems.

---

# 7. Identity Provider — IdP

An **Identity Provider (IdP)** authenticates identities and provides identity information to other systems.

Examples include:

- Microsoft Entra ID
- Keycloak
- Okta
- Ping Identity
- ADFS

Simplified:

```text
User
 |
 v
Identity Provider
 |
 v
Authentication
 |
 v
Application
```

---

# 8. Service Provider / Relying Party

The application relying on the Identity Provider may be called:

```text
Service Provider (SP)
```

in SAML terminology.

In OpenID Connect terminology, the application is typically called:

```text
Relying Party (RP)
```

or an OIDC client.

Simplified:

```text
USER
 |
 v
IdP
 |
 v
SP / Application
```

---

# 9. Federation

Federation establishes trust between separate identity/security domains or systems.

Instead of every application authenticating the user itself:

```text
Application
    |
    v
Trust Identity Provider
```

Example:

```text
Microsoft Entra ID
        |
        | Trust
        v
   SaaS Application
```

The application accepts identity information from the trusted Identity Provider.

---

# 10. Federation Example

Alice wants to access a SaaS application.

```text
Alice
  |
  v
SaaS Application
  |
  v
Redirect to IdP
  |
  v
Microsoft Entra ID
  |
  v
Authenticate Alice
  |
  v
Send trusted identity information
  |
  v
SaaS Application
  |
  v
Access
```

The SaaS application does not need to maintain Alice's password.

---

# 11. SAML

SAML stands for:

```text
Security Assertion Markup Language
```

It is commonly used for enterprise web SSO and federation.

Main actors:

```text
USER
 |
 v
Identity Provider (IdP)
 |
 v
Service Provider (SP)
```

The IdP provides a **SAML assertion** to the Service Provider.

Simplified:

```text
User
 |
 v
Service Provider
 |
 v
Identity Provider
 |
 | Authenticate
 |
 v
SAML Assertion
 |
 v
Service Provider
 |
 v
Access
```

The assertion can contain information about the authenticated user.

---

# 12. OpenID Connect — OIDC

OpenID Connect is an identity layer built on top of OAuth 2.0.

Its primary purpose is authentication and identity information.

Simplified:

```text
User
 |
 v
Application
 |
 v
Identity Provider
 |
 v
Authentication
 |
 v
ID Token
 |
 v
Application
```

OIDC commonly uses JSON Web Tokens (JWTs).

A key concept is the:

```text
ID Token
```

which contains information about the authenticated identity.

---

# 13. OAuth 2.0

OAuth 2.0 is primarily an **authorization framework**.

It allows an application to obtain limited access to a resource on behalf of a user or itself without receiving the user's password.

Simplified example:

```text
User
 |
 v
Application
 |
 v
Authorization Server
 |
 v
Access Token
 |
 v
API / Resource Server
```

The important distinction:

```text
OAuth 2.0
=
Authorization
```

```text
OIDC
=
Authentication / Identity layer
on top of OAuth 2.0
```

---

# 14. Tokens

Modern authentication and authorization systems frequently use tokens.

Two important examples are:

```text
ID Token
```

and:

```text
Access Token
```

Simplified distinction:

```text
ID TOKEN
=
Information about authentication
and identity
```

```text
ACCESS TOKEN
=
Used to access a protected resource/API
```

Think:

```text
ID Token
-> WHO
```

```text
Access Token
-> ACCESS
```

This is simplified but useful for the first mental model.

---

# 15. SAML vs OIDC

Both can be used for federation and SSO.

A simplified comparison:

```text
SAML
 |
 +-- XML
 +-- Enterprise SSO
 +-- IdP / SP
 +-- SAML Assertion
```

```text
OIDC
 |
 +-- Built on OAuth 2.0
 +-- Modern web/mobile applications
 +-- JSON / JWT commonly used
 +-- ID Token
```

Do not think:

```text
SAML = old and useless
OIDC = always better
```

Both are widely used.

The appropriate protocol depends on the application and environment.

---

# 16. Authentication vs Federation vs SSO

These terms are related but not identical.

```text
AUTHENTICATION
=
Prove identity
```

```text
FEDERATION
=
Trust identity information
from another identity domain/system
```

```text
SSO
=
Authenticate once and access
multiple applications
```

Example:

```text
Alice
 |
 v
Entra ID
 |
 | Authentication + MFA
 |
 v
Federation
 |
 +---- SAML ----> Application A
 |
 +---- OIDC ----> Application B
```

Alice experiences SSO.

---

# 17. Authentication vs Authorization

This distinction is extremely important.

Example:

```text
Alice successfully authenticates.
```

This proves:

```text
Alice is Alice.
```

It does NOT automatically mean:

```text
Alice can approve payments.
```

That requires authorization.

```text
Authentication
      |
      v
Identity Established
      |
      v
Authorization
      |
      v
Access Decision
```

Think:

```text
Authentication
=
WHO?
```

```text
Authorization
=
WHAT?
```

---

# 18. Conditional Access

Modern identity platforms can also make access decisions using contextual information.

Examples:

- User
- Group
- Device state
- Location
- Application
- Risk
- Authentication strength

Example:

```text
User authenticated
      |
      v
Check Conditions
      |
      +-- Managed device?
      +-- Allowed location?
      +-- MFA completed?
      +-- Risk acceptable?
      |
      v
Access Decision
```

Microsoft Entra Conditional Access is a common example.

This also connects with concepts from ABAC.

---

# 19. Authentication Risks

Common risks include:

- Weak passwords
- Password reuse
- Credential theft
- Phishing
- MFA fatigue / push bombing
- Session theft
- Token theft
- Misconfigured federation
- Excessive token lifetime
- Weak recovery processes

Authentication security is not limited to passwords.

---

# 20. Federation Risks

Federation creates powerful trust relationships.

If the Identity Provider is compromised, multiple connected applications may be affected.

```text
             +--> App A
             |
Compromised  +--> App B
IdP          |
             +--> App C
```

Therefore Identity Providers are critical security infrastructure.

Important controls include:

- Strong authentication
- MFA
- Secure federation configuration
- Certificate/key management
- Token validation
- Monitoring
- Logging
- Conditional access
- Privileged administration controls

---

# 21. Relationship with IAM

Authentication is one part of IAM.

```text
IDENTITY
   |
   v
Authentication
   |
   v
Authorization
   |
   v
Access
```

But the complete lifecycle is larger:

```text
Authoritative Source
       |
       v
      JML
       |
       v
Identity
       |
       v
Authentication
       |
       v
Authorization
       |
       v
Roles / Entitlements
       |
       v
Access
       |
       v
Recertification
```

---

# 22. What to Remember

```text
AUTHENTICATION
=
Who are you?
```

```text
AUTHORIZATION
=
What can you do?
```

```text
MFA
=
Multiple independent authentication factors
```

```text
SSO
=
Authenticate once, access multiple applications
```

```text
FEDERATION
=
Trust identity from another system/domain
```

```text
SAML
=
Federation / SSO protocol
```

```text
OAuth 2.0
=
Authorization framework
```

```text
OIDC
=
Authentication / identity layer on OAuth 2.0
```

```text
ID TOKEN
=
Identity / authentication information
```

```text
ACCESS TOKEN
=
Access to protected resource/API
```

---

# Key Mental Model

```text
                    USER
                      |
                      v
              IDENTITY PROVIDER
                      |
             Authentication
                      |
             +--------+--------+
             |                 |
             v                 v
          SAML               OIDC
             |                 |
             v                 v
        Application       Application
             |
             v
        Authorization
             |
             v
          ACCESS
```

The most important distinction is:

> Authentication establishes identity. Authorization determines access.
