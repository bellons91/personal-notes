---
tags: az-204, azure, container, aci, docker, azure-certifications/az900 containers, paas
---

# Azure ACI Environment Variables

Setting environment variables in your container instances allows you to provide dynamic configuration of the application or script run by the container.

If you need to pass secrets as environment variables, Azure Container Instances supports **secure values for both Windows and Linux containers**.

Using the Bash Shell or the Cloud Shell, you can define them as key-value pairs:

```bash
--environment-variables 'NumWords'='5' 'MinLength'='8'
```

You can also define secure values (secrets) in the container. These values are not visible when accessing the container's properties.

When using YAML, you must use the `secureValue` property to mark an environment variable as secure. If the variable must not be treated as secure, you can use `value`.

```yml
apiVersion: 2018-10-01
location: eastus
name: securetest
properties:
  containers:
    - name: mycontainer
      properties:
        environmentVariables:
          - name: "NOTSECRET"
            value: "my-exposed-value"
          - name: "SECRET"
            secureValue: "my-secret-value"
        image: nginx
        ports: []
        resources:
          requests:
            cpu: 1.0
            memoryInGB: 1.5
  osType: Linux
  restartPolicy: Always
tags: null
type: Microsoft.ContainerInstance/containerGroups
```
