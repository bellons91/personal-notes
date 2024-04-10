---
tags: az-204, azure, containers, aci, docker, az-900 containers, paas
---

# Azure ACI Restart Policies

With a configurable restart policy, you can specify that your containers are stopped when their processes are completed.

Because **container instances are billed by the second**, you're charged only for the compute resources used while the container executing your task is running.

Possible values are:

- **Always**: Containers in the container group are always restarted. This is the **default** setting applied when no restart policy is specified at container creation.
- **Never**: Containers in the container group are never restarted. **The containers run at most once**.
- **OnFailure**: **Containers in the container group are restarted only when the process executed in the container fails** (when it terminates with a nonzero exit code). The containers are run at least once.

Azure Container Instances starts the container, and then stops it when its application, or script, exits.
When Azure Container Instances stops a container whose restart policy is Never or OnFailure, the container's status is set to Terminated.
