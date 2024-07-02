---
tags: az-204, authentication, shared-access-signature, sas
---

# Shared Access Signatures

A shared access signature (SAS) is a **signed URI** that points to one or more storage resources and includes a token that contains a special set of query parameters.

The token indicates how the resources might be accessed by the client. One of the query parameters, the signature, is constructed from the SAS parameters and signed with the key that was used to create the SAS. This signature is used by Azure Storage to authorize access to the storage resource.

There are three types of shared access signatures:

- **User delegation SAS**: A user delegation SAS is **secured with Microsoft Entra credentials** and also by the permissions specified for the SAS. A user delegation SAS applies to Blob storage only.
- **Service SAS**: A service SAS is secured with the storage account key. A service SAS delegates access to a resource.
- **Account SAS**: An account SAS is secured with the storage account key. All of the operations available via a service or user delegation SAS are also available via an account SAS.

**Note**: When your application design requires shared access signatures for access to Blob storage, use Microsoft Entra credentials to create a user delegation SAS when possible for superior security.

## SAS in query string

When you access an element using a SAS, you pass it via query string.

For example, `https://medicalrecords.blob.core.windows.net/patient-images/patient-116139-nq8z7f.jpg?sp=r&st=2020-01-20T11:42:32Z&se=2020-01-20T19:42:32Z&spr=https&sv=2019-02-02&sr=b&sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D` is made up of two parts: the URI (`https://medicalrecords.blob.core.windows.net/patient-images/patient-116139-nq8z7f.jpg`) and the SAS token (`sp=r&st=2020-01-20T11:42:32Z&se=2020-01-20T19:42:32Z&spr=https&sv=2019-02-02&sr=b&sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D`).

The SAS token is made up of several parts:

|Component| Description|
|--|--|
|`sp=r` |Controls the access rights. The values can be `a` for add, `c` for create, `d` for delete, `l` for list, `r` for read, or `w` for write. This example is read only. The example sp=acdlrw grants all the available rights.|
|`st=2020-01-20T11:42:32Z` |The date and time when access starts.|
|`se=2020-01-20T19:42:32Z` |The date and time when access ends. This example grants eight hours of access.|
|`sv=2019-02-02`| The version of the storage API to use.|
|`sr=b`| The kind of storage being accessed. In this example, b is for blob.|
|`sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D` |The cryptographic signature.|

There are some best practices to follow:

- To securely distribute a SAS and prevent man-in-the-middle attacks, **always use HTTPS**.
- **The most secure SAS is a user delegation SAS**. Use it wherever possible because it removes the need to store your storage account key in code. You must use Microsoft Entra ID to manage credentials. This option might not be possible for your solution.
- Try to **set your expiration time to the smallest useful value**. If a SAS key becomes compromised, it can be exploited for only a short time.
- **Apply the rule of minimum-required privileges**. Only grant the access that's required. For example, in your app, read-only access is sufficient.
- There are some situations where a SAS isn't the correct solution. When there's an unacceptable risk of using a SAS, create a middle-tier service to manage users and their access to storage.

## When to use SAS?

A common scenario where a SAS is useful is a service where users read and write their own data to your storage account.

In a scenario where a storage account stores user data, there are two typical design patterns, that can be mixed depending on the needs.

1. Clients upload and download data via a **front-end proxy service**, which performs authentication. This front-end proxy service has the advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale to match demand may be expensive or difficult.

![Scenario with frontend proxy](https://learn.microsoft.com/en-us/training/wwl-azure/implement-shared-access-signatures/media/storage-proxy-service.png)

2. **A lightweight service authenticates the client** as needed and then generates a SAS. Once the client application receives the SAS, they can access storage account resources directly with the permissions defined by the SAS and for the interval allowed by the SAS. **The SAS mitigates the need for routing all data through the front-end proxy service**.

![Scenario with lightweight SAS provider service](https://learn.microsoft.com/en-us/training/wwl-azure/implement-shared-access-signatures/media/storage-provider-service.png)

