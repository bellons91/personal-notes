---
tags: azure, cloud, azure-certifications/az204, autoscaling
---

# Azure App Service Autoscale

Autoscaling is a cloud system or process that adjusts available resources based on the current demand.

Autoscaling performs [[scale-in-out]], as opposed to scaling up and down.

Autoscaling can be triggered according to a schedule, or by assessing whether the system is running short on resources.

Autoscaling responds to changes in the environment by adding or removing web servers and balancing the load between them.

Autoscaling doesn't have any effect on the CPU power, memory, or storage capacity of the web servers powering the app, **it only changes the number of web servers**.

Autoscaling makes its decisions based on rules that you define. A rule specifies the **threshold for a metric**, and triggers an autoscale event when this threshold is crossed. Autoscaling can also deallocate resources when the workload has diminished.

Autoscaling should only be used on *genuine* requests. For example, a [[DoS]] attack will flood the server with malicious resources. It's useless (and expensive) to try handle these requests, so it's better to detect them and discard these requests.

Autoscaling provides [[elasticity]] for your services, allowing to add resources during peaks like special events or removing resources during weekends. It also improves [[availability]] and [[Fault tolerance]], ensuring that a client requests won't be denied because the instance has crashed.

**Autoscaling isn't the best approach to handling long-term growth.** You might have a web app that starts with a few users, but increases in popularity over time. **Autoscaling has an overhead associated with monitoring resources and determining whether to trigger a scaling event**. In this scenario, if you can anticipate the rate of growth, manually scaling the system over time may be a more cost effective approach.

Autoscaling is also affected by the number of instances of the service. The fewer the number of instances initially, the less capacity you have to handle an increasing workload while autoscaling spins up more instances.

