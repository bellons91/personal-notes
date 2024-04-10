---
tags: azure, cloud, az-900, security
---

# Conditional Access

Conditional Access is a tool that Azure Active Directory uses to **allow (or deny) access to resources** based on **identity signals**. These signals include who the user is, where the user is, and what device the user is requesting access from.

Conditional Access can be used to protect the organization's assets.

Conditional Access also provides a more **granular multifactor authentication experience** for users. For example, a user might not be challenged for a second authentication factor if they're at a known location.

During sign-in, **Conditional Access collects signals from the user**, makes decisions based on those signals, and then enforces that decision by allowing or denying the access request or challenging for a multifactor authentication response.

Only available with Azure AD Premium P1 licenses.

## Signals

Conditional Access uses signals to define what actions take (if any).

Some signals are:

- User or group membership
- IP Location information: Organizations can create trusted IP address ranges that can be used when making policy decisions. Administrators can specify entire countries/regions IP ranges to block or allow traffic from.
- Device
- Application: Users attempting to access specific applications can trigger different Conditional Access policies.
- Real-time and calculated risk detection
