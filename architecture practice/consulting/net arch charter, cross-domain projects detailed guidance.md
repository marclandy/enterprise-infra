# Detailed Network Architecture Guidance by Project Type

Guidance document designed to provide direction based on encountered projects from the field with common scenarios. 
- This document is to be used as a guide only. 
- Establishing customer requirements per project is paramount to ensuring great outcomes are achieved for the enterpise projects teams. 

---

## Enterprise Architecture Integration Summary

**New Standards Required:**
1. Zero Trust Network Architecture Standard
2. Container Platform Network Architecture Standard  
3. Virtual Desktop Infrastructure Network Standard
4. Enterprise Data Platform Network Architecture Standard
5. Multi-Tenant Observability Architecture Standard

**Existing Standards Updates:**
1. Enterprise Network Security Standard → Add microsegmentation
2. PKI Infrastructure Standard → Add network isolation requirements  
3. End User Computing Standard → Add multi-cloud VDI networking
4. Enterprise Monitoring Standard → Add cloud-native requirements

**Common Network Patterns Across All Projects:**
- **Management Networks:** 192.168.100.0/22 (OOB) + 172.16.0.0/12 (In-band)
- **DMZ Zones:** 10.100.0.0/16 
- **Application Networks:** 10.0.0.0/8 with /16 per major system
- **Cloud Integration:** ExpressRoute/DirectConnect with BGP routing
- **Security Zones:** Microsegmentation with VXLAN overlays
  
<details>
<summary><strong> 1. Cyber Security Programs </strong></summary>

### Network Segmentation Strategy & VLAN/VXLAN Schemes

**Design Decision Framework:**
- **Macro-segmentation:** Business unit/function-based (Finance, HR, Engineering)
- **Micro-segmentation:** Application tier-based (Web, App, DB)
- **Zero-trust zones:** Device trust levels (Managed, BYOD, Guest, IoT)

**Common IP Addressing Pattern:**
```
Corporate Core: 10.0.0.0/8
├── Finance Zone: 10.10.0.0/16
│   ├── Finance Workstations: 10.10.1.0/24
│   ├── Finance Servers: 10.10.10.0/24
│   └── Finance DMZ: 10.10.100.0/24
├── Engineering Zone: 10.20.0.0/16
│   ├── Dev Environment: 10.20.1.0/24
│   ├── Test Environment: 10.20.2.0/24
│   └── Prod Access: 10.20.10.0/24
└── DMZ Zones: 10.100.0.0/16
    ├── Web DMZ: 10.100.1.0/24
    ├── App DMZ: 10.100.2.0/24
    └── Partner DMZ: 10.100.10.0/24
```

**VXLAN Design Pattern:**
- VNI 1000-1999: Corporate zones
- VNI 2000-2999: DMZ zones  
- VNI 3000-3999: Management networks
- VNI 9000-9999: Quarantine/remediation

**Standards Reference Required:**
- Update Enterprise Network Security Standard to include microsegmentation requirements
- Develop new "Zero Trust Network Architecture" standard section

### Firewall Placement & Security Zones Architecture

**Three-Tier Security Model:**
1. **Perimeter Firewalls:** Internet edge, partner connections
2. **Internal Segmentation Firewalls:** Inter-zone traffic control
3. **Host-based Firewalls:** Endpoint protection

**Design Decision Matrix:**
- High-security zones: Stateful inspection + DPI
- Medium-security zones: Stateful inspection
- Low-security zones: Access control lists

### SASE Edge Connectivity & SD-WAN Integration

**Integration Pattern:**
- Primary: SASE cloud pop (99% traffic)
- Backup: On-premises firewall (1% + failover)
- Management: Dedicated OOB network

**Bandwidth Planning:**
- 2x current internet bandwidth for SASE overhead
- QoS marking preservation through SASE fabric

</details>  

---

## 2. IAM & Certificate Platforms (Microsoft Cloud PKI + Cisco ISE)

### NAC Deployment Architecture & Switch Port Configurations

**802.1X Deployment Phases:**
1. **Phase 1:** Wired corporate devices (low risk)
2. **Phase 2:** Wireless devices (medium risk) 
3. **Phase 3:** IoT/specialty devices (high complexity)

**Switch Port Template Standards:**
```
interface GigabitEthernet1/0/1
 description Corporate-Wired-Access
 switchport mode access
 switchport access vlan 100
 authentication event fail action authorize vlan 999
 authentication host-mode multi-auth
 authentication port-control auto
 dot1x pae authenticator
 spanning-tree portfast
```

