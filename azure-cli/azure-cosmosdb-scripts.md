---
tags: azure, cloud, azure-certifications/az900, azure-cli
---

# Operations on CosmosDB with Cloud CLI

This page lists some scripts useful for operating on [[azure-cosmos-db]].

## Create a CosmosDB account

The name must be:

- lowercase
- with only numbers, letters, hyphens
- between 3 and 31 char long

```cli
az cosmosdb create --name <myCosmosDBacct> --resource-group <resource-group-name>
```

This command returns several info, such as the `documentEndpoint`.

## Get the primary key

```cli
az cosmosdb keys list --name <myCosmosDBacct> --resource-group <resource-group-name>
```
