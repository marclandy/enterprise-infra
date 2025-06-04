# Enterprise Backup & DR Technical Design Framework
## Commvault & Veeam Implementation for Hybrid Infrastructure

---

## Day 0: Planning & Design Phase

### **Architecture Overview**

#### **Platform Segregation Strategy**
- **Commvault**: Enterprise applications (SAP, Workday, databases), file systems, NAS, cloud workloads
- **Veeam**: VMware/Hyper-V virtualized infrastructure, VMs, cloud-native Azure/AWS resources
- **Hybrid Integration**: Cross-platform orchestration for disaster recovery scenarios

#### **Infrastructure Requirements**

**Commvault Infrastructure:**
- **CommServe (Master Server)**: 
  - Windows Server 2022, 32GB RAM, 8 vCPU
  - 500GB system disk + 2TB CommServe DB storage (SSD)
  - SQL Server 2019/2022 Enterprise
- **MediaAgents (Storage Nodes)**:
  - Linux RHEL 8.x or Windows Server 2022
  - 64GB RAM, 16 vCPU per node
  - 10GbE network connectivity
  - Deduplication storage pools (Dell EMC, HPE, Pure Storage)
- **Access Nodes**:
  - Distributed across data centers
  - 16GB RAM, 4 vCPU minimum
  - Proximity to protected workloads

**Veeam Infrastructure:**
- **Veeam Backup & Replication Server**:
  - Windows Server 2022, 16GB RAM, 4 vCPU
  - SQL Server 2019 Standard/Express
- **Veeam Proxy Servers**:
  - 2-4 proxies per site
  - 8GB RAM, 4 vCPU each
  - Hot-add/Network transport modes
- **Veeam Repository Servers**:
  - Scale-out repositories with per-VM backup chains
  - Linux hardened repositories for immutable backups
  - Integration with AWS S3/Azure Blob for archive tiers

### **Network Design Considerations**

#### **Bandwidth Allocation**
- **Production Impact**: Max 30% network utilization during business hours
- **Backup Windows**: 8 hours (6 PM - 2 AM) for full backups
- **WAN Optimization**: Riverbed/Silver Peak for remote sites
- **Dedicated Backup VLANs**: Isolated traffic, QoS enabled

#### **Security Framework**
- **Network Segmentation**: Dedicated backup subnets
- **Firewall Rules**: Palo Alto integration
  - Commvault: TCP 8400-8403, 8600-8609
  - Veeam: TCP 9392-9395, 2500-3300
- **Encryption**: AES-256 in-flight and at-rest
- **Certificate Management**: PKI integration with enterprise CA

---

## Day 1: Implementation & Configuration

### **Commvault Deployment**

#### **Storage Policy Configuration**
```
Gold Tier (Business Critical):
- Primary Copy: Local deduplication storage
- Secondary Copy: Offsite tape/cloud (4-hour delay)
- Archive Copy: AWS S3 Glacier (7-day delay)
- Retention: 7 years

Silver Tier (Production):
- Primary Copy: Local disk pool
- Secondary Copy: DR site (8-hour delay)  
- Archive Copy: Azure Archive (30-day delay)
- Retention: 3 years

Bronze Tier (Development/Test):
- Primary Copy: Local SATA storage
- Archive Copy: Cloud storage (90-day delay)
- Retention: 1 year
```

#### **Application-Specific Configurations**

**SAP HANA/ERP:**
- Database-consistent backups using CommVault IntelliSnap
- Log shipping every 15 minutes
- Cross-platform disaster recovery to Azure VMs
- Integration with SAP HANA native tools

**Workday Integration:**
- API-based tenant backup
- Encrypted data extraction
- Compliance reporting automation

**Active Directory:**
- System State backups (daily)
- SYSVOL replication monitoring
- Authoritative restore capabilities
- Cross-forest recovery procedures

### **Veeam Deployment**

#### **Job Configuration Framework**

**VM Backup Jobs:**
- **Application-aware processing** for SQL, Exchange, Oracle
- **Guest OS quiescing** via VMware Tools/Hyper-V IC
- **Incremental backup chains** with weekly active fulls
- **Health check verification** post-backup

**Cloud Integration:**
- **Azure Backup integration** for IaaS workloads
- **AWS EC2 snapshot coordination**
- **Cross-cloud replication** for DR scenarios

### **Monitoring & Alerting Setup**

#### **Integration Points**
- **SIEM Integration**: Splunk/QRadar log forwarding
- **ITSM Integration**: ServiceNow incident creation
- **Network Monitoring**: Integration with Cisco Prime/SolarWinds
- **Palo Alto Firewall**: Traffic analysis and security monitoring

---

## Day 2: Operations & Optimization

### **Operational Procedures**

#### **Daily Operations**
- **Backup Status Dashboard**: Real-time monitoring console
- **Failed Job Analysis**: Root cause identification within 2 hours
- **Capacity Planning**: Growth trending and forecasting
- **Performance Optimization**: Throughput analysis and tuning

