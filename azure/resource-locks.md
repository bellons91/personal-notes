---
tags: azure, cloud, azure-certifications/az900, governance
---

# Resource locks

A resource lock prevents resources from being accidentally deleted or changed (depending on the type of lock).

Resource locks can be inherited.

There are two types of Resource locks:

- **Delete**: authorized users can read and update a resource, but they cannot delete it;
- **ReadOnly**: users can read a resource, but they cannot delete or update it.

Resource locks can be applied using the Azure portal, PowerShell, Azure CLI, or via [[Azure Resource Manager templates]].
