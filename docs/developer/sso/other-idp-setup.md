# Other Identity Providers

Scholaro works with any identity provider that supports **OpenID Connect (OIDC)** or **SAML 2.0** — including OneLogin, Ping, ADFS, Shibboleth, and others.

Before you start, read the [SSO overview](../sso.md) for how the managed setup process works. Use the tab below that matches the protocol your identity provider uses.

=== "OIDC"

    **1. Register an application**

    In your identity provider, create a new **web / confidential** OIDC application — one that can hold a client secret and uses the authorization-code flow.

    Set the **Redirect URI** (also called the sign-in redirect or callback URL) to the value Scholaro provided:

    `https://www.scholaro.com/login/sso/<your-connection>/callback`

    **2. Configure scopes**

    Make sure the application can return the **openid**, **profile**, and **email** scopes. If your provider supports **offline_access**, include it so Scholaro can detect when a user is later disabled at the IdP.

    **3. Send Scholaro your connection details**

    | Value | Notes |
    | --- | --- |
    | Issuer / Authority URL | The provider's OIDC issuer; its discovery document is at `<issuer>/.well-known/openid-configuration` |
    | Client ID | From the application you registered |
    | Client secret | Send through a secure channel |
    | Email domain(s) | e.g. `university.edu` |

=== "SAML 2.0"

    **1. Create a SAML application**

    In your identity provider, create a new **SAML 2.0** application and enter the service-provider values Scholaro provided:

    - **ACS URL** (Assertion Consumer Service / reply URL): `https://www.scholaro.com/login/sso/<your-connection>/Acs`
    - **SP Entity ID** (audience): `https://www.scholaro.com/login/sso/<your-connection>/Saml2`
    - **Name ID**: the user's email address (`EMAIL` format).

    **2. Confirm the email attribute**

    Ensure the assertion includes the user's email — as the Name ID or as an attribute. If your IdP uses a non-standard attribute name (for example the eduPerson / LDAP OID `urn:oid:0.9.2342.19200300.100.1.3` for email), note which attribute carries the email and name so Scholaro can map them.

    **3. Send Scholaro your connection details**

    | Value | Notes |
    | --- | --- |
    | IdP metadata URL or metadata XML | Preferred — Scholaro reads the signing certificate and endpoints from it |
    | IdP Entity ID | The identity provider's issuer / entity ID |
    | Email domain(s) | e.g. `university.edu` |
    | Attribute names (if non-standard) | Which attribute carries email / name |

!!! note
    The Redirect URI, ACS URL, and SP Entity ID shown above are **examples**. Always use the exact values Scholaro provides for your connection.
