---
tags: azure, cloud, azure-certifications/az900, paas, azure-certifications/az204
---

# Azure App Service

Build and host web apps, background jobs, mobile back-ends, and RESTful APIs **without managing infrastructure**.

It offers automatic scaling and high availability.

It is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends.

With Azure App Service you can both [[scale-up-down]] and [[scale-in-out]].

You can use CI/CD and [[azure-app-services-deployment-slots]].

Each App Service belongs to an [[azure-app-service-plan]], which defines the compute capabilities.

## Types of App Services

### Web apps

Used for hosting web applications. You can choose the OS: Windows or Linux.

### API apps

Build REST-based web applications.

**It supports Swagger**, and it allows to publish the APIs in Azure Marketplace.

### WebJobs

Used to run a program or a script in the same context as a Web App.

Jobs can be scheduled or can be triggered by an event.

Since they run in the same context of the application, they can be useful to perform background tasks.

### Mobile apps

Used to build a backend for iOS and Android applications.

- Store mobile app data in a cloud-based SQL database.
- Use social authentication such as MSA, Google, Twitter, and Facebook.
- Send push notifications.
- Execute custom back-end logic in C# or Node.js.

## Deployment types

There are two main deployment types, depending on the [[azure-app-service-plan]].

- **multitenant public service**: host App Service plans in
  - Free
  - Shared
  - Basic
  - Standard
  - Premium, PremiumV2, PremiumV3
- **single-tenant environment**: available for Isolated SKU.

Related: [[azure-app-services-multitenant-networking]]

## Autoscaling

[[azure-app-service-autoscale]] monitors the resource metrics of a web app as it runs. It detects situations where other resources are required to handle an increasing workload, and ensures those resources are available before the system becomes overloaded.
