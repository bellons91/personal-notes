---
tags: azure, cloud, az-900, networking, iaas
---

# Azure Virtual Network

It's a virtual network that allows services within Azure to communicate.

You can also add on-prem endpoints and add them to the Virtual Network.

You can create both private and public endpoints:

- **public endpoints**: these endpoints have a public IP that can be accessed from everywhere;
- **private endpoints**: these endpoints have an IP that can be accessed only within the same network.

## Isolation and Segmentation

You can create multiple isolated networks, defining a **private IP address space**.

The IP range only exists within the virtual network and **isn't internet routable**. You can divide that IP address space into **subnets** and allocate part of the defined address space to each named subnet.

You can resolve the names using the built-in name resolution service.

## Internet communications

Each service within the Azure Virtual Network can have a set of public IPs so that they can be accessed by external clients.

You can configure a load balancer to handle resources usage.

## Communication between Azure resources

You can have Azure Resources communicate in two ways:

- **Virtual networks**: several Azure resources can communicate using the same network, and share the same traffic.
- **Service endpoints**: specific endpoints to communicate with an Azure resource, like Azure SQL databases.

## Communicate with on-premises resources

You can link on-prem resources using an Azure subscription, so that the network includes both services hosted on Azure and services hosted on a local environment.

You can achieve this kind of connectivity using:

- **Point-to-site VPN** connections: using a VPN, you can access an Azure Resources from a computer outside that network;
- **Site-to-site VPN**: link your local VPN with an Azure VPN, to make it appear to be a single, local, network;
- **[[azure-expressroute]]**: it's a dedicated connectivity to Azure that does not travel over the internet. Useful when you need greater bandwidth and higher levels of security.

## Route network traffic

By default, Azure routes traffic between subnets on any connected virtual networks, on-premises networks, and the internet.

You also can control routing and override those settings, as follows:

- **[[Route tables]]** allow you to define rules about how traffic should be directed. You can create custom route tables that control **how packets are routed between subnets**.
- **[[Border Gateway Protocol (BGP)]]** works with Azure VPN gateways, Azure Route Server, or Azure ExpressRoute to propagate on-premises BGP routes to Azure virtual networks

## Filter network traffic

Azure virtual networks enable you to filter traffic between subnets by using the following approaches:

- **Network security groups** are Azure resources that can contain **multiple inbound and outbound security rules**. You can define these rules to allow or block traffic, based on factors such as source and destination IP address, port, and protocol.
- **Network virtual appliances** are **specialized VMs** that can be compared to a hardened network appliance. A network virtual appliance carries out a particular network function, such as running a firewall or performing wide area network (WAN) optimization.

## Network Peering

You can link virtual networks together by using **virtual network peering**.

Network traffic between peered networks is private, and travels on the Microsoft backbone network, **never entering the public internet**.

[[User-defined routes (UDR)]] allow you to control the routing tables between subnets within a virtual network or between virtual networks. This allows for greater control over network traffic flow.

## Additional resources

You can use the Azure Shell to operate on a Virtual Network: [[azure-network-scripts]].
