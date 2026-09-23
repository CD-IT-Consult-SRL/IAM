# Authentication & Federation — Cheat Sheet

## The Most Important Distinction

```text
AUTHENTICATION
=
WHO?
```

```text
AUTHORIZATION
=
WHAT?
```

---

## MFA

```text
KNOW
+
HAVE
+
ARE
```

Examples:

```text
Know = Password

Have = Phone / Token / Security Key

Are = Fingerprint / Face
```

---

## SSO

```text
Login once
   |
   v
Multiple applications
```

---

## Federation

```text
IdP
 |
 | TRUST
 v
Application
```

---

## SAML

```text
IdP
 |
 v
SAML Assertion
 |
 v
SP
```

Remember:

```text
SAML
=
IdP + SP + Assertion
```

---

## OAuth 2.0

```text
OAuth
=
AUTHORIZATION
```

Think:

```text
Access Token -> API
```

---

## OIDC

```text
OIDC
=
AUTHENTICATION / IDENTITY
on top of OAuth 2.0
```

Think:

```text
ID Token -> Identity
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

## Protocol Map

```text
SAML
    -> Federation / SSO

OAuth 2.0
    -> Authorization

OIDC
    -> Authentication / Identity
```

---

## Full Picture

```text
             USER
               |
               v
              IdP
               |
          Authenticate
               |
        +------+------+
        |             |
       SAML          OIDC
        |             |
        v             v
      APP           APP
        |
        v
   Authorization
        |
        v
      ACCESS
```

---

# 10-Second Memory

```text
Authentication = WHO

Authorization  = WHAT

MFA            = multiple factors

SSO            = login once

Federation     = trust another IdP

SAML           = IdP / SP / Assertion

OAuth 2.0      = Authorization

OIDC           = Authentication / Identity

ID Token       = WHO

Access Token   = ACCESS
```
