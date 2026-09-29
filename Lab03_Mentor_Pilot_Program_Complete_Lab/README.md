<div align="center">

## Azure Functions Serverless HTTP Endpoint Deployment

**Author:** Wadondera A. Collins  
**Role:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Platform:** Microsoft Azure  
**Project Type:** Serverless Computing & Monitoring  

</div>

---

# Project Overview

This project demonstrates the deployment, testing, monitoring, and security hardening of a serverless application using Azure Functions. The lab focused on creating an Azure Function App using the Flex Consumption hosting plan, deploying an HTTP-triggered function through Azure Cloud Shell, validating public accessibility, enabling monitoring through Application Insights, restricting endpoint access using Function Keys, reviewing invocation logs, and performing complete resource cleanup.

The implementation showcases modern cloud-native development practices and serverless architecture principles where compute resources are provisioned automatically and billed only during execution.

---

# Executive Summary

The objective of this lab was to build and manage a production-style serverless endpoint in Microsoft Azure.

During the exercise, an Azure Function App was deployed using the Node.js runtime and the Flex Consumption plan. An HTTP-triggered function named GetStatus was created and published through Azure Functions Core Tools. The endpoint was tested for public accessibility and later secured by modifying the authorization level from anonymous to function.

Monitoring and observability were implemented through Application Insights and Log Analytics integration, allowing request tracking, performance monitoring, and invocation analysis.

The project concluded with resource cleanup to prevent unnecessary Azure consumption costs.

---

# Recruiter-Focused Skills Demonstrated

## Cloud Computing
- Microsoft Azure Administration
- Azure Function Apps
- Serverless Architecture
- Resource Group Management
- Application Monitoring

## DevOps & Automation
- Azure Cloud Shell
- Azure CLI
- Azure Functions Core Tools
- Command Line Operations
- Application Deployment Automation

## Security
- Function Key Authentication
- Endpoint Access Restriction
- Authentication Configuration
- Least Privilege Concepts

## Monitoring & Observability
- Azure Application Insights
- Log Analytics
- Transaction Search
- Request Monitoring
- Performance Analysis

## Troubleshooting
- Deployment Validation
- Endpoint Testing
- Log Investigation
- Runtime Verification

---

# Project Objectives

- Create a serverless Function App.
- Configure a Flex Consumption hosting plan.
- Enable Application Insights monitoring.
- Create an HTTP-triggered Azure Function.
- Deploy the function through Azure Cloud Shell.
- Test internet accessibility.
- Secure the endpoint using Function Keys.
- Review invocation logs and telemetry.
- Clean up Azure resources.

---

# Architecture Overview

```text
User Browser
      |
      v
Azure Function Endpoint
      |
      v
Azure Function App
      |
      +----------------+
      |                |
      v                v
Application Insights  Log Analytics
      |
      v
Monitoring & Diagnostics
```

---

# Technologies and Services Used

## Microsoft Azure Services

- Azure Function App
- Azure Resource Groups
- Azure Cloud Shell
- Azure Functions Core Tools
- Application Insights
- Log Analytics Workspace
- Azure CLI

## Runtime Stack

- Node.js (Latest LTS)
- JavaScript Programming Model V4

## Hosting Configuration

- Flex Consumption Plan
- Serverless Execution Model
- 2048 MB Instance Size

---

# Lab Environment

| Component | Configuration |
|------------|--------------|
| Cloud Platform | Microsoft Azure |
| Compute Model | Serverless |
| Runtime | Node.js |
| Language | JavaScript |
| Monitoring | Application Insights |
| Logging | Log Analytics |
| Deployment Method | Azure Functions Core Tools |
| Shell Environment | Azure Cloud Shell (Bash) |

---

# Recommended Repository Structure

```text
mentor-pilot-azure-functions/
├── README.md
├── src/
│   └── functions/
│       └── GetStatus.js
├── host.json
├── package.json
└── .gitignore
```

> A separate project report and its screenshot evidence can be added later without making the README unnecessarily heavy.

---

# Implementation Methodology

## Phase 1: Environment Preparation

Created a dedicated resource group:

```bash
rg-gp-functions-endpoint
```

Purpose:

- Resource organization
- Easier lifecycle management
- Simplified cleanup
- Cost management

---

## Phase 2: Function App Deployment

Configured:

- Resource Group
- Node.js Runtime
- Flex Consumption Plan
- Monitoring Integration
- Application Insights

