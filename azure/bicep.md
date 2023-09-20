---
tags: azure, cloud, azure-certifications/az900
---

# Bicep

It's a language that uses declarative syntax simpler than the JSON structure used by [[arm-templates]].

Bicep files define both the infrastructure and configuration.

Some benefits:

- **Support for all resource types and API versions**: Bicep immediately supports all preview and GA versions for Azure services.
- **Simple syntax**: Compared to the equivalent JSON template, Bicep files are more concise and easier to read.
- **Repeatable results**: Bicep files are idempotent, which means you can deploy the same file many times and get the same resource types in the same state. You can develop one file that represents the desired state rather than developing lots of separate files to represent updates.
- **Orchestration**: Resource Manager orchestrates the deployment of interdependent resources so they're created in the correct order. When possible, Resource Manager deploys resources in parallel.
- **Modularity**: You can break your Bicep code into manageable parts by using **modules**. The module deploys a set of related resources. Modules enable you to reuse code and simplify development. Add the module to a Bicep file anytime you need to deploy those resources.