**VLAN Assignment Pattern:**
- VLAN 100-199: Authenticated corporate devices
- VLAN 200-299: Authenticated contractor devices  
- VLAN 300-399: Authenticated IoT devices
- VLAN 999: Quarantine/guest network

### Certificate Distribution Infrastructure

**PKI Network Design:**
```
Root CA: Offline (air-gapped)
├── Issuing CA Tier 1: 172.16.10.0/24 (Primary DC)
├── Issuing CA Tier 2: 172.16.11.0/24 (DR DC)
└── SCEP/NDES Servers: 172.16.12.0/24 (DMZ)
```

**Network Requirements:**
- Dedicated management VLAN for CA infrastructure
- HSM network connectivity (typically requires specific latency <10ms)
- Certificate revocation distribution (CDP/OCSP) placement in DMZ

**Standards Updates Required:**
- PKI Infrastructure Standard: Add network isolation requirements
- Certificate Lifecycle Standard: Include network-based distribution methods

---

## 3. SaaS Migrations (O365 Focus)

### Internet Breakout Strategy & Local Egress Points

**Microsoft 365 Network Connectivity Principles:**
1. **Optimize Category:** Direct internet breakout (bypassing proxy/inspection)
2. **Allow Category:** Regional internet breakout acceptable  
3. **Default Category:** Can traverse security stack

**Branch Office Breakout Design:**
```
Branch Sites (>100 users): Direct internet breakout
├── Primary ISP: Business broadband
├── Backup ISP: 4G/5G cellular
└── QoS Policy: O365 traffic priority

Hub Sites: Concentrated breakout
├── Multiple ISP connections
├── SD-WAN intelligence
└── Centralized security inspection for non-O365
```

### QoS Policies for SaaS Traffic

**DSCP Marking Strategy:**
- Teams Real-time (Audio/Video): EF (46)
- Teams Interactive (Sharing): AF41 (34)  
- SharePoint/Exchange: AF31 (26)
- General O365: BE (0)

**Bandwidth Allocation:**
- Teams calls: 100Kbps per concurrent call
- Teams meetings: 500Kbps-8Mbps per participant
- OneDrive sync: Burst to 80% available bandwidth

---

## 4. DevOps & Container Platforms

### Container Networking (CNI) Strategy

**IP Address Management Pattern:**
```
Kubernetes Cluster Network Design:
├── Node Network: 10.50.0.0/16 (VM/bare-metal hosts)
├── Pod Network: 10.60.0.0/14 (Pod IP allocation)
├── Service Network: 10.64.0.0/16 (ClusterIP services)  
└── External LB: 10.65.0.0/24 (LoadBalancer services)
```

**CNI Selection Decision Matrix:**
- **Calico:** High-performance, network policies required
- **Flannel:** Simple overlay, basic connectivity
- **Cilium:** Advanced security, service mesh integration

### Service Mesh Integration Design

**Istio Network Pattern:**
- Data plane: Envoy sidecars (no additional IP space)
- Control plane: Dedicated namespace/VLAN (10.66.0.0/24)
- Ingress gateways: DMZ placement (10.100.50.0/24)

**Standards Development Required:**
- New "Container Platform Network Architecture" standard
- Integration with existing "Application Deployment Standards"

---

## 5. Integration Platforms (ESB/API)

### API Gateway Network Placement & DMZ Architecture

**Three-Tier API Architecture:**
```
Internet → External DMZ → Internal DMZ → Application Network
         (10.100.20.0/24) (10.100.21.0/24) (10.30.0.0/16)
```

**Load Balancer Design:**
- External LB: Public-facing API endpoints
- Internal LB: East-west API traffic
- Health check networks: OOB management (192.168.100.0/24)

**Network Security Zones:**
- **Zone A:** Public API endpoints (external partners)
- **Zone B:** Internal API endpoints (corporate applications)
- **Zone C:** Backend integration services

---

## 6. EUC/VDI Modernisation (Azure AVD + Citrix + AWS WorkSpaces)

### Low-Latency Network Paths for VDI Traffic

**Multi-Platform Network Design:**
```
VDI Network Architecture:
├── Azure AVD: 10.70.0.0/16
│   ├── Session Hosts: 10.70.1.0/24
│   ├── Domain Controllers: 10.70.10.0/24
│   └── File Services: 10.70.20.0/24
├── Citrix Cloud: 10.71.0.0/16  
│   ├── VDA Pool: 10.71.1.0/23
│   ├── Citrix Connectors: 10.71.10.0/24
│   └── StoreFront: 10.71.20.0/24
└── AWS WorkSpaces: 10.72.0.0/16
    ├── WorkSpaces Instances: 10.72.1.0/23
    ├── Directory Services: 10.72.10.0/24
    └── WorkDocs: 10.72.20.0/24
```

