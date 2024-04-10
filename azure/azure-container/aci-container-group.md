---
tags: az-204, azure, containers, aci, docker, az-900, paas
---

# Azure Container Instances Container Group

It's the top-level resource in [[azure-container-instances]].

A container group is a collection of containers that get scheduled on the same host machine.

**The containers in a container group share a lifecycle, resources, local network, and storage volumes**. It's similar in concept to a [[pod]] in [[Kubernetes]].

![A container group that includes multiple containers](https://learn.microsoft.com/en-us/training/wwl-azure/create-run-container-images-azure-container-instances/media/container-groups-example.png)

**Multi-container groups currently support only Linux containers**. For Windows containers, Azure Container Instances only supports deployment of a single instance.

Multi-container groups are useful in cases where you want to divide a single functional task into a few container images. These images might be delivered by different teams and have separate resource requirements.

Common scenarios for multi-container groups are:

- A container serving a web application and a container pulling the latest content from source control.
- An application container and a _logging_ container. The logging container collects the logs and metrics output by the main application and writes them to long-term storage.
- An application container and a _monitoring_ container. The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly, and raises an alert if it's not. You can use it to handle [[health-checks]].
- A front-end container and a back-end container. The front end might serve a web application, with the back end running a service to retrieve data.

## Resource Allocation

Azure Container Instances allocates resources such as **CPUs, memory, and optionally GPUs** (preview) to a container group by adding the resource requests of the instances in the group. Using CPU resources as an example, if you create a container group with two instances, each requesting one CPU, then the container group is allocated two CPUs.

## Networking

Container groups share an **IP address and a port namespace on that IP address**.

To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.

Because containers within the group share a port namespace, **port mapping isn't supported**.

**Containers within a group can reach each other via localhost** on the ports that they exposed, even if those ports aren't exposed externally on the group's IP address.

## Storage

You can **specify external volumes** to mount within a container group. You can **map those volumes into specific paths within the individual containers** in a group. See [[azure-aci-volumes]].

Supported volumes include Azure file share, Secret, Empty directory, Cloned git repo.
