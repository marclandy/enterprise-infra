**User:** Marc Landy 
- **Created:** 5/30/2025 17:33  
- **Updated:** 5/31/2025 16:16  

## CAF ALZ Design Areas: Components

| Legend | Design Area                          | Objective                                                                                         |
|--------|--------------------------------------|---------------------------------------------------------------------------------------------------|
| A      | Azure billing and Active Directory tenant | Proper tenant creation, enrollment, and billing setup are important early steps.                  |
| B      | Identity and access management       | Identity and access management is a primary security boundary in the public cloud. It's the foundation for any secure and fully compliant architecture. |
| C      | Resource organization                | As cloud adoption scales, considerations for subscription design and management group hierarchy have an impact on governance, operations management, and adoption patterns. |
| E      | Network topology and connectivity    | Networking and connectivity decisions are an equally important foundational aspect of any cloud architecture. |
| F      | Security                             | Implement controls and processes to protect your cloud environments.                             |
| D, G, H| Management                           | For stable, ongoing operations in the cloud, a management baseline is required to provide visibility, operations compliance, and protect and recover capabilities. |
| C, D   | Governance                           | Automate auditing and enforcement of governance policies.                                         |
| I      | Platform automation and DevOps       | Align the best tools and templates to deploy your landing zones and supporting resources.         |

---

## CAF ALZ Implementation Option

https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options

---

## **Network Design Decision Workbook** template based on Enterprise ALZ Network Service patterns. 

| Service | Requirement Category | Requirement Description | Available Options |
| --- | --- | --- | --- |
| DNS | Resolution Scope | Should DNS resolve only within VNet, across VNets, or include on-prem? | Private Resolver | Azure DNS | Custom Forwarder | Conditional Forwarding |
| DNS | Zone Management | How are DNS zones created and delegated? | Azure DNS Zones | Manual Zone Delegation | IaC Managed |
| Firewall | Control Plane | What is the central control point for firewall policy? | Azure Firewall | 3rd Party NVA | Hybrid |
| Firewall | Threat Intelligence | How are threat feeds integrated into firewall inspection? | Azure TI | External Feed | None |
| Bastion | Access Scope | What subnets or VMs require secure jump-box access? | All subnets | Selected subnets | Dev/Test only |
| Bastion | Identity Controls | How is access to Bastion controlled? | AAD P2 | PIM | RBAC + Just-in-Time |
| NSGs | Granularity | Should NSG policy be centralized or VNet/subnet-specific? | Centralized via IaC | Delegated to App Teams | Hybrid |
| NSGs | Logging | How is NSG logging captured and analyzed? | NSG Flow Logs v2 | Azure Monitor | 3rd Party SIEM |
| DDoS Protection | Coverage Level | Should DDoS protection be Basic or Standard? | Basic | Standard |
| DDoS Protection | Alerting & Response | How is a DDoS incident detected and acted upon? | Azure Alerts | Manual Review | SOC Integration |
| Routing | Routing Model | What model governs traffic routing between VNets and on-prem? | UDR | BGP via ER/ExpressRoute | Hub/Spoke Propagation |
| Routing | Inspection | Where is routing inspected (e.g. forced tunneling)? | Azure Firewall | NVA | None |

**Usage:**  
workbook - customer workshops or discovery phases to:
*   Confirm business and compliance requirements.  
*   Evaluate and agree on service implementation options.
*   Maintain a source of truth for ALZ customisation decisions.

---

### Azure Landing Zone Preparation → Enterprise-scale Hub and Spoke Mapping Table (Extended)
- Key Design Decisions (Network)
- Lifecycle Considerations (Network Ops)
  
