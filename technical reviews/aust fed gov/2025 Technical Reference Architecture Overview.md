### 2025 Technical Reference Architecture Overview

This architecture represents a federated government environment supporting secure collaboration, 
cloud connectivity, and compliant surveillance systems. 
The use-cases reflect hybrid operations with regional sites, shared services, and strong data governance.

---

## Enterprise Collaboration & AV Services

```
[ Microsoft 365 ] - Exchange Online, Teams, OneDrive
        |
[ Microsoft Teams Rooms (MTR) ]
        |
    [ Crestron AV System ] <—> [ Room Control + Digital Signage + Scheduling ]
        |                              
    [ AV VLAN ]  <—> [ Cisco LAN Switches ] —> [ QoS Policies | AV over IP ]
```

- **Crestron Integration**: Supports Microsoft Teams Room (MTR) automation, scheduling, and room control.
- **QoS and AV Segmentation**: Video and control traffic separated via VLANs and QoS classification.
- **Monitoring/Management**: SNMP or API integration with NMS (e.g., Cisco DNAC, Crestron XiO Cloud).

---

## Telephony & Voice Recording Architecture

```
[ Avaya Call Manager / Aura ] —> [ Contact Centre | Internal Voice | SIP Gateway ]
        |
[ Voice Recording System (e.g., Verint / NICE) ] —> [ Archive Storage | Playback ]
        |
[ Cisco WAN/MPLS ] —> [ SD-WAN Edge / DIA / VPN ] —> [ AWS VPC / Cloud Services ]
```

- **Avaya Platforms**: Core IP telephony for operations, potentially hybrid with Teams Direct Routing.
- **Voice Recording**: Used for compliance, safeguarding, and quality monitoring.
- **SD-WAN**: Ensures traffic prioritization and WAN failover resilience.

---

## Hybrid Cloud Network & Security Framework

```
[ AWS VPC / TGW / GWLB / Direct Connect ]
        |
[ Transit VPC / Shared Services VPC ]
        |
[ Azure AD / AADDS / SSO + MFA ]
        |
[ Citrix Netscaler / Palo Alto Firewalls for Zoning ]
```

- **AWS AU-Central (GovCloud)**: IRAP-protected cloud hosting for sensitive workloads.
- **Transit Gateway (TGW)**: Simplified routing between NDIA environments and shared services.
- **Citrix Netscaler + Palo Alto**: Enforces access zoning, policy-based routing, and app isolation.
- **Identity Governance**: Federated identity with AAD, enforcing Zero Trust access control.

---

## Security, Privacy & Compliance Considerations

- All components use-cases align with:
  - **Australian Government ISM / PSPF**
  - **Data Sovereignty (AU hosted)**
  - Secure logging, auditing, and RBAC controls are mandatory across AV, voice, and network layers.

---

## Notes

- Designed with a distributed, multi-office and hybrid workforce in mind.
- Optimised for service centres, partner collaboration, and cloud-enablement goals.
- Easily extendable to other federal agencies with similar security/compliance requirements.
