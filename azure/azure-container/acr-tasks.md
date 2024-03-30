---
tags: az-204, azure, container, acr, docker
---

# ACR Tasks

ACR Tasks is a suite of features within [[azure-container-registry]].

With ACR Tasks, to automatically rebuild application images when their base images are updated. You can also automate image builds when there is a new code commit in the source Git repository.

You can use ACR Tasks to streamline building, testing, pushing, and deploying images in Azure.

It provides cloud-based container image building for platforms including Linux, Windows, and [[azure-resource-manager]], and can automate OS and framework patching for your Docker containers.

Each ACR Task has an **associated source code context** - the location of a set of source files used to build a container image or other artifact. Example contexts include a Git repository or a local filesystem.

## Quick Tasks

Quick tasks provide an integrated development experience by offloading your container image builds to Azure.

With quick tasks, you can verify your automated build definitions and catch potential problems prior to committing your code.

Build and push a single container image to a container registry on-demand, in Azure, without needing a local Docker Engine installation.

They are the corresponding for `docker build` and `docker push` for the cloud.

An example of command is `az acr build`, which takes the context, sends it to ACR Tasks, and pushes the built image to its registry upon completion.

## Automatically triggered tasks

Enable one or more triggers to **build an image**:

- **Trigger on source code update**: you can configure to build the image every time new code is committed, or a pull request is made or updated, by using `az acr task create`, specifying the Git repo, the branch and the [[docker-file]].
- **Trigger on base image update**: You can set up an ACR task to **track a dependency on a base image** when it builds an application image. When the updated base image is pushed to your registry, or a base image is updated in a public repo such as in [[Docker Hub]], ACR Tasks can automatically build any application images based on it.
- **Trigger on a schedule**: set up one or more timer triggers when you create or update the task. Scheduling a task is useful for running container workloads on a defined schedule, or running **maintenance operations or tests on images** pushed regularly to your registry.

## Multi-step tasks

Extend the single image build-and-push capability of ACR Tasks with multi-step, multi-container-based workflows.

Multi-step tasks, **defined in a YAML file** specify individual build and push operations for container images or other artifacts. They can also define the execution of one or more containers, with each step using the container as its execution environment.