Validation included:

- Successful deployment
- Running status verification
- Monitoring configuration confirmation

---

## Phase 3: Function Creation

Created project folder:

```bash
mkdir func-gp-endpoint && cd func-gp-endpoint
```

Initialized Azure Functions project:

```bash
func init --worker-runtime node --language javascript --model V4
```

Generated HTTP Trigger Function:

```bash
func new --name GetStatus --template "HTTP trigger" --authlevel anonymous
```

Validation:

```bash
ls src/functions/
```

Expected result:

```text
GetStatus.js
```

---

## Phase 4: Deployment

Retrieved Function App name:

```bash
FUNC_APP_NAME=$(az functionapp list \
--resource-group rg-gp-functions-endpoint \
--query "[0].name" -o tsv)
```

Published function:

```bash
func azure functionapp publish $FUNC_APP_NAME
```

Outcome:

- HTTP endpoint generated
- Public invoke URL created
- Cloud deployment completed successfully

---

## Phase 5: Endpoint Validation

Initial Testing:

- Browser validation
- Incognito browser validation
- Anonymous access validation

Expected response:

```text
Hello, world!
```

Key Findings:

- Endpoint accessible publicly
- No authentication required
- Function responding successfully

---

## Phase 6: Monitoring Validation

Verified:

- Application Insights Connected
- Logging Enabled
- Telemetry Collection Active

Reviewed:

- Transaction Search
- Request Tracking
- Invocation Records
- Execution Status
- Request Duration

Sample Query:

```kusto
requests
| order by timestamp desc
```

---

## Phase 7: Security Hardening

Changed authorization level:

```bash
sed -i "s/authLevel: 'anonymous'/authLevel: 'function'/" src/functions/GetStatus.js
```

Verified:

```bash
grep authLevel src/functions/GetStatus.js
```

Redeployed function.

Security Improvements:

- Anonymous access removed
- Function Key authentication required
- Endpoint protection enforced

Expected behavior:

Without key:

```text
401 Unauthorized
```

With key:

```text
Hello, world!
```

---

# Validation Checklist

## Infrastructure

- [x] Resource Group Created
- [x] Function App Created
- [x] Flex Consumption Enabled
- [x] Application Insights Enabled

## Function Deployment

- [x] Function Project Initialized
- [x] GetStatus Function Created
- [x] Function Published Successfully
- [x] Invoke URL Generated

## Function Testing

- [x] Browser Access Confirmed
- [x] Anonymous Access Validated
- [x] HTTP Response Validated

## Security Validation

- [x] Authorization Level Modified
- [x] Function Key Retrieved
- [x] Unauthorized Requests Blocked
- [x] Authorized Requests Successful

## Monitoring Validation

- [x] Telemetry Captured
- [x] Transactions Logged
- [x] Request Analytics Available
- [x] Application Insights Connected

---

# Lessons Learned

- Serverless applications reduce infrastructure management overhead.
- Flex Consumption provides cost-efficient execution.
- Application Insights is essential for observability.
- Function Keys improve endpoint security.
- Validation after every deployment stage reduces troubleshooting complexity.
- Monitoring is a critical component of production cloud workloads.

---

# Business Value

This implementation demonstrates practical cloud engineering skills directly applicable to enterprise environments:

- Serverless application deployment
- Monitoring and diagnostics
- Azure administration
- Security hardening
- Infrastructure validation
- Cloud troubleshooting
- Cost-conscious resource management

These competencies are highly relevant for Cloud Engineer, Azure Administrator, Cloud Security Engineer, and DevOps Engineer roles.

---

# Cleanup Activities Performed

- Deleted Resource Group
- Removed Azure Function App
- Deleted Monitoring Resources
- Removed Log Analytics Workspace (where applicable)
- Deleted Cloud Shell project files
- Verified endpoint no longer responded

---

# Project Outcome

The project successfully delivered a fully operational Azure Function App hosting an HTTP-triggered serverless endpoint. The function was deployed, tested, monitored, secured using Function Keys, and validated through Application Insights logging. All temporary resources were identified and removed to prevent unnecessary Azure charges.

---

# Disclaimer

This project was completed within a Microsoft Learn / Skillable lab environment for educational and skills-development purposes. Resources, names, identifiers, and configurations may differ from production environments.

---

# Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11   
Cloud Security Engineering   

GitHub Portfolio Project Documentation