**Latency Requirements by Protocol:**
- **RDP (AVD):** <150ms for acceptable, <50ms for optimal
- **HDX (Citrix):** <100ms for acceptable, <30ms for optimal  
- **PCoIP (AWS):** <100ms for acceptable, <40ms for optimal

**ExpressRoute/Direct Connect Design:**
```
On-Premises DC ←→ Azure (ExpressRoute)
                ├── AVD Regional Hub: Australia East
                └── Backup Region: Australia Southeast
                
On-Premises DC ←→ AWS (Direct Connect)  
                ├── WorkSpaces Primary: ap-southeast-2
                └── WorkSpaces DR: ap-southeast-1
```

### QoS Policies for Real-Time VDI Protocols

**Traffic Classification & Marking:**
- **Interactive/Real-time:** DSCP EF (46) - Mouse/keyboard input
- **Bulk Data:** DSCP AF31 (26) - File transfers, printing
- **Management:** DSCP CS2 (16) - Health checks, policies

**Bandwidth Allocation per User:**
- Standard Office: 150-300 Kbps average, 1 Mbps burst
- Graphics Workstation: 5-15 Mbps sustained
- Video Conferencing: +2 Mbps additional

### Graphics & Multimedia Workload Considerations

**GPU Acceleration Network Requirements:**
- **NVIDIA Grid/Tesla:** Dedicated VLAN for GPU licensing (10.70.30.0/24)
- **AMD MxGPU:** License server placement in management network
- **Graphics Streaming:** Minimum 10 Mbps per concurrent CAD session

**Profile & Application Streaming Optimization:**
- **FSLogix (AVD):** SMB 3.1.1 over 445/tcp, 1 Gbps LAN minimum
- **Citrix Profile Management:** HTTP/HTTPS to cloud storage
- **AWS WorkSpaces:** S3 integration for persistent storage

**Standards Updates Required:**
- New "Virtual Desktop Infrastructure Network Standard"
- Update "End User Computing Standard" with multi-cloud networking section

---

## 7. Data Platform Initiatives (Databricks + AWS + Azure)

### Multi-Cloud Data Architecture Network Design

**Data Platform Network Topology:**
```
Multi-Cloud Data Network:
├── Databricks (Primary): 10.80.0.0/14
│   ├── Driver Nodes: 10.80.0.0/16
│   ├── Worker Nodes: 10.81.0.0/16  
│   ├── Delta Lake Storage: 10.82.0.0/16
│   └── ML Compute: 10.83.0.0/16
├── AWS Data Services: 10.84.0.0/16
│   ├── EMR Clusters: 10.84.1.0/24
│   ├── Redshift: 10.84.10.0/24
│   ├── Kinesis Endpoints: 10.84.20.0/24
│   └── S3 Gateway Endpoints: Private DNS
└── Azure Data Services: 10.85.0.0/16
    ├── Synapse Analytics: 10.85.1.0/24
    ├── Data Factory: 10.85.10.0/24
    ├── Event Hubs: 10.85.20.0/24
    └── Storage Account: Private Endpoints
```

### Data Center Interconnect Architecture

**High-Bandwidth Interconnect Design:**
- **Primary Path:** 100 Gbps dark fiber between DCs
- **Secondary Path:** 40 Gbps MPLS backup
- **Cloud Connectivity:** Multiple 10 Gbps ExpressRoute/DirectConnect

**Standard-Bandwidth Interconnect Design:**
- **Primary Path:** 10 Gbps dark fiber between DCs
- **Secondary Path:** 10 Gbps MPLS backup
- **Cloud Connectivity:** Multiple 1 Gbps ExpressRoute/DirectConnect Hosted

**BGP Routing Strategy:**
```
AS 65001 (Primary DC) ←→ AS 65002 (DR DC)
├── Data Replication: Preferred path via dark fiber
├── Control Plane: MPLS backup for management
└── Cloud Egress: Local breakout per DC
```

### Streaming vs Batch Processing Networks

**Real-Time Streaming Architecture:**
- **Kafka Clusters:** Dedicated 40 Gbps network fabric
- **Stream Processing:** Low-latency compute network (RDMA capable)
- **Hot Path Storage:** NVMe over Fabrics for sub-millisecond access

