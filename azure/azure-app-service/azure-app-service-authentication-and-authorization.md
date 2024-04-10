---
tags: azure, cloud, az-204, authentication, authorization, azure-app-services
---

# Azure App Service Authentication and Authorization

The built-in authentication feature for App Service provides out-of-the-box authentication with **federated identity providers** (a third-party identity provider manages the user identities and authentication flow for you).

Azure App Service allows you to integrate various auth capabilities into your web app or API without implementing them yourself.

It’s built directly into the platform and **doesn’t require any particular language**, SDK, security expertise, or code.

You can **integrate with multiple login providers**. For example:

- Microsoft Entra ID
- Facebook
- Google
- Twitter
- GitHub
- other OpenID Connect providers

When you enable authentication and authorization with one of these providers, its sign-in endpoint is available for user authentication and for validation of authentication tokens from the provider.

## Authentication module

**The authentication and authorization module runs in the same sandbox as your application code**. When it's enabled, every incoming HTTP request passes through it before being handled by your application code. This module handles several things for your app:

- Authenticates users and clients with the specified identity provider(s)
- **Validates, stores, and refreshes OAuth tokens** issued by the configured identity provider(s)
- Manages the authenticated session
- **Injects identity information into HTTP request headers**

The authentication module is independent from the application, and it can be configured using [[azure-resource-manager]] or a configuration file.

Note that **in Linux and containers the authentication and authorization module runs in a separate container**, isolated from your application code. Because it does not run in-process, no direct integration with specific language frameworks is possible.

## Authentication flow

The authentication flow is the same for all providers, but differs depending on whether you want to sign in with the provider's SDK.

### With provider SDK

The application signs users in to the provider manually and then **submits the authentication token to App Service** for validation.

This is typically the case with **browser-less apps**, which can't present the provider's sign-in page to the user.

The application code manages the sign-in process, so it's also called **client-directed flow** or **client flow**. This applies to REST APIs, Azure Functions, JavaScript browser clients, and native mobile apps that sign users in using the provider's SDK.

Steps are:

1. **Sign user in**: client code signs user in directly with provider's SDK and receives an authentication token.
2. **Post-authentication**: client code posts token from provider to `/.auth/login/<provider>` for validation.
3. **Establish authenticated session**: App Service returns **its own authentication token** to client code.
4. **Serve authenticated content**: Client code presents authentication token in `X-ZUMO-AUTH` header.

### Without provider SDK

The application **delegates federated sign-in to App Service**. This is typically the case with **browser apps**, which can present the provider's login page to the user.

The server code manages the sign-in process, so it's also called **server-directed flow** or **server flow**.

Steps are:

1. **Sign user in**: Redirects client to `/.auth/login/<provider>`;
2. **Post-authentication**: Provider redirects client to `/.auth/login/<provider>/callback`.
3. **Establish authenticated session**: App Service adds authenticated cookie to response.
4. **Serve authenticated content**: Client includes authentication cookie in subsequent requests (_automatically handled by browser_).

## What happens when a request is not authenticated

You can configure App Services to act in two ways when a request is not authenticated:

- **Allow unauthenticated requests**: this options **defers authentication to the application code**. It gives flexibility in handling anonymous requests. It lets you present **multiple sign-in providers to your users**.
- **Require authentication**: This option rejects any unauthenticated traffic to your application. Two possible behaviors: 1. If the application is browser-based, this rejection can be a redirect action to one of the configured identity providers. 2. If the application is a mobile app, it returns a HTTP 401 or HTTP 403 response.

## Token store

App Service provides a built-in token store, which is a **repository of tokens** that are associated with the users of your web apps, APIs, or native mobile apps. When you enable authentication with any provider, this token store is immediately available to your app.

## Logging and tracing

If you enable application logging, **authentication and authorization traces are collected directly in your log files**. If you see an authentication error that you didn't expect, you can conveniently find all the details by looking in your existing application logs.

## External links

🔗 [Authentication and authorization in Azure App Service and Azure Functions](https://learn.microsoft.com/en-us/azure/app-service/overview-authentication-authorization)
