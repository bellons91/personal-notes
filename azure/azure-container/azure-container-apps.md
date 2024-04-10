---
tags: az-204, az-900, azure, containers, azure-container-apps, docker, k8s
---

# Azure Container Apps

Azure Container Apps enables you to run microservices and containerized applications on a serverless platform that runs on top of [[azure-kubernetes-service]].

Azure Container Apps doesn't provide direct access to the underlying Kubernetes APIs. If you require access to the [[Kubernetes]] APIs and control plane, you should use AKS.

You don't have to manage containers manually.

Common uses of Azure Container Apps include:

- Deploying API endpoints
- Hosting background processing applications
- Handling event-driven processing
- Running microservices

It's a #paas service.

It's optimized for running general purpose containers, especially for applications that span many microservices deployed in containers.

It incorporates **Service Discovery**, **Load Balancing** and **Scaling**.

Azure Container Apps provides the flexibility you need with a serverless container service built for microservice applications and robust autoscaling capabilities without the overhead of managing complex infrastructure.
