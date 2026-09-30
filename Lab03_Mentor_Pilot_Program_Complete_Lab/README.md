<div align="center">

# ⚡ Azure Functions Serverless HTTP Endpoint: Complete Guide

### Mentor Pilot Program | Completed Assignment

**Prepared by:** Wadondera A. Collins  
**Program:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Completion Date:** September 30, 2026

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Functions-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Node.js](https://img.shields.io/badge/Runtime-Node.js-339933?logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Learning](https://img.shields.io/badge/Focus-Serverless%20Security-6F42C1)](#-skills-demonstrated)

*A hands-on journey through Azure Functions provisioning, Node.js development, cloud deployment, HTTP testing, Application Insights monitoring, Function Key security, validation, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Prepare the Azure Environment](#-exercise-1-prepare-the-azure-environment)
- [Exercise 2: Create and Deploy the HTTP Function](#-exercise-2-create-and-deploy-the-http-function)
- [Exercise 3: Test and Monitor the Endpoint](#-exercise-3-test-and-monitor-the-endpoint)
- [Exercise 4: Secure the Endpoint with Function Keys](#-exercise-4-secure-the-endpoint-with-function-keys)
- [Exercise 5: Clean Up the Environment](#-exercise-5-clean-up-the-environment)
- [Validation Results](#-validation-results)
- [Command Reference](#-command-reference)
- [Troubleshooting](#-troubleshooting)
- [Skills Demonstrated](#-skills-demonstrated)
- [Key Takeaways](#-key-takeaways)
- [Completion Checklist](#-completion-checklist)
- [Author](#-author)
- [Acknowledgements](#-acknowledgements)
- [Disclaimer](#-disclaimer)

---

## 🚀 Project Overview

This repository documents the successful completion of the **Azure Functions Serverless HTTP Endpoint Deployment** project in the **Mentor Pilot Program**. The lab demonstrated the complete lifecycle of a cloud-native serverless application using Azure Functions, from environment provisioning and code deployment to monitoring, security hardening, validation, and cleanup.

The project covered the following workflow:

1. Create a dedicated Azure resource group.
2. Deploy an Azure Function App using the Flex Consumption hosting plan.
3. Configure the Node.js runtime and JavaScript programming model v4.
4. Enable Application Insights and Log Analytics integration.
5. Initialize an Azure Functions project in Azure Cloud Shell.
6. Create an HTTP-triggered function named `GetStatus`.
7. Publish the project with Azure Functions Core Tools.
8. Validate the public HTTP endpoint.
9. Review requests, invocations, duration, and execution status.
10. Change the authorization level from anonymous to function.
11. Validate blocked requests without a key and successful requests with a key.
12. Delete the lab resources and local Cloud Shell project files.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

By completing this project, I demonstrated the ability to:

- Create and manage an Azure resource group.
- Deploy an Azure Function App with a serverless hosting plan.
- Configure a Node.js runtime for Azure Functions.
- Initialize a JavaScript programming model v4 project.
- Generate an HTTP-triggered function with Azure Functions Core Tools.
- Publish function code from Azure Cloud Shell.
- Retrieve Azure resource information with Azure CLI queries.
- Validate an HTTP endpoint through a browser and private browsing session.
- Enable and verify Application Insights monitoring.
- Review telemetry with Transaction Search and Kusto Query Language.
- Replace anonymous access with Function Key authorization.
- Validate unauthorized and authorized endpoint behavior.
- Remove temporary resources to prevent unintended consumption and charges.
- Document cloud work without exposing secrets or reusable function keys.

---

## 🏗️ Architecture and Resources

```text
User or Test Client
        │
        │ HTTPS request
        ▼
Azure Functions HTTP Endpoint
        │
        ▼
Function App: Flex Consumption
└── Function: GetStatus
    ├── Runtime: Node.js
    ├── Language: JavaScript
    ├── Programming Model: v4
    ├── Initial Authorization: Anonymous
    └── Final Authorization: Function Key
        │
        ├───────────────┐
        ▼               ▼
Application Insights   Log Analytics Workspace
        │               │
        └───────┬───────┘
                ▼
       Monitoring and Diagnostics
```

| Resource or Component | Configuration | Purpose |
|---|---|---|
| Resource group | `rg-gp-functions-endpoint` | Logical container for the project resources |
| Function App | Dynamically retrieved during the lab | Hosts the deployed serverless function |
| Function | `GetStatus` | Provides the HTTP-triggered endpoint |
| Hosting plan | Flex Consumption | Provides event-driven serverless execution |
| Instance memory | 2048 MB | Memory configuration selected for the lab |
| Runtime | Node.js, latest LTS offered by the lab | Executes the JavaScript function |
| Programming model | JavaScript model v4 | Provides code-centric function registration |
| Application Insights | Enabled | Captures requests, logs, performance, and errors |
| Log Analytics | Connected | Supports centralized telemetry analysis |
| Deployment environment | Azure Cloud Shell, Bash | Hosts CLI and Functions Core Tools operations |

> [!NOTE]
> **Final state:** All temporary Azure resources and Cloud Shell project files were removed after validation. The architecture represents the deployed environment before cleanup.

> [!IMPORTANT]
> Function App names must be globally unique. The lab retrieved the generated Function App name dynamically rather than publishing a tenant-specific value in this repository.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An authorized Azure subscription or temporary Skillable lab subscription
- Permission to create and delete Azure resources
- Azure Cloud Shell configured in Bash mode
- Azure CLI available in Cloud Shell
- Azure Functions Core Tools available in Cloud Shell
- Basic familiarity with JavaScript, HTTP, and command-line operations

### Tools and Environment

| Tool or Service | Version or Edition | Purpose |
|---|---|---|
| Microsoft Azure portal | Web service; build not provided | Resource provisioning and configuration |
| Azure Function App | Service version not provided | Hosts the serverless endpoint |
| Azure Functions Core Tools | Version not provided | Creates and publishes the function project |
| Azure CLI | Cloud Shell-provided version | Queries and manages Azure resources |
| Azure Cloud Shell | Bash | Provides the deployment environment |
| Node.js | Latest LTS offered during the lab | Function runtime |
| JavaScript programming model | v4 | Function project and trigger model |
| Application Insights | Service version not provided | Application telemetry and diagnostics |
| Log Analytics | Service version not provided | Query and analysis of monitoring data |
| Web browser | Version not provided | Endpoint and authentication testing |

> [!NOTE]
> Exact portal, browser, CLI, Core Tools, Node.js, and Azure service versions were not provided in the assignment. They are intentionally listed as not specified rather than estimated.

### Security Notice

Passwords, Temporary Access Pass values, subscription identifiers, tenant details, function keys, connection strings, instrumentation details, and other secrets are intentionally **not included** in this README.

> [!CAUTION]
> Never commit Function Keys, host keys, storage keys, connection strings, tokens, or other credentials to GitHub. If a key is exposed, revoke or regenerate it immediately through the appropriate Azure management process.

Function Keys provide a basic access-control mechanism for HTTP-triggered functions. Production workloads should select authentication and authorization controls according to organizational security requirements and threat models.

---

## 🧭 Exercise 1: Prepare the Azure Environment

### 1. Launch Azure Cloud Shell

1. Sign in to the Azure portal.
2. Open **Cloud Shell**.
3. Select **Bash** when prompted.
4. Confirm that the command prompt becomes available.

**Validation:** Azure Cloud Shell opened successfully in Bash mode.

### 2. Create the Resource Group

The project used the following dedicated resource group:

```text
rg-gp-functions-endpoint
```

The resource group supported:

- Logical resource organization
- Simplified lifecycle management
- Centralized cleanup
- Cost-conscious lab administration

**Validation:** `rg-gp-functions-endpoint` was created successfully in the assigned subscription and region.

### 3. Deploy the Function App

Configure the Function App with the following project settings:

| Setting | Value |
|---|---|
| Resource group | `rg-gp-functions-endpoint` |
| Hosting plan | Flex Consumption |
| Runtime | Node.js |
| Runtime version | Latest LTS offered by the lab |
| Instance memory | 2048 MB |
| Monitoring | Application Insights enabled |
| Logging | Log Analytics integration |

**Validation:** The Function App deployment completed successfully and displayed a running state.

### 4. Verify Monitoring Integration

Open the Function App monitoring configuration and confirm that Application Insights is connected.

**Validation:** Application Insights integration was enabled for the Function App.

---

## 🛠️ Exercise 2: Create and Deploy the HTTP Function

### 1. Create the Project Directory

```bash
mkdir func-gp-endpoint && cd func-gp-endpoint
```

**Validation:** The `func-gp-endpoint` directory was created and selected as the working directory.

### 2. Initialize the Functions Project

```bash
func init --worker-runtime node --language javascript --model V4
```

This command initialized a Node.js Azure Functions project using JavaScript programming model v4.

**Validation:** Project files such as `host.json` and `package.json` were generated successfully.

### 3. Generate the HTTP Trigger

```bash
func new \
  --name GetStatus \
  --template "HTTP trigger" \
  --authlevel anonymous
```

List the generated function file:

```bash
ls src/functions/
```

Expected result:

```text
GetStatus.js
```

**Validation:** `src/functions/GetStatus.js` was created successfully.

### 4. Review the Repository Structure

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

> [!NOTE]
> A separate formal report and screenshot evidence can be maintained outside this README to keep the repository landing page concise and recruiter-friendly.

### 5. Retrieve the Function App Name

```bash
FUNC_APP_NAME=$(az functionapp list \
  --resource-group rg-gp-functions-endpoint \
  --query "[0].name" \
  --output tsv)
```

Verify the stored value without publishing it in the repository:

```bash
printf '%s\n' "$FUNC_APP_NAME"
```

**Validation:** The variable contained the Function App associated with `rg-gp-functions-endpoint`.

### 6. Publish the Function

```bash
func azure functionapp publish "$FUNC_APP_NAME"
```

**Validation:** Azure Functions Core Tools completed the cloud deployment and returned an HTTP invoke URL for `GetStatus`.

---

## 📊 Exercise 3: Test and Monitor the Endpoint

### 1. Test Anonymous Access

Open the generated invoke URL in a web browser and repeat the test in a private or incognito browsing session.

Expected response:

```text
Hello, world!
```

**Validation:** The endpoint responded successfully without requiring authentication while its authorization level was set to anonymous.

### 2. Confirm Runtime Behavior

Review the Function App and function details in the Azure portal.

**Validation:** `GetStatus` was visible in the deployed Function App and responded successfully to HTTP requests.

### 3. Review Application Insights

Use Application Insights to review:

- Transaction Search
- Request telemetry
- Invocation records
- Execution result
- Request duration
- Recent endpoint activity

**Validation:** Requests to the HTTP endpoint appeared in Application Insights telemetry.

### 4. Query Recent Requests

Run the following Kusto query in the appropriate Logs experience:

```kusto
requests
| order by timestamp desc
```

**Validation:** Recent request records were returned in descending timestamp order.

> [!TIP]
> Telemetry can take time to appear after an invocation. Refresh the query results after generating a new test request if no recent event is visible immediately.

---

## 🔑 Exercise 4: Secure the Endpoint with Function Keys

### 1. Change the Authorization Level

Update the `GetStatus` function from anonymous access to Function Key authorization:

```bash
sed -i \
  "s/authLevel: 'anonymous'/authLevel: 'function'/" \
  src/functions/GetStatus.js
```

Verify the updated setting:

```bash
grep authLevel src/functions/GetStatus.js
```

**Validation:** The function source displayed `authLevel: 'function'`.

### 2. Redeploy the Secured Function

```bash
func azure functionapp publish "$FUNC_APP_NAME"
```

**Validation:** The updated function code was published successfully.

### 3. Test a Request Without a Key

Call the endpoint without including a valid Function Key.

Expected behavior:

```text
401 Unauthorized
```

**Validation:** The request without a Function Key was rejected.

### 4. Test a Request with a Key

Retrieve the Function Key through the authorized Azure interface. Use it only for validation and do not record it in screenshots, source files, shell history, or repository documentation.

Expected response:

```text
Hello, world!
```

**Validation:** The request containing a valid Function Key succeeded.

### 5. Review Secured Invocation Telemetry

Generate both authorized and unauthorized requests, then review the corresponding monitoring records.

**Validation:** Application Insights captured endpoint activity after security hardening.

> [!WARNING]
> Function Keys are secrets. Redact them from screenshots, terminal output, issue descriptions, reports, and public repositories.

---

## 🧹 Exercise 5: Clean Up the Environment

### 1. Delete the Resource Group

Delete `rg-gp-functions-endpoint` through the Azure portal or the approved lab cleanup procedure.

**Validation:** The resource group, Function App, monitoring resources, and associated lab components were removed.

### 2. Remove Cloud Shell Project Files

From the parent directory, remove the local lab project after confirming it is no longer needed:

```bash
cd ..
rm -rf func-gp-endpoint
```

**Validation:** The Cloud Shell project directory was removed.

### 3. Verify Final Cleanup

Confirm that:

- `rg-gp-functions-endpoint` no longer appears in the Azure portal.
- The Function App is no longer available.
- Monitoring resources created for the lab are removed.
- The saved endpoint no longer responds.
- The local Cloud Shell project directory is absent.

**Validation:** Azure and Cloud Shell cleanup checks completed successfully.

> [!WARNING]
> Resource-group and file deletion are permanent. Verify the target names before confirming either operation.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Cloud Shell opened in Bash mode | ✅ Passed |
| Resource group created | ✅ Passed |
| Function App deployed | ✅ Passed |
| Flex Consumption configured | ✅ Passed |
| Node.js runtime configured | ✅ Passed |
| Application Insights enabled | ✅ Passed |
| Functions project initialized | ✅ Passed |
| `GetStatus` function created | ✅ Passed |
| Function source file verified | ✅ Passed |
| Function App name retrieved | ✅ Passed |
| Function published successfully | ✅ Passed |
| HTTP invoke URL generated | ✅ Passed |
| Anonymous browser access validated | ✅ Passed |
| Expected HTTP response validated | ✅ Passed |
| Request telemetry captured | ✅ Passed |
| Kusto request query completed | ✅ Passed |
| Authorization changed to `function` | ✅ Passed |
| Secured function redeployed | ✅ Passed |
| Request without key rejected | ✅ Passed |
| Request with valid key succeeded | ✅ Passed |
| Secured activity reviewed in monitoring | ✅ Passed |
| Resource group deleted | ✅ Passed |
| Cloud Shell project files removed | ✅ Passed |
| Final endpoint cleanup verified | ✅ Passed |

---

## 📚 Command Reference

| Goal | Command |
|---|---|
| Create and enter the project directory | `mkdir func-gp-endpoint && cd func-gp-endpoint` |
| Initialize a Node.js v4 project | `func init --worker-runtime node --language javascript --model V4` |
| Create the HTTP trigger | `func new --name GetStatus --template "HTTP trigger" --authlevel anonymous` |
| List generated functions | `ls src/functions/` |
| Retrieve the Function App name | `az functionapp list --resource-group rg-gp-functions-endpoint --query "[0].name" --output tsv` |
| Publish the function project | `func azure functionapp publish "$FUNC_APP_NAME"` |
| Change authorization level | `sed -i "s/authLevel: 'anonymous'/authLevel: 'function'/" src/functions/GetStatus.js` |
| Verify authorization setting | `grep authLevel src/functions/GetStatus.js` |
| Remove the local project | `rm -rf func-gp-endpoint` |

### Monitoring Query Reference

```kusto
requests
| order by timestamp desc
```

---

## 🧰 Troubleshooting

### The Function App variable is empty

Confirm that the resource group contains a Function App:

```bash
az functionapp list \
  --resource-group rg-gp-functions-endpoint \
  --output table
```

Then rerun the variable assignment.

### Functions Core Tools cannot find the project

Confirm that the current directory contains `host.json` and `package.json`:

```bash
pwd
ls -la
```

### `GetStatus.js` is missing

Check the functions directory:

```bash
ls -la src/functions/
```

If the file is absent, rerun the approved `func new` command from the project root.

### Publishing fails

Verify that:

- The correct Azure subscription is active.
- The Function App exists and is running.
- `$FUNC_APP_NAME` contains the intended app name.
- The current directory is the Functions project root.
- Cloud Shell has not lost the authenticated session.

### The endpoint does not respond

Confirm that deployment completed, the Function App is running, and the invoke URL belongs to the deployed `GetStatus` function.

### The endpoint still allows anonymous access

Confirm that `GetStatus.js` contains:

```javascript
authLevel: 'function'
```

Republish the project and retest without reusing a previously generated URL that contains a key.

### Requests with a key fail

Confirm that the key is current, complete, and associated with the intended function or host. Do not paste the key into source-controlled files.

### Telemetry is not visible

Generate a new request, confirm Application Insights integration, wait for ingestion, refresh the monitoring view, and broaden the selected time range if needed.

### Cleanup is incomplete

Confirm that the resource-group deletion operation has finished and verify whether any monitoring resource was created outside the project resource group.

---

## 🧠 Skills Demonstrated

- Microsoft Azure administration
- Azure Functions deployment
- Serverless architecture fundamentals
- Flex Consumption hosting
- Azure resource-group lifecycle management
- Azure Cloud Shell navigation
- Azure CLI resource discovery
- Azure Functions Core Tools
- Node.js and JavaScript programming model v4
- HTTP-triggered function development
- Command-line application deployment
- Public endpoint validation
- Function Key authentication
- Endpoint access restriction
- Least-privilege security awareness
- Application Insights monitoring
- Log Analytics fundamentals
- Kusto Query Language basics
- Request and invocation analysis
- Deployment troubleshooting
- Secure credential handling
- Cost-aware resource cleanup

---

## 💡 Key Takeaways

1. **Serverless platforms reduce infrastructure administration.** Azure Functions manages the execution environment while developers focus on trigger-driven application logic.
2. **Flex Consumption supports event-driven execution.** It provides a serverless hosting model with configurable memory and scaling capabilities.
3. **Repeatable deployment improves reliability.** Azure Functions Core Tools and Azure CLI make deployment steps reviewable and reusable.
4. **Validation should follow every deployment stage.** Checking files, runtime state, endpoint responses, and telemetry helps isolate faults quickly.
5. **Monitoring is part of the application.** Application Insights provides visibility into requests, performance, logs, and errors.
6. **Anonymous endpoints should be intentional.** Public accessibility must be evaluated against the application's security requirements.
7. **Function Keys improve basic endpoint protection.** Keys prevent unauthenticated invocation when the function authorization level requires them.
8. **Secrets do not belong in source control.** Function Keys and connection details must be protected and rotated if exposed.
9. **Cleanup is part of responsible engineering.** Removing temporary compute and monitoring resources reduces unnecessary cost and exposure.

### Business Value

This implementation demonstrates practical capabilities relevant to Cloud Engineer, Azure Administrator, Cloud Security Engineer, and DevOps Engineer roles:

- Serverless application deployment
- Cloud-native monitoring and diagnostics
- Command-line deployment automation
- Endpoint security hardening
- Infrastructure and runtime validation
- Cloud troubleshooting
- Cost-conscious resource management

---

## ☑️ Completion Checklist

- [x] Signed in to the authorized Azure environment
- [x] Opened Azure Cloud Shell in Bash mode
- [x] Created `rg-gp-functions-endpoint`
- [x] Created the Function App
- [x] Selected Flex Consumption
- [x] Configured the Node.js runtime
- [x] Selected a 2048 MB instance size
- [x] Enabled Application Insights
- [x] Initialized the JavaScript v4 project
- [x] Created the `GetStatus` HTTP trigger
- [x] Verified `GetStatus.js`
- [x] Retrieved the Function App name
- [x] Published the function
- [x] Tested the public endpoint
- [x] Confirmed the expected response
- [x] Reviewed request telemetry
- [x] Queried recent requests
- [x] Changed authorization from anonymous to function
- [x] Republished the secured function
- [x] Confirmed requests without a key were rejected
- [x] Confirmed requests with a valid key succeeded
- [x] Reviewed secured invocation activity
- [x] Deleted the resource group
- [x] Removed the Cloud Shell project directory
- [x] Confirmed final cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical cloud-security, Azure-administration, and DevOps portfolio, demonstrating serverless deployment, monitoring, endpoint protection, validation, troubleshooting, and responsible cloud-resource management.

---

## 🙏 Acknowledgements

This guided project was completed as part of the **Mentor Pilot Program** within a Microsoft Learn / Skillable lab environment. Mentor supported the learning experience by helping with lab navigation, instruction comprehension, and troubleshooting.

Official reference material:

- [Azure Functions Flex Consumption plan hosting](https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan)
- [Create and manage Function Apps in a Flex Consumption plan](https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-how-to)
- [Azure Functions Node.js developer reference](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node)
- [Configure monitoring for Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/configure-monitoring)
- [Monitor executions in Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitoring)

---

## ⚖️ Disclaimer

This repository is an educational record of a completed guided project in a temporary Microsoft Learn / Skillable lab environment. It is not a production-ready architecture and does not replace official Microsoft documentation, organizational security policies, or professional cloud architecture guidance. Azure services, interfaces, pricing, runtime support, limits, and features may change over time. Commands and configurations should be checked against current Microsoft documentation before reuse.

Resource names and configurations are documented for learning and portfolio purposes. Passwords, access tokens, Function Keys, host keys, storage keys, connection strings, subscription identifiers, tenant details, monitoring secrets, and other sensitive information are intentionally excluded. Production deployments require an independent review of authentication, authorization, networking, secret management, availability, monitoring, incident response, cost controls, and regulatory requirements.

---

<div align="center">

### 🎉 Lab Completed Successfully

**Azure Functions skills: deployed, monitored, secured, validated, and ready for the next challenge.**

Made with curiosity, care, and a commitment to responsible cloud engineering.  

**Wadondera A. Collins**  
*ICDFA Trainee | Cohort 11 | Cloud Security Engineering*

</div>
