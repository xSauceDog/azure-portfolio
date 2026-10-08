# Roadmap

Progress tracker. Detailed write-ups are in the linked docs, chronological work is in [deployment-log.md](deployment-log.md), and the reasoning behind choices is in [decisions/](decisions/).

**Status:** ✅ Done · 🔄 In progress · ⬜ Not started · ⏱ Short-lived (deploy, verify, destroy) · 📐 Conceptual only
**Method:** Phases 3-15 are built in the Portal first, then rebuilt in Terraform in phase 16.

*Last updated: 2026-10-07*

| # | Phase | Status | AZ-104 domain | Doc |
|---|---|---|---|---|
| 1 | Strategy | ✅ | n/a | [01](01-strategy.md) |
| 2 | Plan and design (diagrams, address plan) | ✅ | n/a | [diagrams/](../diagrams/) |
| 3 | Management groups and subscription structure | ✅ | Identity and governance | [02](02-governance-identity.md) |
| 4 | Hybrid identity (Entra Connect, groups, break-glass, Conditional Access) | ⬜ | Identity and governance | [02](02-governance-identity.md) |
| 5 | RBAC, Policy, Tags, Budgets | 🔄 | Identity and governance | [02](02-governance-identity.md) |
| 6 | Hub-and-spoke networking | ⬜ | Networking | [03](03-networking.md) |
| 7 | Hybrid connectivity (S2S VPN, hybrid DNS) | ⏱ | Networking | [03](03-networking.md) |
| 8 | Private DNS and private endpoints | ⬜ | Networking | [03](03-networking.md) |
| 9 | Application Gateway and WAF | ⏱ | Networking | [03](03-networking.md) |
| 10 | App Service | ⬜ | Compute | [04](04-workloads.md) |
| 11 | SQL and Storage | ⬜ | Storage | [04](04-workloads.md) |
| 12 | Dev VM (IaaS) | ⬜ | Compute | [04](04-workloads.md) |
| 13 | Monitoring and alerts | ⬜ | Monitoring and maintenance | [05](05-operations-security.md) |
| 14 | Backup and recovery | ⬜ | Monitoring and maintenance | [05](05-operations-security.md) |
| 15 | Security hardening | ⬜ | Cross-cutting | [05](05-operations-security.md) |
| 16 | IaC (Terraform) and CI/CD | ⬜ | Outside AZ-104 | 06 (created when started) |
| 17 | Testing and troubleshooting | ⬜ | All | [runbooks/](../runbooks/) |
| 18 | Documentation and portfolio polish | 🔄 | n/a | [README](../README.md) |

## Conceptual only (documented, not deployed)

| Service | Why not deployed | What it would do |
|---|---|---|
| Azure Firewall | Cost | Central egress filtering and spoke-to-spoke control via UDRs |
| Azure Bastion | Cost | Browser-based RDP/SSH without public IPs |
| DNS Private Resolver | Cost | On-prem to Azure private DNS resolution |
| Extra subscriptions (platform, prod, dev, sbx) | Trial limit | Isolation of RBAC, policy and cost per environment |
