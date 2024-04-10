---
tags: azure, cloud, az-204, storage, azure-blob-storage
---

# Azure Blob Container

A container organizes a set of blobs, **similar to a directory** in a file system. A storage account can include an **unlimited number of containers**, and a container can store an unlimited number of blobs.

A container name must be a **valid DNS name**, as it forms part of the unique URI (Uniform resource identifier) used to address the container or its blobs. Follow these rules when naming a container:

1. Container names can be between **3 and 63 characters long**.
2. Container names must start with a letter or number, and can contain only lowercase letters, numbers, and the dash (-) character.
3. Two or more consecutive dash characters aren't permitted in container names.