#### **Weekly Operations**
- **Recovery Testing**: Automated restore validation
- **Compliance Reporting**: Audit trail generation
- **Security Patching**: Coordinated maintenance windows
- **DR Site Synchronization**: Replication health checks

#### **Monthly Operations**
- **Full DR Testing**: End-to-end failover scenarios
- **Capacity Expansion**: Storage and compute scaling
- **Performance Baselining**: SLA compliance verification
- **Documentation Updates**: Runbook maintenance

---

## RPO/RTO Service Level Framework

### **Gold Tier - Business Critical**
**Scope**: SAP Production, Core AD, Primary financial systems, Core network infrastructure (Palo Alto, Cisco ISE)

**Backup Requirements:**
- **RPO**: 15 minutes (continuous data protection)
- **RTO**: 2 hours for full system recovery
- **Backup Frequency**: Continuous + Daily application-consistent
- **Retention**: 7 years (regulatory compliance)
- **Recovery Testing**: Monthly automated testing

**Technology Stack:**
- Commvault Live Sync for near-zero RPO
- VMware vSphere Replication for VM-level protection
- Database log shipping (15-minute intervals)
- Instant recovery capabilities from storage snapshots

### **Silver Tier - Production Standard**
**Scope**: Secondary business applications, departmental systems, standard user VMs

**Backup Requirements:**
- **RPO**: 4 hours (incremental backups every 4 hours)
- **RTO**: 8 hours for full application stack recovery
- **Backup Frequency**: 4x daily incremental, nightly full
- **Retention**: 3 years
- **Recovery Testing**: Quarterly automated testing

**Technology Stack:**
- Veeam backup jobs with 4-hour intervals
- Commvault for database and application data
- Storage-based snapshots for quick recovery
- Cross-site replication for DR

### **Bronze Tier - Development/Test**
**Scope**: Development environments, test systems, non-critical applications

**Backup Requirements:**
- **RPO**: 24 hours (daily backup acceptable)
- **RTO**: 24-48 hours (best effort recovery)
- **Backup Frequency**: Daily incremental, weekly full
- **Retention**: 1 year
- **Recovery Testing**: Annual or on-demand

**Technology Stack:**
- Basic Veeam backup jobs
- Cloud-tier storage (AWS S3 IA, Azure Cool)
- Simplified recovery procedures
- Self-service restore capabilities

---

## DR Strategy Essentials

### **Multi-Site Architecture**

#### **Primary Data Center (Production)**
- Full Commvault and Veeam infrastructure
- Real-time replication to DR site
- Local high-performance storage

#### **DR Site (Recovery)**
- Scaled Commvault/Veeam infrastructure (60% capacity)
- Automated failover capabilities
- Network connectivity via dedicated circuits

#### **Cloud DR (Tertiary)**
- AWS/Azure disaster recovery orchestration
- Cost-optimized compute instances
- Automated scaling based on recovery needs

### **Recovery Orchestration**

#### **Automated Failover Triggers**
- Network monitoring integration
- Application health checks
- Manual override capabilities
- Stakeholder notification workflows

#### **Recovery Procedures**
1. **Impact Assessment** (15 minutes)
2. **Stakeholder Notification** (30 minutes)
3. **Infrastructure Recovery** (Gold: 2hrs, Silver: 8hrs, Bronze: 24hrs)
4. **Application Stack Recovery** (Sequential by tier priority)
5. **User Access Restoration** (Network, authentication, applications)
6. **Business Validation** (Application owners sign-off)

---

## Key Assumptions & Standards

### **Technical Assumptions**
- **Network Bandwidth**: Minimum 10Gbps between sites
- **Storage Performance**: 50,000 IOPS capability for backup storage
- **Virtualization**: VMware vSphere 7.x/8.x environment
- **Cloud Connectivity**: ExpressRoute/Direct Connect established
- **Security Compliance**: SOX, PCI-DSS, GDPR requirements

### **Operational Standards**
- **Maintenance Windows**: Saturdays 2 AM - 6 AM
- **Change Management**: 72-hour advance notice for infrastructure changes
- **Documentation**: All procedures maintained in enterprise wiki
- **Training**: Quarterly DR drills for operations staff
- **Vendor Support**: 24x7 support contracts for critical systems

### **Performance Baselines**
- **Backup Throughput**: 2-5 TB/hour per MediaAgent
- **Deduplication Ratio**: 15:1 average across enterprise data
- **Cloud Transfer**: 100 Mbps minimum to cloud repositories
- **Recovery Performance**: 1 TB/hour restore capability

### **Compliance Requirements**
- **Audit Logging**: All backup/restore activities logged
- **Encryption**: AES-256 for data at rest and in transit
- **Access Control**: Role-based permissions with quarterly review
- **Retention Policies**: Automated lifecycle management
- **Reporting**: Monthly compliance dashboards for stakeholders
