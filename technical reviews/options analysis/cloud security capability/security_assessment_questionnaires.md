# Cloud Security Assessment Questionnaires
## CSPM, SSPM, and DSPM Project Assessment Templates

*Based on CSA Data Security Lifecycle, Cloud Controls Matrix, NIST SP 800-53 Rev 5, Cybersecurity Framework, APRA CPS 234, and ISO 27001*

This includes ready-to-use questionnaires for all three areas:

CSPM Assessment - 18 question categories covering current state, technical capabilities, and tool selection
SSPM Assessment - 11 question categories focused on development environment and supply chain visibility
DSPM Assessment - 15 question categories covering data discovery, classification, and protection

Each questionnaire is mapped to the frameworks you specified:

CSA Data Security Lifecycle and Cloud Controls Matrix
NIST SP 800-53 Rev 5 and Cybersecurity Framework
APRA CPS 234 and ISO 27001 requirements

---

## 1. CLOUD SECURITY POSTURE MANAGEMENT (CSPM) ASSESSMENT

### A. Current State Assessment

#### Infrastructure Configuration
- [ ] **Q1.1** What cloud platforms are currently deployed? (AWS, Azure, GCP, Multi-cloud)
- [ ] **Q1.2** How many active cloud accounts/subscriptions exist across the organization?
- [ ] **Q1.3** What is the current approach to cloud resource configuration management?
- [ ] **Q1.4** Are Infrastructure as Code (IaC) templates being used? (Terraform, ARM, CloudFormation)
- [ ] **Q1.5** How frequently are configuration changes made to cloud resources?

#### Compliance & Governance
- [ ] **Q2.1** Which regulatory frameworks must be adhered to? (ISO 27001, APRA CPS 234, SOC 2, PCI-DSS)
- [ ] **Q2.2** What is the current process for compliance monitoring and reporting?
- [ ] **Q2.3** How are security policies currently enforced across cloud environments?
- [ ] **Q2.4** What is the frequency of compliance audits and assessments?
- [ ] **Q2.5** Are there existing security baselines or configuration standards?

#### Risk Management
- [ ] **Q3.1** What is the current approach to identifying cloud security risks?
- [ ] **Q3.2** How are security incidents currently detected and responded to?
- [ ] **Q3.3** What is the mean time to detection (MTTD) for misconfigurations?
- [ ] **Q3.4** What is the mean time to remediation (MTTR) for security issues?
- [ ] **Q3.5** Are there existing risk registers or threat models for cloud infrastructure?

### B. CSPM Implementation Assessment

#### Technical Capabilities (CSA Cloud Controls Matrix Alignment)
- [ ] **Q4.1** **Identity & Access Management (IAM)**
  - Are privileged accounts properly managed and monitored?
  - Is multi-factor authentication enforced for admin access?
  - Are service accounts and API keys regularly rotated?

- [ ] **Q4.2** **Network Security**
  - Are network segmentation policies properly configured?
  - Are security groups and firewall rules regularly reviewed?
  - Is network traffic monitoring and logging enabled?

- [ ] **Q4.3** **Data Protection**
  - Are encryption policies enforced for data at rest and in transit?
  - Are backup and recovery procedures tested regularly?
  - Is data classification and handling properly implemented?

- [ ] **Q4.4** **Monitoring & Logging**
  - Are comprehensive audit logs enabled across all services?
  - Is log retention compliant with regulatory requirements?
  - Are security monitoring alerts configured and tuned?

#### NIST SP 800-53 Rev 5 Controls Assessment
- [ ] **Q5.1** **Access Control (AC)**
  - AC-1: Are access control policies documented and implemented?
  - AC-2: Is account management properly configured?
  - AC-3: Are access enforcement mechanisms in place?

- [ ] **Q5.2** **Configuration Management (CM)**
  - CM-1: Are configuration management policies established?
  - CM-2: Are baseline configurations maintained?
  - CM-3: Are configuration changes controlled?

- [ ] **Q5.3** **System and Information Integrity (SI)**
  - SI-1: Are system integrity policies implemented?
  - SI-4: Is system monitoring comprehensive?
  - SI-7: Are integrity verification mechanisms in place?

### C. CSPM Tool Selection Criteria

#### Functional Requirements
- [ ] **Q6.1** Multi-cloud support required? (Rate: Critical/Important/Nice-to-have)
- [ ] **Q6.2** Real-time monitoring capabilities needed?
- [ ] **Q6.3** Automated remediation required?
- [ ] **Q6.4** Integration with existing SIEM/SOAR tools needed?
- [ ] **Q6.5** Custom policy creation capabilities required?

#### Business Requirements
- [ ] **Q7.1** What is the expected ROI timeline for CSPM implementation?
- [ ] **Q7.2** What is the available budget range for CSPM solution?
- [ ] **Q7.3** Are there preferred vendor relationships or restrictions?
- [ ] **Q7.4** What is the required implementation timeline?
- [ ] **Q7.5** What level of ongoing support is required?

---

## 2. SOFTWARE SUPPLY CHAIN SECURITY (SSPM) ASSESSMENT

### A. Current State Assessment

#### Development Environment
- [ ] **Q8.1** What development platforms and tools are currently used?
- [ ] **Q8.2** Are CI/CD pipelines implemented across all applications?
- [ ] **Q8.3** What is the current approach to dependency management?
- [ ] **Q8.4** How are third-party libraries and components vetted?
- [ ] **Q8.5** Are container images scanned for vulnerabilities?

