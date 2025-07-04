# PKI/Digital Certificate Management Standard v1.0

**Document Classification:** Corporate IT Standard  
- **Author:** Marc Landy, Network Architect
- **Effective Date:** 8th June 2025  
- **Review Cycle:** Annual  
- **Stakeholders:** Operations, Engineering, Designers, Architects  

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 8th June 2025
- **Next Review**: June 2026
- **Owner**: Enterprise Architecture Team
- **Approver**: Chief Information Security Officer
---

## Key Features of the Standard:

1. **Day 0/1/2 Model** - Provides a phased approach to PKI implementation from planning through operations.
2. **Corporate Use Cases** - Detailed certificate types, flows, and implementation guidance
3. **Comprehensive Standard Requirements** 
   * CA/RA Policies
   * Certificate Lifecycle Management
   * Key Management
   * Trust Model
   * Certificate Enrollment
   * CRL Management
   * Storage & Retrieval
   * Security Controls
   * Compliance
   * Monitoring & Auditing
   * Business Continuity
   * Personnel Security
   * Data-in-Transit Protection
   * Data Integrity & Confidentiality
4. **Decision Framework** - Practical guidance for different stakeholder domains (Infrastructure, Network, Security, IAM, Application, Data, Integration)
5. **Reference Links** 

---

## 1. Day 0 / Day 1 / Day 2 Model – PKI for Corporate IT

### 1.1 Day 0 – Planning & Design

| **Activity** | **Description** |
|--------------|-----------------|
| **Identify Use Cases** | Define certificate requirements for device authentication, user authentication, secure email (S/MIME), and application-to-application communications |
| **Select Trust Model** | Determine between Private CA vs Public CA deployment; evaluate Cloud PKI vs On-premises PKI solutions |
| **Define Certificate Profiles** | Establish key usage parameters, validity periods, subject name conventions, renewal schedules, and grace periods |
| **PKI Topology Design** | Design Root CA and Issuing CA hierarchy (single-tier or two-tier), determine CA placement, and establish security boundaries |
| **Integration Planning** | Plan integration with Microsoft Intune, JAMF, Active Directory Certificate Services (ADCS), Microsoft 365, VPN infrastructure, and Network Access Control (NAC)/RADIUS systems |
| **Access Control Framework** | Define roles and responsibilities for PKI issuance and operations across IAM, Security, and Infrastructure teams |
| **Compliance Alignment** | Ensure adherence to NIST frameworks, ISO 27001, CIS benchmarks, and CA/Browser Forum guidelines |

### 1.2 Day 1 – Deployment & Issuance

| **Activity** | **Description** |
|--------------|-----------------|
| **CA Infrastructure Build** | Deploy cloud or on-premises Certificate Authority infrastructure and configure issuing certificate templates |
| **Automation Implementation** | Configure automated provisioning through Intune SCEP, PowerShell scripts, and ACME client configurations |
| **Profile Deployment** | Distribute certificate profiles to designated user and device groups via Group Policy Objects (GPO) or Mobile Device Management (MDM) |
| **Logging and Audit Setup** | Enable comprehensive logging, certificate issuance monitoring, and key usage alerting systems |
| **Administrative Testing** | Conduct thorough testing of certificate issuance, revocation, and renewal processes across all defined use cases |
| **Certificate Binding** | Verify certificates properly bind to services, devices, and identities according to design specifications |

### 1.3 Day 2 – Operations & Lifecycle Management

| **Activity** | **Description** |
|--------------|-----------------|
| **Continuous Monitoring** | Monitor certificate expiration dates, revocation status, CA health metrics, and issuance trend analysis |
| **Renewal Process Management** | Implement automated renewal workflows, configure pre-expiration alerts, and manage reissuance of compromised certificates |
| **Rotation Policy Enforcement** | Maintain and audit validity windows: Device certificates (1 year), User certificates (6-12 months), Email certificates (1-2 years) |
| **Revocation Management** | Maintain Certificate Revocation Lists (CRL) and Online Certificate Status Protocol (OCSP), integrate with Security Information and Event Management (SIEM) and Security Orchestration, Automation and Response (SOAR) systems |
| **Certificate Hygiene** | Remove obsolete certificates, prevent certificate sprawl, and ensure non-reuse of cryptographic keys |
| **Documentation Maintenance** | Keep current documentation of PKI architecture, certificate profiles, and renewal schedules |
| **Post-Incident Response** | Execute certificate rotation procedures, manage key compromise reissuance, and validate audit trails following security incidents |

---

## 2. Corporate Certificate Use Cases and Implementation

### 2.1 Certificate Use Cases, Flows, and Types

