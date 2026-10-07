# ADR-004: Build in the Portal first, rebuild in Terraform later

- **Status:** Accepted
- **Date:** 2026-10-07

## Context
Terraform has not been learned yet (course in progress, certification planned). AZ-104 itself is mostly Portal, CLI and PowerShell.

## Options considered
1. Wait to start until Terraform is learned.
2. Build in the Portal, then codify in Terraform after learning it.
3. Learn Terraform on the fly while building.

## Decision
Option 2. Early phases are tagged `ManagedBy = Portal`. Phase 16 rebuilds or imports resources into Terraform and flips the tag.

## Consequences
Manual steps get documented as they happen, which doubles as exam practice. Expect some drift between Portal-built resources and Terraform state, so plan for `terraform import` or a clean rebuild.
