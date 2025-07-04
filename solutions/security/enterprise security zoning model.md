## **Security Zone Table**

| **Zone Number** | **Zone Name** | **Sub-Level Names** | **Zone Attributes** |
| :-- | :-- | :-- | :-- |
| 7 | Internet | Public Networks, Untrusted Users | **Uncontrolled, Untrusted, Unmanaged**; open access; no internal controls; only connects to Extranet/PAZ |
| 6 | Extranet | Partner Portals, B2B Interfaces | **External Controlled, Untrusted, Externally Managed**; limited trust; managed by third parties; restricted connectivity to internal zones |
| 0 | Public Zone (PZ) | Internet, External Users | Untrusted, open access, no internal controls, only connects to PAZ |
| 1 | Public Access Zone (PAZ) | DMZ, Web Servers, Reverse Proxies | Limited trust, exposed to public, strong perimeter controls, minimal services, monitored, connects to OZ/RZ via ZIP |
| 2 | Operations Zone (OZ) | User Workstations, Internal Apps | Trusted, business operations, authenticated users, moderate controls, connects to RZ/PAZ |
| 3 | Restricted Zone (RZ) | Data Center, Sensitive Repositories | Highly trusted, business-critical IT, strong access controls, encrypted comms, all entities authenticated |
| 4 | Highly Restricted Zone (HRZ) | Safety Systems, Critical Assets | Maximum trust, safety-critical/sensitive data, strictest controls, no direct public access, rigorous monitoring |

**table** including **Zone-6 (Extranet)** and **Zone-7 (Internet)**
- Internet: Uncontrolled, Untrusted, Unmanaged                                                                                    
- Extranet: External Controlled, Untrusted, Externally Managed

## **Detailed Conceptual Zoning Architecture**

```mermaid
architecture
    group "Zone-7: Internet" {
        service internet[Public Networks]
        service untrustedUsers[Untrusted Users]
    }
    group "Zone-6: Extranet" {
        service partnerPortal[Partner Portals]
        service b2b[B2B Interfaces]
    }
    group "Zone-0: Public Zone (PZ)" {
        service extUser[External Users]
    }
    group "Zone-1: Public Access Zone (PAZ)" {
        service dmz[DMZ]
        service web[Web Servers]
        service proxy[Reverse Proxy]
    }
    group "Zone-2: Operations Zone (OZ)" {
        service workstations[User Workstations]
        service intApps[Internal Applications]
    }
    group "Zone-3: Restricted Zone (RZ)" {
        service appSrv[Application Servers]
        service dbSrv[Database Servers]
        service backup[Backup Systems]
    }
    group "Zone-4: Highly Restricted Zone (HRZ)" {
        service safety[Safety Systems]
        service critical[Critical Assets]
    }

    internet:R --> L:partnerPortal
    internet:R --> L:dmz
    untrustedUsers:R --> L:partnerPortal
    partnerPortal:R --> L:dmz
    partnerPortal:R --> L:workstations
    b2b:R --> L:appSrv
    extUser:R --> L:dmz
    dmz:R --> L:workstations
    dmz:B --> T:appSrv
    workstations:R --> L:appSrv
    intApps:R --> L:dbSrv
    appSrv:R --> L:dbSrv
    dbSrv:R --> L:backup
    backup:R --> L:safety
    safety:R --> L:critical
```

**Notes:**

- **Zone-7 (Internet)** is the most untrusted and unmanaged, only interfacing with Extranet and PAZ.
- **Zone-6 (Extranet)** is for third-party/partner access, with limited, externally managed connections.
- **Zone numbering** is now in descending order of trust (higher number = less trusted).
- **Connectivity** between zones is shown by arrows; adjust or expand as needed for your specific architecture.
