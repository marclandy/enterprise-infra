### 🔹 Cisco SD-WAN Design Model Options Summary (My Notes)

| Model # | Model Name | Description |
| --- | --- | --- |
| 1 | Traditional (non-SD-WAN) | Static routing, IPSec, MPLS—high TCO, low agility |
| 2 | Classic Over-engineered SD-WAN | Multi-controller, HA everything, focused on large-scale resilience, may be overkill for mid-tier |
| 3 | Network as a Service + DIA | Lean WAN, internet-first with optional SD-WAN overlay—ideal for cost control |
| 4 | SD-WAN + SSE | Integrated security with ZTNA/SASE principles (Prisma Access, Umbrella, Netskope etc.)—modern, scalable |

* * *

🔸 Cisco SD-WAN (Viptela/Catalyst) vs Meraki SD-WAN Comparison Table
--------------------------------------------------------------------

| Feature/Aspect | **Cisco SD-WAN (Viptela/Catalyst)** | **Meraki SD-WAN (MX Series)** |
| --- | --- | --- |
| **Target Market** | Medium to large enterprise | SMB to mid-market & distributed enterprises |
| **Architecture Type** | Controller-based (vManage, vBond, vSmart) | Cloud-managed (Meraki Dashboard) |
| **WAN Overlay** | Advanced: App-aware routing, multiple TLOCs, BFD, SLA monitoring | Simplified: Dual uplinks, load balancing, basic policy-based routing |
| **Security Integration** | Native: Umbrella, ZScaler, IPS, Zone-based FW | Native NGFW, IDPS, content filtering, Umbrella integration |
| **Management Interface** | CLI + vManage GUI (complex, flexible) | Meraki Dashboard (intuitive, GUI-first) |
| **Failover/HA** | High: Multiple TLOCs, real-time failover, DCI options | Medium: Warm/Hot spare MXs, failover between WAN ports |
| **Analytics & Monitoring** | Deep: App visibility, SLA performance, telemetry to vAnalytics | Moderate: Summary reports, alerts, SD-WAN performance stats |
| **Cloud Access Optimization** | Cloud OnRamp (SaaS, IaaS optimized ingress) | Auto-VPN to cloud hubs, SD-WAN policies to cloud edge |
| **SASE Readiness** | Full: Integrates easily with SSE solutions (Umbrella, PAN, Prisma) | Partial: Supports Umbrella and some third-party FWaaS |
| **Licensing Model** | DNA Advantage/Prem with optional security bundles | Advanced Security License for SD-WAN/Security |
| **Implementation Complexity** | High: Best for large or segmented networks | Low: Quick to deploy, ideal for IT lean environments |
| **API & Automation** | Yes: vManage REST APIs, Ansible modules | Limited: Webhooks, API access (but less granular) |
| **ZTP (Zero-Touch Provisioning)** | Supported (Plug-n-Play via vManage) | Supported (Out-of-box via Meraki Dashboard) |
| **Best Fit Use Case** | Complex topologies, hybrid DC/cloud, high app segmentation | Rapid deployment, lean IT ops, retail/branch-heavy networks |

* * *

🔸 Strengths & Weaknesses Summary
---------------------------------

### ✅ Cisco SD-WAN (Viptela/Catalyst)

* **Strengths**
    
    * Enterprise-grade control and segmentation
        
    * Suits hybrid WAN with MPLS/Internet/SASE
        
    * Robust controller-driven model for app-SLA enforcement
        
    * Integrates seamlessly into larger Cisco ecosystems
        
* **Weaknesses**
    
    * Higher TCO (HW + DNA licenses + controllers)
        
    * Complex to implement/manage without strong IT maturity
        
    * Longer ramp-up for ZTP and site deployment
        

* * *

### ✅ Cisco Meraki SD-WAN

* **Strengths**
    
    * Rapid provisioning and centralized GUI management
        
    * Ideal for lean IT teams
        
    * Full-stack Meraki (Switch, Wi-Fi, Camera) benefits
        
    * Security + SD-WAN bundled in MX with minimal overhead
        
* **Weaknesses**
    
    * Less granular control for routing/SLA/path policies
        
    * Scalability capped for very large WANs
        
    * Limited SSE-native support compared to Viptela + Umbrella/Prisma combo
        

* * *

🔸 Suggested Models for Mid-Tier Construction Customer
------------------------------------------------------

### A. **Meraki SD-WAN with Umbrella + AutoVPN Hubs**

* _Architecture:_ Spoke-Hub with MX at each branch + cloud-hosted services
    
* _Use Case:_ Lean, quick setup for mobile construction offices and depots
    
* _Security:_ Enable Advanced Security + Umbrella integration
    

### B. **Cisco SD-WAN (Viptela) with Direct Internet Access + SSE (Umbrella or Prisma)**

* _Architecture:_ DIA-first model with centralized SSE policy enforcement
    
* _Use Case:_ If customer has regional data centers or larger core infrastructure
    
* _Security:_ Integrate SASE stack and enforce ZTNA policies
    

* * *
