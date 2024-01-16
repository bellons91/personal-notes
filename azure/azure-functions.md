---
tags: azure, cloud, azure-certifications/az900 serverless, paas, azure-certifications/az204, azure-functions
---

# Azure Functions

Azure Functions is an **event-driven**, **serverless** compute option that doesn’t require maintaining virtual machines or containers.

With Azure Functions, an event wakes the function, alleviating the need to keep resources provisioned when there are no events.

Since the function runs only after an event is triggered and then all the resources are deallocated, you only **pay for the CPU time** used by the function.

Azure Functions supports **triggers**, which are ways to start execution of your code, and **bindings**, which are ways to simplify coding for input and output data.

## Functions timeout

The `functionTimeout` property in the `host.json` project file specifies the timeout duration for functions in a function app. This property applies specifically to function executions. After the trigger starts function execution, the function needs to return/respond within the timeout duration.

## Required storage account

On any plan, a function app requires a general [[azure-storage-account]], which supports Azure Blob, Queue, Files, and Table storage. This is because **Functions rely on Azure Storage for operations such as managing triggers and logging function executions**, but some storage accounts don't support queues and tables.

The same storage account used by your function app can also be used by your triggers and bindings to store your application data. However, for storage-intensive operations, you should use a separate storage account.

## Hosting plans

| Plan  | Benefits | Available on  |Scale out| Max # of instances | Function app timeout (minutes) |
|--|--|--|--|--|--|
|Consumption plan|It scales automatically and **you only pay for compute resources when your functions are running**. **Instances of the Functions host are dynamically added and removed** based on the number of incoming events.| Windows, Linux| **Event driven**. Scale out automatically, even during periods of high load. Azure Functions infrastructure **scales CPU and memory resources by adding more instances of the Functions host**, based on the number of incoming trigger events. |Windows: 200. Linux: 100. This is the max instances give on a **per-function app** basis.| 5 (default) to 10 (max)|
|Premium plan | Automatically scales based on demand using **pre-warmed workers**, which run applications with no delay after being idle, runs on more powerful instances, and **connects to virtual networks**.| Windows, Linux| Event driven|Windows: 100. Linux: 20-100 Per-plan basis. | 30 (default) to unlimited|
|Dedicated plan|Run your functions within an App Service plan at regular App Service plan rates. Best **for long-running scenarios** where Durable Functions can't be used.|Windows, Linux|Manual/autoscale | 10-20|30 (default) to unlimited|
| ASE | [[App Service Environment]] (ASE) is an App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale. | | Manual/autoscale| 100|
|Kubernetes |Fully isolated and dedicated environment running on top of the Kubernetes platform.| Direct or with [[azure-arc]]|Event-driven autoscale for Kubernetes clusters using KEDA. |Varies by cluster|

## Use cases

* you don't care about the underlying infrastructure;
* you have to respond to an event;
* the work will take not more that a few seconds;
* you need **automatic scalability**;
