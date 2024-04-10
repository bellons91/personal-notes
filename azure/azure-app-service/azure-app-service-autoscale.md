---
tags: azure, cloud, az-204, autoscaling
---

# Azure App Service Autoscale

Autoscaling is a cloud system or process that adjusts available resources based on the current demand.

Autoscaling performs [[scale-in-out]] as opposed to scaling up and down.

Autoscaling can be triggered according to a schedule or by assessing whether the system is running short on resources.

Autoscaling responds to changes in the environment by adding or removing web servers and balancing the load between them.

Autoscaling doesn't have any effect on the CPU power, memory, or storage capacity of the web servers powering the app; **it only changes the number of web servers**.

Autoscaling makes its decisions based on rules that you define. A rule specifies the **threshold for a metric**, and triggers an autoscale event when this threshold is crossed. Autoscaling can also deallocate resources when the workload has diminished.

Autoscaling should only be used on _genuine_ requests. For example, a [[DoS]] attack will flood the server with malicious resources. Trying to handle these requests is useless (and expensive), so it's better to detect them and discard them.

Autoscaling provides [[elasticity]] for your services, allowing you to add resources during peaks like special events or remove resources during weekends. It also improves [[availability]] and [[Fault tolerance]], ensuring that client requests won't be rejected because the instance has crashed.

**Autoscaling isn't the best approach to handling long-term growth.** You might have a web app that starts with a few users but increases in popularity over time. **Autoscaling has an overhead associated with monitoring resources and determining whether to trigger a scaling event**. In this scenario, if you can anticipate the rate of growth, manually scaling the system over time may be a more cost-effective approach.

Autoscaling is also affected by the number of instances of the service. The fewer the number of instances initially, the less capacity you have to handle an increasing workload while autoscaling spins up more instances.

Autoscaling is a feature tightly bound to [[azure-app-service-plan]]. Each Service Plan has an associated scaling limit that cannot be surpassed. Not all service plans support autoscaling. **The development pricing tiers are either limited to a single instance (the F1 and D1 tiers)**, or they only provide **manual scaling (the B1 tier)**. If you've selected one of these tiers, you must first scale up to the S1 or any of the P-level production tiers.

## Autoscale conditions and rules

You indicate how to autoscale by creating **autoscale conditions**. Azure provides two options for autoscaling:

- Scale based on a **metric**, such as the length of the [[disk queue]] or the number of HTTP requests awaiting processing.
- Scale to a specific instance count according to a **schedule**. For example, you can arrange to scale out at a particular time of day or on a specific date or day of the week. You also specify an end date, and the system scales back in at that time.

![Autoscale settings](./autoscale-settings.png)

Scaling to a specific instance count only enables you to scale out to a defined number of instances. If you need to scale out incrementally, you can combine metric and schedule-based autoscaling in the same autoscale condition.

You can create multiple autoscale conditions to handle different schedules and metrics. Azure auto-scales your service when any of these conditions apply.

An App Service Plan also has a **default condition** that is used if none of the other conditions are applicable. **This condition is always active and doesn't have a schedule**.

An **autoscale rule** specifies a metric to monitor and how autoscaling should respond when this metric crosses a defined threshold. The metrics you can monitor for a web app are:

- **CPU Percentage**. This metric is an indication of the CPU utilization across all instances. A high value shows that instances are becoming CPU-bound, which could cause delays in processing client requests.
- **Memory Percentage**. This metric captures the memory occupancy of the application across all instances. A high value indicates that free memory could be running low and could cause one or more instances to fail.
- **Disk Queue Length**. This metric is a measure of the **number of outstanding I/O requests** across all instances. A high value means that disk contention could be occurring.
- **Http Queue Length**. This metric shows **how many client requests are waiting for processing by the web app**. If the length of the [[http queue]] is large, client requests might fail with HTTP 408 (Timeout) errors.
- **Data In**. This metric is the number of bytes received across all instances.
- **Data Out**. This metric is the number of bytes sent by all instances.
- **Custom, Azure-based metrics**: You can define thresholds based on metrics on other Azure resources, such as the number of messages stored in an Azure Service Bus queue.

Autoscale works by analyzing trends in metric values over time across all instances. This analysis is a multi-step process:

1. Aggregate values for the metrics for all instances across a period of time called **time grain**. Generally, the time grain is 1 minute. Then it aggregates the values (available **time grain statistics** are _Average_, _Minimum_, _Maximum_, _Sum_, _Last_, _Count_), and stores the aggreagate value (known as **time aggregation**).
2. After a user-defined period (known as **duration**), the process re-runs the calculations. Duration must be longer than time grain. **The minimum duration value is 5 minutes**.

An autoscale action has a **cool down period**, specified in minutes (minimum 5 minutes), during which the scale rules won't be triggered again. This is done to stabilize the system between autoscale events.

Ideally, **you should pair autoscale rules**: you should create one rule to scale in and one rule to scale out based on the same metric.

**A single autoscale condition can contain several autoscale rules** (for example, a scale-out rule and the corresponding scale-in rule). However, the autoscale rules in an autoscale condition don't have to be directly related.
You could define the following four rules in the same autoscale condition:

- If the HTTP queue length exceeds 10, scale-out by 1
- If the CPU utilization exceeds 70%, scale-out by 1
- If the HTTP queue length is zero, scale-in by 1
- If the CPU utilization drops below 50%, scale-in by 1

When determining whether to **scale out**, the autoscale action is performed if **any** of the scale-out rules are met (HTTP queue length exceeds 10 **or** CPU utilization exceeds 70%).
When **scaling in**, the autoscale action runs only if **all** of the scale-in rules are met (HTTP queue length drops to zero **and** CPU utilization falls below 50%).

If you need to scale in if only one of the scale-in rules is met, you must define the rules in separate autoscale conditions.

All autoscale successes and failures are logged in the Activity Log. You can then **configure an activity log** alert to notify you via email, SMS, or webhooks whenever there's activity.

[See more](https://learn.microsoft.com/en-us/azure/azure-monitor/autoscale/autoscale-understanding-settings).

## Best practices

1. Ensure the maximum and minimum values are different and have an adequate margin between them;
2. Choose the appropriate statistic for your diagnostics metric. The most common statistic is _Average_.
3. Carefully choose the threshold. To avoid **Flapping**, the scale-out and scale-in criteria should be carefully planned.
4. Choose a safe default instance count. It's necessary because, when metrics are not available, the service gets scaled to that number.
5. Configure custom notifications (email, webhook) to get notified when an autoscale activity occurs (or fails).

**Flapping** is when scale-in and scale-out actions continually go back and forth. It happens because when you add a new instance during a scale-out action, the total percentage of resources is lower than before the scale-out action. If it's lower than the scale-in threshold, the scale-in action takes place, returning to the original situation.
