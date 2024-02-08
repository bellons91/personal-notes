---
tags: azure, cloud, azure-certifications/az900 storage
---

# Azure Storage Account

Cloud storage solution. It's an entry point to access data over HTTP or HTTPS.

Using storage accounts, data is secure, highly available, durable, and scalable.

## Blobs

The storage service offers three types of blobs: [[azure-blob-storage-block-blobs]], [[azure-blob-storage-append-blobs]], and [[azure-blob-storage-page-blobs]]. You specify the blob type when you create the blob. Once the blob has been created, its type cannot be changed.

All blobs reflect committed changes immediately. Each version of the blob has a unique tag, called an **ETag**, that you can use with access conditions to assure you only change a specific instance of the blob.

Any blob can be **leased for exclusive write access**. When a blob is leased, only calls that include the current lease ID can modify the blob or (for block blobs) its blocks.

## Storage Account Tiers

There are several tiers, each of them with specific usage and supported services.

### Standard general-purpose v2

It's the type best for blobs, file shares, queues, and tables.

Recommended for the most basic scenarios.

Supported services:

- [[azure-blob-storage]]
- [[azure-queue-storage]]
- [[azure-table-storage]]
- [[azure-files]]

It supports all the redundancy options:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])
- Geo-Redundant Storage (GRS) (see: [[azure-storage-redundancy-types#Geo-Redundant Storage (GRS)]])
- Read-Access Geo-Redundant Storage (RA-GRS) (see: [[azure-storage-redundancy-types#Read-Access Geo-Redundant Storage (RA-GRS)]])
- Geo-Zone-Redundant Storage (GZRS) (see:[[azure-storage-redundancy-types#Geo-Zone-Redundant Storage (GZRS)]])
- Read-Access Geo-Zone-Redundant Storage (RA-GZRS) (see: [[azure-storage-redundancy-types#Read-Access Geo-Zone-Redundant Storage (RA-GZRS)]])

### Premium block blobs

Premium storage for [[azure-blob-storage-block-blobs]] and [[azure-blob-storage-append-blobs]].

Recommended for scenarios with **high transaction rates** or that use smaller objects or require consistently low storage latency.

It is available only for [[azure-blob-storage]].

It supports:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])

### Premium file shares

For file shares only.

Recommended for enterprise or high-performance scale applications.

Is available only for [[azure-files]].

It supports:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])

### Premium page blobs

For [[azure-blob-storage-page-blobs]] only.

It supports only Locally Redundant Storage (LRS)
