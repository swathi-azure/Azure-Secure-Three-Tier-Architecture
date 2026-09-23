# Azure-Secure-Three-Tier-Architecture
Azure secure three-tier architecture with network segmentation, NSGs, Application Gateway, Bastion, private database connectivity, and monitoring.
Azure Secure Three-Tier Architecture

## Project Overview

The Azure Secure Three-Tier Architecture project demonstrates the design, implementation, security validation, monitoring, and end-to-end testing of a secure three-tier application environment using Microsoft Azure.

The architecture separates workloads into Web, Application, and Data tiers and applies network segmentation, controlled access, private connectivity, security monitoring, and application-layer validation.

---

## Architecture
[View Architecture Diagram](architecture/File_0000000ACD482078386)
The implemented traffic flow is:

Internet → Application Gateway (WAF_v2) → Web VM (NGINX) → Internal Load Balancer → App VM → SQL Private Endpoint → Azure SQL Database

Supporting Azure services include:

- Azure Bastion
- Network Security Groups (NSGs)
- Microsoft Entra ID
- Azure Key Vault
- Log Analytics Workspace
- Azure Monitor
- Microsoft Defender for Cloud
- Network Watcher

---



## Architecture Components

| Layer / Service | Implementation |
|---|---|
| Web Tier | Ubuntu 24.04 LTS Web VM with NGINX |
| Application Tier | Ubuntu Application VM with Python HTTP demonstration server |
| Data Tier | Azure SQL Database |
| Application Entry Point | Azure Application Gateway with WAF_v2 |
| Internal Traffic Distribution | Azure Internal Load Balancer |
| Private Database Access | Azure SQL Private Endpoint |
| Secure VM Administration | Azure Bastion |
| Network Security | Network Security Groups |
| Identity | Microsoft Entra ID |
| Secrets Management | Azure Key Vault |
| Monitoring | Log Analytics, Azure Monitor, Azure Monitor Agent and Data Collection Rules |
| Security Posture | Microsoft Defender for Cloud |
| Network Validation | Network Watcher |

---

## Network Segmentation

The Azure Virtual Network separates the application workloads into dedicated subnets:

- Web Subnet
- Application Subnet
- Data Subnet
- Application Gateway Subnet
- Azure Bastion Subnet

Network Security Groups were configured to control traffic between the different application layers.

---

## Web Tier

The Web tier uses WebVM01 running Ubuntu 24.04 LTS.

NGINX was installed and configured to serve the demonstration web page.

The Web VM was accessed securely through Azure Bastion.

A login demonstration was also configured on the Web layer.

---

## Application Tier

The Application tier uses App-VM-1.

A lightweight Python HTTP server was used for the application demonstration.

The Application VM was accessed through Azure Bastion and was not exposed through direct public inbound access.

The Internal Load Balancer was used to provide the intended private application path.

---

## Data Tier

The Data tier uses Azure SQL Database.

Public network access was disabled.

A Private Endpoint was configured to provide private connectivity to the SQL Database.

Private DNS resolution was configured so that the SQL hostname resolved to the private endpoint.

TCP connectivity to SQL port 1433 was successfully validated from the Application VM.

---

## Security Controls

The following security controls were implemented and validated:

- VNet segmentation
- Dedicated Web, Application and Data subnets
- Network Security Groups
- Application Gateway WAF_v2
- Internal Load Balancer
- Azure SQL Private Endpoint
- Public SQL access disabled
- Azure Bastion
- Microsoft Entra ID
- Azure Key Vault
- Microsoft Defender for Cloud

Azure Firewall was evaluated as an additional security component but was not integrated into the final tested traffic path because of a subscription/resource allocation constraint.

---

## Monitoring

Monitoring was configured using:

- Log Analytics Workspace
- Azure Monitor
- Azure Monitor Agent
- Data Collection Rules

The Web VM and Application VM were onboarded to the monitoring workflow.

---

## Validation

The project included independent connectivity tests between the application layers.

Web → Application

Result: SUCCESS

The Web VM successfully communicated with the Application tier through the intended private application path.

The Internal Load Balancer also reported the Application VM as healthy.

Application → SQL

Result: SUCCESS

The Application VM successfully established TCP connectivity to the SQL Private Endpoint on port 1433.

Final E2E Browser Test

A final end-to-end browser test was performed through the Application Gateway.

The final flow was:

Internet → Application Gateway WAF → WebVM01 / NGINX → App-VM-1 → SQL Private Endpoint → Azure SQL

Final E2E Result: SUCCESS

The E2E HTML page is a static demonstration of the connectivity tests and is not a live SQL CRUD application.

---



## Validation Summary

| Validation Area | Result |
|---|---|
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
---

## Evidence

The repository contains screenshots captured during implementation and validation, including:

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

---

## Project Lifecycle

The project was implemented and validated through the following major stages:

1. Resource Group creation
2. VNet and subnet configuration
3. NSG configuration
4. Web VM deployment
5. NGINX installation and Web application validation
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

---

## Technologies Used

- Microsoft Azure
- Azure Virtual Network
- Network Security Groups
- Azure Application Gateway
- Web Application Firewall (WAF_v2)
- Azure Virtual Machines
- NGINX
- Python HTTP Server
- Azure Internal Load Balancer
- Azure SQL Database
- Azure Private Endpoint
- Azure Private DNS
- Azure Bastion
- Microsoft Entra ID
- Azure Key Vault
- Log Analytics
- Azure Monitor
- Azure Monitor Agent
- Data Collection Rules
- Microsoft Defender for Cloud
- Network Watcher

---

## Project Outcome

This project demonstrates hands-on implementation and validation of an Azure security-focused three-tier architecture, including:

- Network segmentation
- Layered security controls
- Secure administrative access
- Private database connectivity
- Web Application Firewall protection
- Internal application traffic
- Identity and secrets management
- Monitoring and security posture review
- Layer-by-layer connectivity testing
- End-to-end browser validation

The project was subsequently cleaned up after validation to control Azure costs.
