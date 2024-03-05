---
tags: azure, cloud, azure-certifications/az204, storage, azure-blob-storage
---

# Azure Block Blobs metadata

For each Block Blob you can define key-value pairs as Metadata.

Metadata include:

* **System properties**: System properties exist on each Blob storage resource. Some of them can be read or set, while others are read-only. Under the covers, some system properties correspond to certain standard HTTP headers. The Azure Storage client library for .NET maintains these properties for you.

* **User-defined metadata**: User-defined metadata consists of one or more name-value pairs that you specify for a Blob storage resource. You can use metadata to store additional values with the resource. Metadata values are for your own purposes only, and do not affect how the resource behaves. Their name starts with `x-ms-meta-`.

The standard HTTP headers supported on *containers* include:

* ETag
* Last-Modified

The standard HTTP headers supported on *blobs* include:

* ETag
* Last-Modified
* Content-Length
* Content-Type
* Content-MD5
* Content-Encoding
* Content-Language
* Cache-Control
* Origin
* Range
