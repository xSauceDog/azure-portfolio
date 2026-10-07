# ADR-003: DNS resolution of private endpoints from on-prem

- **Status:** Proposed (decide during phase 7, hybrid connectivity)
- **Date:** 2026-10-07

## Context
Azure VNets resolve `privatelink.*` names through linked private DNS zones automatically. The on-prem domain controller does not, so private endpoint names would resolve publicly (or not at all) from on-prem.

## Options considered
1. **Azure DNS Private Resolver in the hub.** The enterprise answer, but a recurring cost. Conceptual only.
2. **DNS forwarder VM in the hub.** A conditional forwarder on the on-prem DC points `privatelink` zones at the VM, which forwards to Azure DNS (168.63.129.16). Cheap, a bit more to maintain.
3. **Hosts-file entries on lab machines.** Free and fast, not realistic.

## Decision
To be decided. Document option 1 as the target design.

## Consequences
Fill in after deciding. Note the DNS lesson that conditional forwarders and client DNS settings are the most common failure points.
