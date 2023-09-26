---
tags: azure, cloud, azure-certifications/az900 networking, iaas
---

# Azure ExpressRoute

Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a **private connection**, with the help of a connectivity provider.

This connection is called an **ExpressRoute Circuit**. With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365.

This allows you to connect offices, datacenters, or other facilities to the Microsoft cloud. Each location would have its own ExpressRoute circuit.

ExpressRoute connections **don't go over the public internet**. This allows ExpressRoute connections to offer more reliability, faster speeds, consistent latencies, and higher security than typical connections over the internet.

Even if you have an ExpressRoute connection, DNS queries, certificate revocation list checking, and Azure Content Delivery Network requests are still sent over the public internet.

Generally used for **connectivity between on-prem and Azure services**.

It enables global connectivity without using the internet.

Can manage dynamic routing between your network and Microsoft via [[Border Gateway Protocol (BGP)]].

It supports four connectivity models:

- **co-location at a cloud exchange**: connect datacenters, offices, and so on when they are co-located at the same cloud exchange (eg, an ISP).
- **point-to-point Ethernet connection**: connect your physical facilities to the Microsoft cloud;
- **any-to-any networks**: integrate your WAN with Azure;
- **directly using ExpressRoute**: or using a peer region.
