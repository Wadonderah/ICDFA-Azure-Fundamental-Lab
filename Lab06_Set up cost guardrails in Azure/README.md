<div align="center">

# Azure Cost Governance with Tags, Budgets, and Policy

### A Practical Azure Governance Lab for Cost Visibility, Spending Control, and Regional Compliance

**Author:** Wadondera A. Collins  
**Role:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Completion Date:** September 30, 2026  
**Platform:** Microsoft Azure | Skillable Lab Environment  
**Status:** Completed

</div>

---

## Table of Contents

- [Project Overview](#project-overview)
- [Executive Summary](#executive-summary)
- [Project Objectives](#project-objectives)
- [Professional Value](#professional-value)
- [Skills Demonstrated](#skills-demonstrated)
- [Technologies and Services](#technologies-and-services)
- [Lab Environment](#lab-environment)
- [Architecture and Governance Flow](#architecture-and-governance-flow)
- [Implementation](#implementation)
  - [Exercise 1: Apply Cost-Tracking Tags](#exercise-1-apply-cost-tracking-tags)
  - [Exercise 2: Create a Budget and Alerts](#exercise-2-create-a-budget-and-alerts)
  - [Exercise 3: Assign and Test Azure Policy](#exercise-3-assign-and-test-azure-policy)
  - [Clean-Up and Verification](#clean-up-and-verification)
- [Validation Checklist](#validation-checklist)
- [Suggested Screenshot Evidence](#suggested-screenshot-evidence)
- [Results](#results)
- [Security and Governance Considerations](#security-and-governance-considerations)
- [Challenges and Lessons Learned](#challenges-and-lessons-learned)
- [Limitations and Next Steps](#limitations-and-next-steps)
- [Repository Structure](#repository-structure)
- [Conclusion](#conclusion)
- [Disclaimer](#disclaimer)
- [Author](#author)

---

## Project Overview

This project demonstrates the implementation of foundational cost-governance controls in Microsoft Azure. The completed lab combines resource tagging, budget monitoring, cost alerts, and Azure Policy to improve accountability, spending awareness, and deployment compliance.

The solution was implemented around a dedicated resource group named `rg-gp-cost-guardrails`. Resources were organized with cost-tracking tags, monitored through a monthly budget, and governed by an **Allowed locations** policy. Policy enforcement was then tested by attempting deployments in both prohibited and permitted Azure regions.

---

## Executive Summary

Cloud governance requires more than deploying resources successfully. Organizations also need reliable methods to identify resource ownership, track spending, receive early cost warnings, and restrict deployments that do not meet operational requirements.

In this lab, I built a small Azure governance baseline with three complementary controls:

1. **Resource tags** provided ownership and environment context for reporting and filtering.
2. **Azure Cost Management budgets** introduced proactive alerts at 80% and 100% of the configured monthly amount.
3. **Azure Policy** restricted resource deployment to an approved Azure region and demonstrated preventive governance through an enforced denial.

The lab concluded with the removal of the policy assignment, budget, resource group, storage accounts, and test resources to prevent unnecessary charges.

---

## Project Objectives

- Create a dedicated Azure resource group for the governance lab.
- Deploy a test storage account using cost-conscious configuration options.
- Apply consistent `environment` and `owner` tags to Azure resources.
- Create a monthly budget with actionable alert thresholds.
- Assign an Azure Policy at the resource-group scope.
- Test policy behavior in disallowed and allowed Azure regions.
- Review policy compliance information.
- Remove all lab resources and verify successful cleanup.

---

## Professional Value

This project reflects practical responsibilities commonly associated with cloud administration, Cloud Security Engineering, FinOps, and governance roles. It demonstrates the ability to combine visibility, financial control, and policy enforcement rather than managing each area in isolation.

The completed work supports the following professional outcomes:

- Better resource ownership and cost attribution
- Earlier awareness of unexpected cloud spending
- Standardized regional deployment requirements
- Reduced risk of unmanaged or noncompliant resources
- Documented validation and responsible resource cleanup

---

## Skills Demonstrated

- Azure resource-group administration
- Azure Storage account deployment
- Resource tagging and metadata management
- Azure Cost Management configuration
- Monthly budget and cost-alert configuration
- Azure Policy assignment and scope selection
- Policy parameter configuration
- Preventive control testing
- Policy compliance review
- Cloud cost-awareness practices
- Azure resource cleanup and validation
- Technical documentation for a professional portfolio

---

## Technologies and Services

| Technology or Service | Purpose in the Project |
|---|---|
| Microsoft Azure Portal | Primary interface used to configure and validate resources |
| Azure Resource Groups | Logical boundary for the lab resources and policy scope |
| Azure Storage Account | Test workload used for tagging and policy validation |
| Azure Tags | Metadata used for ownership and environment classification |
| Azure Cost Management | Service used to create the monthly budget and alerts |
| Azure Budgets | Spending threshold monitoring at 80% and 100% |
| Azure Policy | Governance control used to restrict allowed deployment locations |
| Skillable Lab Environment | Guided educational environment used to complete the project |

> Exact Azure service versions were not displayed in the supplied lab instructions. Azure services are continuously managed cloud services, so this README records the configuration used rather than assigning unsupported product version numbers.

---

## Lab Environment

| Item | Configuration |
|---|---|
| Environment | Skillable guided lab |
| Azure interface | Azure Portal |
| Resource group | `rg-gp-cost-guardrails` |
| Primary storage account | `stgpcostguard65711345` |
| Budget name | `gp-pilot-budget` |
| Budget reset period | Monthly |
| Test budget amount | 10 in the subscription billing currency |
| Alert thresholds | 80% and 100% |
| Policy definition | Allowed locations |
| Policy scope | `rg-gp-cost-guardrails` |
| Resource tags | `environment: pilot`, `owner: it-team` |
| Storage performance | Standard |
| Storage redundancy | Locally-redundant storage (LRS) |

> **Credential protection:** Lab passwords, Temporary Access Pass tokens, and other sign-in secrets are intentionally excluded from this repository.

---

## Architecture and Governance Flow

```text
Azure Subscription
|
+-- Cost Management
|   +-- Monthly Budget: gp-pilot-budget
|       +-- Actual-cost alert at 80%
|       +-- Actual-cost alert at 100%
|
+-- Resource Group: rg-gp-cost-guardrails
    |
    +-- Tags
    |   +-- environment = pilot
    |   +-- owner = it-team
    |
    +-- Storage Account
    |   +-- Standard performance
    |   +-- LRS redundancy
    |   +-- Matching governance tags
    |
    +-- Azure Policy Assignment
        +-- Allowed locations
        +-- Denies disallowed regional deployments
        +-- Permits deployment in the configured region
```

This layered design combines organizational metadata, financial monitoring, and compliance enforcement within one controlled lab scope.

---

## Implementation

### Exercise 1: Apply Cost-Tracking Tags

#### 1. Prepare the environment

1. Opened **Resource groups** in the Azure Portal.
2. Created `rg-gp-cost-guardrails` in the selected Azure region.
3. Recorded the email address to be used for budget notifications.

#### 2. Create a test storage account

1. Opened **Storage accounts** and selected **Create**.
2. Selected `rg-gp-cost-guardrails` as the resource group.
3. Entered `stgpcostguard65711345` as the storage account name.
4. Used the same region as the resource group.
5. Selected Azure Blob Storage or Azure Data Lake Storage as directed by the lab.
6. Selected **Standard** performance and **Locally-redundant storage (LRS)**.
7. Reviewed, created, and opened the deployed resource.

#### 3. Tag the resource group

The following tags were added to `rg-gp-cost-guardrails`:

| Tag | Value |
|---|---|
| `environment` | `pilot` |
| `owner` | `it-team` |

**Validation:** The resource group displayed both tags after they were applied.

#### 4. Tag the storage account

The same `environment` and `owner` tags were applied to the storage account.

**Validation:** The storage account displayed tags matching those assigned to the resource group.

---

### Exercise 2: Create a Budget and Alerts

#### 1. Open Cost Management

1. Opened **Cost Management** from the Azure Portal search bar.
2. Selected **Budgets** under Monitoring.
3. Selected **Add** and confirmed the intended budget scope.

#### 2. Configure the budget

The budget was configured with the following settings:

| Setting | Value |
|---|---|
| Name | `gp-pilot-budget` |
| Reset period | Monthly |
| Test amount | 10 in the applicable billing currency |
| First alert | Actual cost at 80% |
| Second alert | Actual cost at 100% |
| Alert recipient | Authorized project email address |

**Validation:** `gp-pilot-budget` appeared in the budget list with the two configured alert thresholds.

The 80% threshold provides an earlier warning for investigation, while the 100% threshold indicates that actual cost has reached the full configured budget amount.

---

### Exercise 3: Assign and Test Azure Policy

#### 1. Assign the Allowed locations policy

1. Opened **Policy** in the Azure Portal.
2. Selected **Definitions** under Authoring.
3. Searched for and selected **Allowed locations**.
4. Started a new policy assignment.
5. Scoped the assignment to `rg-gp-cost-guardrails`.
6. Selected one Azure region as the allowed location.
7. Reviewed and created the assignment.

**Validation:** The **Allowed locations** policy appeared as an assignment scoped to the project resource group.

#### 2. Test policy enforcement

A temporary storage account deployment was used to test the policy:

1. Selected `rg-gp-cost-guardrails` as the target resource group.
2. Chose a region that was not included in the policy's allowed locations.
3. Attempted validation and confirmed that the deployment was denied by policy.
4. Returned to the configuration and changed the region to the approved location.
5. Re-ran validation and confirmed that it passed.
6. Created the resource in the allowed location.

**Validation:** The policy denied the deployment in a disallowed region and permitted it in the configured region.

#### 3. Review policy compliance

1. Opened **Policy** and selected **Compliance**.
2. Located the **Allowed locations** assignment.
3. Opened the assignment to review its compliance details.
4. Confirmed the enforcement status for resources deployed in the approved region.

**Validation:** The compliance view displayed the status of the policy assignment and the resources evaluated within its scope.

---

### Clean-Up and Verification

Cleanup was performed in the correct dependency order.

#### 1. Remove the policy assignment

The **Allowed locations** assignment was deleted before the resource group to prevent the governance control from interfering with resource removal.

#### 2. Delete the budget

`gp-pilot-budget` was removed from Azure Cost Management.

#### 3. Delete the resource group

`rg-gp-cost-guardrails` was deleted. This also removed the storage accounts and test resources contained within the group.

#### 4. Verify cleanup

The following checks were completed:

- `rg-gp-cost-guardrails` no longer appeared under Resource groups.
- The **Allowed locations** assignment no longer appeared under Policy assignments.
- `gp-pilot-budget` no longer appeared under Budgets.

---

## Validation Checklist

| Validation Item | Expected Result | Status |
|---|---|---|
| Resource group created | `rg-gp-cost-guardrails` is available | Completed |
| Test storage account created | Storage account deployment succeeds | Completed |
| Resource-group tags applied | `environment: pilot` and `owner: it-team` are visible | Completed |
| Storage-account tags applied | Tags match the resource group | Completed |
| Monthly budget created | `gp-pilot-budget` appears in the budget list | Completed |
| Budget thresholds configured | 80% and 100% alerts are present | Completed |
| Policy assigned | Allowed locations is scoped to the resource group | Completed |
| Disallowed region tested | Deployment is denied by Azure Policy | Completed |
| Allowed region tested | Validation passes and deployment is permitted | Completed |
| Compliance reviewed | Policy status is visible in the compliance dashboard | Completed |
| Policy assignment removed | Assignment no longer appears | Completed |
| Budget removed | Budget no longer appears | Completed |
| Resource group removed | Resource group no longer appears | Completed |

---

## Suggested Screenshot Evidence

If screenshot evidence is added to the repository, each image should be placed directly beneath the matching task. Use the exact visible content of each screenshot to confirm the final filename and caption.

| Suggested Filename | Evidence It Should Show | Recommended Placement |
|---|---|---|
| `Fig01 Resource Group Created.png` | `rg-gp-cost-guardrails` successfully created | Exercise 1, Prepare the environment |
| `Fig02 Storage Account Deployment.png` | Completed storage account deployment | Exercise 1, Create a test storage account |
| `Fig03 Resource Group Tags.png` | Resource-group tags and their values | Exercise 1, Tag the resource group |
| `Fig04 Storage Account Tags.png` | Matching storage-account tags | Exercise 1, Tag the storage account |
| `Fig05 Budget Configuration.png` | Monthly budget name and amount | Exercise 2, Configure the budget |
| `Fig06 Budget Alert Thresholds.png` | 80% and 100% actual-cost alerts | Exercise 2, Configure the budget |
| `Fig07 Allowed Locations Assignment.png` | Policy assignment and resource-group scope | Exercise 3, Assign the policy |
| `Fig08 Policy Denied Deployment.png` | Policy denial for the disallowed region | Exercise 3, Test policy enforcement |
| `Fig09 Allowed Region Validation.png` | Successful validation in the permitted region | Exercise 3, Test policy enforcement |
| `Fig10 Policy Compliance Status.png` | Compliance details for the assignment | Exercise 3, Review compliance |
| `Fig11 Cleanup Verification.png` | Final evidence that lab resources were removed | Clean-Up and Verification |

> Do not add a screenshot under a task unless the image visibly proves that task. Rename files only after confirming that the filename, Markdown link, caption, and screenshot content match exactly.

Example Markdown syntax:

```markdown
![Fig01 Resource Group Created](screenshots/Fig01%20Resource%20Group%20Created.png)

*Figure 1: The Azure Portal displays the successfully created project resource group.*
```

---

## Results

The project achieved its intended governance outcomes:

- Pilot resources were consistently classified for ownership and environment tracking.
- A monthly budget was created with warning thresholds at 80% and 100%.
- Azure Policy was assigned at the resource-group level.
- A deployment to a disallowed region was prevented.
- A deployment to the permitted region passed validation.
- Policy compliance information was reviewed.
- All project resources and governance objects were removed after testing.

Together, these results demonstrate a practical governance pattern that integrates cost visibility, financial monitoring, and preventive cloud controls.

---

## Security and Governance Considerations

- **Secrets were excluded:** No passwords, access tokens, or authentication details are documented in this repository.
- **Scope was limited:** The policy was assigned only to the project resource group, reducing the risk of unintended subscription-wide impact.
- **Policy behavior was tested safely:** Enforcement was validated through a controlled test deployment.
- **Cost exposure was limited:** The lab used a small test budget and LRS storage configuration.
- **Cleanup was verified:** Governance objects and billable resources were removed after use.
- **Resource ownership was documented:** Tags established a basic ownership and environment classification model.

In a production environment, tag naming, allowed regions, budget values, recipients, exemptions, and policy scope should follow approved organizational standards and change-control processes.

---

## Challenges and Lessons Learned

### Scope selection matters

Budgets and policies are effective only when applied to the intended scope. Confirming the subscription or resource-group context before creation helps prevent misplaced controls.

### Tags improve visibility but require consistency

A tagging model becomes useful when the same keys and approved values are applied consistently. Matching tags across the resource group and storage account supported reliable classification.

### Alerts support awareness, not automatic shutdown

Budget thresholds provide notification points for investigation and response. They should be paired with an operational process that defines who reviews alerts and what action should follow.

### Policy provides preventive governance

The policy test demonstrated the difference between guidance and enforcement. A disallowed regional deployment was actively blocked, while a compliant deployment was permitted.

### Cleanup is part of successful cloud operations

Removing test resources, assignments, and budgets prevents unnecessary charges and leaves the environment in a known state.

---

## Limitations and Next Steps

This guided project used a small lab scope and a basic built-in policy. A broader production implementation could include:

- A formal tag taxonomy with required values
- Azure Policy initiatives that group related controls
- Policy exemptions with documented approval and expiration
- Management-group or subscription-level governance design
- Multiple budget recipients and action groups
- Cost analysis by tag, resource group, service, or subscription
- Automated deployment through Bicep, ARM templates, Terraform, or Azure CLI
- Centralized reporting through Azure dashboards or workbooks
- Azure Policy remediation for controls that support deploy-if-not-exists or modify effects
- Periodic governance reviews and budget-threshold tuning

These are recommended extensions and were not part of the completed guided-lab scope.

---

## Repository Structure

```text
azure-cost-governance/
|
+-- README.md
+-- screenshots/
|   +-- Fig01 Resource Group Created.png
|   +-- Fig02 Storage Account Deployment.png
|   +-- Fig03 Resource Group Tags.png
|   +-- Fig04 Storage Account Tags.png
|   +-- Fig05 Budget Configuration.png
|   +-- Fig06 Budget Alert Thresholds.png
|   +-- Fig07 Allowed Locations Assignment.png
|   +-- Fig08 Policy Denied Deployment.png
|   +-- Fig09 Allowed Region Validation.png
|   +-- Fig10 Policy Compliance Status.png
|   +-- Fig11 Cleanup Verification.png
+-- LICENSE
```

Only include screenshot files that are available and that clearly match their labels. Remove unused placeholders from the final repository.

---

## Conclusion

This completed project established a practical Azure cost-governance baseline using resource tags, a monthly budget, cost alerts, and Azure Policy. The lab demonstrated how financial visibility and technical enforcement can work together to improve cloud accountability.

The successful policy test showed that Azure governance can prevent deployments that violate an approved regional requirement while allowing compliant resources to proceed. Final cleanup and verification completed the operational lifecycle responsibly and reduced the risk of ongoing lab charges.

---

## Disclaimer

This repository documents a completed educational lab performed in a temporary Skillable Microsoft Azure environment. Resource names, settings, and values were used for training purposes and may require modification before use in another subscription or production environment.

No passwords, Temporary Access Pass tokens, authentication secrets, or private account details are included. Screenshots should be reviewed and redacted before publication to ensure that they do not expose subscription identifiers, tenant information, email addresses, access tokens, or other sensitive data.

Microsoft Azure and related product names are trademarks of Microsoft Corporation. This project is an independent educational portfolio entry and does not represent an official Microsoft deployment guide.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11  
Cloud Security Engineering  
Focus Areas: Microsoft Azure, Cloud Security, Governance, Identity, and DevOps

---

<div align="center">

**Completed on September 30, 2026**

*Building secure, governed, and cost-aware cloud environments through practical implementation.*

</div>
