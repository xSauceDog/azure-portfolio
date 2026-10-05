# Azure Portfolio - Strategy
## 1. Project Purpose
* Plan, implement, and manage a personal Azure tenant that could be scaled up to meet the demands and requirement of an enterprise environment. I'd like this project to follow industry standards and best practices as closely as possible.
## 2. Project Objectives
  1. Build a production-style Azure environment
     * Design and deploy a small but realistic Azure environment that follows Microsoft-recommended cloud architecture and governance practices. The environment will demonstrate how a production workload can be securely deployed, monitored, and maintained.
  2. Demonstrate core Azure administrative skills
     * Build hands-on experience across the major AZ-104 domains, including identity and governance, storage, compute, networking, monitoring, and backup/recovery.
  3. Implement secure and structured networking
     * Design a hub and spoke network architecture with appropriate segmentation, network security controls, private endpoints, private DNS, centralized connectivity, and controlled internet access.
  4. Demonstrate both IaaS and PaaS capabilities
     * Use Azure-managed services where they provide a practical advantage while retaining selected IaaS workloads to demonstrate VM administration and infrastructure management skills.
  5. Implement cloud governance and operational standards
     * Establish consistent resource organization, naming conventions, tagging, RBAC, Azure Policy, cost controls, and resource lifecycle practices. Governance will be designed so the environment could scale beyond the limitations of the initial single subscription lab.
  6. Implement infrastructure as code and automation
     * Use Terraform, Azure CLI, and PowerShell where appropriate to automate resource deployment and administration. Infrastructure definitions and operational scripts will be maintained in version control to provide a repeatable and auditable deployment process.
  7. Develop monitoring, maintenance, and recovery capabilities
     * Implement Azure Monitor, Log Analytics, alerts, backups, update management, and other operational capabilities necessary to monitor and maintain the environment.
  8. Produce a documented portfolio project
     * Maintain architecture diagrams, deployment history, architectural decisions, troubleshooting documentation, and implementation notes in the GitHub repository. The final project will provide evidence of both technical implementation and the decision-making process behind the environment.
## 3. Target Roles
* Azure Engineer/Administrator, Cloud Engineer/Administrator
## 4. Architecture Goals
* Production-style Azure environment
  * The environment will follow realistic Azure architecture and governance practices while remaining appropriately sized for a personal learning and portfolio environment.
  * The design will prioritize maintainability, security, and operational simplicity over unnecessary enterprise complexity.
* Hub/spoke networking
* PaaS + IaaS
* Security
* Monitoring
* Governance: Establish a consistent Azure resource naming and tagging standard that supports resource identification, cost tracking, lifecycle management, automation, and future policy enforcement.
* Infrastructure as Code: Resources should ultimately be deployed and managed through Terraform where practical, with manual Azure Portal deployments used primarily for learning, troubleshooting, or resources where Terraform is intentionally not being used.
## 5. Azure Region
* By default, resources will be deployed in West US 2 since that is the closest to me. Although if certain resources are cheaper in other regions, I may opt to deploy there.
## 6. Naming Convention
* <resource-type>-<project>-<environment>-<purpose>-<region>
  * <project> = azp
  * <environment>
    1. prod
    2. dev
    3. sbx (sandbox)
    4. plt (platform/shared infrastructure)
  * <region> = wus2 (West US 2)
## 7. Tagging Convention
* Environment
  1. Prod
  2. Dev
  3. Sandbox
  4. Platform 
* Workload
  1. WebApp
  2. Database
  3. Storage
  4. Networking
  5. IaaS-Lab
  6. Monitoring
  7. Security
  8. HybridConnectivity
* Project = AzurePortfolio
* ManagedBy
  1. Terraform
  2. Portal
* CostCenter = Learning
* Criticality
  1. Low
  2. Medium
  3. High
## 8. Cost Strategy
* Free trial credits + cost controls
## 9. Subscription Strategy
* Azure free trial only allows for 1 subscription. I may opt to increase the subscription amounts once the free trial expires.
