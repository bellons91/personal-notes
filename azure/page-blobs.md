---
tags: azure, cloud, azure-certifications/az900
---

# Page Blobs

Page blobs are a collection of 512-byte pages **optimized for random read and write operations**.

Page blobs store random access files up to 8 TiB in size. Page blobs store virtual hard drive (VHD) files and serve as disks for Azure virtual machines.

A write to a page blob can overwrite just one page, some pages, or up to 4 MiB of the page blob. Writes to page blobs happen in-place and are immediately committed to the blob.

They are one of the possible ways to use [[azure-blob-storage]].