| **CAF Component / Concept**                                | **Enterprise-Scale Hub & Spoke Implementation**                                                                                   | **Deployment Script / Bicep / Terraform Reference**                                                                                     | **Key Design Decisions (Network)**                                                                                              | **Lifecycle Considerations (Network Ops)**                                                                                       |
|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| **Management Groups Hierarchy**                             | Implements standard ALZ hierarchy (Platform, Landing Zones, Identity, Connectivity, etc.)                                          | [Terraform - Management Groups](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale/tree/main/modules/management-groups)  | Decide where network services (Firewall, DNS, Bastion) live — Platform or Connectivity MGs                                     | Review MG alignment with evolving service ownership (e.g., central vs. BU-managed networking)                                    |
| **Subscription Design**                                     | Uses predefined subscription archetypes (Management, Identity, Connectivity, Landing Zone)                                         | [Terraform - Scenarios](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale/tree/main/scenarios)                          | Assign network infra (e.g., vWAN or Hub VNets) to dedicated subscriptions for lifecycle separation                             | Adjust subscription boundaries if network scale or service tiers evolve                                                          |
| **Networking Topology**                                     | Hub-and-Spoke using Azure Virtual WAN or traditional VNet peering for regional or global scale                                     | [Terraform - Networking Module](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale/tree/main/modules/networking)         | Choose between vWAN and custom Hub (e.g., NVA vs. Azure Firewall)                                                               | Validate routing updates, NVA scaling, IP space management, and regional resiliency over time                                    |
| **Identity and Access Management**                          | Delegated administration model, RBAC assignments, Azure AD integration                                                              | [Bicep - Role Assignments Module](https://github.com/Azure/Enterprise-Scale/blob/main/ESLZ-Bicep/bicep/modules/roleAssignments.bicep)  | Network Role Definitions (e.g., Network Contributor, DNS Reader) — define early                                                  | Regularly audit access (Privileged Identity Management), especially for third-party MSP access                                  |
| **Security & Governance Policies**                          | Baseline policies for resource locks, allowed regions, naming conventions, diagnostic settings, etc.                               | [Enterprise Policy-as-Code (EPAC)](https://azure.github.io/enterprise-azure-policy-as-code/)                                           | Define NSG/UDR allowed patterns, Azure Firewall default policy sets, and segmentation boundaries                                | Refine policies based on threat landscape and compliance feedback loops                                                          |
| **Logging & Monitoring**                                    | Azure Monitor diagnostic settings and Log Analytics workspace integration                                                           | [Bicep - Monitoring Module](https://github.com/Azure/Enterprise-Scale/blob/main/ESLZ-Bicep/bicep/modules/monitor.bicep)                | Choose logging tiers (Firewall, NSG Flow Logs, DNS, AppGW), define log retention for audit trail                                | Monitor logs for network health, SIEM integration, and alert noise tuning                                                        |
| **Platform Automation (IaC)**                               | Supports both Bicep and Terraform. Modular IaC pattern using ALZ modules                                                            | [Terraform](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale), [Bicep](https://github.com/Azure/Enterprise-Scale)       | Integrate network modules (e.g., Firewall Policy, Route Tables) into deployment pipelines                                        | Enforce IaC drift detection, tagging, and versioned modules                                                                      |
| **Connectivity (Firewall, VPN, ExpressRoute, Bastion)**     | Optional modules for Azure Firewall, Azure Bastion, ExpressRoute Gateway, etc.                                                      | [Terraform - Connectivity Modules](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale/tree/main/modules/connectivity)     | Evaluate need for ER Gateway redundancy, route propagation settings, Firewall DNAT vs App Gateway patterns                      | Monitor latency and throughput baselines, maintain Gateway SKUs, support scaling events (e.g., campaigns, DR)                    |
| **Tagging and Resource Organization**                       | Configured via policy & custom modules. Enforces metadata such as environment, owner, cost center, etc.                            | [Bicep - Tags Module](https://github.com/Azure/Enterprise-Scale/blob/main/ESLZ-Bicep/bicep/modules/tags.bicep)                         | Include "ZoneType", "NetworkBoundary", "ManagedBy" tags to filter NSGs, routing tables, DNS zones                               | Maintain tag hygiene for network diagnostics, enforce tag inheritance through policies                                           |
| **Blueprint or Template Selection**                         | Offers opinionated design decisions that align with CAF guidance                                                                   | [Hub & Spoke Scenario](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale/tree/main/scenarios/hub-spoke-networking)      | Choose scenario fit (e.g., Regional Hub per jurisdiction), assess template extensibility for custom DNS/firewall                | Revalidate base templates annually against updated ALZ patterns and new Azure networking services                                |

- key components listed in that page and how they are implemented when you select the Enterprise-scale hub and spoke deployment option
- understand how each foundational element of an ALZ is translated into deployable, repeatable infrastructure components


## Appendix

ALZ: CAF 
- Landing Zone: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/
- Design Areas: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-areas

alz-visio
- https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/ready/enterprise-scale-architecture.vsdx
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/media/azure-landing-zone-architecture-diagram-hub-spoke.svg

extract tables from | Environment design areas
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-areas#environment-design-areas
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-areas#compliance-design-areas

extract tables from | Azure platform landing zone deployment option
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options#azure-landing-zone-accelerator-approach
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options#customize-approach

extract tables from | network and connectivity
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/network-topology-and-connectivity
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/media/azure-landing-zone-architecture-diagram-hub-spoke.svg

azure-landing-zones-journey
- https://azure.github.io/Azure-Landing-Zones/#the-azure-landing-zones-journey
- https://azure.github.io/Azure-Landing-Zones/img/customer-landing-zone-journey.png

Network & Connectivity 
- https://aacsessionslides.blob.core.windows.net/sessionslides/ESLZ_NetworkDeepDive_AAC.pdf
- https://github.com/Azure/Enterprise-Scale/blob/main/docs/EnterpriseScale-Deploy-reference-implentations.md
- https://github.com/Azure/Enterprise-Scale/wiki/ALZ-Deploy-reference-implementations


