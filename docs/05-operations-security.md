# 05 - Operations and Security

**Roadmap phases:** 13 Monitoring and alerts · 14 Backup and recovery · 15 Security hardening
**Status:** ⬜ Not started · **Method:** Portal · **AZ-104 domain:** Monitoring and maintenance, cross-cutting

## 1. Goals
Observe, protect and recover the environment, and show a hardening pass with evidence.

## 2. Design

### 2.1 Monitoring
- Log Analytics workspace `log-azp-plt-mgmt-wus2` in `rg-azp-plt-management`. Set a daily cap and short retention to control cost.
- Diagnostic settings from App Service, SQL, Storage, VPN Gateway (while up) and NSGs to the workspace.
- Action group with email notification.
- Alerts: budget, VM CPU, App Service HTTP 5xx, Activity Log alerts for role assignment changes, break-glass sign-in.

### 2.2 Backup and recovery
- Recovery Services vault `rsv-azp-plt-mgmt-wus2`, VM backup policy, test restore documented.
- SQL point-in-time restore (built in), blob soft delete.
- Azure Update Manager for the dev VM.

### 2.3 Security hardening checklist
- [ ] MFA and Conditional Access for admins (break-glass excluded)
- [ ] Defender for Cloud free tier reviewed, recommendations triaged
- [ ] No public IPs on workloads, public access disabled on data services
- [ ] Managed identities instead of secrets
- [ ] Policy compliance reviewed
- [ ] NSG rules reviewed for overly broad allows
- [ ] Key Vault documented as conceptual (or deployed if cost allows)

## 3. Implementation checklist
- [ ] Workspace, diagnostics, alerts
- [ ] Backup configured and a restore tested
- [ ] Update Manager schedule
- [ ] Hardening pass completed with before/after evidence

## 4. Verification
- Trigger a test alert and confirm the notification
- Restore a file or disk from backup
- Run a KQL query showing a role assignment change

## 5. Cost
Log Analytics ingestion and VM backup are the main costs. Keep ingestion small with targeted diagnostic settings.

## 6. Lessons and troubleshooting
Link runbooks here.
