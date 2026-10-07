# 03 - Networking

**Roadmap phases:** 6 Hub-and-spoke · 7 Hybrid connectivity · 8 Private DNS and private endpoints · 9 Application Gateway and WAF
**Status:** ⬜ Not started · **Method:** Portal · **AZ-104 domain:** Networking

## 1. Goals
Segmented hub-and-spoke network with private access to PaaS and a documented path to on-prem. Diagram: `diagrams/Network.drawio`.

## 2. Address plan
| VNet | CIDR | Subnet | CIDR | Purpose |
|---|---|---|---|---|
| vnet-azp-plt-hub-wus2 | 10.0.0.0/24 | GatewaySubnet | 10.0.0.0/27 | VPN Gateway (short-lived) |
| | | AzureFirewallSubnet | 10.0.0.64/26 | Conceptual |
| | | AzureBastionSubnet | 10.0.0.128/26 | Conceptual |
| vnet-azp-prod-spoke-wus2 | 10.1.0.0/24 | snet-appgw | 10.1.0.0/27 | App Gateway (short-lived) |
| | | snet-pe | 10.1.0.32/27 | Private endpoints |
| | | snet-web | 10.1.0.64/26 | App Service VNet integration |
| vnet-azp-dev-spoke-wus2 | 10.2.0.0/24 | snet-dev | 10.2.0.0/26 | Dev VM |
| vnet-azp-sbx-spoke-wus2 | 10.3.0.0/24 | (optional) | | Sandbox |
| On-prem LAN | 192.168.1.0/24 | | | Placeholder, replace with real range. Must not overlap. |

## 3. Design notes
- **Peering:** hub to each spoke. Enable gateway transit on the hub and use-remote-gateways on spokes once the VPN gateway exists. Spokes are not peered to each other, so dev and prod stay isolated (no firewall to route between them).
- **NSGs:** one per workload subnet, default-deny inbound, explicit allows only. No NSG on GatewaySubnet.
- **Hybrid connectivity:** site-to-site VPN (local network gateway, VPN gateway, connection). Confirm the home router supports route-based IPsec/IKEv2. If not, document S2S as conceptual and use P2S or a router-based VPN for access.
- **Private DNS:** `privatelink.azurewebsites.net`, `privatelink.database.windows.net`, `privatelink.blob.core.windows.net`, linked to hub and prod. On-prem resolution: [ADR-003](decisions/ADR-003-private-endpoint-dns.md).
- **Private endpoints:** web app, SQL, blob. Public network access disabled on SQL and Storage.
- **Application Gateway WAF:** short-lived. WAF policy in prevention mode, backend is the App Service private endpoint.

## 4. Implementation checklist
- [ ] Create hub and spoke VNets and subnets
- [ ] Create NSGs and associate
- [ ] Peer hub to spokes
- [ ] Create private DNS zones and VNet links
- [ ] Deploy VPN gateway and S2S connection (short-lived), capture evidence, delete
- [ ] Deploy Application Gateway WAF (short-lived), test, capture evidence, delete

## 5. Verification
- Effective routes and effective security rules on the VM NIC
- `nslookup` from the dev VM resolves private endpoint names to 10.1.0.x
- `Test-NetConnection` from on-prem to a private IP while the tunnel is up
- Confirm spoke-to-spoke traffic is blocked

## 6. Cost
| Item | Tier | Notes |
|---|---|---|
| VNets, peering, NSGs | Deployed | Low or no cost; peering has data transfer charges |
| Private DNS zones, private endpoints | Deployed | Small monthly charges |
| VPN Gateway, App Gateway WAF | Short-lived | Hourly billing; check the pricing calculator |
| Firewall, Bastion, Private Resolver | Conceptual | Not deployed |

## 7. Lessons and troubleshooting
Link runbooks here.
