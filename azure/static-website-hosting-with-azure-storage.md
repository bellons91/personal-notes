---
tags: azure, cloud, az-204, storage, azure-storage-account
---

# Static website hosting with Azure Storage

If you have an [[azure-storage-account-scripts]], you can **serve static content** (HTML, CSS, JavaScript, and image files) directly from a storage container named `$web`.

You can make your static website available via a custom domain.

It's easier to enable HTTP access for your custom domain because Azure Storage natively supports it. To enable HTTPS, you have to use Azure CDN because Azure Storage doesn't yet natively support HTTPS with custom domains.

Static websites have some limitations. For example, If you want to configure headers, you have to use Azure Content Delivery Network ([[Azure CDN]]).

There's no way to configure headers as part of the static website feature itself.
Also, [[AuthN]] and [[AuthZ]] aren't supported.

Static website hosting is a feature that you have to enable on the storage account.

You can modify the public access level of the _$web_ container, but making this modification has no impact on the primary static website endpoint because these files are served through **anonymous access requests**. That means public (read-only) access to all files.

While the primary static website endpoint isn't affected, **a change to the public access level does impact the primary blob service endpoint**.

For example, if you change the public access level of the $web container from Private (no anonymous access) to Blob (anonymous read access for blobs only), then the level of public access to the primary static website endpoint h*ttps://contosoblobaccount.**z22**.web.core.windows.net/index.html* doesn't change.

However, the public access to the primary blob service endpoint h*ttps://contosoblobaccount.blob.core.windows.net/**$web**/index.html>* does change from private to public. Now, users can open that file by using either of these two endpoints.

Disabling public access on a storage account by using the public access setting of the storage account doesn't affect static websites that are hosted in that storage account.
