---
tags: azure, cloud, az-900, virtual-machines, iaas
---

# Azure Virtual Machines

VMs provide [[iaas]] in the form of a **virtualized server**. You don't have to handle physical hardware, but you still need to configure, update, and maintain the software that runs on the VM.

You can create and provision a VM by selecting a preconfigured **VM image**. An image is a template used to create a VM and may already include an OS and other software, like development tools or web hosting environments.

You must choose the best [[virtual-machines-size]] based on the expected usage. There are some ways to [[optimize-virtual-machines]].

VMs are an ideal choice when you need the following:

1. Total control over the operating system (OS).
2. The ability to run custom software.
3. To use custom hosting configurations.

## Good usages of VMs

- **minor tasks** that require a single VM;
- testing and development **environments**;
- high **availability**, **scalability**, **redundancy** (using VM sets);
- running applications on the cloud in an IaaS way;
- cutting costs by shutting down VMs when they are not needed;
- **extending on-prem network** by adding cloud-based VMs to the existing on-prem datacenter.
- moving to the cloud (known as #lift-and-shift)

## Virtual Machines Scale Sets

Virtual machine scale sets let you create and manage a **group of identical, load-balanced VMs**. You can the ensure that they have been **configured identically** and that they have the **same networking rules**.

It allows you to have some **monitoring** that helps determine if you need to increase or decrease the number of VMs inside that Scale Set. **You can have the number of VMs adjusted automatically based on the workload or based on a defined schedule**.

## Virtual Machines Availability Sets

Availability sets allow you to use different power sources, network connectivity, and OS update time to avoid having too many failures in a set (if all the updates are scheduled the same day at the same hour, all the VMs will be down at the same time). Availability Sets are free (you only pay for the VM instances).

Two ways to define Availability Sets:

- **Update domain groups**: you create a group with a subset of VMs to be updated at the same time. This way, you know that all the other VMs will be up while this group is being updated. Azure will wait 30 minutes before updating another _update domain group_.
- **Fault domain groups**: groups that have in common the same physical infrastructure (network and/or power). By default, an availability set will split your VMs across up to **three fault domains**.

## Additional resources

Operate on VM using Azure CLI: [[azure-vm-scripts]]
