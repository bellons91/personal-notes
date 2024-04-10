---
tags: azure, cloud, az-204, azure-cosmos-db
---

# Azure Cosmos DB User-defined functions

User-defined function can be used inside a query.

```js
function tax(income) {
  if (income == undefined) throw "no input";
  if (income < 1000) return income * 0.1;
  else if (income < 10000) return income * 0.2;
  else return income * 0.4;
}
```

You have to register it using the SDK:

```cs
await client
  .GetContainer("database", "container")
  .Scripts
  .CreateUserDefinedFunctionAsync(new UserDefinedFunctionProperties
  {
      Id = "Tax",
      Body = File.ReadAllText(@"..\js\Tax.js")
  });
```

and then you can use it:

```cs
var iterator = client
.GetContainer("database", "container")
.GetItemQueryIterator<dynamic>("SELECT * FROM Incomes t WHERE udf.Tax(t.income) > 20000");

while (iterator.HasMoreResults)
{
    var results = await iterator.ReadNextAsync();
    foreach (var result in results)
    {
        //iterate over results
    }
}
```
