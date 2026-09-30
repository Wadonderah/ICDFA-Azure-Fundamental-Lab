<div align="center">

# Cost Governance Documentation Report

## Azure Cost Tracking, Budget Monitoring, and Policy Enforcement

**Prepared by:** Wadondera A. Collins  
**Programme:** ICDFA Trainee | Cohort 11  
**Professional Focus:** Cloud Security Engineering  
**Lab Platform:** Microsoft Azure | Skillable  
**Report Date:** September 30, 2026  
**Project Status:** Completed

</div>

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Executive Summary](#2-executive-summary)
3. [Project Objectives](#3-project-objectives)
4. [Professional Value](#4-professional-value)
5. [Skills Demonstrated](#5-skills-demonstrated)
6. [Technologies and Tools Used](#6-technologies-and-tools-used)
7. [Lab Environment](#7-lab-environment)
8. [Repository Structure](#8-repository-structure)
9. [Methodology](#9-methodology)
10. [Implementation, Evidence, and Analysis](#10-implementation-evidence-and-analysis)
11. [Results and Validation](#11-results-and-validation)
12. [Security and Governance Notes](#12-security-and-governance-notes)
13. [Challenges and Lessons Learned](#13-challenges-and-lessons-learned)
14. [Limitations and Next Steps](#14-limitations-and-next-steps)
15. [Conclusion](#15-conclusion)
16. [Disclaimer](#16-disclaimer)
17. [Author](#17-author)

---

## 1. Project Overview

This report documents the completion of an Azure cost-governance lab that combined resource organization, cost visibility, budget monitoring, and regional deployment control. The work was performed in a controlled Microsoft Azure lab environment and focused on three governance capabilities:

- applying cost-tracking tags to Azure resources;
- creating a monthly budget for proactive spending awareness; and
- assigning and testing the built-in **Allowed locations** Azure Policy.

The implementation used the resource group `rg-gp-cost-guardrails` as the primary governance scope. A storage account was configured as the test workload, consistent metadata was applied to the resource group and storage account, and an Azure Policy restriction was validated by attempting deployment in a disallowed region.

This document is a formal project report rather than a repository landing page. It emphasizes implementation evidence, technical analysis, validation, governance reasoning, and lessons learned.

---

## 2. Executive Summary

The completed project established a small but practical Azure governance baseline. The solution addressed three common cloud-management requirements: understanding who owns a resource, receiving early notice of potential overspending, and preventing deployment outside an approved region.

A dedicated resource group was configured in **East US**, and a storage account named `stgpcostguard65711345` was prepared with Standard performance and locally redundant storage. The tags `environment: pilot` and `owner: it-team` were applied consistently to both the resource group and the storage account. A monthly budget named `gp-pilot-budget` was created with a value of **$10.00**, while the lab procedure specified actual-cost alert thresholds at 80% and 100%.

The built-in **Allowed locations** policy was then configured with **East US** as an approved location. A test storage deployment in **West US 2** failed validation because the selected region did not satisfy the policy. This provided direct evidence that the preventive governance control was working as intended.

The project concluded with cleanup instructions covering removal of the policy assignment, deletion of the budget, deletion of the resource group, and final verification. The result is a documented governance workflow that links cost classification, cost monitoring, preventive policy enforcement, and responsible cloud-resource lifecycle management.

---

## 3. Project Objectives

The objectives of the assignment were to:

1. Create a dedicated Azure resource group for the guided project.
2. Configure a storage account as a governed test resource.
3. Apply consistent ownership and environment tags.
4. Create a monthly Azure Cost Management budget.
5. Configure actual-cost notifications at 80% and 100% of the budget.
6. Assign the built-in **Allowed locations** policy at resource-group scope.
7. Confirm that a deployment in a disallowed region was denied.
8. Confirm that the selected allowed location was correctly configured.
9. Review the policy-enforcement outcome.
10. Remove project resources and governance objects to avoid ongoing charges.
11. Produce an evidence-based professional report suitable for a technical portfolio.

---

## 4. Professional Value

This project demonstrates applied knowledge relevant to cloud administration, Cloud Security Engineering, governance, compliance, and FinOps-oriented operations.

### Business value

- **Cost attribution:** Tags provide useful metadata for filtering and reporting by environment and ownership.
- **Budget awareness:** Budget alerts support earlier investigation before costs move beyond the intended target.
- **Deployment standardization:** Azure Policy helps enforce approved resource locations consistently.
- **Risk reduction:** Resource-group-level scope limits the policy assignment to the intended lab boundary.
- **Operational discipline:** Validation and cleanup demonstrate responsible control of the complete cloud-resource lifecycle.

### Career value

The assignment shows the ability to move beyond simple resource deployment and apply governance controls that support accountability, compliance, and cost-conscious cloud operations. The documented evidence also demonstrates attention to validation, security, and technical communication.

---

## 5. Skills Demonstrated

- Azure Portal navigation
- Azure Resource Group administration
- Azure Storage account configuration
- Resource naming and organization
- Azure tag design and application
- Cost-allocation metadata management
- Azure Cost Management navigation
- Monthly budget configuration
- Cost-alert planning
- Azure Policy discovery and assignment
- Policy parameter selection
- Policy-scope management
- Preventive control testing
- Deployment validation and error interpretation
- Governance evidence collection
- Resource cleanup planning
- Professional technical reporting

---

## 6. Technologies and Tools Used

| Technology or Tool | Use in the Assignment |
|---|---|
| Microsoft Azure Portal | Graphical interface used to configure and validate the lab |
| Azure Resource Manager | Resource organization and management context |
| Azure Resource Groups | Governance boundary for project resources |
| Azure Storage Account | Test workload for tags and policy enforcement |
| Azure Tags | Environment and ownership classification |
| Azure Cost Management | Budget creation and cost monitoring |
| Azure Budgets | Monthly spending target and alert configuration |
| Azure Policy | Regional deployment restriction and compliance control |
| Allowed locations policy | Built-in policy used to limit approved Azure regions |
| Skillable | Temporary guided-lab environment |
| Markdown | Format used for professional project documentation |

> Azure is a continuously managed cloud platform. The lab evidence did not display fixed service-version numbers, so unsupported version values have not been added to this report.

---

## 7. Lab Environment

| Environment Item | Recorded Configuration |
|---|---|
| Lab type | Guided Skillable Azure lab |
| Azure interface | Microsoft Azure Portal |
| Subscription display | MOC Subscription-lod53256907 |
| Resource group | `rg-gp-cost-guardrails` |
| Resource-group region | East US |
| Storage account | `stgpcostguard65711345` |
| Primary storage service | Azure Blob Storage or Azure Data Lake Storage |
| Storage performance | Standard |
| Storage redundancy | Locally redundant storage (LRS) |
| Environment tag | `environment: pilot` |
| Ownership tag | `owner: it-team` |
| Budget | `gp-pilot-budget` |
| Budget period | Monthly |
| Budget amount shown | $10.00 |
| Required alert thresholds | 80% and 100% actual cost |
| Policy definition | Allowed locations |
| Allowed location shown | East US |
| Disallowed test location shown | West US 2 |

### Credential handling

Authentication secrets from the temporary lab are intentionally excluded. The report does not reproduce passwords, Temporary Access Pass tokens, or other sign-in credentials.

---

## 8. Repository Structure

```text
Cost-Governance-Documentation/
|
+-- Cost_Governance_Documentation_Report.md
+-- screenshots/
    +-- Fig01 Resource Group Configuration.png
    +-- Fig02 Storage Account Configuration.png
    +-- Fig03 Resource Group Cost Tracking Tags.png
    +-- Fig04 Storage Account Cost Tracking Tags.png
    +-- Fig05 Monthly Budget Created.png
    +-- Fig06 Allowed Locations Policy Parameter.png
    +-- Fig07 Policy Denied Disallowed Region.png
```

For this downloadable report, the image links use filenames in the same directory as the Markdown file. If the images are moved into a `screenshots` folder, update each link from `./Fig...png` to `./screenshots/Fig...png`.

---

## 9. Methodology

The assignment followed a staged governance methodology.

### Phase 1: Establish the scope

A dedicated resource group was configured to provide a clear administrative and policy boundary for the project.

### Phase 2: Deploy a representative workload

A storage account was configured to act as the test resource for metadata and regional policy enforcement.

### Phase 3: Apply cost-classification metadata

The same `environment` and `owner` tags were applied to the resource group and storage account to establish consistent classification.

### Phase 4: Configure financial monitoring

A monthly budget was created in Azure Cost Management. The lab procedure required actual-cost alerts at 80% and 100% to create early and final notification points.

### Phase 5: Implement preventive governance

The built-in **Allowed locations** policy was configured with East US as the approved region and scoped to the lab resource group.

### Phase 6: Test enforcement

A storage account deployment was attempted in West US 2. Azure validation denied the request and identified the **Allowed locations** policy as the reason.

### Phase 7: Validate and document

Each screenshot was matched only to the task it visibly supports. Evidence analysis distinguishes between what is directly visible and what is specified by the lab procedure but not shown in the available screenshots.

### Phase 8: Clean up

The completion procedure required the policy assignment to be removed first, followed by the budget and resource group. Final checks were then required to confirm that the project objects no longer appeared.

---

## 10. Implementation, Evidence, and Analysis

### 10.1 Resource Group Configuration

The project began by configuring `rg-gp-cost-guardrails` in the East US region. The dedicated resource group established the logical boundary used by the storage resource and policy assignment.

<img width="1095" height="572" alt="Fig01 Resource Group Configuration" src="https://github.com/user-attachments/assets/905bca70-8437-40c4-85ef-ac2030c729b5" />


*Figure 1: Azure Resource Manager displays the configuration of `rg-gp-cost-guardrails` in East US.*

#### Evidence analysis

The screenshot visibly shows the **Create a resource group** page, the resource-group name `rg-gp-cost-guardrails`, the selected subscription, and the **East US** region. The **Review + create** button is available, which indicates that the required configuration values were entered. The image documents the configuration stage rather than the final deployment-completion notification.

---

### 10.2 Storage Account Configuration

A storage account was configured within the project workflow. The visible settings show a Standard storage configuration with locally redundant storage.

<img width="1086" height="559" alt="Fig02 Storage Account Configuration" src="https://github.com/user-attachments/assets/ce3dc872-b113-4df8-b15b-66df11298c4b" />


*Figure 2: Storage account configuration showing the assigned account name, East US region, Standard performance, and LRS redundancy.*

#### Evidence analysis

The screenshot identifies the storage account as `stgpcostguard65711345`. It shows **East US** as the selected region, **Azure Blob Storage or Azure Data Lake Storage** as the primary service, **Standard** performance, and **Locally redundant storage (LRS)** as the redundancy option. The resource-group selector is visible but does not display a selected value in this capture. Therefore, the image supports the storage configuration choices but does not independently prove the resource-group association or completed deployment.

---

### 10.3 Resource Group Cost-Tracking Tags

The resource group was assigned two governance tags:

- `environment` with the value `pilot`
- `owner` with the value `it-team`

<img width="1089" height="562" alt="Fig03 Resource Group Cost Tracking Tags" src="https://github.com/user-attachments/assets/78df6c0e-f66c-45c7-a365-7056eaa25810" />


*Figure 3: Cost-tracking tags entered for the `rg-gp-cost-guardrails` resource group.*

#### Evidence analysis

The Azure Tags blade visibly displays the resource group `rg-gp-cost-guardrails` and both required name-value pairs. The interface also shows **2 to be added**, and the **Apply** button remains visible. This provides strong evidence that the correct tags were entered, but the screenshot was captured before the Azure Portal confirmed that the changes had been applied. A stronger final-state screenshot would show the tags after selecting **Apply**.

---

### 10.4 Storage Account Cost-Tracking Tags

The same tag model was entered for the storage account to maintain consistent metadata between the containing resource group and the workload.

<img width="1091" height="564" alt="Fig04 Storage Account Cost Tracking Tags" src="https://github.com/user-attachments/assets/f6d4edb4-ad3e-4f67-8602-1aebc08a7968" />


*Figure 4: Matching `environment` and `owner` tags entered for storage account `stgpcostguard65711345`.*

#### Evidence analysis

The screenshot visibly identifies the storage account and shows `environment: pilot` and `owner: it-team`. As with Figure 3, the page shows **2 to be added**, while **Apply** is still available. The evidence confirms correct and consistent tag entry, but it does not show the post-application state.

The matching values support a consistent governance approach. In broader environments, standardized tags can support cost reporting, ownership lookup, automation, and policy evaluation when naming rules are governed centrally.

---

### 10.5 Monthly Budget Creation

A monthly budget named `gp-pilot-budget` was created through Azure Cost Management.

<img width="1092" height="550" alt="Fig05 Monthly Budget Created" src="https://github.com/user-attachments/assets/7c658348-855b-468b-a593-72d2fc37f006" />


*Figure 5: Cost Management budget list showing `gp-pilot-budget` with a monthly reset period and a $10.00 budget.*

#### Evidence analysis

The screenshot provides direct final-state evidence that `gp-pilot-budget` exists. The row shows a **Monthly** reset period, a budget value of **$10.00**, evaluated spend of **$0.00**, and progress of **0.00%** at the time of capture.

The lab procedure required actual-cost thresholds at 80% and 100%. Those alert details are not visible in this screenshot, so this report does not claim that the image independently proves both recipients or thresholds. A dedicated budget-details screenshot would strengthen that validation.

---

### 10.6 Allowed Locations Policy Configuration

The built-in **Allowed locations** policy was configured to permit East US.

<img width="1091" height="565" alt="Fig06 Allowed Locations Policy Parameter" src="https://github.com/user-attachments/assets/79e73d78-dd3a-439f-bcf6-9325cecb3434" />


*Figure 6: Azure Policy assignment Parameters tab showing East US selected as an allowed location.*

#### Evidence analysis

The screenshot visibly shows the **Assign policy** workflow on the **Parameters** tab. The **Allowed locations** field contains **East US**, and the region-selection menu shows East US selected. This confirms the intended policy parameter.

The screenshot does not display the Basics tab, final assignment confirmation, assignment scope, or compliance dashboard. Consequently, it supports the selected parameter but not every part of the completed assignment lifecycle.

---

### 10.7 Policy Enforcement Test

The policy was tested using a storage account deployment in West US 2, which was outside the configured allowed location.

<img width="1089" height="561" alt="Fig07 Policy Denied Disallowed Region" src="https://github.com/user-attachments/assets/856fe6a9-6954-45d8-8b47-8a81245fc98c" />


*Figure 7: Azure validation failure showing that the West US 2 storage account deployment was denied by the Allowed locations policy.*

#### Evidence analysis

This is the strongest enforcement evidence in the report. The **Review + create** page shows:

- resource group `rg-gp-cost-guardrails`;
- location **West US 2**;
- a storage account test name;
- the banner **Validation failed**; and
- an error stating that the resource was disallowed by policy.

The error panel explicitly references **Policy: Allowed locations** and reports the `RequestDisallowedByPolicy` code. The result confirms that the policy operated as a preventive control by blocking a deployment that did not meet the configured location requirement.

The displayed replication option for this test is read-access geo-redundant storage. This differs from the LRS configuration recorded for the original cost-governance storage account, but the regional denial remains the relevant policy test because the reported error identifies the location policy as the blocking control.

---

### 10.8 Cleanup Procedure

The prescribed cleanup sequence was:

1. Remove the **Allowed locations** policy assignment.
2. Delete `gp-pilot-budget`.
3. Delete `rg-gp-cost-guardrails` and its contained resources.
4. Verify that the assignment, budget, and resource group no longer appear.

No cleanup screenshot was included in the supplied evidence set. Therefore, the report records the required cleanup procedure but does not present visual proof of final deletion.

---

## 11. Results and Validation

| Control or Task | Expected Outcome | Evidence Status | Assessment |
|---|---|---|---|
| Resource-group configuration | `rg-gp-cost-guardrails` configured in East US | Figure 1 | Configuration shown; final creation notification not shown |
| Storage-account configuration | Standard storage with LRS in East US | Figure 2 | Required configuration values shown |
| Resource-group tags | `environment: pilot`, `owner: it-team` | Figure 3 | Correct values entered; post-Apply state not shown |
| Storage-account tags | Matching tags on the storage account | Figure 4 | Correct values entered; post-Apply state not shown |
| Monthly budget | `gp-pilot-budget`, monthly, $10.00 | Figure 5 | Final budget-list evidence shown |
| Budget alerts | 80% and 100% actual-cost thresholds | No direct screenshot | Required by lab procedure, not visually verified in supplied evidence |
| Policy parameter | East US selected as allowed | Figure 6 | Parameter selection shown |
| Policy assignment scope | Resource-group scope | No direct assignment-summary screenshot | Described by lab procedure, not fully visible in Figure 6 |
| Disallowed-region test | West US 2 deployment denied | Figure 7 | Directly verified by policy error |
| Allowed-region test | Deployment validation succeeds in East US | No direct screenshot | Not visually verified in supplied evidence |
| Compliance review | Assignment compliance status displayed | No direct screenshot | Not visually verified in supplied evidence |
| Cleanup | Policy, budget, and resource group removed | No direct screenshot | Procedure documented; final state not visually verified |

### Overall assessment

The supplied evidence is well aligned with the central governance workflow and directly demonstrates resource configuration, consistent tag entry, budget existence, allowed-location selection, and policy denial. The evidence set would be more complete with screenshots showing:

- tags after **Apply**;
- the 80% and 100% budget-alert details;
- the final policy-assignment overview and scope;
- successful validation in East US;
- the Policy Compliance page; and
- cleanup verification.

These are evidence-quality recommendations, not indications that the documented procedure was incorrect.

---

## 12. Security and Governance Notes

- Authentication details are excluded from the report and repository.
- Screenshots should be reviewed before public upload because Azure interfaces can display tenant names, subscription identifiers, account labels, and email addresses.
- Policy scope should be confirmed before assignment to avoid affecting unrelated resources.
- Budget notifications should be sent only to approved recipients.
- Tags should avoid passwords, secrets, personal data, and other sensitive values.
- Budget alerts provide notification and awareness. The documented budget does not by itself prove automatic resource shutdown.
- Cleanup is essential in temporary labs because deployed resources can continue to incur charges until removed.
- Production deployments should use approved change-management, naming, tagging, cost-management, policy-exemption, and access-control standards.

---

## 13. Challenges and Lessons Learned

### Evidence must capture the final state

Several screenshots capture settings immediately before they are applied. This is useful implementation evidence, but a post-action confirmation is stronger because it proves persistence rather than data entry alone.

### Governance controls work best as a set

Tags, budgets, and policy serve different purposes. Tags classify resources, budgets monitor spending, and policy restricts configuration. Combining the three produces a stronger governance baseline than using any one control independently.

### Scope is a critical design decision

The policy was intended for a single resource group. Carefully selecting the scope helps enforce the requirement where needed while minimizing unintended effects elsewhere.

### Error messages are useful validation evidence

The policy-denial message did more than show that deployment failed. The message identified the specific **Allowed locations** policy, providing a clear connection between the configured control and the blocked deployment.

### Cleanup is part of implementation quality

A cloud lab is not complete when configuration ends. Removing temporary controls and resources, then checking that deletion succeeded, is part of responsible cloud administration.

---

## 14. Limitations and Next Steps

### Current limitations

- The lab used a temporary educational environment rather than a production subscription.
- The budget amount was intentionally small and intended for testing.
- Only one built-in policy was evaluated.
- Alert-delivery evidence was not supplied.
- Policy compliance and cleanup were not included in the screenshot set.
- The work was completed through the Azure Portal rather than infrastructure-as-code automation.

### Recommended next steps

1. Capture final-state screenshots for the missing validation points.
2. Place all screenshots in a dedicated `screenshots` directory and update the Markdown links.
3. Add a formal tag standard covering permitted keys, values, ownership, and review intervals.
4. Explore Azure Policy initiatives for grouping multiple governance requirements.
5. Evaluate budget action groups and operational escalation procedures in an authorized environment.
6. Reproduce the deployment with Bicep, Terraform, Azure CLI, or PowerShell.
7. Add cost analysis by resource group and tag after sufficient usage data is available.
8. Define an approval and expiration process for policy exemptions.

---

## 15. Conclusion

The Azure Cost Governance project successfully demonstrated how resource metadata, budget monitoring, and policy enforcement can be combined into a coherent governance workflow. The evidence shows the configuration of a dedicated resource group and storage account, consistent entry of cost-tracking tags, creation of a monthly budget, selection of East US as an allowed location, and denial of a West US 2 deployment by Azure Policy.

The project is professionally relevant because it connects financial awareness with technical control. Rather than treating cost management and compliance as separate concerns, the lab shows how Azure governance services can work together to improve accountability, standardization, and operational discipline.

The strongest validation result is the explicit policy-denial error, which confirms that the configured preventive control actively blocked a noncompliant regional deployment. With the addition of final-state screenshots for alerts, compliance, successful allowed-region deployment, and cleanup, the evidence package would provide end-to-end visual coverage of the full lab lifecycle.

---

## 16. Disclaimer

This report documents an educational Microsoft Azure lab completed in a temporary Skillable environment. The configuration values, resource names, budget amount, and policy scope were selected for guided training and should not be copied directly into a production environment without review.

No password, Temporary Access Pass token, or authentication secret is included. Before publishing screenshots, account labels, subscription identifiers, tenant names, email addresses, and other environment-specific information should be reviewed and redacted where appropriate.

Microsoft Azure and related product names are trademarks of Microsoft Corporation. This report is an independent educational portfolio document and is not official Microsoft documentation.

---

## 17. Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11  
Cloud Security Engineering  
Professional Interests: Microsoft Azure, Cloud Governance, Identity, Security, and DevOps

<div align="center">

**Report completed on September 30, 2026**

*Documenting secure, governed, and cost-aware cloud engineering through verifiable evidence.*

</div>