#### Supply Chain Visibility
- [ ] **Q9.1** Is there a complete inventory of all software components?
- [ ] **Q9.2** Are Software Bill of Materials (SBOMs) generated and maintained?
- [ ] **Q9.3** How are open-source components tracked and managed?
- [ ] **Q9.4** What is the process for vulnerability disclosure and patching?
- [ ] **Q9.5** Are there approved vendor/supplier lists maintained?

### B. SSPM Implementation Assessment

#### NIST Cybersecurity Framework Alignment
- [ ] **Q10.1** **Identify (ID)**
  - ID.AM: Are all software assets identified and inventoried?
  - ID.RA: Are supply chain risks regularly assessed?
  - ID.SC: Are supply chain dependencies mapped?

- [ ] **Q10.2** **Protect (PR)**
  - PR.DS: Are data security measures implemented in development?
  - PR.IP: Are information protection processes established?
  - PR.MA: Are maintenance activities properly managed?

- [ ] **Q10.3** **Detect (DE)**
  - DE.CM: Are continuous monitoring capabilities implemented?
  - DE.AE: Are anomaly detection mechanisms in place?
  - DE.DP: Are detection processes tested regularly?

#### CSA Data Security Lifecycle Controls
- [ ] **Q11.1** **Create Phase**
  - Are secure coding standards enforced?
  - Is data classification applied during development?
  - Are security requirements defined upfront?

- [ ] **Q11.2** **Store Phase**
  - Are code repositories properly secured?
  - Is version control access properly managed?
  - Are artifacts signed and verified?

- [ ] **Q11.3** **Use Phase**
  - Are runtime security controls implemented?
  - Is application behavior monitored?
  - Are security updates applied promptly?

---

## 3. DATA SECURITY POSTURE MANAGEMENT (DSPM) ASSESSMENT

### A. Current State Assessment

#### Data Discovery & Classification
- [ ] **Q12.1** What data discovery tools are currently implemented?
- [ ] **Q12.2** Is there a comprehensive data inventory across all systems?
- [ ] **Q12.3** Are data classification schemes defined and enforced?
- [ ] **Q12.4** How is sensitive data identified and tracked?
- [ ] **Q12.5** Are data flows mapped and documented?

#### Data Protection
- [ ] **Q13.1** What encryption standards are currently implemented?
- [ ] **Q13.2** Are data masking and tokenization used where appropriate?
- [ ] **Q13.3** How are encryption keys managed and rotated?
- [ ] **Q13.4** Are data loss prevention (DLP) controls in place?
- [ ] **Q13.5** What is the current approach to data backup and recovery?

### B. DSPM Implementation Assessment

#### ISO 27001 Annex A Controls
- [ ] **Q14.1** **A.8 Asset Management**
  - A.8.1: Are information assets identified and inventoried?
  - A.8.2: Are assets classified according to importance?
  - A.8.3: Are media handling procedures established?

- [ ] **Q14.2** **A.10 Cryptography**
  - A.10.1: Are cryptographic controls policies established?
  - A.10.2: Is key management properly implemented?

- [ ] **Q14.3** **A.13 Communications Security**
  - A.13.1: Are network security controls implemented?
  - A.13.2: Are information transfer controls established?

#### APRA CPS 234 Requirements
- [ ] **Q15.1** **Information Security Capability**
  - Is there a comprehensive information security capability?
  - Are information security policies regularly reviewed?
  - Are security roles and responsibilities clearly defined?

- [ ] **Q15.2** **Information Asset Management**
  - Are information assets identified and classified?
  - Are information asset registers maintained?
  - Are information asset owners assigned?

- [ ] **Q15.3** **Information Security Controls**
  - Are controls implemented commensurate with risk?
  - Are controls regularly tested and validated?
  - Are control deficiencies tracked and remediated?

---

## 4. INTEGRATED ASSESSMENT SCORING MATRIX

### Risk Assessment Scale
- **Critical (4)**: Immediate action required, significant risk exposure
- **High (3)**: Action required within 30 days, elevated risk
- **Medium (2)**: Action required within 90 days, moderate risk
- **Low (1)**: Action required within 180 days, minimal risk

### Compliance Scoring
- **Fully Compliant (4)**: All requirements met with evidence
- **Largely Compliant (3)**: Most requirements met, minor gaps
- **Partially Compliant (2)**: Some requirements met, significant gaps
- **Non-Compliant (1)**: Requirements not met, major gaps

### Implementation Priority Matrix
| **Impact** | **Effort** | **Priority** |
|------------|------------|--------------|
| High | Low | P1 - Immediate |
| High | Medium | P2 - Short-term |
| High | High | P3 - Medium-term |
| Medium | Low | P2 - Short-term |
| Medium | Medium | P3 - Medium-term |
| Medium | High | P4 - Long-term |
| Low | Low | P3 - Medium-term |
| Low | Medium | P4 - Long-term |
| Low | High | P5 - Future |

---

## 5. ASSESSMENT REPORT TEMPLATE

### Executive Summary
- Overall security posture rating
- Key findings and recommendations
- Resource requirements and timeline
- Business impact and risk assessment

### Detailed Findings
- Technical gaps and vulnerabilities
- Compliance deficiencies
- Process and governance issues
- Tool and technology recommendations

### Implementation Roadmap
- Phase 1: Critical items (0-3 months)
- Phase 2: High priority items (3-6 months)
- Phase 3: Medium priority items (6-12 months)
- Phase 4: Long-term improvements (12+ months)

### Success Metrics
- Key performance indicators (KPIs)
- Measurement methods and frequency
- Reporting and governance structure
- Continuous improvement processes