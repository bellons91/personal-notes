---
tags: azure, cloud, az-204, serverless, azure-functions, azure-logic-apps
---

# Azure Functions vs WebJobs

Both [[azure-functions]] and [[Azure App Service WebJobs]] are built on top of [[azure-app-service]].

They both support integrations with [[application-insights]].

**Azure Functions is built on the WebJobs SDK**, so it shares many of the same event triggers and connections to other Azure services.

Azure Functions offers more developer productivity than Azure App Service WebJobs does. It also offers more options for programming languages, development environments, Azure service integration, and pricing.

|                                             | Functions                                                                                                                                                     | WebJobs with WebJobs SDK                                                                                                   |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Serverless app model with automatic scaling | Yes                                                                                                                                                           | No                                                                                                                         |
| Develop and test in browser                 | Yes                                                                                                                                                           | No                                                                                                                         |
| Pay-per-use pricing                         | Yes                                                                                                                                                           | No                                                                                                                         |
| Integration with Logic Apps                 | Yes                                                                                                                                                           | No                                                                                                                         |
| Trigger events                              | Timer, Azure Storage queues and blobs, Azure Service Bus queues and topics, Azure Cosmos DB, Azure Event Hubs, HTTP/WebHook (GitHub, Slack), Azure Event Grid | Timer, Azure Storage queues and blobs, Azure Service Bus queues and topics, Azure Cosmos DB, Azure Event Hubs, File system |
