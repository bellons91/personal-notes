---
tags: az-204, azure, container, acr, docker
---

# Azure Container Registry (ACR)

ACR is a registry for [[Docker Containers]].

You can use ACR to manage containerized applications across clusters of hosts, like [[Kubernetes]], [[DC/OS]], and [[Docker Swarm]].

There are Azure services that pull the application content from ACR, such as [[Azure Kubernetes Service (AKS)]], [[azure-app-service]], [[Service Fabric]], and others.

Developers can push [[Docker Images]] to ACR from a CI pipeline.

You can use [[acr-tasks]] to automatically rebuild application images when their base images are updated. You can also automate image builds when there is a new code commit in the source Git repository.

In Azure Container Registry you can also store [[Helm charts]].

There are several pricing tiers:

- **Basic**: cost-optimized version, just for learning. It provides lower storage and throughput.
- **Standard**: ideal for most production scenarios. It has more storage and image throughput.
- **Premium**: it also has _zone-replication_ of the registry (the registry is replicated to a minimum of three separate zones in each enabled region), [[content trust]] for image tag signing, and private link with private endpoints to restrict the access to the registry.

**All container images in your registry are encrypted at rest**. Azure automatically encrypts an image before storing it, and decrypts it on-the-fly when you or your applications and services pull the image.

Azure Container Registry **stores data in the region where the registry is created**, to help customers meet data residency and compliance requirements. Azure may also store registry data in a paired region in the same geography. If a regional outage occurs, the registry data may become unavailable and isn't automatically recovered. You can then choose to enable geo-replication.

Azure Container Registry allows you to create as many repositories, images, layers, or tags as you need, up to the registry storage limit. The number of images and tags affects the performance of the registry, so you should remember to delete older versions and unused images.
