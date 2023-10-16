---
tags: azure, cloud, azure-certifications/az204, linux
---

# Azure App Service on Linux

You can choose to host a web app on Linux for supported application stacks.

You can run *custom* Linux containers using **Web App for Containers**.

Natively, App Service on Linux supports several frameworks, such as:

- .NET
- NodeJs
- Java
- Go
- Python
- PHP
- Ruby

If a framework is missing, you can deploy a custom container.

To see which are the supported versions, you can run this command:

[[azure-app-service-scripts#List the available runtimes]]

## Known Limitations

App Service on Linux **isn't supported on Shared pricing tier**.

When deployed to built-in images, your code and content are allocated a storage volume for web content, backed by Azure Storage. *The disk latency of this volume is higher* and more variable than the latency of the container filesystem. Apps that require heavy read-only access to content files may benefit from the custom container option, which places files in the container filesystem instead of on the content volume.
