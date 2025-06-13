<details>
<summary><strong> 👉
## Key Network Architecture Principles Across All Projects:
</strong></summary>
  
| Principles | Description | 
|------------|-------------|
| **Security-First Design:** | Every project should incorporate network security controls from the ground up, not as an afterthought. |
| **Scalability Planning:** | Design network solutions that can grow with business needs and handle projected traffic volumes. |
| **Resilience & Redundancy:** | Ensure network designs include appropriate failover mechanisms and eliminate single points of failure. |
| **Performance Optimization:** | Consider latency, bandwidth, and QoS requirements specific to each application or service. |
| **Operational Excellence:** | Design networks that are monitorable, manageable, and supportable by operations teams. |
| **Standards Compliance:** | Ensure all network designs align with enterprise architecture standards and regulatory requirements. |
  
</details>  

# Network Architect Cross-Domain Project Contribution Matrix

| Project Name | Typical Role | Why You're Needed | Network Architect Contribution Items |
|--------------|--------------|-------------------|-------------------------------------|
| **Cyber Security Programs** | Contributor | Microsegmentation, SASE integration | • Design network segmentation strategy and VLAN/VXLAN schemes<br/>• Define firewall placement and security zones architecture<br/>• Assess current network for zero-trust readiness<br/>• Plan SASE edge connectivity and SD-WAN integration<br/>• Review network access control policies and enforcement points<br/>• Design secure network monitoring and logging infrastructure<br/>• Validate bandwidth requirements for security tools and encryption overhead |
| **IAM & Certificate Platforms** | Consultant | Secure device access, NAC, PKI infra | • Design NAC deployment architecture and switch port configurations<br/>• Plan certificate distribution infrastructure and SCEP/CMP protocols<br/>• Assess network readiness for 802.1X authentication<br/>• Design secure RADIUS/LDAP connectivity paths<br/>• Plan network isolation for non-compliant devices<br/>• Review DNS and PKI infrastructure placement<br/>• Design secure management networks for certificate authorities |
| **SaaS Migrations (e.g. O365)** | Contributor | WAN breakout, perf optimization | • Design internet breakout strategy and local egress points<br/>• Plan QoS policies for SaaS traffic prioritization<br/>• Assess WAN bandwidth requirements and upgrade planning<br/>• Design SD-WAN policies for optimal SaaS routing<br/>• Plan DNS optimization and split-DNS configurations<br/>• Review proxy bypass strategies for trusted SaaS traffic<br/>• Design network monitoring for SaaS performance metrics |
| **DevOps & Container Platforms** | Support | Infra, storage, DNS, overlay networking | • Design container networking (CNI) strategy and IP addressing<br/>• Plan overlay network architecture (VXLAN, Calico, etc.)<br/>• Design east-west traffic patterns and service mesh integration<br/>• Plan DNS service discovery and internal load balancing<br/>• Design network policies for container microsegmentation<br/>• Plan ingress/egress controllers and external connectivity<br/>• Assess network performance requirements for distributed storage |
| **Integration Platforms (ESB/API)** | Support | Zoning, infra readiness | • Design API gateway network placement and DMZ architecture<br/>• Plan network security zones for different integration tiers<br/>• Design load balancer architecture for API endpoints<br/>• Plan network monitoring for API traffic patterns<br/>• Design secure connectivity for external partner integrations<br/>• Plan bandwidth and latency requirements for integration flows<br/>• Review network resilience and failover strategies |
| **EUC/VDI Modernisation** | Support | Network latency, profile tuning | • Design low-latency network paths for VDI traffic<br/>• Plan QoS policies for real-time VDI protocols<br/>• Assess network capacity for graphics and multimedia workloads<br/>• Design printing and peripheral network access strategies<br/>• Plan network optimization for profile and application streaming<br/>• Review branch office connectivity for remote VDI access<br/>• Design network monitoring for user experience metrics |
| **Data Platform Initiatives** | Support | Peering, IP range mgmt, transit encryption | • Design data center interconnect architecture<br/>• Plan IP address management and subnet allocation strategies<br/>• Design network encryption for data in transit<br/>• Plan network peering arrangements and BGP routing<br/>• Assess bandwidth requirements for large data transfers<br/>• Design network isolation for sensitive data workloads<br/>• Plan network monitoring for data flow visibility |
| **Observability & ITOM Uplift** | Contributor | Infra telemetry, SNMP, syslog, CMDB | • Design centralized logging and telemetry collection architecture<br/>• Plan SNMP monitoring infrastructure and polling strategies<br/>• Design syslog forwarding and aggregation topology<br/>• Plan network discovery and asset inventory automation<br/>• Design monitoring network isolation and out-of-band management<br/>• Plan bandwidth allocation for monitoring traffic<br/>• Review network device configuration management integration |

