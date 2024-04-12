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

With Azure Container Apps, you can:

- Run **multiple container revisions** and manage the container app's application lifecycle.
- **Autoscale** your apps based on any [[KEDA-supported scale trigger]]. Most applications can scale to zero. (Applications that scale on CPU or memory load can't scale to zero.)
- **Enable HTTPS ingress** without having to manage other Azure infrastructure.
- **Split traffic** across multiple versions of an application for [[Blue/Green deployments]] and [[A/B testing]] scenarios.
- Use **internal ingress** and **[[service discovery]]** for secure internal-only endpoints with built-in [[DNS]]-based service discovery.
- Build microservices with [[Dapr]] and access its rich set of APIs.
- Run containers from any registry, public or private, including Docker Hub and  [[azure-container-registry]].
- Use the Azure CLI extension, Azure portal or ARM templates to manage your applications.
- Provide an existing virtual network when creating an environment for your container apps.
- Securely manage secrets directly in your application.
- Monitor logs using Azure Log Analytics.

Applications built on Azure Container Apps can **dynamically scale** based on HTTP traffic, event-driven processing, CPU or memory load, and any KEDA-supported scaler.

It's a #paas service.

It's optimized for running general purpose containers, especially for applications that span many #microservices deployed in containers.

It incorporates **Service Discovery**, **Load Balancing** and **Scaling (also independent)**.

Azure Container Apps provides the flexibility you need with a serverless container service built for microservice applications and robust autoscaling capabilities without the overhead of managing complex infrastructure.

There are two **limitations**:

- you can only use container images based on #Linux;
- you cannot try to perform operations as root.

You can define [[azure-container-apps-authentication]].

There's a great integration with Dapr: [[azure-container-apps-with-dapr]].

## Azure Container Apps environments

Individual container apps are deployed to a **single Container Apps environment**, which acts as a secure boundary around groups of container apps.

Container Apps in the same environment are deployed **in the same virtual network** and **write logs to the same Log Analytics workspace**.

You may provide an existing [[azure-virtual-network]] when you create an environment.

Reasons to use the same environment:

- Manage related services;
- Deploy different applications to the same virtual network;
- Instrument [[Dapr]] applications that communicate via the Dapr service invocation API;
- Have applications to share the same Dapr configuration;
- Have applications share the same log analytics workspace;

Reasons to use separate environments:

- Two applications never share the same compute resources;
- Two Dapr applications can't communicate via the Dapr service invocation API;

## Containers

Containers in Azure Container Apps can use any runtime, programming language, or development stack of your choice.

Azure Container Apps supports **any Linux-based x86-64 (linux/amd64)** container image.

If a container crashes it automatically restarts.

When using [[azure-resource-manager]] templates, you can define the info about the containers in the `containers` node of the `properties.template` section.

```json
"containers": [
  {
    "name": "main",
    "image": "[parameters('container_image')]",
    "env": [
      {
        "name": "HTTP_PORT",
        "value": "80"
      },
      {
        "name": "SECRET_VAL",
        "secretRef": "mysecret"
      }
    ],
    "resources": {
      "cpu": 0.5,
      "memory": "1Gi"
    },
    "volumeMounts": [
      {
        "mountPath": "/myfiles",
        "volumeName": "azure-files-volume"
      }
    ]
    "probes":[
    {
        "type":"liveness",
        "httpGet":{
        "path":"/health",
        "port":8080,
        "httpHeaders":[
            {
                "name":"Custom-Header",
                "value":"liveness probe"
            }]
        },
        "initialDelaySeconds":7,
        "periodSeconds":3
// file is truncated for brevity
```

Notice that you can also specify [[probes]] to ensure that the container is live.

You can define **multiple containers** in a single container app to implement the [[sidecar-pattern]]. The containers in a container app share hard disk and network resources and experience the same application lifecycle.

## Container registries

You can deploy images hosted on private registries by providing credentials in the Container Apps configuration.

To use a container registry, you define the required fields in registries array in the properties.configuration section of the container app resource template. The `passwordSecretRef` field identifies the name of the secret in the secrets array name where you defined the password.

```json
{
  ...
  "registries": [{
    "server": "docker.io",
    "username": "my-registry-user-name",
    "passwordSecretRef": "my-password-secret-name"
  }]
}
```

## Versioning / Revisions

In Azure Container Apps, versions are called **Revisions**.

A revision is an **immutable snapshot** of a container app version.

New revisions are created when you update your application with [[revision-scope changes]]. You can also update your container app based on a specific revision.

You can customize the revision name by setting the revision suffix. Revision names are used to identify a revision, and in the revision's URL. By default, Container Apps creates a unique revision name with a suffix consisting of a *semi-random string of alphanumeric characters*.

## Secrets

Once secrets are defined at the application level, secured values are available to container apps.

- **Secrets are scoped to an application**, outside of any specific revision of an application.
- Adding, removing, or changing secrets doesn't generate new revisions.
- Each application revision can reference one or more secrets.
- Multiple revisions can reference the same secret(s).

**An updated or deleted secret doesn't automatically affect existing revisions in your app**. When a secret is updated or deleted, you can respond to changes in one of two ways:

1. Deploy a new revision.
2. Restart an existing revision.

Note: Before you delete a secret, deploy a new revision that no longer references the old secret. Then, deactivate all revisions that reference the secret.

To reference a secret in an environment variable in the Azure CLI, set its value to `secretref:`, followed by the name of the secret. For example:

```bash
az containerapp create \
  --resource-group "my-resource-group" \
  --name myQueueApp \
  --environment "my-environment-name" \
  --image demos/myQueueApp:v1 \
  --secrets "queue-connection-string=$CONNECTIONSTRING" \
  --env-vars "QueueName=myqueue" "ConnectionString=secretref:queue-connection-string"
```
