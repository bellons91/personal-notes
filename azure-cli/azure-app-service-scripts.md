---
type: basic-note
foam_template:
  filepath: './azure-cli/azure-app-service-scripts.md'
tags: azure, cloud, cli
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
