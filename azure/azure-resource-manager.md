---
tags: azure, cloud, azure-certifications/az900, infrastructure
---

# ARM (Azure Resource Manager)

Azure Resource Manager (ARM) is the deployment and management service for Azure.

When a user sends a request from any Azure tools, APIs, or SDKs, ARM receives the request. ARM authenticates and authorizes the request. Then, ARM sends the request to the Azure service, which takes the requested action.

With Azure Resource Manager, you can:

- Manage your infrastructure through **declarative templates** rather than scripts.
- Deploy, manage, and monitor all the resources for your solution as a group rather than handling these resources individually.
- Re-deploy your solution throughout the development life-cycle and have confidence your resources are deployed in a **consistent state**.
- **Define the dependencies between resources**, so they're deployed in the correct order.
- Apply access control to all services because RBAC is natively integrated into the management platform.
- Apply tags to resources to organize all the resources in your subscription logically.
- Clarify your organization's billing by viewing costs for a group of resources with the same tag.
- Orchestrates the creation of those resources in parallel.

You can define the infrastructure using [[arm-templates]] or [[bicep]].
