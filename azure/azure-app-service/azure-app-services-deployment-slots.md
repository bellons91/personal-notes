---
tags: azure, cloud, azure-certifications/az204, azure-app-service, deployment-slots
---

# Azure App Services Deployment Slots

When you deploy your web app, you can use a separate deployment slot instead of the default production slot when running in the **Standard, Premium, or Isolated App Service Plan tier**.

Deployment slots are live apps **with their own host names**.

**App content and configuration elements can be swapped** between two deployment slots, including the production slot.

Deploying an app to a slot first and swapping it into production ensures that all slot instances are **warmed up before being swapped into production**. This eliminates downtime when you deploy your app. **The traffic redirection is seamless**, and no requests are dropped because of swap operations. You can automate this entire workflow by configuring auto-swap when pre-swap validation isn't needed.

Each App Service plan tier supports a different number of deployment slots (Standard: 5 slots. Premium and Isolated: 20 slots). There's no extra charge for using deployment slots.

## Steps performed before swapping instances

Swapping between the source slot (e.g., staging) and the target slot (e.g., production) happens in steps:

1. **Apply the same configurations** existing on the target slot: slot-specific settings, connection strings, continuous deployment settings and App Service authentication settings are copied from the target slot to the source slot, forcing a restart.
2. **Wait for validation**: if the slot is configured to show a preview, the system waits for the validation of the slot before proceeding.
3. **Wait for every instance in the source slot to complete its restart**: if any instance fails to restart, then the system reverts all the changes and stops the swapping;
4. **Initialize local cache**: to wake up the local cache, call the `/` endpoint of each instance on the source slot. This causes the restart of the instances;
5. If auto-swap is enabled with custom warm-up, **initialize each instance in the source slot by calling the `/` endpoint**. If an instance returns _any_ HTTP response, it's considered to be warmed up.
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

You can make one setting stick to a specific slot by editing the _Deployment slot setting_ page.

You can make all settings (except for the ones related to Managed Identity) swappable by setting the `WEBSITE_OVERRIDE_PRESERVE_DEFAULT_STICKY_SLOT_SETTINGS` to `0` or `false`. Every setting then becomes swappable.

## How to swap Deployment slots

### Manual swap

1. Under the Deployment slots page, select Swap.
2. Choose the source and the target slot.
3. Verify the changes by looking at the Target Changes tab.
4. Click Swap

### Swap with preview

1. Select the Source and Target slot.
2. Select _Perform swap with preview_.
3. Click Start Swap. This will allow you to see a preview of the slot, available at `https://<app_name>-<source-slot-name>.azurewebsites.net`.
4. Select _Complete Swap_ or _Cancel Swap_.

### Auto swap

Integrated with Azure DevOps Services pipelines.

Auto swap is **not supported on Linux and Web App for Containers**.

### Custom warm-up

Some applications require you to hit specific pages to complete the warm-up.

To specify which pages to call, you must edit the `applicationInitialization` node in the `web.config` file.

```xml
<system.webServer>
    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostName="[app hostname]" />
    </applicationInitialization>
</system.webServer>
```

You can also customize the warm-up behaviour with one or more of the following _app settings_:

- `WEBSITE_SWAP_WARMUP_PING_PATH`: The path to ping to warm up your site. Add this app setting by specifying a custom path that begins with a slash as the value. An example is `/statuscheck`. The default value is `/`.
- `WEBSITE_SWAP_WARMUP_PING_STATUSES`: Valid HTTP response codes for the warm-up operation. Add this app setting with a comma-separated list of HTTP codes. An example is 200,202 . If the returned status code isn't in the list, the warm-up and swap operations are stopped. **By default, all response codes are valid.**
- `WEBSITE_WARMUP_PATH`: A relative path on the site that should be pinged whenever the site restarts (not only during slot swaps). Example values include `/statuscheck` or the root path, `/`.

## Route traffic in App Service

By default, all client requests to the app's production URL (`http://<app_name>.azurewebsites.net`) are routed to the production slot.

**You can route a portion of the traffic to another slot**. This feature is useful if you need user feedback for a new update but you're not ready to release it to production.

You can define the percentage of clients to use the new slot by navigating under the Deployment Stots settings: you can go to the **Traffic %** column and specify the percentage of traffic you want to route.

**Random** users are routed. Still, when a client is routed to a specific slot, it's pinned to that slot for the rest of the client session, thanks to the usage of the `x-ms-routing-name` cookie.

If the client is pointing to the _staging_ slot, the cookie will be `x-ms-routing-name=staging`.

If the client is pointing to the production slot, the cookie name will be `x-ms-routing-name=self`.

If you want users to move from one app slot to another, you can append in the query string the value of the cookie: `<webappname>.azurewebsites.net/?x-ms-routing-name=staging`.

By default, new slots are given a routing rule of 0%.
