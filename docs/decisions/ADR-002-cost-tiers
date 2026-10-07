# ADR-002: Three cost tiers for resources (deployed, short-lived, conceptual)

- **Status:** Accepted
- **Date:** 2026-10-07

## Context
Several services in a realistic hub-and-spoke design cost far more than the trial credits can sustain if left running.

## Options considered
1. Deploy everything and run out of credits quickly.
2. Skip expensive services entirely and lose the architecture story.
3. Classify every service by cost and deploy accordingly.

## Decision
Option 3.
- **Deployed:** VNets, peering, NSGs, private DNS zones, private endpoints, App Service (Basic tier), SQL, Storage, Linux VM, Log Analytics.
- **Short-lived:** VPN Gateway, Application Gateway WAF. Build, verify, capture evidence, destroy.
- **Conceptual:** Azure Firewall, Bastion, DNS Private Resolver.

## Consequences
Diagrams mark each state visually. Short-lived services should be scripted or built in Terraform so rebuilding is cheap. Verify current pricing in the Azure pricing calculator before each short-lived deployment.
