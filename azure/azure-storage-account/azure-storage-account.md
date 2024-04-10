---
tags: azure, cloud, az-900, az-204, storage
---

# Azure Storage Account

Cloud storage solution, **IaaS**. It's an entry point to access data over HTTP or HTTPS.

Using storage accounts, data is secure, highly available, durable, and scalable.

You can even use Azure Storage publish static content (see [[static-website-hosting-with-azure-storage]]).

You can use it to create a Virtual Machine with consistent disks and storage.

You create a Storage Account in a specific region (to enable redundancy).

Azure Storage Account allows you to use:

- [[azure-file-storage]]
- [[azure-blob-storage]]
- [[azure-table-storage]]
- [[azure-queue-storage]]

You can also use [[hierarchical-namespaces]].

## Storage Account Tiers

There are several tiers, each of them with specific usage and supported services.

### Standard general-purpose v2

It's the type best for blobs, file shares, queues, and tables.

Recommended for the most basic scenarios.

Supported services:

- [[azure-blob-storage]]
- [[azure-queue-storage]]
- [[azure-table-storage]]
- [[azure-file-storage]]

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

Is available only for [[azure-file-storage]].

It supports:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])

### Premium page blobs

For [[azure-blob-storage-page-blobs]] only.

It supports only Locally Redundant Storage (LRS)
