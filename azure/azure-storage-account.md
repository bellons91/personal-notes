---
tags: azure, cloud, azure-certifications/az900 storage
---

# Azure Storage Account

Cloud storage solution. It's an entry point to access data over HTTP or HTTPS.

Using storage accounts, data is secure, highly available, durable, and scalable.

There are several tiers, each of them with specific usage and supported services.

## Standard general-purpose v2

It's the type best for blobs, file shares, queues, and tables.

Recommended for the most basic scenarios.

Supported services:

- [[azure-blob-storage]]
- [[azure-queue-storage]]
- [[azure-table-storage]]
- [[azure-files]]

It supports all the redundancy options:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Geo-Redundant Storage (GRS) (see: [[azure-storage-redundancy-types#Geo-Redundant Storage (GRS)]])
- Read-Access Geo-Redundant Storage (RA-GRS) (see: [[azure-storage-redundancy-types#Read-Access Geo-Redundant Storage (RA-GRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])
- Geo-Zone-Redundant Storage (GZRS) (see:[[azure-storage-redundancy-types#Geo-Zone-Redundant Storage (GZRS)]])
- Read-Access Geo-Zone-Redundant Storage (RA-GZRS) (see: [[azure-storage-redundancy-types#Read-Access Geo-Zone-Redundant Storage (RA-GZRS)]])

## Premium block blobs

Premium storage for [[block blobs]] and [[append blobs]].

Recommended for scenarios with **high transaction rates** or that use smaller objects or require consistently low storage latency.

It is available only for [[azure-blob-storage]].

It supports:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])

## Premium file shares

For file shares only.

Recommended for enterprise or high-performance scale applications.

Is available only for [[azure-files]].

It supports:

- Locally Redundant Storage (LRS) (see :[[azure-storage-redundancy-types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[azure-storage-redundancy-types#Zone-Redundant Storage (ZRS)]])

## Premium page blobs

For [[page blobs]] only.

It supports only Locally Redundant Storage (LRS)
