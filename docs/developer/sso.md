# Single Sign-On (SSO)

Single Sign-On (SSO) lets your users sign in to Scholaro through your organization's identity provider (IdP) using their existing work credentials, instead of a separate Scholaro email and password.

Scholaro supports both **OpenID Connect (OIDC)** and **SAML 2.0**, so any standards-compliant identity provider can be connected.

## How Scholaro SSO works

- Your users go to the Scholaro sign-in page and enter their work email address.
- Scholaro routes them to your organization's identity provider based on their **email domain** (for example, `@university.edu`).
- They authenticate with your IdP and are returned to Scholaro, already signed in.
- On a user's first sign-in, Scholaro **creates their account automatically** (just-in-time provisioning). There is no need to pre-create users in Scholaro.

!!! warning "Your IdP controls access to Scholaro"
    When SSO is enabled for your domain, anyone your identity provider can authenticate for that domain can sign in to Scholaro. If your IdP is compromised, unauthorized parties could gain access to your Scholaro account. Scholaro only trusts your IdP to assert identities **within your verified email domain**.

## Enabling SSO

SSO connections are configured by the Scholaro team. The high-level process is:

1. **Request SSO.** Contact your Scholaro representative and provide your email domain (or domains) and which identity provider you use.
2. **Receive your service-provider details.** Scholaro sends you the exact values to enter in your IdP — a **Redirect URI** (for OIDC) or an **ACS URL** and **SP Entity ID** (for SAML).
3. **Register Scholaro in your IdP.** Create the application in your identity provider using the values from step 2. See the provider-specific guide below.
4. **Send Scholaro your connection details.** Return the values your IdP generates (each guide lists exactly what to send).
5. **Test.** Scholaro enables the connection and confirms with you, then you sign in with a test account from your domain.

!!! note
    The Redirect URI and ACS URL shown in these guides are **examples**. Always use the exact URLs Scholaro provides for your connection.

## Set up SSO with your identity provider

- [Microsoft Entra ID](sso/entra-id-setup.md) — Microsoft 365 / Azure AD, via OIDC.
- [Google Workspace](sso/google-workspace-setup.md) — via a custom SAML app.
- [Okta](sso/okta-setup.md) — via OIDC.
- [Other identity providers](sso/other-idp-setup.md) — any OIDC or SAML 2.0 provider (OneLogin, Ping, ADFS, Shibboleth, and more).

## Supported features

- **OpenID Connect (OIDC) and SAML 2.0** identity providers.
- **Email-domain routing** — users are sent to the right IdP automatically based on their email address.
- **Just-in-time provisioning** — Scholaro accounts are created on first sign-in.
- **Automatic deprovisioning** — when you disable a user at your IdP, their Scholaro access is revoked within the re-authentication interval.
- **Custom attribute mapping** — if your IdP sends email or name under non-standard attribute names, Scholaro can map them.

## Limitations

- **Managed setup.** SSO connections are configured by the Scholaro team; there is not yet a self-service dashboard.
- **One identity provider per email domain.**
- **SCIM is not supported.** User deprovisioning takes effect at the next re-authentication rather than instantly through directory sync.
