# ADR-001: Single subscription now, multi-subscription as the documented target

- **Status:** Accepted
- **Date:** 2026-10-07

## Context
The Azure free trial allows one subscription. An enterprise design would separate platform, production, development and sandbox into their own subscriptions under management groups.

## Options considered
1. **One subscription, environments separated by resource group, VNet, tags and RBAC scope.** Works on the trial and costs nothing extra.
2. **Pay-as-you-go with multiple subscriptions from day one.** Matches enterprise layout but ends the trial benefit and adds cost.

## Decision
Option 1. Create `mg-azp` and place the subscription under it. Show the full management group and subscription layout as a target design in `Subscription_Overview.drawio`.

## Consequences
Policy and RBAC are assigned at subscription scope instead of management group scope. Revisit when more subscriptions become available. Moving resources between subscriptions and re-scoping assignments will be the migration work.
