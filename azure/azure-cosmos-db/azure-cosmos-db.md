---
tags: azure, cloud, azure-certifications/az204, azure-cosmos-db
---

# Azure Cosmos DB

Azure Cosmos DB is a **fully managed NoSQL database** designed to provide low latency, elastic scalability of throughput, well-defined semantics for data consistency, and high availability.

You can configure your databases to be globally distributed and available in any of the [[azure-region]]. To lower the latency, place the data close to where your users are.

It uses **multi-master replication protocol**, meaning that all regions support both reads and writes. Multi-master replication protocol provides some functionalities:

- Unlimited elastic write and read scalability.
- 99.999% read and write availability all around the world.
- Guaranteed reads and writes served in less than 10 milliseconds at the 99th [[percentile]].

However, you can configure it to have only one region enabled for writing.

Your application can perform near **real-time reads and writes against all the regions** you chose for your database. Azure Cosmos DB internally handles the data replication between regions with consistency level guarantees of the level you've selected.

To use CosmoDB you have to create a [[azure-cosmos-db-account]]. Every account can have one or more [[azure-cosmos-db-database]], each containing one or more [[azure-cosmos-db-container]]. Each container then is a collection of [[azure-cosmos-db-item]].

![CosmosDB Hierarcy](./cosmosdb-resources-hierarchy.png)

For each account you can define its [[azure-cosmos-db-consistency-levels]].
