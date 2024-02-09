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
