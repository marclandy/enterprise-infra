**User:** Marc Landy 
- **Created:** 5/30/2025 17:33  
- **Updated:** 5/31/2025 16:16  

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
    
