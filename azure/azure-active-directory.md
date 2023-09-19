---
tags: azure, cloud, azure-certifications/az900, authentication
---

# Azure Active Directory

For on-premises environments, **Active Directory runs on Windows Server** instances. It provides an identity and access management service that your organization manages.

While Active Directory is the on-prem solution, Azure Active Directory is the cloud solution.

When using Azure AD, Microsoft can help protect you by **detecting suspicious sign-in attempts** at no extra cost.

Azure AD provides several services:

- **Authentication**: verify identity to access applications and resources. It also includes functionality such as self-service password reset, **multifactor authentication**, a custom list of banned passwords, and more.
- **Single sign-on**: a single identity is tied to a user. As users change roles or leave an organization, having access modifications tied to that identity reduces the effort needed to change or disable accounts.
- **Application management**: you can manage your cloud and on-premises apps by using Azure AD. Features like Application Proxy, SaaS apps, the My Apps portal, and single sign-on provide a better user experience.
- **Device management**: Along with accounts for individual people, Azure AD supports the registration of devices. Registration enables devices to be managed through tools like Microsoft Intune. It also allows for device-based **Conditional Access policies** to restrict access attempts to only those coming from known devices, regardless of the requesting user account.

If you have an on-prem Active Directory and want to synchronize the data with Azure AD, you can use **Azure AD Connect**. Data is synchronized in both ways so that you can use SSO and MFA on both systems.

You can use domain services with [[azure-active-directory-domain-services]].

Azure AD can handle several types of authentication:

- SSO
- MFA
- passwordless authentication (eg, Windows Hello for Business)
- [[fido2-authentication]]

You can finally manage users from external sources by using [[azure-ad-external-identities]].

## Conditional Access

Conditional Access is a tool that Azure Active Directory uses to **allow (or deny) access to resources** based on **identity signals**. These signals include who the user is, where the user is, and what device the user is requesting access from.

Conditional Access can be used to protect the organization's assets.

Conditional Access also provides a more **granular multifactor authentication experience** for users. For example, a user might not be challenged for a second authentication factor if they're at a known location.

During sign-in, **Conditional Access collects signals from the user**, makes decisions based on those signals, and then enforces that decision by allowing or denying the access request or challenging for a multifactor authentication response.
