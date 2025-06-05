# Integrating SD-WAN and Firewall Solutions Within an Azure Hub-and-Spoke Architecture

This decision framework summarises routing strategy options when integrating SD-WAN appliances and firewalls into an Azure hub-and-spoke architecture. Each question includes a table highlighting the routing choices—static, dynamic, or overlay—and their respective pros and cons.

---

## Question 1: Routing Firewall-to-SDWAN – Static or Dynamic?

This decision pertains to how the firewall directs traffic to SD-WAN appliances.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| 1a: Static Routing | Configure static routes on the firewall NICs pointing to SD-WAN appliances via an Azure Load Balancer. | Simple setup; no need for dynamic routing protocols. | Lacks flexibility; cannot direct specific branches to specific SD-WAN NVAs; potential issues with single-attached branches. |
| 1b: Dynamic Routing with BGP | SD-WAN appliances advertise routes via Azure Route Server to the firewall NICs. | Enables specific branch-to-NVA routing; dynamic adaptation to network changes. | More complex configuration; requires careful route propagation management to avoid loops. |
| 1c: Overlay Tunnels | Establish overlay tunnels between firewall and SD-WAN appliances. | Simplifies routing decisions; encapsulates traffic between endpoints. | Adds complexity in tunnel management; potential performance overhead. |

---

## Question 2: Routing SDWAN-to-Firewall – Static or Dynamic?

This decision focuses on how SD-WAN appliances route traffic back to the firewall.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| 2a: Static Routing | SD-WAN appliances use static routes to forward traffic to the firewall. | Cost-effective; straightforward configuration. | Requires manual updates; not scalable in dynamic environments. |
| 2b: Dynamic Routing with BGP | SD-WAN appliances use BGP to learn routes to the firewall. | Automatically adapts to network changes; scalable. | Increased complexity; requires BGP configuration and management. |
| 2c: Overlay Tunnels | Use overlay tunnels from SD-WAN appliances to the firewall. | Simplifies routing; encapsulates traffic. | Tunnel management overhead; potential performance impact. |

---

## Question 3: Route Advertisement into SDWAN – Static or Dynamic?

This decision involves how routes are advertised from Azure into the SD-WAN network.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| 3a: Static Advertisement | Manually configure route advertisements into SD-WAN. | Full control over advertised routes. | High operational overhead; not suitable for large or dynamic environments. |
| 3b: Dynamic Advertisement with BGP | Use BGP to dynamically advertise routes into SD-WAN. | Scales well; reduces manual configuration. | Requires BGP setup and monitoring; potential for route flapping. |

---

## Question 4: Routing Spoke-to-Firewall – Static or Dynamic?

This decision addresses how spoke VNets route traffic to the firewall in the hub.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| 4a: Static UDRs | Apply static User Defined Routes in spoke VNets pointing to the firewall. | Simple to implement; predictable routing. | Manual updates needed; not scalable for numerous spokes. |
| 4b: Dynamic Routing with Azure Route Server | Use Azure Route Server to propagate routes to spokes. | Centralized route management; scalable. | Requires Azure Route Server setup; increased complexity. |

---

## Question 5: Do You Need Routing to ExpressRoute?

This decision determines whether routing to on-premises networks via ExpressRoute is necessary.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| 5a: No ExpressRoute | All traffic remains within Azure or uses internet-based connections. | Simplifies network design; reduces costs. | Limited connectivity to on-premises resources. |
| 5b: Yes, with Static Routing | Use static routes to direct traffic to ExpressRoute. | Predictable routing; straightforward setup. | Manual route management; less adaptable to changes. |
| 5c: Yes, with Dynamic Routing | Use BGP to dynamically route traffic to ExpressRoute. | Automatically adapts to network changes; scalable. | Requires BGP configuration; increased complexity. |

---

## Question 6: Routing to Other Azure Regions – Static or Dynamic?

This decision pertains to how traffic is routed between Azure regions.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| 6a: Static Routing | Manually configure routes between regions. | Full control over inter-regional traffic paths. | High maintenance; not scalable for multiple regions. |
| 6b: Dynamic Routing with BGP | Use BGP to dynamically manage inter-regional routes. | Scales well; adapts to network changes. | Requires BGP setup and management; potential for increased complexity. |

---

**Source:** [Cloudtrooper: Designing your SDWAN and Firewall into Azure Hub and Spoke (2023)](https://blog.cloudtrooper.net/2023/11/24/designing-your-sdwan-and-firewall-into-azure-hub-and-spoke/)
