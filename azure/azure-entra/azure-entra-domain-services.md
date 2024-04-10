---
tags: azure, cloud, az-900, authentication, paas
---

# Azure Entra Domain Services

Part of [[azure-entra]], Azure Entra DS is a service that provides [[managed domain]] services such as:

- domain join
- group policy
- [[LDAP]]
- [[Kerberos]] authentication
- [[NTLM]] authentication

Azure Entra DS allows you to migrate your [[Domain Controllers]] to Azure, allowing you to run legacy applications that cannot support modern authentication and force you to use the older, on-prem, technologies.

Azure Entra DS integrates with your existing Azure Entra tenant. This integration lets users sign into services and applications connected to the managed domain using their existing credentials. You can also use existing groups and user accounts to secure resource access. These features provide a smoother lift-and-shift of on-premises resources to Azure.

A managed domain is configured to perform a **one-way synchronization from Azure Entra to Azure Entra DS**.