| **Use Case** | **Flow Logic** | **Certificate Type & Attributes** |
|--------------|----------------|-----------------------------------|
| **Device Authentication (MDM/SCEP)** | Devices enroll through Mobile Device Management systems using Simple Certificate Enrollment Protocol to obtain device certificates for network and service authentication | **Device Certificates**: Issued via SCEP with device identifiers in Common Name (CN) and Subject Alternative Name (SAN). Key Usage: Digital Signature, Key Encipherment |
| **User Authentication (PFX/Intune)** | Users receive Personal Information Exchange certificates through Microsoft Intune or similar platforms for service authentication and secure communications | **User Certificates**: Delivered as PFX files containing user credentials. CN as username, SAN for email addresses. Key Usage: Client Authentication, Email Protection |
| **Secure Email (S/MIME)** | Secure/Multipurpose Internet Mail Extensions enable email encryption and digital signing through public key exchange between users | **S/MIME Certificates**: Issued for email security with email address in SAN, CN as username. Key Usage: Digital Signature, Non-Repudiation, Key Encipherment |
| **Digital Signing (Non-Repudiation)** | Users digitally sign documents or transactions to ensure authenticity and non-repudiation, with signature verification of origin and content integrity | **Signing Certificates**: Issued to individuals or entities with CN as signer name and organization details. Key Usage: Digital Signature, Non-Repudiation |
| **Regulatory/Compliance Communications** | Communications requiring regulatory compliance (HIPAA, GDPR) use certificates to ensure data integrity, confidentiality, and authenticity | **Compliance Certificates**: Tailored to specific regulatory standards with organization details and policy identifiers. Key Usage: As required by regulations |

### 2.2 S/MIME Deployment Considerations

**Current Industry Status:**
- **Heavily Regulated Industries** (finance, government, healthcare, legal): Common and often mandatory
- **General Corporate IT**: Used selectively for executives, legal teams, or external high-trust communications
- **Technology Companies**: Rare, with preference for secure web-based communications platforms

**Implementation Challenges:**
- Requires comprehensive user certificate lifecycle management
- Email systems typically don't enforce encryption or signing by default
- End-user experience friction from lost PFX files, device transfers, or key mismatches
- Often supplemented by secure email gateways or message encryption portals

### 2.3 Certificate Distribution Model

**Typical Corporate User Certificate Profile:**
- **Device Certificate**: Authenticates device to Wi-Fi, VPN, NAC, or Intune (delivered via SCEP/Intune Device Profile)
- **User Certificate**: Enables user authentication for 802.1x, VPN, VDI (delivered via PFX/Intune User Profile)
- **Secure Email Certificate**: Provides digital signing and encryption for email (delivered via PFX/Intune with S/MIME profile)

**Certificate Management Separation:**
- User Authentication and S/MIME certificates are typically separate despite both being distributed as PFX files
- Different certificate profiles serve distinct Extended Key Usage (EKU) purposes
- Operational management often spans multiple teams (Infrastructure/Identity for User Auth, Security/Messaging for S/MIME)

---

## 3. Enterprise PKI Certificate Decision Framework

### 3.1 Certificate Use-Case Decision Framework (Designer View)

| **Designer Domain** | **Key Use-Case** | **Decision Points** | **Certificate Profile(s)** | **Recommended Flow** | **Implementation Notes** |
|---------------------|------------------|--------------------|-----------------------------|---------------------|-------------------------|
| **Infrastructure** | Device trust (laptops, endpoints, servers) | Domain-join vs non-domain, MDM integration, SCEP or Intune deployment | Device Certificate | SCEP Flow | Intune or third-party MDMs handle provisioning |
| **Network** | 802.1X authentication | Wired vs Wireless networks, per-device certificates, NAC integration | Device/User Certificate | SCEP + RADIUS | Coordinate with Security team for implementation |
| **Security** | VPN, VDI, Admin PAM, Endpoint posture | Trust source selection, MFA/SSO integration, privileged access rules | User Certificate | PFX Flow | May require hardened certificate profiles |
| **IAM** | Identity binding, authentication, SSO enforcement | PKI vs FIDO2, smart card vs biometrics, lifecycle integration | User Certificate | PFX Flow | Certificate binding to Azure AD, LDAP, or IDP |
| **Application** | App-to-app trust, messaging, API authentication | Internal app communications, messaging queues, mTLS support | Application/Service Certificate | Manual or scripted deployment | ACME/Custom CA as certificate source |
| **Data** | Data at rest/in transit encryption, S/MIME | Data classification policies, legal holds, secure email usage | S/MIME Certificate | PFX Flow | Integration with Microsoft 365 or mail infrastructure |
| **Integration** | External API integrations, third-party trust | SaaS/vendor trust anchors, certificate pinning, external validation | Public Certificate, ACME-issued | Let's Encrypt or Commercial CA | Implement certificate expiration monitoring |

