---
tags: azure, cloud, azure-certifications/az204, 
---

# Multitenant App Service networking

The roles that handle incoming HTTP or HTTPS requests are called **front ends**.

The roles that host the customer workload are called **workers**. If you scale out the worker, all the apps in that App Service plan are replicated on a new worker for each instance in your App Service plan.

All the roles in an App Service deployment exist in a multi-tenant network. Because there are many different customers in the same App Service scale unit, **you can't connect the App Service network directly to your network**.

Since you cannot connect directly to the App Service, you have to use the functionalities provided by Azure to handle inbound and outbound connections.

**Inbound** features:

- App-assigned address:
  - Support IP-based SSL needs for your app
  - Support unshared dedicated inbound address for your app
- Access restrictions
  - Restrict access to your app from a set of well-defined addresses
- Service endpoints
- Private endpoints

**Outbound** features:

- Hybrid connections
- Gateway-required virtual network integration
- [[azure-virtual-network]]

## Outbound addresses

Depending on the [[azure-app-service-plan]], you use a different set of worker VMs, each with a different set of outbound addresses.

There are three groups:

- Free, Shared, Basic, Standard, Premium
- PremiumV2
- PremiumV3

The outbound addresses used by your app for making outbound calls are listed in the properties for your app. These addresses are shared by all the apps running on the same worker VM family in the App Service deployment

You can see the list of outbound addresses available for your Scale unit by accessing a property named `possibleOutboundIpAddresses`.

Using the CLI, you can see:

- the list of outbound addresses available for your app
- the list of all possible outbound addresses for your app, regardless of the pricing tier.

See [[azure-app-service-scripts#List available outbound addresses]].
