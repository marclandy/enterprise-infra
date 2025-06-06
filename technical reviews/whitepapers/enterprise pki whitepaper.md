---
Title: "Enterprise Certificate Management for Mid-Tier Organisations: Integrating PKI Across IT, OT, and EUC Architectures"
Author: Marc Landy, Network & Infrastructure Architecture Team  
Repo: Internal Architecture Standards
Last Updated: 6th June 2025  
Referenced document: https://medium.com/@marclandy.me/euc-reference-architecture-83286cb1c359
---

## Executive Summary

Mid-tier organisations in sectors such as retail, healthcare, manufacturing, and energy are undergoing digital transformation across hybrid environments. As the perimeter dissolves, the **trust fabric of the enterprise is increasingly underpinned by certificate-based authentication**—for devices, users, services, workloads, and data.

This whitepaper provides a pragmatic and reference-driven overview of certificate use-cases in a typical enterprise, considerations for consolidating on a modern PKI platform, and comparative guidance on integrating **DigiCert PKI Platform** and **Microsoft Cloud PKI** with Microsoft Intune.

> *Refer also to the companion EUC Reference Architecture article: [https://medium.com/@marclandy.me/euc-reference-architecture-83286cb1c359](https://medium.com/@marclandy.me/euc-reference-architecture-83286cb1c359)*

---

## 1. Certificate Use Cases Across the Enterprise

### EUC: Devices and Access

| <span style="background-color: #90EE90;">**Category**</span>     | <span style="background-color: #90EE90;">**System/Platform**</span>                              | <span style="background-color: #90EE90;">**Certificate Function**</span>                                  |
|------------------|--------------------------------------------------|------------------------------------------------------------|
| **Devices**      | Windows, macOS, iOS, Android, Linux              | Device identity (SCEP/PFX), Wi-Fi (802.1X), VPN auth       |
| **EUC Access**   | Intune, JAMF, AVD, Citrix, Conditional Access    | PFX provisioning, compliance token binding                 |

### Network & Security

| <span style="background-color: #90EE90;">**Category**</span>         | <span style="background-color: #90EE90;">**System/Platform**</span>                          | <span style="background-color: #90EE90;">**Certificate Function**</span>                                  |
|----------------------|----------------------------------------------|------------------------------------------------------------|
| **Core Infrastructure** | Cisco ISE, RADIUS, NAC, ClearPass         | Certificate auth for user/device onboarding                |
| **Firewall & SSE**   | Palo Alto, Fortinet, Zscaler, Netskope       | SSL inspection, decrypt policies, cert-based access        |
| **Network Layer**    | VPN, ZTNA, SSE, SASE                         | mTLS tunnels, certs for mutual auth and dynamic routing policies |

### Core Infra & Platforms

| <span style="background-color: #90EE90;">**Category**</span>         | <span style="background-color: #90EE90;">**System/Platform**</span>                          | <span style="background-color: #90EE90;">**Certificate Function**</span>                                  |
|----------------------|----------------------------------------------|------------------------------------------------------------|
| **DNS/DHCP/IPAM**    | Infoblox, Route53, Unbound                   | TLS for DoH, cert-based API authentication                 |
| **Email Security**   | Outlook, M365, Exchange Online               | S/MIME for encryption and digital signing                  |
| **Monitoring/SIEM**  | Sentinel, ELK, Splunk                        | TLS for telemetry/logs, cert-auth for agents               |
| **DevOps Pipelines** | GitHub, Jenkins, Terraform, Ansible          | Code signing, secure API interactions                      |
| **Data Platforms**   | Snowflake, Azure Data Lake, S3               | TLS, certificate-based access, service auth                |
| **Messaging Systems**| Apache Kafka, RabbitMQ, Azure Event Hub      | mTLS between producers/consumers                           |
| **Application Security** | Imperva, Azure Front Door, Akamai, F5 WAF | TLS termination, client auth, mTLS to origin               |
| **Cloud Workloads**  | Kubernetes, App Services, Functions, VMs     | SPIFFE/SPIRE, x.509 identity, mTLS in service mesh         |

---

## 2. PKI Platform Integration with Intune

### 2.1 SCEP Flow

[ Intune ] → issues SCEP request → [ SCEP Connector (on-prem or cloud) ] → forwards to → [ CA / DigiCert Cloud ]

- Ideal for device certificates, MDM-based workflows
- Stateless provisioning

### 2.2 PFX Flow

[ Intune ] → PFX cert request → [ DigiCert CA ] → cert generated & escrowed → returned securely to device

- Ideal for S/MIME, secure email, user certificates
- Certificate escrow supported (DigiCert)

---

## 3. Microsoft Cloud PKI vs DigiCert PKI Platform

| <span style="background-color: #90EE90;">**Capability**</span>                         | <span style="background-color: #90EE90;">**Microsoft Cloud PKI**</span>                           | <span style="background-color: #90EE90;">**DigiCert PKI Platform**</span>                      |
|----------------------------------------|--------------------------------------------------|-----------------------------------------------|
| Deployment Model                       | Native to Entra + Intune                         | Cloud-native, vendor-agnostic                 |
| Intune Integration                     | Native                                          | Via DigiCert Intune Connector                 |
| Certificate Flows Supported            | SCEP, PFX (limited)                              | SCEP, PFX, S/MIME, Code Signing               |
| S/MIME Escrow Support                  | ❌                                              | ✅ Escrow & recovery supported                |
| External Device Support (IoT, OT)      | Limited                                         | Full CA lifecycle support                     |
| Automation APIs                        | Microsoft Graph                                 | DigiCert REST APIs                            |
| Token/SSO Cert Usage                   | Entra token signing only                        | Supports OIDC/OAuth2 token signing            |
| Advanced Use Cases (Kafka, TLS Pinning)| Manual                                          | Templates & SDK available                     |
| Support & Expertise                    | Microsoft Premier Support                       | CA-specialist enterprise-grade support        |
| Cost Model                             | Included in Microsoft E5/Intune P2               | Per-cert, subscription-based                  |

---

## 4. S/MIME Use-Cases

S/MIME is used for:
- Secure internal/external corporate email
- Non-repudiation (digital signing)
- Regulatory or compliance-aligned communications

[ Outlook ] ↔ [ Exchange / M365 ] → Email signed/encrypted using user's private key/cert
→ Recipient decrypts using sender's public cert


---

## 5. Enterprise EUC Architecture Layers & Certificate Touchpoints

| <span style="background-color: #90EE90;">**EUC Layer**</span>               | <span style="background-color: #90EE90;">**Technologies**</span>                              | <span style="background-color: #90EE90;">**Certificate Usage**</span>                                                                 |
|-----------------------------|-----------------------------------------------|----------------------------------------------------------------------------------------|
| Monitoring & Insights       | Azure Monitor, Splunk, Grafana                | TLS for telemetry, cert-auth for agent integrity                                     |
| Application Delivery        | AVD, Citrix, Intune Store                     | HTTPS certs, app signing, SCEP for remote agents                                      |
| Access Layer (ZTNA/SSE)     | Conditional Access, Netskope, Zscaler         | Device/user certs for policy enforcement, tunnel auth                                |
| Identity & Policy Layer     | Entra ID, Intune, JAMF, MDM                   | User certs, SSO token signing, secure profile distribution                           |
| Device Layer                | Windows/macOS, JAMF, Autopilot                | Device identity via SCEP/PFX, trusted MDM channels                                    |
| Network Layer               | VPN, SASE, Private Access                     | mTLS tunnels, certs for mutual auth and dynamic routing policies                      |

## Scenario: Access Flow Sequence – Cert Perspective

User connects to corporate SaaS application (via ZTNA)

1. Device boots and connects to Wi-Fi
- Uses device certificate for 802.1X (RADIUS/NAC)
- NAC inspects posture (ISE, ClearPass)

2. VPN/SASE/ZTNA agent starts
- Authenticates using mTLS (cert provisioned by Intune/PFX)
- Tunnel is established to SSE broker (e.g., Netskope)

3. User signs in with Entra ID
- SSO token issued (signed by IdP cert)
- Conditional Access checks compliance and risk

4. Application accessed (e.g., Salesforce)
- TLS session terminated at WAF (e.g., Imperva)
- Optional mTLS from broker to app backend

5. Email or messaging used (e.g., Outlook)
- S/MIME cert encrypts and signs email

6. Logs & telemetry sent to SIEM
- TLS protected channel with cert-auth agent

<details>
<summary> <strong> **User Journey: Accessing Corporate SaaS Application via ZTNA** </strong></summary>

<br>

```
┌──────────────────────────────────────────────────┐
│         📱 DEVICE BOOT & NETWORK                 │
└──────────────────────────────────────────────────┘
                        │
┌─────────────┐ 📜 802.1X ┌─────────────┐ 🔍 Posture
│   Device    │ ────────► │   Wi-Fi/NAC │ ─────────►
└─────────────┘           └─────────────┘
                        │
┌──────────────────────────────────────────────────┐
│            🔐 ZTNA AGENT STARTUP                 │
└──────────────────────────────────────────────────┘
                        │
┌─────────────┐ 📋 mTLS  ┌─────────────┐ 🌐 Tunnel
│ ZTNA Agent  │ ────────► │ SSE Broker  │ ─────────►
└─────────────┘           └─────────────┘
                        │
┌──────────────────────────────────────────────────┐
│           👤 USER AUTHENTICATION                 │
└──────────────────────────────────────────────────┘
                        │
┌─────────────┐ 🎫 SSO   ┌─────────────┐ ✅ Policy
│    User     │ ────────► │  Entra ID   │ ─────────►
└─────────────┘           └─────────────┘
                        │
┌──────────────────────────────────────────────────┐
│            💼 APPLICATION ACCESS                 │
└──────────────────────────────────────────────────┘
                        │
┌─────────────┐ 🔒 TLS   ┌─────────────┐ 🔗 mTLS
│  SaaS App   │ ◄─────── │     WAF     │ ◄────────
└─────────────┘           └─────────────┘
                        │
┌─────────────┐ 📧 S/MIME ┌─────────────┐
│    Email    │ ────────► │   Outlook   │
└─────────────┘           └─────────────┘
                        │
┌─────────────┐ 📡 TLS    ┌─────────────┐
│    Logs     │ ────────► │    SIEM     │
└─────────────┘           └─────────────┘
```

**Certificate Flow Summary:**
- **Device cert**: 802.1X network access (RADIUS/NAC posture check)
- **mTLS cert**: Secure tunnel to SSE broker (Intune/PFX provisioned)  
- **IdP cert**: Signs SSO tokens (Conditional Access policy enforcement)
- **TLS cert**: Application traffic security (WAF termination + optional backend mTLS)
- **S/MIME cert**: Email encryption/signing (Outlook/Exchange)
- **Agent cert**: Authenticated telemetry channels (SIEM/logging)
</details>

---

## 6. Certificate Management for Cloud Workloads

Cloud workloads—such as containerized applications, serverless functions, and microservices—often do not fit neatly into SCEP or PFX flows. Instead, they require **custom CA integration** for workload identity, typically through service mesh, orchestrator-native tooling, or secrets management systems.

### Common Approaches

| <span style="background-color: #90EE90;">**Technology**</span>         | <span style="background-color: #90EE90;">**Certificate Management Method**</span>                            | <span style="background-color: #90EE90;">**Use Case**</span>                                          |
|------------------------|---------------------------------------------------------------|--------------------------------------------------------|
| **SPIFFE/SPIRE**       | Issues x.509 SVIDs (SPIFFE Verifiable Identity Documents)     | Secure service-to-service mTLS in Kubernetes, VMs     |
| **Istio / Linkerd**    | Integrated CA or plugged-in CA (e.g., Citadel, Vault, Cert-Manager) | Auto-issued mTLS certs for east-west traffic         |
| **HashiCorp Vault**    | PKI secrets engine to issue short-lived certs dynamically     | Workload identity, app identity, CI/CD pipelines       |
| **Kubernetes Cert-Manager** | Issues certs via ACME, Vault, or custom issuers         | TLS certs for Ingress, webhook validation             |
| **AWS ACM / Azure Key Vault** | Stores and manages TLS certs for App Services, Functions | Bind HTTPS endpoints, manage SSL lifecycle            |

> **Recommendation**: While not covered by SCEP or PFX, workload identity is mission-critical and should align to a centralized CA (e.g., DigiCert, Vault) with short TTLs and lifecycle automation.

---


## Final Recommendations 

- Intune + DigiCert offers best-of-both-worlds: native MDM workflows with strong enterprise-grade PKI lifecycle.

- Expand certificate inventory: capture Kafka, SIEM, WAF, telemetry, and automation tooling in your CMDB.

- Align with ZTNA and SSE adoption: Ensure every endpoint and access layer service is identity-bound using certs.

- Standardise on a certificate lifecycle approach: automate renewals, alerts, expiry checks across hybrid landscape.

---
