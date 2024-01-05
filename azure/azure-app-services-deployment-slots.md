---
tags: azure, cloud, azure-certifications/az204, azure-app-service
---

# Azure App Services Deployment Slots

When you deploy your web app, you can use a separate deployment slot instead of the default production slot when running in the **Standard, Premium, or Isolated App Service Plan tier**.

Deployment slots are live apps **with their own host names**.

**App content and configuration elements can be swapped** between two deployment slots, including the production slot.

Deploying an app to a slot first and swapping it into production ensures that all slot instances are **warmed up before being swapped into production**. This eliminates downtime when you deploy your app. **The traffic redirection is seamless**, and no requests are dropped because of swap operations. You can automate this entire workflow by configuring auto-swap when pre-swap validation isn't needed.

Each App Service plan tier supports a different number of deployment slots (Standard: 5 slots. Premium and Isolated: 20 slots). There's no extra charge for using deployment slots.

## Steps performed before swapping instances

Swapping between the source slot (e.g.: staging) and the target slot (e.g.: production) happens in steps:

1. **Apply the same configurations** existing on the target slot: slot-specific settings, connection strings, continuous deployment settings and App Service authentication settings are copied from the target slot to the source slot, forcing a restart.
2. **Wait for validation**: if the slot is configured to show a preview, the system waits for the validation of the slot before proceeding.
3. **Wait for every instance in the source slot to complete its restart**: if any instance fails to restart, then the system reverts all the changes and stops the swapping;
4. **Initialize local cache**: to wake up the local cache, call the `/` endpoint of each instance on the source slot. This causes the restart of the instances;
5. If auto-swap is enabled with custom warm-up, **initialize each instance in the source slot by calling the `/` endpoint**. If an instance returns *any* HTTP response, it's considered to be warmed up.
6. When all the source slots are warmed up, **switch the routing rules for the two slots**. Now, the source slot becomes the new target slot, and vice versa.
7. Apply steps 1-5 to warm up the "new" source slot in case another swap is required.

## Slot configurations

When you clone configuration from another deployment slot, **the cloned configuration is editable**.

Some configuration elements follow the content across a swap (**not slot specific**):

- Publishing endpoints
- Custom domain names
- Non-public certificates and TLS/SSL settings
- Scale settings
- WebJobs schedulers
- IP restrictions
- Always On
- Diagnostic log settings
- Cross-origin resource sharing (CORS)
- Virtual network integration
- Managed identities
- Settings that end with the suffix `_EXTENSION_VERSION`

Other configuration elements stay in the same slot after a swap (**slot specific**):

- App settings (can be configured to stick to a slot)
- Connection strings (can be configured to stick to a slot)
- Handler mappings
- Public certificates
- WebJobs content
- Hybrid connections (planned to be unswapped)
- Azure Content Delivery Network (planned to be unswapped)
- Service endpoints (planned to be unswapped)
- Path mappings

You can make one setting stick to a specific slot by editing the *Deployment slot setting* page.

You can make all settings (except for the ones related to Managed Identity) swappable by setting the `WEBSITE_OVERRIDE_PRESERVE_DEFAULT_STICKY_SLOT_SETTINGS` to `0` or `false`. Every setting then becomes swappable.

https://learn.microsoft.com/en-us/training/modules/understand-app-service-deployment-slots/4-swap-deployment-slots