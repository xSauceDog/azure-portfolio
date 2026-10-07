# 02 - Governance and Identity

**Roadmap phases:** 3 Management groups · 4 Hybrid identity · 5 RBAC, Policy, Tags, Budgets
**Status:** 🔄 In progress · **Method:** Portal · **AZ-104 domain:** Identity and governance

## 1. Goals
Establish a secure, auditable identity and governance baseline before any workload is deployed.

## 2. Design

### 2.1 Management group and subscription structure
Today: `Tenant Root` → `mg-azp` → `sub-azp-portfolio`. Target design is in `diagrams/Subscription_Overview.drawio`. Rationale: [ADR-001](decisions/ADR-001-subscription-strategy.md).

### 2.2 Admin model
| Account | Purpose | Notes |
|---|---|---|
| Daily admin account | Day-to-day administration | Member of the Azure admin group |
| Break-glass account | Emergency access only | Cloud-only, strong password stored offline, excluded from Conditional Access, sign-in alert (phase 13) |

Open item: Microsoft recommends two break-glass accounts. Document the decision to keep one.
Note: Entra *Global Administrator* is a separate role from Azure RBAC *Owner*. Name groups by purpose (for example `sg-azp-azure-admins`) so it's clear which one a group controls.

### 2.3 Groups and RBAC
| Group | Role | Scope |
|---|---|---|
| sg-azp-azure-admins | Owner | Subscription |
| sg-azp-readers | Reader | Subscription |
| sg-azp-dev-contributors | Contributor | Dev resource groups |

Open item: cloud-only versus Entra Connect-synced groups for Azure RBAC. Cloud-only avoids a dependency on on-prem.

### 2.4 Policy (start in Audit, move to Deny after reviewing compliance)
| Policy | Effect | Scope | Why |
|---|---|---|---|
| Allowed locations | Deny | Subscription | Cost and region control |
| Require tags on resource groups | Deny | Subscription | Governance and cost tracking |
| Inherit tag from resource group | Modify | Subscription | Consistent tagging |
| Network interfaces should not have public IPs | Deny | Prod resource groups | Private-by-default |

### 2.5 Naming and tags
See [01-strategy](01-strategy.md). Exception: resource group names omit the region suffix because a resource group's location is only metadata.

### 2.6 Budgets
| Budget | Amount | Alerts |
|---|---|---|
| Subscription monthly | [fill in] | 50%, 80%, 100% actual; 100% forecast |

## 3. Implementation checklist
- [x] Admin security group created and daily admin added
- [x] Resource groups created
- [ ] Change admin group role from Contributor to Owner
- [ ] Create `mg-azp` and move the subscription under it
- [ ] Configure Entra Connect sync
- [ ] Conditional Access: MFA for admins (break-glass excluded)
- [ ] Create RBAC groups and assignments
- [ ] Assign policies in Audit mode, review, then enforce
- [ ] Create budget and alerts

## 4. Verification
- `az role assignment list --scope <subscription-scope> -o table`
- Policy compliance blade shows expected results
- Sign in as a Reader and confirm writes are denied

## 5. Cost
Management groups, RBAC, Policy and Entra groups are free. Budget alerts are free.

## 6. Lessons and troubleshooting
Link runbooks here.
