---
tags: azure, cloud, azure-certifications/az900 networking
---

# Azure DNS

It's a [[DNS]], so it provides name resolution by using Microsoft Azure infrastructure.

Azure DNS uses [[anycast networking]], so each [[DNS query]] is answered by the closest available DNS server to provide fast performance and high availability for your domain.

You can use [[azure-rbac]] to controll access to specific actions.

All the operations on the DNS are tracked and logged, so that you can find errors details when troubleshooting.

Azure DNS also supports private DNS domains, allowing you to use your own custom domain names.

Azure DNS supports [[alias record]] sets; you can use an alias record set to refer to an Azure resource and, in case it changes, the DNS records are automatically updated.
