---
tags: azure, cloud, azure-certifications/az900, authentication, paas
---

# Azure Entra (aka Active Directory)

For on-premises environments, **Active Entra runs on Windows Server** instances. It provides an identity and access management service that your organization manages.

While Active Entra is the on-prem solution, Azure Active Entra is the cloud solution.

When using Azure Entra, Microsoft can help protect you by **detecting suspicious sign-in attempts** at no extra cost.

Azure Entra provides several services:

- **Authentication**: verify identity to access applications and resources. It also includes functionality such as self-service password reset, **multifactor authentication**, a custom list of banned passwords, and more.
- **Single sign-on**: a single identity is tied to a user. As users change roles or leave an organization, having access modifications tied to that identity reduces the effort needed to change or disable accounts.
- **Application management**: you can manage your cloud and on-premises apps by using Azure Entra. Features like Application Proxy, SaaS apps, the My Apps portal, and single sign-on provide a better user experience.
- **Device management**: Along with accounts for individual people, Azure Entra supports the registration of devices. Registration enables devices to be managed through tools like Microsoft Intune. It also allows for device-based **[[conditional-access]] policies** to restrict access attempts to only those coming from known devices, regardless of the requesting user account.

If you have an on-prem Active Entra and want to synchronize the data with Azure Entra, you can use **Azure Entra Connect**. Data is synchronized in both ways so that you can use SSO and MFA on both systems.

You can use domain services with [[azure-entra-domain-services]].

Azure Entra can handle several types of authentication:

- SSO
- MFA
- passwordless authentication (eg, Windows Hello for Business)
- [[fido2-authentication]]

You can finally manage users from external sources by using [[azure-entra-external-identities]].
