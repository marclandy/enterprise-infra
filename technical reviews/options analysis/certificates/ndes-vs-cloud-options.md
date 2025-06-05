# Microsoft Cloud PKI vs On-Prem NDES vs DigiCert Private PKI

## Overview

This document provides a technical comparison and reference design for evaluating Microsoft Cloud PKI, On-Premises NDES (Network Device Enrollment Service), and DigiCert Private PKI for certificate issuance and lifecycle management. It is tailored for mid-tier enterprises leveraging Intune as their primary MDM solution across a typical fleet (Windows, iOS/iPadOS, Android, macOS).

---

## Comparison Matrix

| Feature | Microsoft Cloud PKI | On-Premises NDES | DigiCert Private PKI |
|--------|----------------------|------------------|-----------------------|
| **Infrastructure** | Fully managed CA and lifecycle by Microsoft | Requires deployment of ADCS, NDES, CRL, and AIA services | Fully managed private or public CA hosted by DigiCert |
| **Integration with Intune** | Native support with PKCS and SCEP | Requires Intune Certificate Connector and SCEP | Supported via SCEP/PKCS or API integration |
| **Device Support** | Windows, macOS, iOS, Android | Windows, iOS, Android (macOS limited) | Windows, macOS, iOS, Android |
| **Management Overhead** | Minimal – no patching or CRL maintenance | High – must manage HA, patching, CRLs, HSMs | Minimal – offloaded to DigiCert |
| **High Availability** | Built-in and managed by Microsoft | Manual HA design required | Built-in cloud-based availability |
| **Security Posture** | Isolated cloud-based CA; integrates with CA logs and Intune RBAC | Local NDES may be exposed, higher risk if misconfigured | Dedicated private CA with modern access control |
| **Certificate Types** | SCEP and PKCS via Intune | SCEP only, PKCS requires additional integration | SCEP, PKCS, and advanced issuance via API |
| **BYOD Support** | Strong – via Intune app and Conditional Access | Complex – requires trusted CA distribution | Strong – trust chain easily distributed via MDM |
| **Trust Anchors** | Cloud-only or hybrid with root distribution | Full on-prem trust chain management | Private root CA distribution required internally |
| **Compliance Requirements** | Meets most standard audit needs | More customizable, better for air-gapped or tightly regulated envs | WebTrust-compliant, supports regulated verticals |
| **Lifecycle Automation** | Built into Intune | Manual scripting often required | Fully automated issuance and revocation workflows |
| **Use Case Maturity** | VPN, Wi-Fi, SSO, ZTNA support native | Legacy support for internal services and infrastructure | VPN, Wi-Fi, code signing, IoT, device ID |
| **Network Requirements** | Internet-accessible devices | Often requires internal network or VPN reachback | Internet-accessible; global endpoints |

---

## Reference Architecture (Plaintext)

```
Option 1: Microsoft Cloud PKI
+-------------------------+                      +--------------------------+
|      Managed Devices    |                      | Microsoft Cloud PKI      |
|  (Windows, iOS, macOS)  +--------------------->| (Cloud Certificate Auth) |
+-------------------------+       SCEP/PKCS     +--------------------------+
            |
            v
+-------------------------+
|   Microsoft Intune      |
+-------------------------+

Option 2: On-Prem NDES with ADCS
+-------------------------+                      +---------------------------+
|      Managed Devices    |                      | On-Prem CA + NDES + CRLs  |
|                         +--------------------->| Requires Intune Connector |
+-------------------------+       SCEP           +---------------------------+
            |
            v
+-------------------------+
|   Microsoft Intune      |
+-------------------------+

Option 3: DigiCert Private PKI
+-------------------------+                      +----------------------------+
|      Managed Devices    |                      | DigiCert Private CA        |
|  (Windows, iOS, macOS)  +--------------------->| via SCEP, PKCS, or API     |
+-------------------------+       SCEP/PKCS     +----------------------------+
            |
            v
+-------------------------+
|   Microsoft Intune      |
+-------------------------+
```

---

## Design Recommendations

### Use Microsoft Cloud PKI if:
- You're adopting Zero Trust, cloud-first principles.
- You want minimal management and modern device support.
- You're using Intune as primary MDM.

### Use On-Prem NDES if:
- You have legacy apps or infrastructure that require on-prem-only issuance.
- You're operating in highly regulated or air-gapped environments.
- You're prepared to manage CRL, AIA, and high availability manually.

### Use DigiCert Private PKI if:
- You want a fully managed private CA without Microsoft lock-in.
- You need to integrate with multiple MDMs or non-Microsoft systems.
- You need both internal and external trust models (e.g., public IoT + private enterprise).
- You require globally available, compliant, high-trust issuance.

---

## Summary

| Scenario | Recommended Option |
|----------|--------------------|
| Intune-only + Cloud-first | Microsoft Cloud PKI |
| Hybrid legacy + compliance | On-Prem NDES with ADCS |
| Multi-MDM, high-scale, global + managed | DigiCert Private PKI |

---

**Author**: Network & Infrastructure Architecture Team  
**Last Updated**: June 2025  
**Repo**: [Internal Architecture Standards](https://github.com/your-org/infra-standards)
