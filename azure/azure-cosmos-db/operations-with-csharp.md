---
tags: cosmosdb, csharp, dotnet
---

# Working on CosmosDB with .NET

You can use NuGet package *Microsoft.Azure.Cosmos* to work with CosmosDB.

## Use and consume a CosmosClient

Creates a new CosmosClient with a connection string.

**CosmosClient is thread-safe**. It's recommended to maintain a single instance of CosmosClient per lifetime of the application that enables efficient connection management and performance.

```cs
CosmosClient client = new CosmosClient(endpoint, key);
```

## Work with database

### Create a db is not exists

Only the database id is used to verify if there's an existing database.

```cs
// An object containing relevant information about the response
DatabaseResponse databaseResponse = await client.CreateDatabaseIfNotExistsAsync(databaseId, throughputInRUsPerSecond);
```

Once you have the `DatabaseResponse`, you can cast it to a `Database`

```cs
Database database = databaseResponse;
```

### Read a database by ID

You can use the reference to the DB to access the content.

```cs
DatabaseResponse readResponse = await database.ReadAsync();
```

### Delete a database

```cs
await database.DeleteAsync();
```

## Work with Container

### Create a container if not exists

Here the `partitionKey` must begin with a `/` (an example is `/LastName`).

```cs
// Set throughput to the minimum value of 400 RU/s
ContainerResponse simpleContainer = await database.CreateContainerIfNotExistsAsync(
    id: containerId,
    partitionKeyPath: partitionKey,
    throughput: 400);
```

### Get a container by id

```cs
Container container = database.GetContainer(containerId);
ContainerProperties containerProperties = await container.ReadContainerAsync();
```

### Delete a container

```cs
await database.GetContainer(containerId).DeleteContainerAsync();
```

## Work with items

### Create an item

```cs
ItemResponse<SalesOrder> response = await container.CreateItemAsync(salesOrder, new PartitionKey(salesOrder.AccountNumber));
```

### Read an item

The method requires type to serialize the item to along with an id property, and a partitionKey.

```cs
string id = "[id]";
string accountNumber = "[partition-key]";
ItemResponse<SalesOrder> response = await container.ReadItemAsync(id, new PartitionKey(accountNumber));
```

### Query an item

The Container.GetItemQueryIterator method creates a query for items under a container in an Azure Cosmos database using a SQL statement with parameterized values. It returns a FeedIterator.

```cs
QueryDefinition query = new QueryDefinition(
    "select * from sales s where s.AccountNumber = @AccountInput ")
    .WithParameter("@AccountInput", "Account1");

FeedIterator<SalesOrder> resultSet = container.GetItemQueryIterator<SalesOrder>(
    query,
    requestOptions: new QueryRequestOptions()
    {
        PartitionKey = new PartitionKey("Account1"),
        MaxItemCount = 1
    });
```

## Work with stored procedures

Before using a stored procedure, you have to register it. A stored procedure is strictly related to a collection.

### Register a stored procedure

```cs
string storedProcedureId = "spCreateToDoItems";
StoredProcedureResponse storedProcedureResponse = await client
    .GetContainer("myDatabase", "myContainer")
    .Scripts
    .CreateStoredProcedureAsync(new StoredProcedureProperties
    {
        Id = storedProcedureId,
        Body = File.ReadAllText($@"..\js\{storedProcedureId}.js")
    });
```

### Execute a stored procedure

```cs
dynamic[] newItems = new dynamic[]
{
    new {
        category = "Personal",
        name = "Groceries",
        description = "Pick up strawberries",
        isComplete = false
    },
    new {
        category = "Personal",
        name = "Doctor",
        description = "Make appointment for check up",
        isComplete = false
    }
};

var result = await client
.GetContainer("database", "container")
.Scripts.ExecuteStoredProcedureAsync<string>(
    "spCreateToDoItem", 
    new PartitionKey("Personal"), new[] { newItems }
    );
```
