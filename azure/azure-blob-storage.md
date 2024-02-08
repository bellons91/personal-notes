---
tags: azure, cloud, azure-certifications/az900, azure-certifications/az204, storage, azure-blob-storage
---

# Azure Blob Storage

Azure Blob Storage is a generic storage solution. You can store **text and binary data** in an unstructured format.

Blob storage can manage thousands of simultaneous uploads.

Blob storage is ideal for:

* Serving images or documents directly to a browser.
* Storing files for distributed access.
* Streaming video and audio.
* Storing data for backup and restore, disaster recovery, and archiving.
* Storing data for analysis by an on-premises or Azure-hosted service.

Objects can be accessed via HTTP or HTTPS, given that every object can be referenced using a specific URL.

**An [[azure-storage-account]] is the top-level container** for all of your Azure Blob storage. The storage account provides a unique namespace for your Azure Storage data.

This service provides a list of endpoints available at  https://{storage-account-name}.blob.core.windows.net

Each Storage Account contains one or more [[azure-blob-container]], and each Blob Container contains

## Blob Storage tiers

To manage costs better you have to pick the right storage tier, depending on the expected usage.

### Hot tier

New storage accounts are created in the **hot tier by default**.

In the Hot tier, you keep your resources always available: it's **good for data that is accessed often** because it allows you to access it quickly.

**Costs are high for the storage** because you need to store the data in an optimized way, but **low for data access** because the data retrieval is optimized for reads.

Some considerations:

* can be set at account level;
* can be set at blob level, during or after the upload;

### Cool tier

Data is stored in a way that is optimal for long-term data storage but whose access is not optimized.

Costs are low for storage but high for data access.

This tier is good **for data that is accessed infrequently** and that does not change for at least 30 days.

Some considerations:

* can be set at account level;
* can be set at blob level, during or after the upload;
* has lower SLA for availability, but higher SLA for durability, latency, and thoughput.

### Cold tier

Data is stored in a way that is optimal for long-term data storage but whose access is not optimized.

This tier is good **for data that is accessed infrequently** and that does not change for at least 90 days.

Some considerations:

* can be set at account level;
* can be set at blob level, during or after the upload;
* has lower SLA for availability, but higher SLA for durability, latency, and thoughput.
  
### Archive tier

This tier is for archiving data, so its costs are **very high for data access** and **very low for data storage**.

It's good for data that does not change for at least 180 days.

Data is stored offline to reduce costs, but you will have higher costs to rehydrate and access data.

The archive tier is available only for individual [[azure-blob-storage-block-blobs]]. This tier is optimized for data that can tolerate several hours of retrieval latency.

## Security

All data (including metadata) written to Azure Storage is **automatically encrypted using Storage Service Encryption (SSE)**.
