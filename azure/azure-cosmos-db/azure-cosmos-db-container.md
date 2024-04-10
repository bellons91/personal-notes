---
tags: azure, cloud, az-204, azure-cosmos-db
---

# Azure CosmosDB Container

An Azure Cosmos DB container is the fundamental unit of **scalability**.

You can virtually have an unlimited provisioned throughput (RU/s) and storage on a container.

Azure Cosmos DB transparently partitions your container using the logical [[partition key]] that you specify in order to elastically scale your provisioned throughput and storage. Containers are **horizontally partitioned**, and data is replicated across multiple regions.

The [[azure-cosmos-db-item]] that you add to the container are automatically grouped into logical partitions, which are distributed across physical partitions, based on the partition key. **The throughput on a container is evenly distributed across the physical partitions**.

When you create a container, you configure throughput in one of the following modes:

- **Dedicated provisioned throughput mode**: The throughput provisioned on a container is exclusively reserved for that container and it's backed by the [[SLAs]].

- **Shared provisioned throughput mode**: These containers share the provisioned throughput with the other containers in the same database (excluding containers that have been configured with dedicated provisioned throughput). In other words, the provisioned throughput on the database is shared among all the “shared throughput” containers.

**A container is a schema-agnostic container of items**. Items in a container can have arbitrary schemas.
