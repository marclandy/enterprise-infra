
## Planning portfolio network & infrastructure standards

Foundational Standards + minor updates:
- Enterprise Network Security Standard → Add microsegmentation
- PKI Infrastructure Standard → Add network isolation requirements
- End User Computing Standard → Add multi-cloud VDI networking
- Enterprise Monitoring Standard → Add cloud-native requirements

New Standards Required:
P1:
Zero Trust Network Architecture Standard
Container Platform Network Architecture Standard
Virtual Desktop Infrastructure Network Standard
Enterprise Data Platform Network Architecture Standard
Multi-Tenant Observability Architecture Standard
P2:
Data Architecture - scope, to be advised

Common Network Patterns Across All Projects:
- Management Networks: 192.168.100.0/22 (OOB) + 172.16.0.0/12 (In-band)
- DMZ Zones: 10.100.0.0/16
- Application Networks: 10.0.0.0/8 with /16 per major system
- Cloud Integration: ExpressRoute/DirectConnect with BGP routing
- Security Zones: Microsegmentation with VXLAN overlays
