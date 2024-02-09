---
tags: azure, cloud, azure-certifications/az204, storage, azure-blob-storage
---

# Blob Storage Tiers

To manage [[azure-blob-storage]] costs better, you have to pick the right storage tier, depending on the expected usage.

The following considerations apply to the different access tiers:

* The access tier can be set on a blob during or after upload.
* **Only the hot and cool access tiers can be set at the account level**. The archive access tier can only be set at the blob level.
* Data in the cool access tier has slightly lower availability, but still has high durability, retrieval latency, and throughput characteristics similar to hot data.
* **Data in the archive access tier is stored offline**. The archive tier offers the lowest storage costs but also the highest access costs and latency.
* **The hot and cool tiers support all [[azure-storage-redundancy-types]] options**. The archive tier supports only LRS, GRS, and RA-GRS.
* **Data storage limits are set at the account level and not per access tier**. You can choose to use all of your limit in one tier or across all three tiers.

## Hot tier

New storage accounts are created in the **hot tier by default**.

In the Hot tier, you keep your resources always available: it's **good for data that is accessed often** because it allows you to access it quickly.

**Costs are high for the storage** because you need to store the data in an optimized way, but **low for data access** because the data retrieval is optimized for reads.

Some considerations:

* can be set at account level;
* can be set at blob level, during or after the upload;

## Cool tier

Data is stored in a way that is optimal for long-term data storage but whose access is not optimized.

Costs are low for storage but high for data access.

This tier is good **for data that is accessed infrequently** and that does not change for at least 30 days.

Some considerations:

* can be set at account level;
* can be set at blob level, during or after the upload;
* has lower SLA for availability, but higher SLA for durability, latency, and thoughput.

## Cold tier

Data is stored in a way that is optimal for long-term data storage but whose access is not optimized.

This tier is good **for data that is accessed infrequently** and that does not change for at least 90 days.

Some considerations:

* can be set at account level;
* can be set at blob level, during or after the upload;
* has lower SLA for availability, but higher SLA for durability, latency, and thoughput.
  
## Archive tier

This tier is for archiving data, so its costs are **very high for data access** and **very low for data storage**.

It's good for data that does not change for at least 180 days.

Data is stored offline to reduce costs, but you will have higher costs to rehydrate and access data.

The archive tier is available only for individual [[azure-blob-storage-block-blobs]]. This tier is optimized for data that can tolerate several hours of retrieval latency.
