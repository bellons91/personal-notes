---
tags: az-204, azure, authentication, entra-id
---

# Application Object

Application objects describe the application to Microsoft Entra ID and can be considered the definition of the application, allowing the service to know how to issue tokens to the application based on its settings.

A Microsoft Entra application is defined by its one and only application object.

The application object will only exist in its "home" tenant, even if it's a multi-tenant application supporting service principals in other directories.

Similar to a class in object-oriented programming, the application object has some static properties that are applied to all the created service principals (or application instances), such as:

- Name, logo, and publisher
- Redirect URIs
- Secrets (symmetric and/or asymmetric keys used to authenticate the application)
- API dependencies ([[OAuth]])
- Published APIs/resources/scopes (OAuth)
- App roles
- Single sign-on ([[SSO]]) metadata and configuration
- User provisioning metadata and configuration
- Proxy metadata and configuration

An application object is used as a template or blueprint to create one or more [[service-principal]] objects. **A service principal is created in every tenant where the application is used.**

The application object describes three aspects of an application:

1. How the service can issue tokens in order to access the application.
2. What are the resources that the application might need to access.
3. Which are the actions that the application can take.

The application object is the global representation of your application for use across all tenants, and the service principal is the local representation for use in a specific tenant. The application object serves as the template from which common and default properties are derived for use in creating corresponding service principal objects.

An application object has:

A one to one relationship with the software application, and
A one to many relationships with its corresponding service principal object(s).
