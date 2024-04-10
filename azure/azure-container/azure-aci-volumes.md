---
tags: az-204, azure, containers, aci, docker, az-900, paas
---

# Azure ACI Volumes

Azure Container Instances can mount an Azure file share created with [[azure-file-storage]].

- You can only mount Azure Files shares to **Linux** containers.
- Azure file share volume mount requires the Linux container run as _root_.
- Azure File share volume mounts are limited to [[CIFS]] support.

When using the Azure CLI, you have to specify `azure-file-volume-account-name`, `azure-file-volume-account-key`, `azure-file-volume-share-name`, `azure-file-volume-mount-path`.

You can also create the Container Group by using YAML. Here's an example of how to create a container group that mounts an Azure file share named _acishare_:

```yml
apiVersion: "2019-12-01"
location: eastus
name: file-share-demo
properties:
  containers:
    - name: hellofiles
      properties:
        environmentVariables: []
        image: mcr.microsoft.com/azuredocs/aci-hellofiles
        ports:
          - port: 80
        resources:
          requests:
            cpu: 1.0
            memoryInGB: 1.5
        volumeMounts:
          - mountPath: /aci/logs/
            name: filesharevolume
  osType: Linux
  restartPolicy: Always
  ipAddress:
    type: Public
    ports:
      - port: 80
    dnsNameLabel: aci-demo
  volumes:
    - name: filesharevolume
      azureFile:
        sharename: acishare
        storageAccountName: <Storage account name>
        storageAccountKey: <Storage account key>
tags: {}
type: Microsoft.ContainerInstance/containerGroups
```

Notice that the volume is defined in a separate node, and then referenced when defining the volume paths:

```yml
volumes:
  - name: filesharevolume
azureFile:
  sharename: acishare
  storageAccountName: <Storage account name>
  storageAccountKey: <Storage account key>
```

You can also mount **multiple volumes**: when using [[arm-templates]], you first need to define the volumes in an array.

```json
"volumes": [{
  "name": "myvolume1",
  "azureFile": {
    "shareName": "share1",
    "storageAccountName": "myStorageAccount",
    "storageAccountKey": "<storage-account-key>"
  }
},
{
  "name": "myvolume2",
  "azureFile": {
    "shareName": "share2",
    "storageAccountName": "myStorageAccount",
    "storageAccountKey": "<storage-account-key>"
  }
}]
```

and then map the paths in the `volumeMounts` section:

```json
"volumeMounts": [{
  "name": "myvolume1",
  "mountPath": "/mnt/share1/"
},
{
  "name": "myvolume2",
  "mountPath": "/mnt/share2/"
}]
```
