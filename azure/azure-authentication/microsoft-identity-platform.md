---
tags: azure, az-204, authentication
---

# Microsoft Identity Platform

The Microsoft identity platform for developers is a set of tools that includes #authentication service, open-source libraries, and application management tools.

It allows to use social accounts of Microsoft Identities to log in to your application, APIs, or [[Microsoft Graph API]].

Microsoft Identity Platform is made of different components:

- [[Oauth20]] and [[OpenId Connect]] compliant authentication services, used to integrate several identity types, such as
  - work or school accounts, provisioned though [[azure-entra]];
  - personal accounts
  - social logins, using [[azure-ad-b2c]]
- Open-source libraries, such as [[Microsoft Authentication Library]] (#MSAL), and other standard-compliant libraries;
- Microsoft identity platform endpoints;
- Application management portal;
- Application configuration via APIs and PowerShell.

You can use it to define #passwordless authentication and [[conditional-access]].

Any web-hosted resource that integrates with the Microsoft identity platform has a resource identifier, or application ID URI. For example:

- Microsoft Graph: <https://graph.microsoft.com>
- Microsoft 365 Mail API: <https://outlook.office.com>
- Azure Key Vault: <https://vault.azure.net>

## Permissions

When using OAuth 2.0, you can define two types of OAuth permissions:

1. **Delegated permissions** are used by apps that have a signed-in user present. For these apps, either the user or an administrator consents to the permissions that the app requests. The app is delegated with the permission to act as a signed-in user when it makes calls to the target resource.
2. **App-only access permissions** are used by apps that run without a signed-in user present, **for example, apps that run as background services or daemons**. Only an administrator can consent to app-only access permissions.

## Consent

Applications in Microsoft identity platform rely on consent in order to gain access to necessary resources or APIs. There are many kinds of consent that your app may need to know about in order to be successful.

- **Static user consent**: you must specify all the permissions it needs in the app's configuration in the Azure portal. Static permissions also enable administrators to consent on behalf of all users in the organization.
- **Incremental and dynamic user consent**: You can ask for a minimum set of permissions upfront and request more over time as the customer uses more app features. To do so, you can specify the scopes your app needs at any time by including the new scopes in the scope parameter when requesting an access token - without the need to predefine them in the application registration information.
- **Admin consent**: Admin consent is required when your app needs access to certain high-privilege permissions. Admin consent ensures that administrators have some other controls before authorizing apps or users to access highly privileged data from the organization.
