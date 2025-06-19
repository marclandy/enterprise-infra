
# Azure Networking Architecture Summary for Network & Infrastructure Architects

This summary extracts the most essential patterns, design decisions, and Azure networking component usage from *Azure Networking* by Adam Stuart & Jose Moreno. It is structured around the core themes:

> **>>> azure network components, component tradeoffs based on topologies, pattern definitions, selection components, explore design options <<<**

---

## 1. Introduction
- **Pattern Definitions**: Sets the stage for Azure Networking importance.
- **Azure Network Components**: IaaS vs. PaaS basics, certification (AZ-700).

## 2. Azure Networking Fundamentals
- **Azure Network Components**: VNets, subnets, NICs, routing (UDR/System), Load Balancer, NVA.
- **Component Tradeoffs**: Public vs. private access, peering vs. gateway.
- **Explore Design Options**: Multi-VNet, DNS, latency.

## 3. Before the Whiteboard, Requirements
- **Selection Components**: SLAs, DR, hybrid, security, performance, cost.
- **Pattern Definitions**: Zero Trust, remote access, DR/RTO models.
- **Component Tradeoffs**: VPN vs. ExpressRoute, cost implications.

## 4. Network Topology
- **Pattern Definitions**: Hub-and-spoke, tiered, AVNM, VWAN.
- **Component Tradeoffs**: Routing scopes, direct connectivity.
- **Explore Design Options**: Custom topologies, disconnected VNets.

## 5. Connectivity to On-premises
- **Azure Network Components**: VPN Gateway, ExpressRoute, AVS.
- **Selection Components**: Redundancy models (bow-tie/square).
- **Explore Design Options**: Coexistence of VPN + ExpressRoute.

## 6. Software-defined Wide Area Networking (SD-WAN)
- **Pattern Definitions**: Cloud-ready SD-WAN overlays.
- **Selection Components**: Integration with VWAN, BGP/IPSec.
- **Component Tradeoffs**: ZTP, NVA-in-hub vs. colocated.
- **Explore Design Options**: Intra-Azure WAN.

## 7. Multicloud Networking
- **Pattern Definitions**: Underlays/overlays, edge models.
- **Component Tradeoffs**: VPN vs. SD-WAN vs. overlay fabric.
- **Explore Design Options**: Shadow IT, M&A-driven design.

## 8. Security
- **Azure Network Components**: NSG, ASG, Firewall, NVA, SSE.
- **Pattern Definitions**: East-West/North-South, GWLB, HA.
- **Component Tradeoffs**: Autoscaling, rule management.
- **Selection Components**: AVNM security rules, UDR drops.

## 9. DNS and Platform as a Service
- **Azure Network Components**: Private DNS, Resolver, Traffic Manager.
- **Pattern Definitions**: Hybrid DNS, custom DNS, PaaS DNS.
- **Component Tradeoffs**: Service Endpoints vs. Private Link.
- **Explore Design Options**: Multi-region DNS integration.

## 10. Application Delivery
- **Pattern Definitions**: L4/L7 load balancers (ALB, AppGW, AFD).
- **Azure Network Components**: Ingress controllers, WAF, NGINX.
- **Component Tradeoffs**: Regional vs. global vs. private delivery.
- **Explore Design Options**: App Gateway + AFD + Kubernetes.

## 11. Management and Monitoring
- **Azure Network Components**: Network Watcher, Monitor, Bastion.
- **Pattern Definitions**: SNMP, packet capture, route inspection.
- **Component Tradeoffs**: CLI vs. Portal, cost insights.
- **Explore Design Options**: IPAM, Azure Policy, IaC, VNet flow logs.

---

## 🧠 Reference Repositories
- [Jose Moreno (erjosito)](https://github.com/erjosito)
- [Adam Stuart (adstuart)](https://github.com/adstuart)
