---
tags: azure, cloud, azure-certifications/az900, security, aws
---

# Microsoft Defender for Cloud

Defender for Cloud is a **monitoring tool** for security management and threat protection, allowing for [[Cloud Security Posture Management]] features to be available in the cloud.

It monitors different environments: cloud, on-prem, hybrid, and multi-cloud.

Defender for Cloud can automatically deploy a **Log Analytics agent** to gather security-related data when necessary.

## Azure protections

Microsoft Defender is already integrated with Azure. Many Azure services are monitored and protected by default with Microsoft Defender.

It works with several PaaS services, such as [[azure-app-service]], [[Azure SQL]], and [[azure-storage-account-scripts]]. It watches for anomalies in the activity logs.

When working with [[Azure SQL]], it can automatically classify data and assess for vulnerabilities in your storage.

Finally, it adds security to the **network connectivity** by monitoring endpoints, ports, and allowed IP addresses.

## Hybrid cloud

Microsoft Defender can work with hybrid environments, where part of the infrastructure is stored in on-premises servers. **Defender for Cloud** can be deployed on on-prem machines using [[azure-arc]].

## Multicloud

If you have an external cloud vendor connected to an Azure subscription, you can enable Defender for Cloud.

In the case of an integration with AWS, you can use:

- **Defender for Cloud**'s CSPM features extend to your AWS resources. This agentless plan assesses your AWS resources according to AWS-specific security recommendations. It includes the results in the secure score.
- **Microsoft Defender for Containers** extends its container threat detection and advanced defences to your Amazon EKS Linux clusters.
- **Microsoft Defender for Servers** brings threat detection and advanced defences to your Windows and Linux EC2 instances.

## Pillars of Defender for Cloud

### Continuously assess

There is a continuous resource assessment to look for vulnerabilities in VMs, SQL server instances, and more.

You also have vulnerability scans that cover your computing, data, and infrastructure.

### Improve resource security

You have to secure your workloads by defining security policies. In Defender for Cloud, you can set your policies to run on management groups, across subscriptions, and even for a whole tenant.

Defender for Cloud constantly monitors new resources being deployed across your workloads.

Defender for Cloud assesses if new resources are configured according to security best practices.

Defender for Cloud creates a set of recommendations for each resource to help you reduce the attack surface across each resource. Recommendations are grouped by type and given a score to help you understand at a glance the current health of your security posture.

### Defend

Create alerts when a threat is detected in your environment. Each alert contains the details of the resource as well as some remediation steps.

Alerts can be correlated to understand the history of a threat.
