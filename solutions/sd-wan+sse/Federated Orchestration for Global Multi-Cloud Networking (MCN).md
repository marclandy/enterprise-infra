# Federated Orchestration for Global Multi-Cloud Networking (MCN) | status: draft

**Service Architecture Pattern Document**

## 1. Executive Summary

The following Service Architecture Pattern outlines a future-ready model for enabling federated orchestration across global connectivity providers, cloud platforms, enterprise WANs, and security fabrics. It is designed to support large enterprises undergoing digital and data transformation, particularly those with globally distributed operations, M&A activity, and a mix of IT/OT workloads. 

The pattern emphasizes software-defined, API-driven service composition and delivery, integrating traditional telco capabilities (e.g., BT, Orange) with interconnect specialists (e.g., Equinix, Megaport) and cloud-native service fabric providers (e.g., Cato, Zscaler, Coevolve).

## 2. Business Drivers

- Accelerated cloud and SaaS adoption across business units
- Increasing reliance on third-party partners and managed service providers
- Demand for just-in-time onboarding of new sites due to M&A
- Security posture shift towards Zero Trust and least-privileged access
- Operational efficiency and automation at the global WAN edge

## 3. Strategic Goals

- Enable dynamic provisioning of end-to-end services across regions and providers
- Centralize visibility, policy enforcement, and identity-driven access
- Abstract complexity of underlay telco infrastructure
- Federate orchestration responsibilities across domains and teams
- Provide a single operating model for global connectivity and access

## 4. Key Stakeholders

| Stakeholder | Responsibility |
|-------------|----------------|
| Enterprise Network Team | Design and manage WAN, interconnects, and SD-WAN overlays |
| Security Architects | Define Zero Trust, SSE, and identity federation models |
| Cloud Platform Teams | Manage CSP landing zones, VNets/VPCs, cloud routers |
| Service Providers (e.g., BT, Orange) | Provision physical circuits and managed CPEs |
| Interconnect Providers (e.g., Equinix, Megaport) | Enable on-demand IX/CX capacity |
| Managed SASE/MSP Partners (e.g., Coevolve) | Integrate and orchestrate end-to-end service across components |

## 5. Core Services & Capabilities

- **Connectivity-as-a-Service (CaaS)**: Consumption-based transport capacity delivered via IX/CX APIs
- **SD-WAN Overlay Fabric**: Application-aware routing and failover
- **SASE/SSE Integration**: Inline security (SWG, CASB, DLP, ZTNA)
- **Cloud Interconnect**: Direct peering with hyperscalers (AWS, Azure, GCP)
- **Federated Orchestration Layer**: Policy engine, telemetry, and API coordination across domains
- **ZTNA for B2B/3rd Party Access**: Role- and risk-based access control with full audit visibility

## 6. The Opportunity — Full-Scope MCN Orchestration 

While existing solutions provide integrated overlays and security controls, most do not orchestrate the full physical and logical path: from enterprise edge to CSP tenant, through IX/CX fabrics and cloud routers, to SaaS front doors or data pipelines.

This federated model highlights a clear opportunity:

- Stitching connectivity services across providers
- Providing secure, policy-based remote access
- Dynamically brokering underlay and overlay capacity

This is especially vital for enterprises undergoing rapid expansion, M&A, or OT/IT convergence.


## 7. Logical Architecture Overview

```
+---------------------------+     +---------------------------+
| Enterprise Edge Sites     |<--->| SD-WAN / SASE Fabric     |
| (Factories, HQ, Branches) |     | (Cato, Zscaler, Prisma)  |
+---------------------------+     +---------------------------+
             |                                 |
             v                                 v
+---------------------------+     +---------------------------+
| IX/CX Fabric (Megaport,   |<--->| Cloud Interconnect (CSPs) |
| Equinix, ConsoleConnect)  |     | AWS DX, Azure Peering,    |
+---------------------------+     | GCP                       |
             |                    +---------------------------+
             v                                 |
+---------------------------+                  v
| Telco / Circuit Underlay  |<--->+---------------------------+
| (BT, Orange, AT&T)        |     | Federated Orchestration   |
+---------------------------+     | Hub (e.g., Coevolve,      |
                                  | Custom NOC)               |
                                  +---------------------------+
```

