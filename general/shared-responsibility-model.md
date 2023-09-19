---
tags: azure, cloud, azure-certifications/az900
---

# Shared Responsibility Model

There are some responsibilities to take into account when building a server factory, such as:

- physical space (buildings, electricity, hardware)
- maintenance
- replacing components
- physical security
- network connectivity

With the Shared Responsibility Model, these responsibilities get shared between the cloud provider and the consumer.

Cloud providers are responsible for the infrastructure of the datacenter: physical security, cooling, building access, and maintenance.

Clients are responsible for the data (both the security and the correctness).

Depending on the **cloud service model**, responsibilities are shared in a different way between cloud vendor and client:

![Shared Responsibility](shared-responsibility-model.svg)

- [[iaas]] places most of the responsibility on the consumer; the cloud vendor is only responsible for physical security and connectivity;
- [[saas]] places most of the responsibilities on the cloud vendor;
- [[paas]] is in the middle.
