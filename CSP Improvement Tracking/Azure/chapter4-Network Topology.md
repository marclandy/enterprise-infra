
# Chapter 4: Routing and Network Segmentation in Azure

## Objective

Define scalable and secure routing strategies for hybrid and cloud-native workloads using Azure-native constructs including UDRs, NSGs, Route Tables, and NVAs.

## 1. Core Routing Constructs

- **User Defined Routes (UDRs)**
- **System Routes**
- **BGP Route Propagation**
- **Virtual Network Peering Routing Considerations**

```mermaid
graph TD
    A[VNet A] --Peering--> B[VNet B]
    B --> C[Route Table with UDRs]
    C --> D[NVA / Firewall]
```

## 2. Hub-and-Spoke Topology with Segmentation

- Central hub with inspection point (Azure Firewall / NVA)
- Spokes with route tables directing default route to hub

```mermaid
graph TD
    A[Spoke VNet] --> B[Route Table]
    B --> C[Hub VNet]
    C --> D[Firewall/NVA]
    D --> E[Internet / On-Prem]
```

## 3. NSG and ASG Use Cases

- Layer 4 access control per subnet/VM
- Application groupings with ASGs

## 4. Common Patterns

| Pattern | Description |
|--------|-------------|
| Hub-and-Spoke | Centralized security and connectivity |
| Firewall Sandwich | NVA in HA pair between tiers |
| Segmented VNet | Subnets with NSG/UDR control |

