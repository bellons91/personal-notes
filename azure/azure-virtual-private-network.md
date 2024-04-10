---
tags: azure, cloud, az-900 networking
---

# Azure Virtual Private Network

A virtual private network (VPN) uses an **encrypted tunnel** within another network. VPNs are typically deployed to connect two or more trusted private networks to one another over an untrusted network (typically the public internet). Traffic is encrypted while travelling over the untrusted network to prevent eavesdropping or other attacks.

## VPN gateways

They act as a virtual network gateway, and they are **deployed in a dedicated subnet** of the virtual network.

They allow for:

- **site-to-site connection**: connect on-prem datacenters to a virtual network;
- **point-to-site connection**: connect individual devices to a virtual network;
- **network-to-network** connection: connect two virtual networks

The whole communication is encrypted inside a **private tunnel**.

There are two ways to define a VPN gateway:

- **Policy-based VPN gateways**: specify statically the IP address of packets that should be encrypted through each tunnel. This type of device evaluates every data packet against those sets of IP addresses to choose the tunnel where that packet is going to be sent through. Policy-based VPNs encrypt and direct packets through IPsec tunnels based on the IPsec policies configured with the combinations of address prefixes between your on-premises network and the Azure VNet. The policy (or traffic selector) is usually defined as an access list in the VPN device configuration.
- **Route-based VPN gateways**: [[IPSec tunnels]] are modelled as a network interface or virtual tunnel interface. **Preferred for on-premises devices.**. Good for point-to-site connections, coexistence with [[azure-expressroute]], connection between different [[azure-virtual-network]]. . RouteBased VPNs use "routes" in the IP forwarding or routing table to direct packets into their corresponding tunnel interfaces. The tunnel interfaces then encrypt or decrypt the packets in and out of the tunnels.

## High-availability settings

VPN gateways must be highly available: without connection, the systems become unreachable.

There are several strategies:

- **active/standby configuration**: by default, together with the main instance of the VPN Gateway, Azure deploys a second instance that is put on standby. In case of an interruption of the communication on the active gateway, the secondary connection handles all the load automatically.
- **active/active configuration**: you can assign a unique public IP to each instance. Every on-prem device then connects to a specific IP address.
- **[[azure-expressroute]] failover**: a VPN gateway is configured to be a failover path for ExpressRoutes connections. It prevents connectivity issues in case of physical damage to the network: you use the VPN gateway in place of the ExpressRoute path, allowing connections to go over the internet.
- **zone-redundancy gateways**: only available in regions that support [[azure-availability-zones]]. Deploying gateways in Azure availability zones physically and logically separates gateways within a region while protecting your on-premises network connectivity to Azure from zone-level failures. They use Standard public IP addresses instead of Basic public IP addresses.