## 8. Operating Model Options

| Model | Description |
|-------|-------------|
| **Fully Managed** | External partner handles orchestration, support, SLAs |
| **Co-Managed** | Enterprise manages policies; partner operates network fabric |
| **Self-Managed + Orchestration-as-a-Service** | Internal team runs stack with external orchestration support |

source: service models adapted from [Coevolve](https://www.coevolve.com/wp-content/uploads/2023/04/Managed_vs_co_managed_diagram-768x768.png)

## 9. Use Cases

- **M&A Onboarding**: Rapid integration of acquired entities into existing cloud and WAN environments
- **Remote OT & SCADA Access**: Secure and optimized paths for telemetry and control systems
- **Third-Party Collaboration**: Conditional access for vendors and service partners using ZTNA
- **Multi-Cloud Peering**: Seamless transport across CSP tenants for distributed workloads
- **SaaS Acceleration**: Performance optimization for Microsoft 365, Salesforce, Zoom, etc.

## 10. Recommendations for Next Steps

1. Establish customer connectivity requirements across, Telcos, SD-WAN, SASE, cloud, SaaS.
2. Map existing provider and platform relationships (Telco, IX/CX, Cloud)
3. Identify orchestration silos (network, cloud, security, identity)
4. Conduct a PoC with a provider ( Coevolve or Expereo )
5. Develop a Federated Service Catalog and standard API interface set
6. Establish governance around SLA, security policy, and identity roles across domains
7. Assess Network Automation Strategy. Revise/refresh the enterprise network roadmap, as per this proposal (including an evaluation of *Intent-Driven Automation*).

## Conclusion: Federated Orchestrator Proposal 

This model acknowledges the policy-plane convergence achieved by companies like Cato—consolidating SD-WAN, SSE, and ZTNA into a unified, managed service. However, enterprise-scale needs such as industrial M&A, remote OT control, and global SaaS optimization demand deeper orchestration across IX fabrics, CSP edge presence, and telco underlay coordination. Independent players like Coevolve have the neutrality and flexibility to deliver this model at scale—especially when combined with infrastructure players like Equinix or Megaport.

This proposal enables enterprises to abstract service delivery complexity, automate site-to-cloud-to-partner provisioning, and bring network, security, and cloud stakeholders under a federated operating envelope. This isn't a reinvention of SD-WAN—it's the logical next phase: dynamic, intent-driven, and API-first connectivity that behaves more like DevOps pipelines than legacy WAN provisioning workflows.

## Appendix: 

### Use Cases for Industrial Customers

- **Oil & Gas**: Federated orchestration to onboard remote rigs to cloud-based SCADA
- **Mining**: Secure ZTNA access for remote contractors during exploration
- **Manufacturing**: Connecting new production lines during global joint ventures

### Strategic Model: Federated Orchestration for Global Enterprise Edge

```
+---------------------------+     +---------------------------+
| Enterprise Edge           |<--->| Global Orchestrator       |<---> APIs to:
| (Branch, OT, Factory)     |     | (e.g., Coevolve, etc.)   |      - Megaport, Equinix Fabric
+---------------------------+     +---------------------------+      - SASE (Netskope, Zscaler)
             ^                                 ^                      - CSP (AWS, Azure, GCP)
             |                                 |
             |            +-------------+     +------------------+
             |            | ZTNA /      |---->| Identity Hub     |
             |            | SSE / FWaaS |     | (Azure AD, Okta) |
             +------------|             |     +------------------+
                          +-------------+
```

### **Enterprise Connectivity Needs | Delivery View**

| **Connectivity Domain** | **Customer Requirement** | **Products / Services** | **Professional Services Scope** | **Operational/Managed Services Needs (TBA)** |
| --- | --- | --- | --- | --- |
| **Telcos** | Global underlay, last mile, private MPLS/Internet links | • Ethernet, MPLS, Internet  
• DIA  
• Layer 2/3 circuits | • WAN architecture  
• Circuit design  
• Diversity planning | • Circuit monitoring  
• SLA enforcement  
• Trouble ticketing  
• Provider management |
| **SD-WAN** | Overlay abstraction, app-aware routing, resiliency | • Cisco Viptela, Fortinet, Aruba, Silver Peak  
• Co-managed appliances | • SD-WAN design & migration  
• QoS policy modeling  
• BGP/MPLS overlay design | • Device config mgmt  
• App telemetry  
• Failover mgmt  
• Zero-touch provisioning |
| **SASE** | Inline security at edge, policy convergence, remote users | • Zscaler, Netskope, Prisma Access, Cato, Versa | • SASE architecture design  
• Integration with IDP (Azure AD, Okta)  
• Traffic steering logic | • Policy updates  
• User access management  
• Threat analytics  
• Tunnel monitoring |
| **Cloud (CSP)** | Tenant-to-tenant, DC-cloud, B2B/B2C flows, native routing | • AWS TGW, Azure vWAN, GCP NCC  
• Direct Connect/ExpressRoute  
• Cloud Routers | • VNet/VPC design  
• Cloud interconnect strategy  
• BGP & IP address design | • Peering validation  
• Inter-region path health  
• Cost & usage optimization |
| **SaaS** | Optimized access, traffic steering, identity-aware routing | • Microsoft 365, Salesforce, Workday acceleration via SASE or SD-WAN | • SaaS path optimization  
• Conditional access policies  
• DLP/SWG/Proxy integrations | • App experience telemetry  
• Threat analytics  
• DNS/IP filtering |
| **MCN Strategy** | Unified model, federation of control, orchestration layer | • Coevolve, Expereo, Megaport, Equinix Fabric  
• Federated API Gateways | • Federated orchestrator design  
• Inter-domain policy modeling  
• Lifecycle automation planning | • Unified NOC/SOC  
• SLA visibility across domains  
• Multi-provider automation gateway |

Table X: **Federated Orchestration as a Service**. It provides a **multi-dimensional view** linking enterprise **business connectivity needs** with **technology**, **design**, and **run-model considerations**.

### Global Products to Investigate as part of this proposal

- Cloud-Native WAN-as-a-Service
- Global Internet Services:
- Managed Network-as-a-Service (MNaaS):
- SD-WAN and SASE Solutions:

### Vendor Comparison — Orchestration Responsibility Matrix: Cato vs. Coevolve

| Capability | Cato Networks | Coevolve / Federated Orchestrator |
|------------|---------------|-----------------------------------|
| SD-WAN Overlay | ✔ Integrated | ✔ Integrated or Multi-vendor |
| SSE / ZTNA | ✔ Native | ✔ Integrated (Zscaler, Netskope, etc.) |
| CSP Interconnect Management | ✖ Not Provided | ✔ Federated via IX or Telco |
| Underlay Path Diversity | ✖ Customer-provided or BYOB | ✔ Brokered via partners (BT, Orange) |
| IX / CX Automation | ✖ Not integrated | ✔ Enabled via Equinix/Megaport APIs |
| 3rd Party Access (OT / B2B / M&A) | ✔ Supported, policy-driven | ✔ Supported + federated access control |
| SLA / Telemetry Federation | Partial (within Cato fabric only) | ✔ Full observability across domains |
| Federated API Governance | ✖ Limited / Internal APIs | ✔ Supports multi-domain automation |

### Intent-driven automation

**Itential and Selector partnership investigation**
- deliver real-time, closed-loop automation for enterprise and service provider infrastructure teams
- investigate the combined capability : "By combining real-time event detection and root cause identification from Selector with policy-driven orchestration and automated remediation from Itential, teams can now detect, diagnose, and resolve issues across hybrid environments automatically — with no manual intervention required."

### References

MCN 4 Towers concept: 
- 1) Enterprise Landing Zone,
- 2) Enterprise WAN,
- 3) Inter-Cloud Tenant + DC/Site/Remote Access,
- 4) Complex & Business-Critical Application flows. 
- Concept adapted from Kyndryl, Robert DeWeese.

* * *

---
