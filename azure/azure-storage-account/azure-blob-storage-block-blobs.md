---
tags: azure, cloud, az-900, az-204, storage, azure-blob-storage
---

# Block Blobs

Block blobs **store text and binary data**. Block blobs are made up of blocks of data that can be managed individually. Block blobs can store up to about 190.7 [[TiB]].

They are one of the possible ways to use [[azure-blob-storage]].

Block blobs are optimized for uploading large amounts of data efficiently.

**Block blobs are composed of blocks, each of which is identified by a block ID**. A block blob can include up to 50,000 blocks. Each block in a block blob can be a different size, up to the maximum size permitted for the service version in use.

To create or modify a block blob, write a set of blocks via the _Put Block_ operation and then commit the blocks to a blob with the _Put Block List_ operation. When you upload a block to a blob in your storage account, it is associated with the specified block blob, but it does not become part of the blob until you commit a list of blocks that includes the new block's ID. This allows you to upload blocks in parallel to optimize upload time.

Each blob can have custom [[azure-blob-metadata]] (returned as HTTP Headers) and some [[Blob Index Tags]].
