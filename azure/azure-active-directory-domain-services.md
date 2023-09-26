---
tags: azure, cloud, azure-certifications/az900, authentication, paas
---

# Azure Active Directory Domain Services

Part of [[azure-active-directory]], Azure AD DS is a service that provides [[managed domain]] services such as:

- domain join
- group policy
- [[LDAP]]
- [[Kerberos]] authentication
- [[NTLM]] authentication

Azure AD DS allows you to migrate your [[Domain Controllers]] to Azure, allowing you to run legacy applications that cannot support modern authentication and force you to use the older, on-prem, technologies.

Azure AD DS integrates with your existing Azure AD tenant. This integration lets users sign into services and applications connected to the managed domain using their existing credentials. You can also use existing groups and user accounts to secure resource access. These features provide a smoother lift-and-shift of on-premises resources to Azure.

A managed domain is configured to perform a **one-way synchronization from Azure AD to Azure AD DS**.
