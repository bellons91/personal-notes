---
tags: azure, cloud, azure-certifications/az900 serverless, paas
---

# Azure Functions

Azure Functions is an **event-driven**, **serverless** compute option that doesn’t require maintaining virtual machines or containers.

With Azure Functions, an event wakes the function, alleviating the need to keep resources provisioned when there are no events.

Since the function runs only after an event is triggered and then all the resources are deallocated, you only **pay for the CPU time** used by the function.

## Use cases

* you don't care about the underlying infrastructure;
* you have tor espond to an event;
* the work will take not more that a few seconds;
* you need **automatic scalability**;
  