<div align="center">

# Azure Functions Serverless Endpoint Deployment

## Technical Assignment Report

**Prepared by:** Wadondera A. Collins  
**Programme:** ICDFA Trainee | Cohort 11  
**Specialization:** Cloud Security Engineering  
**Platform:** Microsoft Azure  
**Assignment Status:** Completed

</div>

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Executive Summary](#executive-summary)
3. [Objectives](#objectives)
4. [Professional Value](#professional-value)
5. [Skills Demonstrated](#skills-demonstrated)
6. [Technologies and Tools Used](#technologies-and-tools-used)
7. [Lab Environment](#lab-environment)
8. [Solution Architecture](#solution-architecture)
9. [Repository Structure](#repository-structure)
10. [Methodology](#methodology)
11. [Implementation, Evidence, and Analysis](#implementation-evidence-and-analysis)
12. [Results](#results)
13. [Validation Matrix](#validation-matrix)
14. [Security Considerations](#security-considerations)
15. [Challenges and Lessons Learned](#challenges-and-lessons-learned)
16. [Limitations and Next Steps](#limitations-and-next-steps)
17. [Cleanup and Cost Control](#cleanup-and-cost-control)
18. [Conclusion](#conclusion)
19. [Disclaimer](#disclaimer)
20. [Author](#author)

---

## Project Overview

This project documents the deployment, validation, security configuration, monitoring workflow, and cleanup of a serverless HTTP endpoint using Microsoft Azure Functions.

The assignment combined Azure portal administration with command-line development in Azure Cloud Shell. A JavaScript HTTP function named `GetStatus` was created with Azure Functions Core Tools and published to a Linux-based Function App running on the Flex Consumption plan.

> **Security notice:** Temporary credentials, passwords, access tokens, Temporary Access Pass tokens, function keys, and secret-bearing URLs are intentionally excluded.

---

## Executive Summary

A dedicated resource group named `rg-gp-functions-endpoint` was prepared to organize the project resources. A Function App named `func-gp-endpoint-65652145` was provisioned on Linux using Flex Consumption with 2048 MB instance memory.

A Node.js Azure Functions project was initialized in Azure Cloud Shell using JavaScript programming model V4. The `GetStatus` HTTP trigger was created and published with Azure Functions Core Tools. Deployment output confirmed successful publication and generated an invoke URL. Browser testing returned `Hello, world!`, confirming successful endpoint execution. Azure Portal also listed `GetStatus` as an enabled HTTP function.

The lab additionally covered function-level authorization, Application Insights, Log Analytics, transaction review, and resource cleanup. The report distinguishes screenshot-verified results from assignment activities for which no matching image was supplied.

---

## Objectives

1. Create a dedicated Azure resource group.
2. Provision an Azure Function App using Flex Consumption.
3. Configure Node.js and JavaScript programming model V4.
4. Enable monitoring through Application Insights.
5. Create the `GetStatus` HTTP trigger.
6. Deploy the function through Azure Cloud Shell.
7. Verify Function App availability and endpoint execution.
8. Apply function-level authorization after public testing.
9. Review request telemetry.
10. Remove temporary resources to prevent ongoing charges.
11. Document the completed work with accurately matched evidence.

---

## Professional Value

The project demonstrates practical capabilities relevant to Cloud Engineer, Azure Administrator, Cloud Security Engineer, DevOps Engineer, and Platform Engineer roles.

- Serverless workload deployment without traditional server management
- Consumption-based hosting and cost awareness
- Azure resource organization and lifecycle management
- Command-line development and deployment
- HTTP endpoint validation
- Endpoint authorization concepts
- Azure-native monitoring workflows
- Evidence-based technical documentation

---

## Skills Demonstrated

### Cloud Engineering

- Azure resource provisioning
- Azure Functions administration
- Flex Consumption hosting
- Linux cloud configuration
- Resource lifecycle management

### DevOps and Automation

- Azure Cloud Shell
- Bash
- Azure CLI
- Azure Functions Core Tools
- Command-line publishing

### Application Development

- Node.js runtime configuration
- JavaScript model V4
- HTTP trigger creation
- Endpoint testing

### Security and Monitoring

- Anonymous and function-level authorization concepts
- Function key protection
- Credential-handling awareness
- Application Insights concepts
- Log Analytics query usage

---

## Technologies and Tools Used

| Technology or Service | Purpose |
|---|---|
| Microsoft Azure | Cloud platform |
| Azure Resource Groups | Resource organization and cleanup |
| Azure Functions | Serverless compute platform |
| Flex Consumption | Consumption-based hosting |
| Node.js | Function runtime |
| JavaScript model V4 | Function programming model |
| Azure Cloud Shell | Browser-based command-line environment |
| Bash | Shell used for project commands |
| Azure CLI | Azure resource discovery |
| Azure Functions Core Tools | Project creation and publishing |
| Application Insights | Application telemetry |
| Log Analytics | Query-based diagnostics |
| Web browser | Endpoint validation |

---

## Lab Environment

| Component | Configuration |
|---|---|
| Resource group | `rg-gp-functions-endpoint` |
| Function App | `func-gp-endpoint-65652145` |
| Function | `GetStatus` |
| Trigger | HTTP |
| Runtime | Node.js |
| Language | JavaScript |
| Programming model | V4 |
| Operating system | Linux |
| Hosting plan | Flex Consumption |
| Instance memory | 2048 MB |
| Deployment environment | Azure Cloud Shell using Bash |
| Monitoring workflow | Application Insights and Log Analytics |

---

## Solution Architecture

```text
Client Browser
      |
      | HTTPS request
      v
Azure Functions Host
      |
      v
GetStatus HTTP Trigger
      |
      +-----------------------------+
      |                             |
      v                             v
HTTP Response                 Application Insights
"Hello, world!"                    |
                                      v
                                Log Analytics
```

---

## Repository Structure

```text
azure-functions-serverless-endpoint/
├── README.md
├── REPORT.md
├── images/
│   ├── Fig01 Resource Group Configuration.png
│   ├── Fig02 Function App Running Overview.png
│   ├── Fig03 Cloud Shell Deployment Command and Progress.png
│   ├── Fig04 Successful Deployment and Generated Invoke URL.png
│   ├── Fig05 Browser Displaying Hello World.png
│   ├── Fig06 GetStatus HTTP Function Enabled.png
│   └── Fig07 Resource Group Cleanup Verification.png
└── src/
    └── functions/
        └── GetStatus.js
```

The `README.md` should provide a concise repository introduction. This `REPORT.md` contains the full implementation record, evidence analysis, validation, and lessons learned.

---

## Methodology

### Phase 1: Prepare

- Review the lab requirements.
- Define resource names.
- Prepare the dedicated resource group.

### Phase 2: Provision

- Create the Function App.
- Select Flex Consumption.
- Configure Node.js and Linux.
- Enable Application Insights.

### Phase 3: Develop and Deploy

- Open Azure Cloud Shell in Bash mode.
- Initialize the JavaScript function project.
- Create the `GetStatus` HTTP trigger.
- Publish the project to Azure.

### Phase 4: Validate

- Review deployment output.
- Test the invoke URL.
- Confirm the function in Azure Portal.

### Phase 5: Secure and Monitor

- Change authorization from anonymous to function level.
- Republish the function.
- Test requests with and without a key.
- Review invocation telemetry.

### Phase 6: Clean Up and Document

- Delete project resources.
- Check monitoring resources separately.
- Remove the Cloud Shell project folder.
- Match every screenshot to the exact task supported by its visible content.

---

## Implementation, Evidence, and Analysis

## Exercise 1: Create the Function App

### Task 1: Prepare the Azure Environment

A dedicated resource group was configured to contain the project resources:

```text
rg-gp-functions-endpoint
```

<img width="644" height="415" alt="Fig01 Resource Group Configuration" src="https://github.com/user-attachments/assets/0ee71b28-94eb-47f1-b62d-6c327164120d" />


*Figure 1: Resource group configuration on the Azure portal Review + create page.*

**Evidence analysis:** The screenshot shows the `Create a resource group` page, the `Review + create` tab, resource group name `rg-gp-functions-endpoint`, and region `East US`. The visible `Create` button indicates that the configuration reached final review. The image proves configuration readiness rather than completed resource creation.

### Task 2: Configure the Function App

The Function App was configured for Node.js on Linux using the Flex Consumption plan with 2048 MB instance memory. Application Insights formed part of the monitoring workflow.

### Task 3: Verify the Function App Deployment

<img width="790" height="517" alt="Fig02 Function App Running Overview" src="https://github.com/user-attachments/assets/57a8dda9-dcfe-4ec6-aeac-50fa7f21e28b" />


*Figure 2: Function App overview showing the application in a running state.*

**Evidence analysis:** The screenshot identifies `func-gp-endpoint-65652145` and resource group `rg-gp-functions-endpoint`. Visible properties include `Status: Running`, `Operating System: Linux`, `Plan Type: Flex Consumption`, `Instance Memory: 2048 MB`, and location `West US 3`.

**Regional observation:** Figure 1 shows the resource group region as `East US`, while Figure 2 shows the Function App location as `West US 3`. The report records both visible values without claiming that the resources used the same region.

**Task result:** The Function App was running with the expected serverless hosting configuration.

---

## Exercise 2: Deploy an HTTP-Triggered Function

### Task 1: Open Azure Cloud Shell

Azure Cloud Shell was opened in Bash mode for project creation and deployment.

### Task 2: Create the Function Project

```bash
mkdir func-gp-endpoint && cd func-gp-endpoint
func init --worker-runtime node --language javascript --model V4
func new --name GetStatus --template "HTTP trigger" --authlevel anonymous
ls src/functions/
```

Expected project file:

```text
GetStatus.js
```

### Task 3: Publish the Function to Azure

```bash
FUNC_APP_NAME=$(az functionapp list \
  --resource-group rg-gp-functions-endpoint \
  --query "[0].name" \
  -o tsv)

echo "$FUNC_APP_NAME"
func azure functionapp publish "$FUNC_APP_NAME"
```

<img width="644" height="415" alt="Fig03 Cloud Shell Deployment Command and Progress" src="https://github.com/user-attachments/assets/4cdc1b67-b15c-4be4-ac3e-7085de37b55f" />




*Figure 3: Azure Cloud Shell running the publication command and processing the Function App deployment.*

**Evidence analysis:** The screenshot shows `GetStatus.js`, the Azure CLI query used to retrieve the Function App name, the returned app name, and execution of `func azure functionapp publish $FUNC_APP_NAME`. Publication is still in progress in this image.

<img width="780" height="318" alt="Fig04 Successful Deployment and Generated Invoke URL" src="https://github.com/user-attachments/assets/7ea6c789-04b7-4fa7-ab6a-7872587b9e9f" />




*Figure 4: Azure Cloud Shell confirming successful deployment of the GetStatus HTTP trigger and generation of its invoke URL.*

**Evidence analysis:** The terminal displays `Deployment successful`, lists `GetStatus - [httpTrigger]`, and shows an invoke URL. Later shell errors in the same terminal occurred after the successful deployment and do not invalidate the deployment result.

**Task result:** The `GetStatus` HTTP trigger was published successfully.

---

## Exercise 3: Test, Secure, and Monitor the Endpoint

### Task 1: Test the HTTP Endpoint

<img width="775" height="466" alt="Fig05 Browser Displaying Hello World" src="https://github.com/user-attachments/assets/cbc60923-3dae-49a8-a5ca-fe7ee945c751" />


*Figure 5: Browser displaying the expected Hello, world! response from the GetStatus endpoint.*

**Evidence analysis:** The browser is open to the Function App `/api/getstatus` path and displays `Hello, world!`. The image proves endpoint reachability and successful function execution during the anonymous-access stage.

### Task 2: Verify the Function in Azure Portal

<img width="775" height="461" alt="Fig06 GetStatus HTTP Function Enabled" src="https://github.com/user-attachments/assets/dd393d96-0581-40f1-a547-c54904dfb1d4" />


*Figure 6: GetStatus listed as an enabled HTTP-triggered function in Azure Portal.*

**Evidence analysis:** The Function App list shows function name `GetStatus`, trigger type `HTTP`, and status `Enabled`.

### Task 3: Verify Monitoring

The assignment required confirmation that Application Insights was connected to the Function App and that monitoring resources were identified for cleanup.

**Evidence status:** No supplied screenshot opens the Application Insights connection page, Transaction Search, or Log Analytics results. Monitoring remains part of the documented workflow but is not marked as screenshot-verified.

### Task 4: Restrict Access

```bash
sed -i "s/authLevel: 'anonymous'/authLevel: 'function'/" \
  src/functions/GetStatus.js

grep authLevel src/functions/GetStatus.js
func azure functionapp publish "$FUNC_APP_NAME"
```

**Evidence status:** No supplied screenshot shows `authLevel: 'function'` or the post-change redeployment.

### Task 5: Test Restricted Access

The intended validation covered two conditions:

1. A request without a function key should be rejected.
2. A request with a valid function key should succeed.

> **Security requirement:** Function keys must not be included in public documentation or screenshots.

**Evidence status:** No supplied screenshot shows the unauthorized response or key-authorized success.

### Task 6: Review Invocation Logs

```kusto
requests
| order by timestamp desc
```

**Evidence status:** No supplied screenshot shows Transaction Search or Log Analytics query results.

---

## Cleanup: Remove Project Resources

```bash
cd ~ && rm -rf func-gp-endpoint
```

<img width="775" height="529" alt="Fig07 Resource Group Cleanup Verification" src="https://github.com/user-attachments/assets/ed205cfe-7ae3-4a89-9f9e-5f0bfaa7e35d" />


*Figure 7: Azure Resource Groups page showing no resource groups in the active subscription view after cleanup.*

**Evidence analysis:** The page displays `No resource groups to display` and `0 of 0`. This confirms that no resource groups were visible in the displayed subscription context. The image does not independently prove removal of monitoring resources in another group or deletion of the Cloud Shell project folder.

---

## Results

### Screenshot-Verified Results

- Resource group configuration reached final review.
- The Function App displayed a running status.
- Linux, Flex Consumption, and 2048 MB instance memory were visible.
- `GetStatus.js` was present in the function project.
- Function publication was initiated and completed successfully.
- Azure generated an invoke URL.
- The endpoint returned `Hello, world!`.
- `GetStatus` appeared as an enabled HTTP trigger.
- No resource groups were visible after cleanup.

### Documented but Not Screenshot-Verified

- Application Insights connection
- Transaction Search results
- Log Analytics query results
- Authorization changed to `function`
- Unauthorized request rejected
- Key-authorized request succeeded
- Cloud Shell project folder removed
- Separate monitoring resources removed

---

## Validation Matrix

| Requirement | Status | Evidence |
|---|---|---|
| Resource group configuration reviewed | Verified | Figure 1 |
| Function App running | Verified | Figure 2 |
| Linux, Flex Consumption, and 2048 MB visible | Verified | Figure 2 |
| `GetStatus.js` present | Verified | Figure 3 |
| Function publication initiated | Verified | Figure 3 |
| Function deployment completed | Verified | Figure 4 |
| Invoke URL generated | Verified | Figure 4 |
| Public endpoint returned expected response | Verified | Figure 5 |
| `GetStatus` listed as enabled HTTP trigger | Verified | Figure 6 |
| Application Insights connected | Not visibly verified | No matching screenshot supplied |
| Function-level authorization applied | Not visibly verified | No matching screenshot supplied |
| Unauthorized request rejected | Not visibly verified | No matching screenshot supplied |
| Key-authorized request succeeded | Not visibly verified | No matching screenshot supplied |
| Invocation telemetry reviewed | Not visibly verified | No matching screenshot supplied |
| Resource group view empty after cleanup | Verified | Figure 7 |
| Cloud Shell folder removed | Not visibly verified | No matching screenshot supplied |

---

## Security Considerations

- Temporary lab credentials, administrator passwords, TAP tokens, and function keys are excluded.
- Anonymous authorization should be used only when deliberately required.
- Function keys must not be committed to GitHub.
- Screenshots should be reviewed for usernames, subscription information, hostnames, and resource identifiers before publication.
- Production improvements may include Microsoft Entra ID authentication, managed identity, Azure Key Vault, least-privilege roles, network controls, and centralized alerting.

---

## Challenges and Lessons Learned

- Copy only executable commands from technical instructions.
- Replace placeholders before running commands.
- Treat output labels as results rather than commands.
- Validate each stage before continuing.
- Separate screenshot-verified outcomes from undocumented activities.
- Check monitoring resources separately when Azure creates them outside the main resource group.

---

## Limitations and Next Steps

### Current Limitations

- Application Insights connection is not shown.
- Invocation logs are not shown.
- The authorization change is not shown.
- Unauthorized and authorized key tests are not shown.
- Cloud Shell folder deletion is not shown.

### Recommended Next Steps

- Add monitoring-connection evidence.
- Add redacted authorization-test evidence.
- Add Application Insights or Log Analytics results.
- Export `GetStatus.js` into the repository.
- Add an appropriate `.gitignore` file.
- Add GitHub Actions for repeatable deployment.
- Define infrastructure using Bicep or Terraform.
- Add automated endpoint tests and operational alerts.

---

## Cleanup and Cost Control

Deleting the dedicated resource group removes resources contained within the group. Application Insights or Log Analytics resources created elsewhere must be reviewed separately. Before deleting a Log Analytics workspace, confirm that unrelated workloads do not depend on it.

Figure 7 confirms only that no resource groups were displayed in the active subscription view. The report does not extend that claim beyond the visible evidence.

---

## Conclusion

The project demonstrated successful deployment and validation of an Azure Functions serverless HTTP endpoint. The evidence confirms a running Linux Function App on Flex Consumption, successful publication of the `GetStatus` HTTP trigger, generation of an invoke URL, a working `Hello, world!` response, function availability in Azure Portal, and an empty resource-group view after cleanup.

This document is a detailed technical assignment report rather than a GitHub repository introduction. A separate `README.md` should remain concise and direct readers to this report for the full methodology, evidence, validation, security considerations, limitations, and lessons learned.

---

## Disclaimer

This project was completed in a temporary Microsoft Learn or Skillable lab environment for educational and portfolio-development purposes. Azure interfaces, resource names, regions, and features may differ in other environments. Review every screenshot for sensitive lab or account information before public publication.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
Azure Project Documentation
