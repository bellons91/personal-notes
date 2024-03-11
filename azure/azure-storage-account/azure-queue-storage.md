---
tags: azure, cloud, azure-certifications/az900, azure-certifications/az204, storage
---

# Azure Queue Storage

Its purpose is to store a large number of messages. Once stored, those messages can be accessed using HTTP or HTTPS (only under authentication) messages.

**Each individual message can be up to 64KB in size**, but you don't have a limited number of messages (the only limit is the total storage of the storage account).

This service provides a list of endpoints available at https://{storage-account-name}.queue.core.windows.net

These messages are stored on disk until they are removed from the queue.
