# ADR-001: Subcription has been upgraded to pay-as-you-go. 

- **Status:** Accepted
- **Date:** 2026-10-26

## Context
I was hitting limitations with deploying a few resources with the free trial subscription. The VM sizes/images  I was looking at weren't available, and the SQL server couldn't be hosted in West US 2. I wanted to keep everything consistent, and have everything in the same region if possible. I only have about a week left of free trial credits anyways, so I moved forward with upgrading to pay-as-you-go. 
The end goal will still be to migrate to the enterprise design, with separate platform, production, development and sandbox subscriptions.

## Options considered
1. **Continue with one subscription, by deploying resources in other regions when required.** I wanted to avoid this to keep everything consistent.
2. **Upgrade to pay-as-you-go in order to deploy the exact resources I wanted in the exact region.**

## Decision
Option 2. Subscription has been upgraded. I was going to upgrade at the end of the trial period anyways, but wouldn't have been able to deploy those couple resources exactly how I wanted until the upgrade happened. 

## Consequences
I will have to be more careful with costs and setting up additional monitoring alerts. For the VM, I enabled auto-shutdown at 7PM everyday, and will manually shut the VM down whenever I am not actively working on it or needing the compute.
