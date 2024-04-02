---
tags: azure, cloud, azure-certifications/az900, azure-cli, networking
---

# Operations on Azure Virtual Network with Cloud CLI

This page lists some scripts useful for operating on [[azure-virtual-network]].

## List Network Security Groups

With this script you can list the [[azure-virtual-network]] that are associated with your VM:

```bash
az network nsg list
  --resource-group  ID-RESOURCE-GROUP
  --query '[].name'
  --output tsv
```

## List all rules associated with a Security Groups

```bash
az network nsg rule list
  --resource-group ID-RESOURCE-GROUP
  --nsg-name my-vmNSG
```

will return

```json
[
  {
    "access": "Allow",
    "destinationAddressPrefix": "*",
    "destinationAddressPrefixes": [],
    "destinationPortRange": "22",
    "destinationPortRanges": [],
    "direction": "Inbound",
    "etag": "W/\"82cb791f-ba84-474a-9480-40e40ee60f2a\"",
    "id": "/subscriptions/a-guid/resourceGroups/resource-group-id/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/default-allow-ssh",
    "name": "default-allow-ssh",
    "priority": 1000,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "resource-group-id",
    "sourceAddressPrefix": "*",
    "sourceAddressPrefixes": [],
    "sourcePortRange": "*",
    "sourcePortRanges": [],
    "type": "Microsoft.Network/networkSecurityGroups/securityRules"
  }
]
```

You can return a subset of those fileds by specifying only the fields you need (you can even rename them):

```bash
--query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}'
```

## How to add a security rule on an existing Security Groups

```bash
az network nsg rule create
  --resource-group RESOURCE-GROUP-ID
  --nsg-name SECURITY-GROUP-ID
  --name RULE-NAME
  --protocol tcp
  --priority 100
  --destination-port-range 80
  --access Allow
```
