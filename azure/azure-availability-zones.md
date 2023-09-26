---
tags: azure, azure-certifications/az900
---

# Azure Availability Zones

Availability zones are physically separate datacenters within an [[azure-region]].

Each availability zone is independent, and the internal datacenters have independent power, cooling, and networking. They are **isolated** from other Availability Zones.

Availability Zones are connected through a secure, high-speed network.

**Not all Azure Regions currently support availability zones.** When a Region supports Availability Zones, there are at least three zones within that region.

## Practical usage

- achieve **high-availability**
- co-locate computing, storage, networking
- replicate data

## Azure Services that support Availability Zones

Availability zones are primarily for VMs, managed disks, load balancers, and SQL databases.

Not every Azure Service supports Availability Zones (sometimes, it's not even necessary).

There are 3 categories of service usage:

### Zonal Services

A service is pinned to a specific zone. You can combine multiple zonal deployments across different zones to meet high reliability requirements.

**You're responsible for managing data replication** and distributing requests across zones.

If an outage occurs in a single availability zone, **you're responsible for failover** to another availability zone.

A resource can be deployed to a specific, self-selected availability zone to achieve **more stringent latency or performance requirements**.

Eg: [[azure-virtual-machines]], IP Addresses. **Typically supported by [[iaas]]**.

### Zone-redundant service

Some services are replicated across several zones (eg: [[Azure SQL]]); Microsoft manages spreading requests across zones and the replication of data across zones. If an outage occurs in a single availability zone, Microsoft manages failover automatically. **Typically supported by [[paas]]**.

Zone-redundant services replicate the data across multiple zones so that a failure in one zone doesn't affect the high availability of the data.

### Non-regional services (Always-available services)

Some services must be available regardless of the actual location so they span across worldwide zones.

These services must be resilient to zone-wide outages and region-wide outages

Eg: Azure Active Directory
