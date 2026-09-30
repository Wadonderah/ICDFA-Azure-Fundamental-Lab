<div align="center">

# 💰 Azure Cost Governance: Tags, Budgets, and Policy

### Mentor Pilot Program | Completed Assignment

**Author:** Wadondera A. Collins  
**Role:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Completion Date:** September 30, 2026

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Governance-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![FinOps](https://img.shields.io/badge/Focus-Cost%20Governance-00A4EF)](#-skills-demonstrated)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Policy](https://img.shields.io/badge/Azure%20Policy-Allowed%20Locations-6F42C1)](#-exercise-3-assign-and-test-azure-policy)

*A practical Azure governance lab covering cost-tracking tags, monthly budgets, alert thresholds, regional policy enforcement, compliance validation, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Apply Cost-Tracking Tags](#-exercise-1-apply-cost-tracking-tags)
- [Exercise 2: Create a Budget and Alerts](#-exercise-2-create-a-budget-and-alerts)
- [Exercise 3: Assign and Test Azure Policy](#-exercise-3-assign-and-test-azure-policy)
- [Exercise 4: Clean Up and Verify](#-exercise-4-clean-up-and-verify)
- [Screenshot Evidence](#-screenshot-evidence)
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

This repository documents the successful completion of the **Azure Cost Governance with Tags, Budgets, and Policy** lab in the **Mentor Pilot Program**. The project combined resource metadata, financial monitoring, and preventive governance within a dedicated Azure resource-group scope.

The solution used `environment` and `owner` tags to establish cost and ownership context, a monthly Azure Cost Management budget to provide alerts at 80% and 100%, and the built-in **Allowed locations** policy to restrict resource deployment to an approved Azure region.

The project covered the following workflow:

1. Create a dedicated governance resource group.
2. Deploy a cost-conscious test storage account.
3. Apply matching ownership and environment tags.
4. Create a monthly budget with two alert thresholds.
5. Assign the **Allowed locations** policy at resource-group scope.
6. Test a deployment in a prohibited region.
7. Test a deployment in the approved region.
8. Review policy compliance information.
9. Remove the policy assignment, budget, resources, and test objects.
10. Verify final cleanup.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

By completing this lab, I demonstrated the ability to:

- Create and manage an isolated Azure resource group.
- Deploy a Standard LRS storage account.
- Apply consistent resource tags for ownership and environment classification.
- Configure an Azure Cost Management budget.
- Configure actual-cost alerts at 80% and 100%.
- Assign a built-in Azure Policy at resource-group scope.
- Configure an approved Azure location as a policy parameter.
- Validate policy denial in a prohibited region.
- Validate successful deployment in an approved region.
- Review policy compliance information.
- Remove governance objects and billable resources responsibly.

---

## 🏗️ Architecture and Resources

```text
Azure Subscription
├── Cost Management
│   └── Budget: gp-pilot-budget
│       ├── Actual-cost alert: 80%
│       └── Actual-cost alert: 100%
│
└── Resource Group: rg-gp-cost-guardrails
    ├── Tags
    │   ├── environment = pilot
    │   └── owner = it-team
    ├── Storage Account: stgpcostguard65711345
    │   ├── Performance: Standard
    │   ├── Redundancy: LRS
    │   └── Matching governance tags
    └── Policy Assignment: Allowed locations
        ├── Disallowed region: Denied
        └── Approved region: Permitted
```

| Resource or Control | Name or Configuration | Purpose |
|---|---|---|
| Resource group | `rg-gp-cost-guardrails` | Lab boundary and policy scope |
| Storage account | `stgpcostguard65711345` | Test workload for tags and policy validation |
| Resource tags | `environment=pilot`, `owner=it-team` | Ownership and environment classification |
| Budget | `gp-pilot-budget` | Monthly spending visibility |
| Budget amount | `10` in the applicable billing currency | Test spending threshold |
| Alerts | 80% and 100% actual cost | Early and full-threshold notification |
| Policy definition | `Allowed locations` | Regional deployment restriction |
| Storage configuration | Standard, LRS | Cost-conscious test configuration |

> [!NOTE]
> **Final state:** The policy assignment, budget, resource group, storage accounts, and test resources were removed after validation.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An authorized Skillable Azure lab subscription
- Permission to create resource groups and storage accounts
- Permission to create budgets at the selected scope
- Permission to assign Azure Policy at resource-group scope
- An authorized email address for budget notifications

### Tools and Environment

| Tool or Service | Version or Status | Purpose |
|---|---|---|
| Microsoft Azure portal | Version not provided | Resource, cost, and policy administration |
| Azure Resource Groups | Managed Azure service | Project boundary and policy scope |
| Azure Storage | API version not recorded | Test workload |
| Azure Tags | Managed Azure feature | Ownership and environment metadata |
| Azure Cost Management | Managed Azure service | Budget and alert configuration |
| Azure Policy | Managed Azure service | Regional policy enforcement |
| Skillable Lab Environment | Version not provided | Guided educational subscription |

> [!NOTE]
> Exact Azure service versions were not displayed in the lab instructions. The configuration is documented without unsupported version estimates.

### Security Notice

Passwords, Temporary Access Pass codes, authentication secrets, subscription identifiers, tenant information, and private account details are intentionally **not included**.

> [!CAUTION]
> Review screenshots before publication and redact email addresses, subscription IDs, tenant IDs, access tokens, and other sensitive values.

---

## 🏷️ Exercise 1: Apply Cost-Tracking Tags

### 1. Prepare the Environment

1. Open **Resource groups** in the Azure portal.
2. Create:

```text
rg-gp-cost-guardrails
```

3. Select the assigned subscription and lab region.
4. Record the authorized email address for budget notifications without publishing it.

**Validation:** The resource group appeared in the Azure portal.

### 2. Create the Test Storage Account

Configure the storage account with the following values:

| Setting | Value |
|---|---|
| Resource group | `rg-gp-cost-guardrails` |
| Storage account | `stgpcostguard65711345` |
| Region | Same region as the resource group |
| Performance | Standard |
| Redundancy | Locally-redundant storage (LRS) |

**Validation:** The storage account deployed successfully.

### 3. Tag the Resource Group

Apply the following tags:

| Tag | Value |
|---|---|
| `environment` | `pilot` |
| `owner` | `it-team` |

**Validation:** Both tags appeared on `rg-gp-cost-guardrails`.

### 4. Tag the Storage Account

Apply the same tags to `stgpcostguard65711345`.

**Validation:** The storage account displayed matching `environment` and `owner` tags.

> [!TIP]
> A tagging model is most useful when approved keys and values are applied consistently across related resources.

---

## 💳 Exercise 2: Create a Budget and Alerts

### 1. Open Cost Management

1. Search for **Cost Management**.
2. Open **Budgets** under Monitoring.
3. Select **Add**.
4. Confirm the intended budget scope.

### 2. Configure the Monthly Budget

| Setting | Value |
|---|---|
| Name | `gp-pilot-budget` |
| Reset period | Monthly |
| Test amount | `10` in the applicable billing currency |
| First alert | Actual cost at 80% |
| Second alert | Actual cost at 100% |
| Recipient | Authorized project email address |

**Validation:** `gp-pilot-budget` appeared in the budget list with both alert thresholds.

> [!IMPORTANT]
> Budget alerts provide cost awareness. They should be paired with an operational response process that defines ownership and follow-up actions.

---

## 🛡️ Exercise 3: Assign and Test Azure Policy

### 1. Assign the Allowed Locations Policy

1. Open **Policy** in the Azure portal.
2. Select **Definitions**.
3. Search for **Allowed locations**.
4. Start a new assignment.
5. Set the scope to `rg-gp-cost-guardrails`.
6. Select the approved Azure region.
7. Review and create the assignment.

**Validation:** The policy appeared as an assignment scoped to the project resource group.

### 2. Test a Disallowed Region

1. Start a temporary storage-account deployment in `rg-gp-cost-guardrails`.
2. Select a region not included in the allowed-locations parameter.
3. Run validation.

**Validation:** Azure Policy denied the deployment in the prohibited region.

### 3. Test the Approved Region

1. Change the temporary storage account to the approved location.
2. Run validation again.
3. Create the resource after validation succeeds.

**Validation:** Validation passed and deployment was permitted in the approved region.

### 4. Review Compliance

1. Open **Policy**.
2. Select **Compliance**.
3. Locate the **Allowed locations** assignment.
4. Review its compliance information and evaluated resources.

**Validation:** The compliance view displayed the assignment and its evaluated resources.

---

## 🧹 Exercise 4: Clean Up and Verify

### 1. Remove the Policy Assignment

Delete the **Allowed locations** assignment before removing the resource group.

**Validation:** The assignment no longer appeared under Policy assignments.

### 2. Delete the Budget

Delete `gp-pilot-budget` from Azure Cost Management.

**Validation:** The budget no longer appeared under Budgets.

### 3. Delete the Resource Group

Delete `rg-gp-cost-guardrails`. This removes the storage accounts and contained test resources.

**Validation:** The resource group no longer appeared in the resource-group list.

> [!WARNING]
> Resource-group deletion permanently removes contained resources. Verify the selected resource group before confirming deletion.

---

## 🖼️ Screenshot Evidence

Add only screenshots whose visible content proves the matching task. Keep filenames, links, captions, and placement synchronized.

| Filename | Required Evidence | Placement |
|---|---|---|
| `Fig01 Resource Group Created.png` | Project resource group created | Exercise 1, Prepare the Environment |
| `Fig02 Storage Account Deployment.png` | Successful storage deployment | Exercise 1, Create the Test Storage Account |
| `Fig03 Resource Group Tags.png` | Resource-group tag values | Exercise 1, Tag the Resource Group |
| `Fig04 Storage Account Tags.png` | Matching storage tags | Exercise 1, Tag the Storage Account |
| `Fig05 Budget Configuration.png` | Budget name and amount | Exercise 2, Configure the Monthly Budget |
| `Fig06 Budget Alert Thresholds.png` | 80% and 100% alerts | Exercise 2, Configure the Monthly Budget |
| `Fig07 Allowed Locations Assignment.png` | Policy and scope | Exercise 3, Assign the Policy |
| `Fig08 Policy Denied Deployment.png` | Denial in prohibited region | Exercise 3, Test a Disallowed Region |
| `Fig09 Allowed Region Validation.png` | Successful approved-region validation | Exercise 3, Test the Approved Region |
| `Fig10 Policy Compliance Status.png` | Assignment compliance details | Exercise 3, Review Compliance |
| `Fig11 Cleanup Verification.png` | Final removal evidence | Exercise 4, Clean Up and Verify |

Example:

```markdown
![Fig01 Resource Group Created](screenshots/Fig01%20Resource%20Group%20Created.png)

*Figure 1: The Azure portal displays the successfully created project resource group.*
```

> [!IMPORTANT]
> Do not attach a screenshot unless it visibly proves the task. Redact sensitive values before publication.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Resource group created | ✅ Passed |
| Test storage account created | ✅ Passed |
| Resource-group tags applied | ✅ Passed |
| Storage-account tags applied | ✅ Passed |
| Monthly budget created | ✅ Passed |
| 80% actual-cost alert configured | ✅ Passed |
| 100% actual-cost alert configured | ✅ Passed |
| Allowed locations policy assigned | ✅ Passed |
| Assignment scoped to resource group | ✅ Passed |
| Disallowed-region deployment denied | ✅ Passed |
| Approved-region validation passed | ✅ Passed |
| Policy compliance reviewed | ✅ Passed |
| Policy assignment removed | ✅ Passed |
| Budget removed | ✅ Passed |
| Resource group removed | ✅ Passed |
| Final cleanup verified | ✅ Passed |

---

## 📚 Command Reference

This assignment was completed through the Azure portal.

| Goal | Azure Portal Path |
|---|---|
| Create the resource group | **Resource groups** → **Create** |
| Create the storage account | **Storage accounts** → **Create** |
| Apply tags | Resource → **Tags** |
| Create the budget | **Cost Management** → **Budgets** → **Add** |
| Find the policy | **Policy** → **Definitions** → **Allowed locations** |
| Assign the policy | Policy definition → **Assign** |
| Review compliance | **Policy** → **Compliance** |
| Remove the assignment | **Policy** → **Assignments** → **Delete assignment** |
| Delete the budget | **Cost Management** → **Budgets** → Select budget → **Delete** |
| Delete the project | Resource group → **Delete resource group** |

### Repository Structure

```text
azure-cost-governance/
├── README.md
├── screenshots/
│   ├── Fig01 Resource Group Created.png
│   ├── Fig02 Storage Account Deployment.png
│   ├── Fig03 Resource Group Tags.png
│   ├── Fig04 Storage Account Tags.png
│   ├── Fig05 Budget Configuration.png
│   ├── Fig06 Budget Alert Thresholds.png
│   ├── Fig07 Allowed Locations Assignment.png
│   ├── Fig08 Policy Denied Deployment.png
│   ├── Fig09 Allowed Region Validation.png
│   ├── Fig10 Policy Compliance Status.png
│   └── Fig11 Cleanup Verification.png
└── LICENSE
```

---

## 🧰 Troubleshooting

### The budget controls are unavailable

Confirm the active subscription and cost-management scope. Verify that the signed-in identity can view and manage budgets at that scope.

### Budget alerts do not trigger immediately

Confirm the budget amount, reset period, alert conditions, and recipient. Cost data and alert evaluation are not the same as real-time resource enforcement.

### The policy assignment does not appear

Verify the active subscription, assignment scope, and policy definition. Refresh the Policy assignments view if the assignment was recently created.

### A prohibited deployment is not denied

Confirm that the deployment's resource location is outside the configured allowed list and that the assignment is scoped to the target resource group.

### An approved deployment is denied

Confirm the exact allowed-location parameter and the resource's selected location. Review the validation details for other policy assignments that may also apply.

### Compliance information is incomplete

Confirm the assignment scope and refresh the compliance view. Policy evaluation and compliance reporting may not appear immediately after assignment or deployment.

### Tags appear on the resource group but not the resource

Tags do not automatically transfer in every scenario. Apply the required tags directly or use an approved Azure Policy-based inheritance design.

### Cleanup appears incomplete

Verify the active subscription and independently check Policy assignments, Budgets, and Resource groups.

---

## 🧠 Skills Demonstrated

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
- Governance cleanup and validation
- Professional technical documentation

---

## 💡 Key Takeaways

1. **Tags improve visibility when applied consistently.** Matching metadata supports ownership, filtering, reporting, and cost attribution.
2. **Budgets provide early spending awareness.** The 80% and 100% thresholds created clear monitoring points.
3. **Budget alerts are controls for awareness, not automatic shutdown.** Operational owners still need defined response procedures.
4. **Policy scope determines impact.** Resource-group scope limited enforcement to the lab boundary.
5. **Azure Policy can provide preventive governance.** The prohibited-region test demonstrated an enforced denial.
6. **Positive and negative testing strengthen validation.** Both denied and permitted deployments were tested.
7. **Compliance review supplements deployment testing.** The dashboard provided a governance view of evaluated resources.
8. **Cleanup is part of cost governance.** Removing budgets, assignments, and resources reduced the risk of lingering charges or controls.

---

## ☑️ Completion Checklist

- [x] Created `rg-gp-cost-guardrails`
- [x] Created `stgpcostguard65711345`
- [x] Applied `environment=pilot`
- [x] Applied `owner=it-team`
- [x] Created `gp-pilot-budget`
- [x] Configured the monthly reset period
- [x] Configured the 80% alert
- [x] Configured the 100% alert
- [x] Assigned **Allowed locations**
- [x] Scoped the assignment to the resource group
- [x] Tested a prohibited region
- [x] Confirmed policy denial
- [x] Tested the approved region
- [x] Confirmed successful validation
- [x] Reviewed policy compliance
- [x] Removed the policy assignment
- [x] Removed the budget
- [x] Deleted the resource group
- [x] Confirmed final cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical Azure governance and cloud-security portfolio, demonstrating cost visibility, financial monitoring, preventive policy enforcement, compliance validation, and responsible cleanup.

---

## 🙏 Acknowledgements

This guided project was completed as part of the **Mentor Pilot Program** in a Skillable Azure environment. Mentor supported the learning experience through lab navigation, instruction comprehension, and troubleshooting.

Official reference material:

- [Use Azure Policy to enforce tagging conventions](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-policies)
- [Manage tag governance with Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/tutorials/govern-tags)
- [Azure Policy documentation](https://learn.microsoft.com/en-us/azure/governance/policy/)
- [Set spending guardrails](https://learn.microsoft.com/en-us/azure/well-architected/cost-optimization/set-spending-guardrails)

---

## ⚖️ Disclaimer

This repository documents a completed educational lab performed in a temporary Skillable Microsoft Azure environment. It is not a production-ready governance architecture and does not replace official Microsoft documentation, organizational policy, financial guidance, or professional cloud-security advice. Resource names, settings, budget values, recipients, allowed regions, and policy scope require review before reuse.

Passwords, Temporary Access Pass codes, authentication secrets, subscription identifiers, tenant information, email addresses, access tokens, and private account details are intentionally excluded. Screenshots must be reviewed and redacted before publication. Azure services, interfaces, roles, pricing, limits, and features may change over time.

---

<div align="center">

### 🎉 Lab Completed Successfully

**Azure cost governance: tagged, monitored, enforced, validated, and responsibly removed.**

Made with curiosity, care, and a commitment to secure, governed, and cost-aware cloud engineering.  

**Wadondera A. Collins**  
*ICDFA Trainee | Cohort 11 | Cloud Security Engineering*

</div>
