# Deployment Log

## 5OCT2026
* Created global admin security group and added my 2-letter admin acccount
* Granted global admin group the "contributor" role for the root subscription
* Created resource groups
* Strategy documentation

## 6OCT2026
* Signed up for Microsoft 365 Business Premium (30-day trial licenses)
* Assigned license to my admin account and normal user account
* Updated roadmap doc
* Created "decisions" folder and underlying documents
* Created network diagram
* Updated existing diagrams and uploaded .png files for viewing instead of the draw.io file
* Updated DNS records on Porkbun to connect 365 tenant for mail
* Completed the remaining documents in the "docs/" folder

## 7OCT2026 
* Created management group and nested the existing subscription under it
* Renamed existing global admin security group to sg-azp-azure-admins and assigned it the owner role at the management group level
* Assigned my 2-letter admin account to the group
* Created the sg-azp-entra-global-admins and assigned it the global admin role
* Assigned 2-leter admin to the group
* Uploaded higher resolution png images for the architecture diagrams
* Created the sg-azp-dev-contributors group and sg-azp-readers security groups

## 21OCT2026
* Assigned the "reader" role to the sg-azp-readers security group at the subscription level
* Assigned the "contributor" role to the sg-azp-dev-contributors security group, on both of the "dev" resource groups
* Created a policy at the subscription level to require the tag "Environment" on all resource groups
* Created a policy for each "prod" resource group, prohibiting the NIC containing a public IP

## 22OCT2026
* Created the hub and spoke virtual networks, as well as the corresponding subnets
* Created an NSG for each subnet and assigned to the corresponding subnet
* Created peering links between the hub VNet and both of the spoke VNets
* Created private DNS zones and linked them to both the hub and prod VNets
