# 01 - Strategy

**Roadmap phase:** 1 Strategy
**Status:** ✅ Done · **Method:** n/a · **AZ-104 domain:** n/a

## 1. Purpose
Plan, implement, and manage a personal Azure tenant that could scale up to meet the demands of an enterprise environment, following industry standards and best practices as closely as practical.

## 2. Objectives
| # | Objective | Outcome | Details |
|---|---|---|---|
| 1 | Production-style environment | A small but realistic Azure environment built on Microsoft-recommended architecture and governance practices, showing how a production workload is securely deployed, monitored, and maintained | [README](../README.md) |
| 2 | Core Azure administration skills | Hands-on experience across the AZ-104 domains: identity and governance, storage, compute, networking, monitoring, backup and recovery | [02](02-governance-identity.md), [03](03-networking.md), [04](04-workloads.md), [05](05-operations-security.md) |
| 3 | Secure, structured networking | Hub-and-spoke design with segmentation, NSGs, private endpoints, private DNS, centralized connectivity, and controlled internet access | [03](03-networking.md) |
| 4 | IaaS and PaaS | Managed services where they offer a practical advantage, plus selected IaaS workloads to demonstrate VM administration | [04](04-workloads.md) |
| 5 | Governance and operational standards | Consistent resource organization, naming, tagging, RBAC, Azure Policy, cost controls, and lifecycle practices, designed to scale beyond a single-subscription lab | [02](02-governance-identity.md), [ADR-001](decisions/ADR-001-subscription-strategy.md) |
| 6 | Infrastructure as code and automation | Terraform, Azure CLI, and PowerShell kept in version control for repeatable, auditable deployments | [ADR-004](decisions/ADR-004-portal-first-terraform-later.md), roadmap phase 16 |
| 7 | Monitoring, maintenance, and recovery | Azure Monitor, Log Analytics, alerts, backups, and update management | [05](05-operations-security.md) |
| 8 | Portfolio documentation | Architecture diagrams, deployment history, decision records, troubleshooting notes, and implementation notes in GitHub, showing both the implementation and the reasoning behind it | [decisions/](decisions/), [deployment-log](deployment-log.md) |

## 3. Target roles
Azure Engineer / Administrator · Cloud Engineer / Administrator

## 4. Architecture principles
| Principle | How it shows up |
|---|---|
| Production-oriented | Realistic Azure architecture and governance, sized for a personal learning environment. Favors maintainability, security, and operational simplicity over unnecessary enterprise complexity. |
| Hub-and-spoke | Platform, production, development, and sandbox workloads are separated by VNet, subnet, resource group, and NSG. Shared connectivity is centralized in the hub where practical. |
| PaaS plus IaaS | Prefer managed services for practical advantage. Keep selected IaaS workloads to demonstrate VM administration. |
| Security by design | Private connectivity where practical, least-privilege access, segmentation, NSGs, controlled internet access, and identity and security controls built in from the start. |
| Availability and scalability | Production components can be scaled or made highly available where appropriate, without adding unnecessary cost or complexity. |
| Governance | A consistent naming and tagging standard supports identification, cost tracking, lifecycle management, automation, and future policy enforcement. |
| Infrastructure as code | Resources are ultimately deployed through Terraform where practical. The Portal is used for learning, troubleshooting, and resources intentionally not in Terraform. |

## 5. Azure region
Default: **West US 2** (`wus2`), the closest region to me. I may deploy elsewhere if a resource is meaningfully cheaper there.

## 6. Naming convention
**Pattern:** `{resource-type}-{project}-{environment}-{purpose}-{region}`

| Segment | Values |
|---|---|
| resource-type | Standard Cloud Adoption Framework abbreviation (`vnet`, `snet`, `nsg`, `vm`, `app`, `sql`, `log`, `rsv`) |
| project | `azp` |
| environment | `prod`, `dev`, `sbx` (sandbox), `plt` (platform / shared infrastructure) |
| purpose | Short workload or function name (`hub`, `web`, `data`, `lab`) |
| region | `wus2` (West US 2) |

**Examples:** `vnet-azp-plt-hub-wus2` · `app-azp-prod-web-wus2` · `vm-azp-dev-lab-wus2`

**Exceptions**
| Resource | Rule | Example |
|---|---|---|
| Resource groups | No region suffix, because a resource group's location is only metadata | `rg-azp-plt-management` |
| Storage accounts | No hyphens, lowercase only, 3-24 characters | `stazpproddatawus2` |

## 7. Tagging convention
| Tag | Values |
|---|---|
| Environment | Prod · Dev · Sandbox · Platform |
| Workload | WebApp · Database · Storage · Networking · IaaS-Lab · Monitoring · Security · HybridConnectivity |
| Project | AzurePortfolio |
| ManagedBy | Terraform · Portal |
| CostCenter | Learning |
| Criticality | Low · Medium · High |

Tag names and values are case-sensitive in practice for reporting, so use the capitalization above exactly. Tags are enforced through Azure Policy (see [02](02-governance-identity.md)).

## 8. Cost strategy
- Free trial credits plus cost controls.
- Every resource is classified as **deployed**, **short-lived**, or **conceptual**. See [ADR-002](decisions/ADR-002-cost-tiers.md).
- Budget alerts at 50%, 80%, and 100% of actual spend, plus 100% forecast. Details in [02](02-governance-identity.md).

## 9. Subscription strategy
The Azure free trial allows one subscription. The enterprise layout (platform, prod, dev, sandbox subscriptions under management groups) is documented as a target design. I may add subscriptions after the trial ends. Rationale: [ADR-001](decisions/ADR-001-subscription-strategy.md).
