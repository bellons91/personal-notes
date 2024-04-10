---
tags: azure, cloud, az-204, azure-cosmos-db
---

# Azure Cosmos DB Pre-triggers and Post-triggers

Azure Cosmos DB supports pretriggers and post-triggers.

Triggers aren't automatically executed, **they must be specified for each database operation where you want them to execute**.

After you define a trigger, you should register it by using the Azure Cosmos DB SDKs.

## Pre-triggers

Pretriggers are executed before modifying a database item. **Pretriggers can't have any input parameters**.

Here's an example of pre-trigger that manipulates the request message associated with the operation.

```js
function validateToDoItemTimestamp() {
  var context = getContext();
  var request = context.getRequest();

  // item to be created in the current operation
  var itemToCreate = request.getBody();

  // validate properties
  if (!("timestamp" in itemToCreate)) {
    var ts = new Date();
    itemToCreate["timestamp"] = ts.getTime();
  }

  // update the item that will be created
  request.setBody(itemToCreate);
}
```

When triggers are registered, you can specify the operations that it can run with. For example, you can define that a trigger runs only before the creation of an element, and not during the update.

So, you first have to register the trigger:

```cs
await client
  .GetContainer("database", "container")
  .Scripts
  .CreateTriggerAsync(new TriggerProperties
  {
      Id = "trgPreValidateToDoItemTimestamp",
      Body = File.ReadAllText("@..\js\trgPreValidateToDoItemTimestamp.js"),
      TriggerOperation = TriggerOperation.Create,
      TriggerType = TriggerType.Pre
  });
```

Then, every time you execute an operation, you have to list the triggers to execute by specifying the ID.

```cs
dynamic newItem = new
{
    category = "Personal",
    name = "Groceries",
    description = "Pick up strawberries",
    isComplete = false
};

await client
  .GetContainer("database", "container")
  .CreateItemAsync(newItem, null, new ItemRequestOptions
  {
    PreTriggers = new List<string> { "trgPreValidateToDoItemTimestamp" }
  });
```

## Post-triggers

Post-triggers are executed after modifying a database item.

The following trigger queries for the metadata item and updates it with details about the newly created item.

```js
function updateMetadata() {
  var context = getContext();
  var container = context.getCollection();
  var response = context.getResponse();

  // item that was created
  var createdItem = response.getBody();

  // query for metadata document
  var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
  var accept = container.queryDocuments(
    container.getSelfLink(),
    filterQuery,
    updateMetadataCallback
  );

  if (!accept) throw "Unable to update metadata, abort";

  function updateMetadataCallback(err, items, responseOptions) {
    if (err) throw new Error("Error" + err.message);

    if (items.length != 1) throw "Unable to find metadata document";

    var metadataItem = items[0];

    // update metadata
    metadataItem.createdItems += 1;
    metadataItem.createdNames += " " + createdItem.id;
    var accept = container.replaceDocument(
      metadataItem._self,
      metadataItem,
      function (err, itemReplaced) {
        if (err) throw "Unable to update metadata, abort";
      }
    );

    if (!accept) throw "Unable to update metadata, abort";

    return;
  }
}
```

The post-trigger runs as part of the same transaction for the underlying item itself. **An exception during the post-trigger execution fails the whole transaction**. Anything committed is rolled back and an exception returned.

You have to register the trigger using the SDK:

```cs
await client
      .GetContainer("database", "container")
      .Scripts
      .CreateTriggerAsync(new TriggerProperties
      {
          Id = "trgPostUpdateMetadata",
          Body = File.ReadAllText(@"..\js\trgPostUpdateMetadata.js"),
          TriggerOperation = TriggerOperation.Create,
          TriggerType = TriggerType.Post
      });
```

Then you must specify the triggers to use when creating (or operating on) items.

```cs
var newItem = {
    name: "artist_profile_1023",
    artist: "The Band",
    albums: ["Hellujah", "Rotators", "Spinning Top"]
};

await client
      .GetContainer("database", "container")
      .CreateItemAsync(newItem, null,
      new ItemRequestOptions
      {
        PostTriggers = new List<string> { "trgPostUpdateMetadata" }
      });
```
