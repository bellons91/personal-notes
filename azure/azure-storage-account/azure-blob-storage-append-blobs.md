---
tags: azure, cloud, azure-certifications/az900, azure-certifications/az204, storage, azure-blob-storage
---

# Append Blobs

Append blobs are made up of blocks like block blobs, but are **optimized for append operations**.

Append blobs are ideal for scenarios such as logging data from virtual machines.

When you modify an append blob, blocks are added to the end of the blob only, via the _Append Block_ operation. **Updating or deleting of existing blocks is not supported**. Unlike a block blob, an append blob does not expose its block IDs.

They are one of the possible ways to use [[azure-blob-storage]].
