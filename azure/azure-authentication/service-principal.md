---
tags: az-204, azure, authentication, entra-id
---

# Service Principal

Service principals are what govern an application connecting to Microsoft Entra ID and can be considered the instance of the application in your directory.

The security principal defines the access policy and permissions for the user/application in the Microsoft Entra tenant. This enables core features such as authentication of the user/application during sign-in, and authorization during resource access.

When you register an application in the portal, an [[application-object]] and a [[service-principal-object]] are automatically created in your home tenant.

There are three types of service principal:

1. **Application**: This type of service principal is the local representation, or application instance, of a global [[application-object]] in a single tenant or directory. **A service principal is created in each tenant where the application is used** and references the globally unique app object. The [[service-principal-object]] defines what the app can actually do in the specific tenant, who can access the app, and what resources the app can access.
2. **Managed identity**: This type of service principal is used to represent a [[managed-identity]]. When a managed identity is enabled, a service principal representing that managed identity is created in your tenant. Service principals representing managed identities can be granted access and permissions, but can't be updated or modified directly.
3. **Legacy**: This type of service principal represents a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. A legacy service principal can have credentials, service principal names, and reply URLs.

The service principal can include:

- A reference back to an application object through the application ID property
- Records of local user and group application-role assignments
- Records of local user and admin permissions granted to the application. For example: permission for the application to access a particular user's email
- Records of local policies including Conditional Access policy
- Records of alternate local settings for an application. Eg: Claims transformation rules, Attribute mappings (User provisioning), Directory-specific app roles (if the application supports custom roles), Directory-specific name or logo.
