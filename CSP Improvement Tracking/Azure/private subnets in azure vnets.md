---
layout: post
title: "Azure VNet Private Subnets: General Availability and Default Behavior Change"
date: 2025-05-28
author: Marc Landy
categories: [enterprise, feature-ga, azure-VM, private-subnet-outbound]
---
# Azure VNet Private Subnets: 
- General Availability and Default Behavior Change

## Executive Summary

| Attribute             | Details                                                                                                                                                                                                                                 |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Feature Name**      | Azure VNet Private Subnets                                                                                                                                                                                                             |
| **Feature Arrival Date** | September 30, 2025                                                                                                                                                                                                                      |
| **Problem**           | By default, newly created Azure VNets have outbound internet access enabled, which may conflict with security best practices and compliance requirements.                                                                               |
| **Solution**          | Introduction of private subnets in Azure VNets, with the default setting `defaultOutboundAccess=false` for all new VNets created after September 30, 2025. This change aligns with the "secure by default" principle.                   |
| **Implication**       | New VNets will not have default outbound internet access. To enable outbound connectivity, configurations such as routing through a central firewall, using a NAT Gateway, adding a public load balancer, or assigning a public IP are required. |
| **Rationale**         | Enhancing security posture by minimizing unintended exposure to the internet, thereby aligning with industry best practices and compliance standards.                                                                                   |
| **Benefit**           | Improved default security for Azure VNets, reducing the risk of unauthorized outbound traffic and aligning with organizational security and compliance requirements.                                                                   |
| **Feature URL**       | [Default outbound access for VMs in Azure will be retired—transition to a new method of internet access](https://azure.microsoft.com/en-us/updates/default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access/) |

## Overview

Azure has announced that starting **September 30, 2025**, all newly created Virtual Networks (VNets) will have **private subnets by default**, meaning they will not have outbound internet access unless explicitly configured. This change sets the `defaultOutboundAccess` property to `false`, reinforcing Azure's commitment to the "secure by default" principle.

### Key Points:

- **Default Behavior Change**: New VNets will not have outbound internet access by default.
- **Configuration Options for Outbound Access**:
  - **Routing through a central firewall**: Direct traffic through a managed firewall for inspection and control.
  - **Using a NAT Gateway**: Enable outbound internet access while keeping resources private.
  - **Adding a public load balancer**: Use load balancers to manage outbound connections.
  - **Assigning a public IP**: Directly assign public IPs to resources requiring internet access.
- **Existing VNets**: No changes will be applied to existing VNets. However, administrators can manually update existing subnets to adopt the new private subnet behavior.

## Action Items for Network & Infrastructure Architects

- **Review Deployment Templates**: Ensure that infrastructure-as-code templates (e.g., ARM, Bicep, Terraform) explicitly define outbound access configurations as needed.
- **Update Network Design Documentation**: Reflect the new default behavior in network topology and design documents.
- **Communicate Changes to Stakeholders**: Inform application and security teams about the change to plan for necessary adjustments.
- **Audit Existing VNets**: Consider updating existing VNets to private subnets to enhance security posture.

For more details, refer to the official announcement: [Default outbound access for VMs in Azure will be retired—transition to a new method of internet access](https://azure.microsoft.com/en-us/updates/default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access/)

## Private Subnets in Azure VNet's

![Private Subnets in Azure VNet's](https://github.com/marclandy/enterprise-infra/blob/6aa82a4f025596650f00f71cce182bd1472a9045/CSP%20Improvement%20Tracking/images/Private%20Subnets%20in%20Azure%20VNet's.jpeg)

