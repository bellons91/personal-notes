---
tags: azure, cloud, azure-cli, az-204
---

# Azure App Service Scripts

This page lists some scripts useful for operating with [[azure-app-service]].

## List the available runtimes

You can see the list of available runtimes for Azure App Service instances by specifying the OS, which can only be Linux or Windows

```bash
az webapp list-runtimes --os-type linux
```

or

```bash
az webapp list-runtimes --os-type windows
```

## List available outbound addresses

List available IP addresses

```bash
az webapp show \
    --resource-group <group_name> \
    --name <app_name> \
    --query outboundIpAddresses \
    --output tsv
```

To find all possible outbound IP addresses for your app, regardless of pricing tiers, run the following command in the Cloud Shell.

```bash
az webapp show \
    --resource-group <group_name> \
    --name <app_name> \
    --query possibleOutboundIpAddresses \
    --output tsv
```
