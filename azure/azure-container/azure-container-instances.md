---
tags: az-204, azure, containers, aci, docker, az-900, paas
---

# Azure Container Instances (ACI)

ACI is a solution for any scenario that can operate in **isolated containers**, including simple applications, task automation, and build jobs.

You don't have to manage VMs.

Azure Container Instances is a [[paas]] service.

You can upload your single containers and have them run in the cloud in a single _pod_.

Concepts like scaling, load balancing, and certificates are _not_ provided with ACI containers. For example, to scale to five container instances, you create five distinct container instances.

If you need a more complex orchestrators, you should use [[azure-kubernetes-service]].

You can deploy ACI by using [[arm-templates]] (best suited for complex scenarios) or a YAML file (when you just have one container instance).

## Benefits of ACI

**Fast startup**: ACI can start containers in Azure in seconds, without the need to provision and manage VMs

**Container access**: ACI enables exposing your [[aci-container-group]] directly to the internet with an IP address and a fully qualified domain name ([[FQDN]])

**Hypervisor-level security**: Isolate your application as completely as it would be in a VM.

**Customer data**: The ACI service stores the minimum customer data required to ensure your container groups are running as expected.

**Custom sizes**: ACI provides optimum utilization by **allowing exact specifications of CPU cores and memory**.

**Persistent storage**: Mount **Azure Files shares** directly to a container to retrieve and persist state.

**Linux and Windows**: Schedule both Windows and Linux containers using the same API.
