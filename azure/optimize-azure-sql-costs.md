---
tags: azure, azure-certifications/az900, cost-optimization, azure-sql
---

# Optimize Azure SQL costs

In [[Azure SQL]], costs are determined by two factors:

- **DTUs**: Database Transaction Units;
- **vCores**: Virtual cores;

Depending on the need for each value, you will choose a different tier, and therefore, you'll incur different costs.

To optimize costs, you should use **Elastic pools**: you pay for a single Azure SQL server, and all the databases that are part of that pool share the same resources and costs. In this way, if one DB is temporarily idle, its computation power is available for the other databases.
