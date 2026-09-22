# Azure Secure Three-Tier Architecture

## Validation Documentation

### 1. Project Overview

The Azure Secure Three-Tier Architecture project was designed and implemented as a security-focused Azure cloud architecture separating Web, Application, and Data workloads.

The architecture demonstrates network segmentation, security controls, private connectivity, monitoring, and application-layer validation using Microsoft Azure services.

### 2. Architecture

The implemented architecture follows a three-tier design:

Internet → Application Gateway (WAF_v2) → Web VM (NGINX) → Internal Load Balancer → App VM → SQL Private Endpoint → Azure SQL Database

Supporting security and management services include:

- Azure Bastion
- Network Security Groups
- Microsoft Entra ID
- Azure Key Vault
- Log Analytics
- Azure Monitor
- Microsoft Defender for Cloud
- Network Watcher

The Web, Application, and Data tiers were separated into dedicated subnets within the Azure Virtual Network.

### 3. Web Tier Validation

The Web tier was implemented using WebVM01 running Ubuntu 24.04 LTS.

NGINX was installed and configured to serve the initial "index.html" demonstration page.

The Web VM was accessed securely through Azure Bastion.

The Web VM private IP was:

"10.0.2.4"

The initial Web application page was successfully validated through the Application Gateway path.

### 4. Application Tier Validation

The Application tier was implemented using App-VM-1.

The Application VM used private IP:

"10.0.3.4"

A lightweight Python HTTP server was used to provide the application demonstration endpoint.

The Application VM was accessed through Azure Bastion and was not exposed through direct public inbound access.

### 5. Web-to-Application Connectivity Test

Connectivity between the Web tier and Application tier was independently tested.

The Web VM successfully communicated with the Application tier through the intended private application path.

Result: Web → Application = SUCCESS

The Internal Load Balancer also reported the Application VM as healthy.

### 6. Data Tier Validation

The Data tier was implemented using Azure SQL Database.

Public network access was disabled.

A Private Endpoint was configured for the SQL Database.

The SQL Private Endpoint used private IP:

"10.0.4.4"

Private DNS resolution successfully resolved the SQL hostname to the private endpoint.

TCP connectivity to SQL port "1433" from the Application VM was successfully tested.

Result: Application → SQL Private Endpoint = SUCCESS

### 7. End-to-End Demo Validation

After the individual layer connectivity tests were completed, an additional E2E demonstration configuration was added.

The existing NGINX Web layer was extended with an additional:

"/e2e-test.html"

endpoint.

This endpoint was configured to proxy the request from the Web layer toward the Application VM.

On the Application layer, a lightweight Python HTTP server was configured to serve the corresponding:

"e2e-test.html"

demonstration page.

The final E2E flow was:

Internet → Application Gateway WAF → WebVM01 / NGINX → App-VM-1 → SQL Private Endpoint → Azure SQL

The final browser test successfully reached the E2E demonstration page through the Application Gateway.

The demonstration displayed successful Web-to-App and App-to-SQL validation.

Final E2E Result: SUCCESS

The E2E HTML page is a static demonstration of the connectivity tests and is not a live SQL CRUD application.

### 8. Security Validation

The following security controls were validated:

- VNet segmentation
- Web/Application/Data subnet separation
- Network Security Groups
- Application Gateway WAF_v2
- Internal Application Load Balancer
- Private Azure SQL connectivity
- Public SQL access disabled
- Azure Bastion
- Microsoft Entra ID
- Azure Key Vault
- Microsoft Defender for Cloud

Azure Firewall was evaluated as an additional security component, but its deployment could not be completed because of a subscription/resource allocation constraint.

Therefore, Azure Firewall was not integrated into the final tested traffic path and no Firewall-based validation result is claimed.

### 9. Monitoring Validation

Monitoring components were configured using:

- Log Analytics Workspace
- Azure Monitor
- Azure Monitor Agent
- Data Collection Rules

The Web VM and Application VM were onboarded to the monitoring workflow.

The monitoring configuration was reviewed as part of the project validation.

### 10. Security Posture

Microsoft Defender for Cloud was reviewed to assess the security posture of the Azure environment.

The Secure Score observed during the project was approximately 30%.

The score represents the security posture at the time of assessment and was not treated as a project failure.

Paid Defender CSPM features were not enabled because the project was designed with cost control in mind.

### 11. Validation Summary

| Validation Area | Result |
| --- | --- |
| VNet and Subnets | SUCCESS |
| NSG Configuration | SUCCESS |
| Web VM / NGINX | SUCCESS |
| Application VM | SUCCESS |
| Application Gateway WAF | SUCCESS |
| Application Gateway Backend Health | Healthy 1/1 |
| Internal Load Balancer | SUCCESS |
| Internal Load Balancer Health | 100% Healthy |
| Web → Application | SUCCESS |
| Application → SQL Private Endpoint | SUCCESS |
| SQL TCP 1433 | SUCCESS |
| Key Vault | SUCCESS |
| Log Analytics | SUCCESS |
| Azure Monitor | SUCCESS |
| Microsoft Entra ID | SUCCESS |
| Defender for Cloud Review | COMPLETED |
| Final E2E Demonstration | SUCCESS |
| Azure Firewall | Not deployed / not integrated |

### 12. Evidence

The following evidence was captured during project validation:

1. Resource Group / Azure deployment
2. VNet and Subnets
3. Network Security Groups
4. Web VM
5. Application VM
6. Application Gateway / WAF
7. Application Gateway Backend Health
8. Internal Load Balancer
9. Internal Load Balancer Health
10. Azure SQL / Private Endpoint
11. Web Virtual Machine NGINX Login Demo
12. Application-to-SQL Connectivity Test
13. Azure Key Vault
14. Log Analytics
15. Azure Monitor
16. Microsoft Entra ID
17. Microsoft Defender for Cloud
18. Final E2E Browser Test

### 13. Project Lifecycle

1. Resource Group creation
2. VNet and subnet configuration
3. NSG configuration
4. Web VM deployment
5. NGINX installation and initial Web application validation
6. Application VM deployment
7. Azure Bastion configuration
8. Internal Load Balancer configuration
9. Application Gateway WAF configuration
10. Azure SQL Database and Private Endpoint configuration
11. Key Vault configuration
12. Log Analytics and Azure Monitor configuration
13. Microsoft Entra ID configuration
14. Defender for Cloud review
15. Network connectivity testing
16. Final E2E demonstration configuration
17. Final End-to-End validation
18. Evidence capture and project documentation
19. Project resource cleanup

The final project demonstrates hands-on experience with Azure networking, security controls, private connectivity, monitoring, application-layer validation, and End-to-End testing.