### 3.2 Certificate Provider Recommendations

| **Use Case** | **Certificate Type** | **Recommended Providers** | **Private CA Option** |
|--------------|---------------------|---------------------------|----------------------|
| **Device Certificates** | Device Authentication (SCEP/NDES) | Microsoft Cloud PKI, ADCS, Intune, JAMF | ✅ Recommended |
| **User Certificates** | User Authentication (802.1x) | Microsoft Cloud PKI, Entrust, DigiCert | ✅ Recommended |
| **S/MIME Email** | Secure Email | Entrust, DigiCert, GlobalSign, Intune (PFX) | ⚠️ Possible (rarely used) |

### 3.3 Certificate Lifecycle and Rotation Policy

| **Certificate Type** | **Recommended Validity** | **Renewal Lead Time** | **Rotation Method** | **Implementation Notes** |
|---------------------|-------------------------|----------------------|---------------------|-------------------------|
| **Device Certificate** | 1 year | 30 days | Auto-rotation via Intune | Renewal through SCEP/NDES |
| **User Certificate** | 1-2 years | 30 days | Automatic or manual PFX reissue | Managed via MDM or user portal |
| **S/MIME Certificate** | 1 year | 30 days | Manual renewal or Intune automation | Must maintain key history for email decryption |

### 3.4 Certificate Delivery Method | <placeholder>

### 3.5 Authentication Flow Integration

| **Flow Type** | **Certificate-Based Authentication** | **SSO/MFA Use Case** | **Implementation Guidance** |
|---------------|-------------------------------------|---------------------|----------------------------|
| **Device to Wi-Fi/VPN** | ✅ Primary method | ❌ Not required | Certificate-based device authentication |
| **VPN Access** | ✅ Optional additional factor | ✅ Required (2FA enforced) | Combine certificate and interactive authentication |
| **VDI/Remote Applications** | ✅ Optional | ✅ Primary method (SSO/Azure AD MFA) | Certificate for device trust, SSO for user authentication |
| **Web Applications (SaaS)** | ❌ Rarely used | ✅ Primary method | SSO/MFA as standard approach |

## 4. Comprehensive PKI Standard Requirements

### 4.1 Certificate Authority (CA) and Registration Authority (RA) Policies

**Roles and Responsibilities:**
- Define CA Administrator, RA Administrator, and Certificate Manager roles
- Establish clear segregation of duties for certificate issuance and management
- Document approval workflows for certificate requests and revocations
- Maintain role-based access controls for PKI administrative functions

**Procedures:**
- Certificate issuance procedures with appropriate identity verification
- Certificate management workflows including renewal and revocation processes
- Emergency procedures for CA compromise or operational disruption
- Regular review and update procedures for CA and RA policies

### 4.2 Certificate Lifecycle Management

**Certificate Creation:**
- Standardized certificate request and approval processes
- Automated certificate generation where appropriate
- Certificate template management and version control
- Integration with identity management systems

**Certificate Storage:**
- Secure certificate repository implementation
- Access controls and audit logging for certificate storage systems
- Backup and recovery procedures for certificate stores
- Certificate distribution mechanisms

**Certificate Renewal:**
- Automated renewal processes with configurable lead times
- Manual renewal procedures for special cases
- Grace period policies for expired certificates
- Renewal notification systems

**Certificate Revocation:**
- Immediate revocation procedures for compromised certificates
- Regular revocation procedures for routine certificate lifecycle events
- CRL and OCSP responder management
- Integration with security incident response procedures

### 4.3 Key Management

**Key Generation:**
- Cryptographic key generation standards and algorithms
- Key strength requirements based on use case sensitivity
- Hardware Security Module (HSM) integration for high-value keys
- Key generation audit and logging requirements

**Secure Storage:**
- Key storage security controls and access restrictions
- HSM deployment for critical cryptographic operations
- Key escrow and recovery procedures where required
- Protection against unauthorized key access or extraction

**Key Backup and Recovery:**
- Key backup procedures and secure storage requirements
- Key recovery procedures for business continuity
- Key archive management and retention policies
- Disaster recovery procedures for key material

**Key Destruction:**
- Secure key deletion procedures
- Key destruction verification and audit trails
- Timeline requirements for key destruction
- Compliance with data retention requirements

### 4.4 Trust Model

