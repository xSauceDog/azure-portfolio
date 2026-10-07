# 04 - Workloads

**Roadmap phases:** 10 App Service · 11 SQL and Storage · 12 Dev VM
**Status:** ⬜ Not started · **Method:** Portal · **AZ-104 domains:** Compute, Storage

## 1. Goals
A small but realistic application tier with private data services, plus one IaaS VM to demonstrate VM administration.

## 2. Design
| Resource | Name | Key settings |
|---|---|---|
| App Service plan and web app | app-azp-prod-web-wus2 | Basic tier or higher (needed for VNet integration and private endpoints), managed identity, HTTPS only, VNet integration to snet-web |
| SQL server and database | sql-azp-prod-data-wus2 | Entra admin set, public network access disabled, private endpoint |
| Storage account | stazpproddatawus2 | LRS, TLS 1.2 minimum, public access disabled, blob soft delete, private endpoint |
| Linux VM | vm-azp-dev-lab-wus2 | B-series, no public IP, SSH keys, auto-shutdown, managed disk |

Open item: choose a simple sample app that reads from SQL and writes to blob, so the data path is demonstrable.
Dev VM access without Bastion: reach it over the VPN while the gateway is up, or from the admin side via a temporary approach documented in a runbook.

## 3. Implementation checklist
- [ ] Storage account with private endpoint
- [ ] SQL server and database with private endpoint
- [ ] App Service plan, web app, VNet integration, managed identity access to SQL and Storage
- [ ] Dev VM, NSG, auto-shutdown
- [ ] Sample app deployed and verified end to end

## 4. Verification
- Web app reaches SQL and Storage only over private IPs
- Public endpoints return connection failures from the internet
- VM has no public IP and is reachable only as designed

## 5. Cost
App Service Basic and the VM are the main recurring costs. Stop or deallocate the VM when idle. Check whether the Azure SQL free offer applies to your subscription.

## 6. Lessons and troubleshooting
Link runbooks here.