**Batch Processing Networks:**
- **Hadoop/Spark:** Standard Ethernet, optimized for throughput
- **Cold Storage Access:** Hierarchical storage management
- **Backup/Archive:** Dedicated backup network (10.90.0.0/16)

**Multi-Cloud Data Replication Requirements:**
- **Cross-Region Bandwidth:** 25 Gbps sustained for real-time sync
- **Encryption in Transit:** IPSec tunnels + application-layer TLS
- **Data Sovereignty:** Geo-specific routing policies

**Network Encryption for Data in Transit:**
- **Database Replication:** TLS 1.3 minimum
- **File Transfers:** SFTP/SCP with certificate-based auth
- **API Communications:** mTLS for service-to-service

**Standards Development Required:**
- New "Enterprise Data Platform Network Architecture" standard
- "Multi-Cloud Data Governance" network security section

---

## 8. Observability & ITOM Uplift (Cloud-Native: DataDog + New Relic + Sumo Logic)

### Multi-Tenant Monitoring Architecture

**Cloud-Native Observability Network Design:**
```
Observability Platform Network:
├── Collection Tier: 10.90.0.0/16
│   ├── DataDog Agents: All networks (agent-based)
│   ├── New Relic Infrastructure: 10.90.1.0/24 
│   ├── Sumo Logic Collectors: 10.90.2.0/24
│   └── Custom Exporters: 10.90.10.0/24
├── Aggregation Tier: 10.91.0.0/16
│   ├── Prometheus: 10.91.1.0/24
│   ├── InfluxDB: 10.91.2.0/24  
│   └── OpenTelemetry: 10.91.10.0/24
└── Management Tier: 10.92.0.0/16
    ├── Grafana Dashboards: 10.92.1.0/24
    ├── Alert Manager: 10.92.2.0/24
    └── ITSM Integration: 10.92.10.0/24
```

### Centralized Logging & Telemetry Collection

**Multi-Tenant Data Isolation:**
- **Network Segmentation:** Per-tenant VLANs/VPCs
- **Data Flow Control:** RBAC-based routing policies  
- **Encryption:** Per-tenant encryption keys

**Telemetry Collection Bandwidth Planning:**
- **Metrics:** 1-5 Kbps per monitored endpoint
- **Logs:** 10-100 Kbps per server (varies by verbosity)
- **Traces:** 5-50 Kbps per application instance
- **Total Overhead:** Plan for 10-15% of total network capacity

### SIEM Integration (Hybrid Pattern)

**Hybrid SIEM Architecture:**
```
Security Operations Network:
├── Cloud SIEM (Sumo Logic): SaaS endpoints
├── On-Premises SIEM: 10.93.0.0/24
│   ├── Log Collectors: 10.93.1.0/26
│   ├── Correlation Engine: 10.93.1.64/26  
│   ├── Threat Intel: 10.93.1.128/26
│   └── SOC Workstations: 10.93.2.0/24
└── SIEM-to-Cloud Sync: Dedicated 1 Gbps circuit
```

**Data Flow Patterns:**
- **Real-time Events:** Direct to cloud SIEM via HTTPS
- **Bulk Historical:** Nightly sync via secure file transfer
- **Threat Intelligence:** Bidirectional API integration

### Network Discovery & Asset Inventory Automation

**Discovery Network Design:**
- **SNMP Polling:** Dedicated management network (192.168.200.0/24)
- **Network Scanning:** Isolated security VLAN (192.168.201.0/24)
- **API Collection:** Service account network access

**Bandwidth Allocation for Monitoring:**
- **SNMP Polling:** 64 Kbps per 1000 devices
- **Flow Data (NetFlow/sFlow):** 1-5% of interface bandwidth
- **Packet Mirroring:** Dedicated 10 Gbps monitoring interfaces

**Out-of-Band Management Network:**
```
OOB Management: 192.168.100.0/22
├── Console Servers: 192.168.100.0/24
├── BMC/iDRAC/iLO: 192.168.101.0/24
├── Network Mgmt: 192.168.102.0/24  
└── Monitoring Probes: 192.168.103.0/24
```

**Standards Updates Required:**
- Update "Enterprise Monitoring Standard" with cloud-native requirements
- New "Multi-Tenant Observability Architecture" standard
- "SIEM Integration Network Security" guidelines

**Cloud Connectivity Requirements:**
- **DataDog:** HTTPS/443 outbound, IP whitelist available
- **New Relic:** HTTPS/443, collector.newrelic.com
- **Sumo Logic:** HTTPS/443, multiple regional endpoints

---

