---
tags: azure, cloud, azure-certifications/az204, storage, azure-blob-storage
---

# Azure Blob Storage lifecycle

Early in the lifecycle, people access some data often. But the need for access drops drastically as the data ages. Some data stays idle in the cloud and is rarely accessed once stored. Some data expires days or months after creation, while other data sets are actively read and modified throughout their lifetimes.

Each blob "belongs" to a specific [[azure-blob-storage-tiers]].

However, you can define **lifecycle management policies** to handle the status of a blob. With these policies you can:

* Transition blobs to a **cooler** storage tier (hot to cool, hot to archive, or cool to archive) to optimize for performance and cost;
* Delete blobs at the end of their lifecycles;
* Define rules to be run once per day at the storage account level;
* Apply rules to containers or a subset of blobs (using prefixes as filters);

By adjusting storage tiers in respect to the age of data, you can design the **least expensive storage options** for your needs. To achieve this transition, lifecycle management policy rules are available to move aging data to cooler tiers.

❗Important note: **Data stored in a premium block blob storage account cannot be tiered to Hot, Cool, or Archive using Set Blob Tier or using Azure Blob Storage lifecycle management**. To move data, you must synchronously copy blobs from the block blob storage account to the Hot tier in a different account using the Put Block From URL API or a version of AzCopy that supports this API. The Put Block From URL API synchronously copies data on the server, meaning the call completes only once all the data is moved from the original server location to the destination location. ❗

## Lifecycle Management Policy

A lifecycle management policy is a **collection of rules in a JSON document**.

You can also define such policies using the UI.

Each rule definition within a policy includes a filter set and an action set.

The *filter set* limits rule actions to a certain set of objects within a container or objects names. **Filters are evaluated with logical AND**.

The *action set* applies the tier or delete actions to the filtered set of objects

```json
{
  "rules": [
    {
      "name": "ruleFoo",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": [ "blockBlob" ],
          "prefixMatch": [ "container1/foo" ]
        },
        "actions": {
          "baseBlob": {
            "tierToCool": { "daysAfterModificationGreaterThan": 30 },
            "tierToArchive": { "daysAfterModificationGreaterThan": 90 },
            "delete": { "daysAfterModificationGreaterThan": 2555 }
          },
          "snapshot": {
            "delete": { "daysAfterCreationGreaterThan": 90 }
          }
        }
      }
    }
  ]
}
```

| property name | description | required |
|--|--|--|
| rules | Array of rule objects. Up to 100 rules in a policy. | true |
| rules.name | name of the rule | true |
| rules.enabled | true by default | false |
| rules.type | Lifecycle is the only accepted value | true |
| rules.definition | Each definition is made up of one filter set and one action set | true |
| rules.definition.filters.blobTypes | An array of predefined enum values. | true |
| rules.definition.filters.prefixMatch | An array of strings for prefixes to be match. Each rule can define up to 10 prefixes. A prefix string must start with a container name. | false |
| rules.definition.filters.blobIndexMatch | An array of dictionary values consisting of blob index tag key and value conditions to be matched. Each rule can define up to 10 blob index tag condition. | false |

There are several possible actions:

| action name | available for block blob | available for append blob | available for snapshots|
|--|--|--|--|
| tierToCool | ✅ | ❌ | ✅ |
| enableAutoTierToHotFromCool | ✅ | ❌ | ❌ |
| tierToArchive | ✅ | ❌ | ✅ |
| delete | ✅ | ✅ | ✅ |

Each action runs based on the age of the last action to the blob.

| run condition | description |
|--|--|
| `daysAfterModificationGreaterThan` | The condition for base blob actions |
| `daysAfterCreationGreaterThan` | The condition for blob snapshot actions |
| `daysAfterLastAccessTimeGreaterThan` | The condition for a current version of a blob *when access tracking is enabled* |
| `daysAfterLastTierChangeGreaterThan` | This condition **applies only to tierToArchive actions** and can be used only with the `daysAfterModificationGreaterThan` condition. |
