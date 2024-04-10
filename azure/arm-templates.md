---
tags: azure, cloud, az-900
---

# ARM Templates

JSON templates that allow to use [[azure-resource-manager]] to define and manage resources.

It has some benefits:

- **Declarative syntax**: you declare what you want to deploy but don’t need to write the actual programming commands and sequence to deploy the resources.
- **Repeatable results**: Repeatedly deploy your infrastructure throughout the development lifecycle and have confidence your resources are deployed in a consistent manner. You can use the same ARM template to **deploy multiple dev/test environments**, knowing that all the environments are the same.
- **Orchestration**: Azure Resource Manager orchestrates the deployment of interdependent resources. When possible, Azure Resource Manager deploys resources in parallel.
- **Modular files**: You can break your templates into smaller, **reusable components** and link them together at deployment time. You can also nest one template inside another template.
- **Extensibility**: With deployment scripts, you can **add PowerShell or Bash scripts** to your templates.
