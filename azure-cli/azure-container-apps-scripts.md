---
tags: azure, cloud, az-204, azure-cli, azure-container-apps, containers
---

# Operations on Azure Container Apps with Cloud CLI

This page lists some scripts useful for working with [[azure-container-apps]].

To use the CLI, you first have to install the extensions for running Container Apps commands:

```bash
az extension add --name containerapp --upgrade
```

Then you must register the command namespaces as **providers**:

```bash
az provider register --namespace Microsoft.App
```

## Create environment

```bash
az containerapp env create \
    --name $myAppContEnv \
    --resource-group $myRG \
    --location $myLocation
```

Other commands related to Azure Container Apps Environment are

```bash
az containerapp env create
az containerapp env delete       
az containerapp env list      
az containerapp env list-usages    
az containerapp env show       
az containerapp env update                   
```

## Create a Container App

You can deploy a container image to Azure Container Apps and place it within an environment:

By setting `--ingress` to `external`, you make the container app available to public requests

```bash
az containerapp create \
    --name my-container-app \
    --resource-group $myRG \
    --environment $myAppContEnv \
    --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest \
    --target-port 80 \
    --ingress 'external' \
    --query properties.configuration.ingress.fqdn
```

This command returns the link to access the deployed app, like: "my-container-app.proudfield-2a5e03d1.westeurope.azurecontainerapps.io"

Create a container app and retrieve its fully qualified domain name.

```bash
az containerapp create 
    -n my-containerapp \
    -g MyResourceGroup \
    --image myregistry.azurecr.io/my-app:v1.0 \
    --environment MyContainerappEnv \
    --ingress external \
    --target-port 80 \
    --registry-server myregistry.azurecr.io \
    --registry-username myregistry \
    --registry-password $REGISTRY_PASSWORD \
    --query properties.configuration.ingress.fqdn
```

Create a container app with resource requirements and replica count limits.

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --image nginx \
    --environment MyContainerappEnv \
    --cpu 0.5 \
    --memory 1.0Gi \
    --min-replicas 4 \
    --max-replicas 8
```

Create a container app with **secrets** and **environment variables**. Notice that we used `secretref:` to reference a secret.

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --image my-app:v1.0 \
    --environment MyContainerappEnv \
    --secrets mysecret=secretvalue1 anothersecret="secret value 2" \
    --env-vars GREETING="Hello, world" SECRETENV=secretref:anothersecret
```

Create a container app using a #YAML configuration. Example YAML configuration is here: <https://aka.ms/azure-container-apps-yaml>

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --environment MyContainerappEnv \
    --yaml "path/to/yaml/file.yml"
```

Create a container app with an **http scale rule**

```bash
az containerapp create \
    -n myapp \
    -g mygroup \
    --environment myenv \
    --image nginx \
    --scale-rule-name my-http-rule \
    --scale-rule-http-concurrency 50
```

Create a container app with a **custom scale rule**

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --image my-queue-processor \
    --environment MyContainerappEnv \
    --min-replicas 4 \
    --max-replicas 8 \
    --scale-rule-name queue-based-autoscaling \
    --scale-rule-type azure-queue \
    --scale-rule-metadata "accountName=mystorageaccountname" \
                          "cloud=AzurePublicCloud" \
                          "queueLength": "5" "queueName": "foo" \
    --scale-rule-auth "connection=my-connection-string-secret-name"
```

Create a container app with secrets and mounts them in a volume.

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --image my-app:v1.0 \
    --environment MyContainerappEnv \
    --secrets mysecret=secretvalue1 anothersecret="secret value 2" \
    --secret-volume-mount "mnt/secrets"
```

Create a container apz hosted on a Connected Environment.

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --image my-app:v1.0 \
    --environment MyContainerappConnectedEnv \
    --environment-type connected
```

Create a container app from a new GitHub Actions workflow in the provided GitHub repository

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --environment MyContainerappEnv \
    --registry-server MyRegistryServer \
    --registry-user MyRegistryUser \
    --registry-pass MyRegistryPass \
    --repo https://github.com/myAccount/myRepo
```

Create a Container App from the provided application source

```bash
az containerapp create \
    -n my-containerapp \
    -g MyResourceGroup \
    --environment MyContainerappEnv \
    --registry-server MyRegistryServer \
    --registry-user MyRegistryUser \
    --registry-pass MyRegistryPass \
    --source .
```

## Update a Container App (using Revisions)

With the az containerapp update command you can modify environment variables, compute resources, scale parameters, and deploy a different image.

If your container app update includes revision-scope changes, a new revision is generated.

```bash
az containerapp update \
  --name <APPLICATION_NAME> \
  --resource-group <RESOURCE_GROUP_NAME> \
  --image <IMAGE_NAME>
```

You can list all revisions associated with your container app:

```bash
az containerapp update \
  --name <APPLICATION_NAME> \
  --resource-group <RESOURCE_GROUP_NAME> \
  --image <IMAGE_NAME>
```
