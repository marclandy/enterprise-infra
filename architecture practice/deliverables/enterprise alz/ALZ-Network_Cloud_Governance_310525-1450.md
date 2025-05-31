**User:** Marc Landy   
**Created:** 5/29/2025 11:32  
**Updated:** 5/31/2025 15:47  

**Terraform Rbac Modules**

```
## Cloud Governance: Azure Landing Zone Artefact 

---

### Global Documentation

#### Role Constructs and RBAC Strategy

| Role Construct     | Definition                                                                 |
|--------------------|----------------------------------------------------------------------------|
| **Platform Team**  | Owns and operates Day 0 to Day 2 infrastructure, including automation, controls, and shared services. |
| **App Platform**   | Manages PaaS services and service meshes consumed by multiple App Dev teams. |
| **App Dev**        | Builds and deploys application workloads; typically consumes networking via IaC or pipelines. |
| **SRE**            | Owns observability, incident response, availability SLAs, and operates under Change Management / CAB governance. |

---

### Recommended Role Scopes

| Persona             | Custom Role Name                      | Scope             | Permissions Summary                                                                 |
|---------------------|----------------------------------------|-------------------|-------------------------------------------------------------------------------------|
| Platform Team        | `network_infra_operator`              | Subscription       | Full create/update/delete for VNets, subnets, peerings, NSGs, Private Endpoints    |
| App Platform         | `vnet_contributor_devops`            | Resource Group     | Create/read/update subnet config, IP check, VNet join; no delete or peerings       |
| App Dev              | `vnet_reader_app`                    | Resource Group     | Read-only to VNets and subnets                                                     |
| SRE                  | `sre_network_observer`               | Subscription or RG | Read/diagnostic access; scoped write to NSGs, traffic reroute, DNS override        |

---

### Justification for Dedicated SRE Role

| Area                   | Rationale                                                                 |
|------------------------|--------------------------------------------------------------------------|
| **Observability**      | Read + diagnostic access to networking objects and Azure Monitor entities |
| **Runbook Execution**  | Scoped write rights for DR (e.g., NSG rules, load balancer failover)      |
| **Change Management**  | Operates under CAB-reviewed actions, not requiring delete/ownership rights |
| **Tool Integration**   | Enables seamless monitoring + alerting with tools like Azure Monitor, Sentinel, or third-party AIOps platforms |
| **Zero Trust Operations** | Validates traffic flows, enforces zoning compliance, performs live inspection during outages |

---

## Terraform RBAC Modules Documentation

Terraform RBAC modules will be developed for each team role, per networking service, and follow this documentation pattern:

### RBAC Module: `azurerm_role_definition.<role_name>`

#### Module Attributes

- Role Scope: Resource Group / Subscription level
- Permissions: Read, Write, Action (as per matrix)
- Bound to Principle of Least Privilege

#### Standard Module Structure

- `variables.tf` – Contains all input variables for role customization
- `main.tf` – Implements the custom role definition
- `role_assignment.tf` – Optionally assigns the role to a user, group, or SPN
- `outputs.tf` – Useful outputs for downstream references
- `README.md` – Usage, examples, role scope details

---

### Sample Modules

#### `azurerm_role_definition.sre_network_observer`
| Attribute         | Description                                                                           |
|------------------|---------------------------------------------------------------------------------------|
| Scope             | Subscription or RGs containing critical network infrastructure                       |
| Permissions       | Mostly read-only, diagnostic access, scoped write to NSG rules during DR             |
| Use Case          | Enable SREs to monitor, inspect and participate in network observability workflows   |

📂 Suggested GitHub repo structure:
> 
> ```
> azure-cloud-governance-rbac/
> ├── modules/
> │   └── networking/
> │       ├── virtualNetworks/
> │       └── <service-name>/
> ├── examples/
> │   └── virtualNetworks/
> ├── pipeline/   # Future work for CI/CD
> ├── docs/       # Markdown version of this documentation
> └── roadmap.md  # Explains future CI/CD automation path
> ```

#### Modules Scaffolded
- ✅ `virtualNetworks`
- ✅ `networkSecurityGroups`
- ✅ `privateEndpoints`
- ✅ `azureFirewalls`
- ✅ `applicationGateways`
- ✅ `loadBalancers`
- ✅ `virtualNetworkGateways`
- ✅ `expressRouteCircuits`
- ✅ `networkWatchers`
- ✅ `routeTables`
- ✅ `ddosProtectionPlans`
- ✅ `bastionHosts`
- ✅ `networkManagers`

---
