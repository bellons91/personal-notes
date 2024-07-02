---
tags: az-204, azure, identity, authentication
---

# Microsoft Authentication Library (MSAL)

The Microsoft Authentication Library (MSAL) enables developers to acquire tokens from the Microsoft identity platform in order to authenticate users and access secured web APIs.

MSAL gives you many ways to get tokens, with a consistent API for many platforms. Using MSAL provides the following benefits:

- No need to directly use the OAuth libraries or code against the protocol in your application.
- Acquires tokens on behalf of a user or on behalf of an application (when applicable to the platform).
- Maintains a token cache and refreshes tokens for you when they're close to expire. You don't need to handle token expiration on your own.
- Helps you specify which audience you want your application to sign in.
- Helps you set up your application from configuration files.
- Helps you troubleshoot your app by exposing actionable exceptions, logging, and telemetry.

## How to initialize client applications with MSAL

With MSAL.NET 3.x, the recommended way to instantiate an application is by using the application builders: `PublicClientApplicationBuilder` and `ConfidentialClientApplicationBuilder`. They offer a powerful mechanism to configure the application either from the code, or from a configuration file, or even by mixing both approaches.

**Before initializing an application, you first need to register it** so that your app can be integrated with the Microsoft identity platform. After registration, you may need the following information:

- Client Id
- Identity provider URL
- TenantID
- Application secret or *X509Certificate2* certificate
- RedirectURI, for public websites.

When you register an application, it automatically generates an API permission `user.read` for Microsoft Graph. You can use that permission to acquire a token.

### Initialize public client application

The following code instantiates a public client application, signing-in users in the Microsoft Azure public cloud, with their work and school accounts, or their personal Microsoft accounts.

```cs
IPublicClientApplication app = 
PublicClientApplicationBuilder.Create(clientId).Build();
```

### Initialize Confidential application

The following code instantiates a confidential application (a Web app located at `https://myapp.azurewebsites.net`) handling tokens from users in the Microsoft Azure public cloud, with their work and school accounts, or their personal Microsoft accounts. The application is identified with the identity provider by sharing a client secret:

```cs
string redirectUri = "https://myapp.azurewebsites.net";
IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(clientId)
    .WithClientSecret(clientSecret)
    .WithRedirectUri(redirectUri )
    .Build();
```
