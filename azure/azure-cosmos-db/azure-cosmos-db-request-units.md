---
tags: azure, cloud, azure-certifications/az204, azure-cosmos-db
---

# Azure CosmosDB Request Units

 A request unit represents the system resources such as [[CPU]], [[IOPS]], and memory that are required to perform the database operations supported by Azure Cosmos DB.

The cost to do a point read, which is fetching a single item by its ID *and* partition key value, for a 1-KB item is 1RU.

The type of Azure Cosmos DB account you're using determines the way consumed RUs get charged. There are three modes in which you can create an account:

- **Provisioned throughput mode**: you provision the number of RUs for your application on a per-second basis in increments of **100 RUs per second**. To scale the provisioned throughput for your application, you can increase or decrease the number of RUs at any time in increments or decrements of 100 RUs. **You can provision throughput at container and database** granularity level.
- **Serverless mode**: you don't have to provision any throughput when creating resources in your Azure Cosmos DB account. At the end of your billing period, you get billed for the number of request units that have been consumed by your database operations.
- **Autoscale mode**: ou can automatically and instantly scale the throughput (RU/s) of your database or container based on its usage.
