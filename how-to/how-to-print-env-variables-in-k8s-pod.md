---
tags: K8S
---

# How to print Environment Variables in a K8s Pod

To list all the environment variables in a K8S pod, open the shell of the POD and run

```plaintext
printenv
```

This command lists the environment variables in a key=value format:

```plaintext
MY_POD_SERVICE_ACCOUNT=default
...
MY_POD_NAMESPACE=default
MY_POD_IP=172.17.0.4
...
MY_NODE_NAME=minikube
...
MY_POD_NAME=dapi-envars-fieldref
```

To filter the result, use the `grep` command, and the `-i` flag for case insensitive search:

```plaintext
printenv | grep my-text -i
```

More info at [Expose Pod Information to Containers Through Environment Variables 🔗](https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/)
