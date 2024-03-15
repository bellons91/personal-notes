---
tags: azure, cloud, azure-certifications/az204, azure-cosmos-db
---

# Azure Cosmos DB Stored Procedures

**Stored procedures are registered per collection**, and can operate on any document or an attachment present in that collection.

**Stored procedures are written using JavaScript**. They can create, update, read, query, and delete items within an Azure Cosmos DB container.

For partitioned containers, when you run a stored procedure, you must provide a partition key value in the request options. **Stored procedures are always scoped to a partition key**. Items that have a different partition key value aren't visible to the stored procedure.

Here's a stored procedure that just returns a Hello World response.

```js
var helloWorldStoredProc = {
  id: "helloWorld",
  serverScript: function () {
    var context = getContext();
    var response = context.getResponse();

    response.setBody("Hello, World");
  },
};
```

The context object provides access to all operations that can be performed in Azure Cosmos DB, and access to the request and response objects. In this case, you use the response object to set the body of the response to be sent back to the client.

When you create an item by using a stored procedure, the item is inserted into the Azure Cosmos DB container and **an ID for the newly created item is returned**.

Creating an item is an asynchronous operation and depends on the JavaScript callback functions. **The callback function has two parameters**: one for the error object in case the operation fails, and another for a return value, in this case, the created object. Inside the callback, you can either handle the exception or throw an error. If a callback isn't provided and there's an error, the Azure Cosmos DB runtime throws an error.

The stored procedure also includes a parameter to set the description as a boolean value. When the parameter is set to `true` and the description is missing, the stored procedure throws an exception. Otherwise, the rest of the stored procedure continues to run.

This stored procedure takes as input `documentToCreate`, the body of a document to be created in the current collection. All such operations are asynchronous and depend on JavaScript function callbacks.

```js
var createDocumentStoredProc = {
  id: "createMyDocument",
  body: function createMyDocument(documentToCreate) {
    var context = getContext();
    var collection = context.getCollection();
    var accepted = collection.createDocument(
      collection.getSelfLink(),
      documentToCreate,
      function (err, documentCreated) {
        if (err) throw new Error("Error" + err.message);
        context.getResponse().setBody(documentCreated.id);
      }
    );
    if (!accepted) return;
  },
};
```

When defining a stored procedure in the Azure portal, **input parameters are always sent as a string to the stored procedure**. Even if you pass an array of strings as an input, the array is converted to string and sent to the stored procedure.

All Azure Cosmos DB operations must complete within a limited amount of time. **Stored procedures have a limited amount of time to run on the server**. All collection functions return a Boolean value that represents whether that operation completes or not.

You can implement **transactions** on items within a container by using a stored procedure. JavaScript functions can implement a [[continuation-based model]] to batch or resume execution. The continuation value can be any value of your choice and your applications can then use this value to resume a transaction from a new starting point.

[[transaction continuation]]
