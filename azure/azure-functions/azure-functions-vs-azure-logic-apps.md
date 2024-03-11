---
tags: azure, cloud, azure-certifications/az204, serverless, azure-functions, azure-logic-apps
---

# Azure Functions vs Azure Logic apps

Both [[azure-functions]] and [[azure-logic-apps]] are Azure Services that enable serverless workloads.

Azure Functions is a serverless **compute service**, whereas Azure Logic Apps is a serverless **workflow integration platform**.

Both can create complex **orchestrations**. For Azure Functions you develop orchestrations by writing code that use the [[azure-durable-functions]] extension.

For Logic Apps, you use the GUI or edit the configuration files to orchestrate Actions.

|                   | Azure Functions                                                       | Logic Apps                                                                                             |
| ----------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Development       | Code-first (imperative)                                               | Designer-first (declarative)                                                                           |
| Connectivity      | About a dozen built-in binding types, write code for custom bindings  | Large collection of connectors, Enterprise Integration Pack for B2B scenarios, build custom connectors |
| Actions           | Each activity is an Azure function; write code for activity functions | Large collection of ready-made actions                                                                 |
| Monitoring        | Azure Application Insights                                            | Azure portal, Azure Monitor logs                                                                       |
| Management        | REST API, Visual Studio                                               | Azure portal, REST API, PowerShell, Visual Studio                                                      |
| Execution context | Runs in Azure, or locally                                             | Runs in Azure, locally, or on premises                                                                 |