**PKI Architecture:**
- Public vs Private PKI decision framework
- Cross-certification requirements with external PKIs
- Trust anchor distribution and management
- Certificate path validation procedures

**Trust Relationships:**
- Internal CA trust establishment
- External CA trust evaluation and approval
- Certificate pinning policies for critical applications
- Trust model documentation and maintenance

### 4.5 Certificate Enrollment

**Identity Verification:**
- Identity proofing requirements for different certificate types
- Documentation requirements for certificate requests
- In-person vs remote verification procedures
- Integration with HR and identity management systems

**Enrollment Processes:**
- Automated enrollment via SCEP, ACME, or similar protocols
- Manual enrollment procedures for special cases
- Bulk enrollment procedures for device certificates
- Self-service enrollment portals where appropriate

### 4.6 Certificate Revocation List (CRL) Management

**CRL Distribution:**
- CRL publication schedules and distribution points
- OCSP responder deployment and management
- CRL and OCSP performance monitoring
- Redundancy and availability requirements

**Revocation Procedures:**
- Certificate revocation request and approval processes
- Emergency revocation procedures
- Bulk revocation procedures for security incidents
- Revocation reason code usage and documentation

### 4.7 Certificate Storage and Retrieval

**Secure Storage Guidelines:**
- Certificate store security controls and access restrictions
- Directory services integration for certificate publication
- Certificate repository backup and recovery procedures
- Performance and availability requirements for certificate services

**Access Controls:**
- Role-based access to certificate stores
- Audit logging for certificate access and retrieval
- Integration with identity and access management systems
- Certificate search and discovery capabilities

### 4.8 Security Controls

**PKI Infrastructure Protection:**
- Physical security controls for CA systems and HSMs
- Network security controls and segmentation
- System hardening standards for PKI components
- Vulnerability management for PKI infrastructure

**Access Security:**
- Multi-factor authentication for PKI administrative access
- Privileged access management for CA operations
- Security monitoring and alerting for PKI systems
- Regular security assessments and penetration testing

### 4.9 Compliance Requirements

**Industry Standards:**
- Compliance with relevant industry regulations (PCI DSS, HIPAA, SOX)
- Adherence to cryptographic standards (FIPS 140-2, Common Criteria)
- Certificate policy and practice statement maintenance
- Regular compliance audits and assessments

**Documentation:**
- Comprehensive PKI documentation and procedures
- Certificate policy and certificate practice statement
- Security controls documentation
- Compliance reporting and evidence collection

### 4.10 Monitoring and Auditing

**Infrastructure Monitoring:**
- Continuous monitoring of CA health and availability
- Certificate expiration monitoring and alerting
- Performance monitoring of PKI services
- Security event monitoring and correlation

**Audit Procedures:**
- Regular audits of certificate issuance and management
- Compliance audits against established policies
- Security audits of PKI infrastructure
- Audit log review and analysis procedures

### 4.11 Business Continuity and Disaster Recovery

**Continuity Planning:**
- PKI service availability requirements and SLAs
- Redundancy and failover procedures for critical PKI services
- Backup and recovery procedures for PKI data and systems
- Business impact analysis for PKI service disruptions

**Disaster Recovery:**
- PKI disaster recovery procedures and testing
- Recovery time and recovery point objectives for PKI services
- Alternative PKI service provisioning during outages
- Communication procedures during PKI service disruptions

### 4.12 Personnel Security

**Background Checks:**
- Security clearance requirements for PKI personnel
- Background investigation procedures for sensitive PKI roles
- Ongoing security assessments for PKI personnel
- Personnel termination procedures and access revocation

**Training and Awareness:**
- PKI security training for administrative personnel
- Regular security awareness updates
- Role-specific training for PKI functions
- Security incident response training

### 4.13 Data-in-Transit Protection

**Encryption Requirements:**
- TLS/SSL implementation standards for PKI communications
- Certificate-based authentication for system communications
- VPN and secure channel requirements for PKI data transmission
- End-to-end encryption for sensitive PKI operations

**Protocol Security:**
- Secure protocol selection and configuration
- Certificate validation requirements for secure communications
- Integration with network security controls
- Monitoring and alerting for insecure communications

### 4.14 Data Integrity and Confidentiality

**Data Protection:**
- Encryption requirements for PKI data at rest
- Data integrity verification procedures
- Access controls for sensitive PKI data
- Data classification and handling procedures

**Confidentiality Controls:**
- Information classification for PKI-related data
- Need-to-know access controls
- Data loss prevention for PKI information
- Secure disposal procedures for PKI data

---

## 5. Reference Links

### <>

### <>

---
