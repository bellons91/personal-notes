---
tags: azure, azure-certifications/az900, cost-optimization, virtual-machines
---


# Cost optimization on Virtual Machines

Depending on the average usage of resources, you can understand if you are wasting your [[azure-virtual-machines]] resources and expenses or if you are OK.

If the average usage is **< 10%** of the possible capacity, you are wasting resources.

If the usage is **~90%**, you are using your resources in the best way possible.

If the usage is **> 90%**, you risk having performance issues because all the resources are being used, and there are no more resources available to handle sudden usage peeks.

If you notice that you are using too many (or too few) resources, you might need to adjust the [[virtual-machines-size]].

You can use **[[azure-advisor]]**, a tool that analyzes the usage of a VM for 14 days and gives you hints on how to optimize it. For example, if the **CPU usage is <5% or the network usage is < 7MB, the VM is underutilized**, so you can remove it or use a smaller tier.

You can use **Azure Reserved Instances**: instead of paying for every single VM and having to control the size for each of them, you can **buy upfront** the capacity for 1 or 3 years of resources and share the computational power between all your VMs.


