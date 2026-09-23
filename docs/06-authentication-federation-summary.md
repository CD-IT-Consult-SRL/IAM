# Authentication & Federation — Summary

## Fundamental Distinction

```text
Authentication
=
WHO ARE YOU?
```

```text
Authorization
=
WHAT CAN YOU DO?
```

Successful authentication does not automatically imply authorization.

---

## Authentication Factors

```text
Something you KNOW
=
Password / PIN
```

```text
Something you HAVE
=
Phone / Token / Security Key
```

```text
Something you ARE
=
Fingerprint / Face
```

MFA combines independent factors.

---

## SSO

```text
             +--> App A
             |
User -> IdP -+--> App B
             |
             +--> App C
```

SSO means authenticating once and accessing multiple trusted applications.

---

## Federation

Federation establishes trust between identity/security domains or systems.

```text
Identity Provider
       |
       | TRUST
       v
Application
```

The application relies on authentication performed by the IdP.

---

## IdP

The Identity Provider authenticates the user.

Examples:

- Microsoft Entra ID
- Keycloak
- Okta
- Ping Identity
- ADFS

---

## SAML

```text
User
 |
 v
IdP
 |
 v
SAML Assertion
 |
 v
Service Provider
```

Remember:

```text
SAML
=
IdP + SP + Assertion
```

---

## OAuth 2.0

Primarily an authorization framework.

```text
Application
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

Remember:

```text
OAuth 2.0
=
AUTHORIZATION
```

---

## OIDC

Identity/authentication layer built on OAuth 2.0.

```text
OIDC
=
OAuth 2.0
+
Identity
```

Important concept:

```text
ID Token
```

---

## Tokens

```text
ID Token
=
WHO
```

```text
Access Token
=
ACCESS
```

---

## Protocol Mental Map

```text
SAML
=
Enterprise federation / SSO
```

```text
OAuth 2.0
=
Authorization
```

```text
OIDC
=
Authentication / Identity
```

---

## Conditional Access

```text
Identity
+
Device
+
Location
+
Risk
+
Authentication Strength
        |
        v
Access Decision
```

This connects authentication with ABAC-style contextual controls.

---

## Key Principle

> Authentication establishes identity. Authorization determines access.
