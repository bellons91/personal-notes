---
tags: azure, cloud, azure-cli, az-204
---

# Create Azure Storage Account

First you have to create the resource group, if missing:

```bash
az group create
    --location <myLocation>
    --name az204-blob-rg
```

Then you can create a new Storage Account within that resource group

```bash
az storage account create
    --resource-group az204-blob-rg
    --name <myStorageAcct>
    --location <myLocation>
    --sku Standard_LRS
```

This command returns all the info about the newly created storage account:

```json
{
  "accessTier": "Hot",
  "accountMigrationInProgress": null,
  "allowBlobPublicAccess": false,
  "allowCrossTenantReplication": null,
  "allowSharedKeyAccess": null,
  "allowedCopyScope": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2024-02-19T14:39:30.437545+00:00",
  "customDomain": null,
  "defaultToOAuthAuthentication": null,
  "dnsEndpointType": null,
  "enableHttpsTrafficOnly": true,
  "enableNfsV3": null,
  "encryption": {
    "encryptionIdentity": null,
    "keySource": "Microsoft.Storage",
    "keyVaultProperties": null,
    "requireInfrastructureEncryption": null,
    "services": {
      "blob": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2024-02-19T14:39:30.625055+00:00"
      },
      "file": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2024-02-19T14:39:30.625055+00:00"
      },
      "queue": null,
      "table": null
    }
  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/<subscription>/resourceGroups/az204-blob-rg/providers/Microsoft.Storage/storageAccounts/test15778",
  "identity": null,
  "immutableStorageWithVersioning": null,
  "isHnsEnabled": null,
  "isLocalUserEnabled": null,
  "isSftpEnabled": null,
  "isSkuConversionBlocked": null,
  "keyCreationTime": {
    "key1": "2024-02-19T14:39:30.500056+00:00",
    "key2": "2024-02-19T14:39:30.500056+00:00"
  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "italynorth",
  "minimumTlsVersion": "TLS1_0",
  "name": "test15778",
  "networkRuleSet": {
    "bypass": "AzureServices",
    "defaultAction": "Allow",
    "ipRules": [],
    "ipv6Rules": [],
    "resourceAccessRules": null,
    "virtualNetworkRules": []
  },
  "primaryEndpoints": {
    "blob": "https://test15778.blob.core.windows.net/",
    "dfs": "https://test15778.dfs.core.windows.net/",
    "file": "https://test15778.file.core.windows.net/",
    "internetEndpoints": null,
    "microsoftEndpoints": null,
    "queue": "https://test15778.queue.core.windows.net/",
    "table": "https://test15778.table.core.windows.net/",
    "web": "https://test15778.z38.web.core.windows.net/"
  },
  "primaryLocation": "italynorth",
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "publicNetworkAccess": null,
  "resourceGroup": "az204-blob-rg",
  "routingPreference": null,
  "sasPolicy": null,
  "secondaryEndpoints": null,
  "secondaryLocation": null,
  "sku": {
    "name": "Standard_LRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "statusOfSecondary": null,
  "storageAccountSkuConversionStatus": null,
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"
}
```
