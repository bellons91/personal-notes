---
tags: azure, azure-certifications/az900, cost-optimization, azure-blob-storage
---

# Costs optimizations on Azure Blob Storage

In [[Azure Blob Storage]], you can use different storage tiers:

## Hot tier

In the Hot tier, you keep your resources always available: it's **good for data that is accessed often** because it allows you to access it quickly.

**Costs are high for the storage** because you need to store the data in an optimized way, but **low for data access** because the data retrieval is optimized for reads.

## Cool tier

Data is stored in a way that is optimal for long-term data storage but whose access is not optimized.

Costs are low for storage but high for data access.

This tier is good **for data that is accessed infrequently** and that does not change for at least 30 days.

## Archive tier

This tier is for archiving data, so its costs are **very high for data access** and **very low for data storage**.

It's good for data that does not change for at least 180 days.
