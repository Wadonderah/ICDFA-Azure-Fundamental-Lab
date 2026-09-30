# Azure CLI Lab Professional Documentation Report

## Mentor Pilot Program | Completed Assignment

**Report Type:** Detailed Technical Documentation Report  
**Author:** Wadondera A. Collins  
**Role:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Completion Date:** September 30, 2026  
**Primary Platform:** Microsoft Azure  
**Primary Interface:** Azure Cloud Shell with Bash  
**Project Status:** Completed with documented validation and cleanup

---

## Document Control

| Field | Details |
|---|---|
| Document title | Azure CLI Lab Professional Documentation Report |
| Suggested filename | `Documentation_Report.md` |
| Document purpose | Detailed evidence-based record of the completed Azure CLI lab |
| Intended audience | Instructors, assessors, recruiters, cloud-security professionals, and portfolio reviewers |
| Classification | Educational and portfolio documentation |
| Final environment state | Temporary lab resources deleted after validation |

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Executive Summary](#2-executive-summary)
3. [Objectives](#3-objectives)
4. [Professional Value](#4-professional-value)
5. [Skills Demonstrated](#5-skills-demonstrated)
6. [Technologies and Tools Used](#6-technologies-and-tools-used)
7. [Lab Environment](#7-lab-environment)
8. [Repository Structure](#8-repository-structure)
9. [Architecture and Resource Design](#9-architecture-and-resource-design)
10. [Methodology](#10-methodology)
11. [Implementation and Evidence Analysis](#11-implementation-and-evidence-analysis)
12. [Validation Summary](#12-validation-summary)
13. [Issues Encountered and Resolutions](#13-issues-encountered-and-resolutions)
14. [Security, Governance, and Cost Considerations](#14-security-governance-and-cost-considerations)
15. [Results and Outcomes](#15-results-and-outcomes)
16. [Limitations and Next Steps](#16-limitations-and-next-steps)
17. [Conclusion](#17-conclusion)
18. [Screenshot Renaming Register](#18-screenshot-renaming-register)
19. [References](#19-references)
20. [Disclaimer](#20-disclaimer)

---

## 1. Project Overview

This report documents the completion of an Azure CLI practical lab conducted through the Mentor Pilot Program. The assignment focused on administering Microsoft Azure resources from Azure Cloud Shell rather than relying exclusively on the graphical portal. The lab covered environment discovery, subscription verification, command discovery, Azure region selection, resource provisioning, resource inspection, tag-based governance, JMESPath querying, cross-validation in the Azure portal, troubleshooting, and resource cleanup.

The deployed environment consisted of one Azure resource group and two Azure Storage accounts in the `eastus` region. The resource group provided the management boundary for the lab resources. The storage accounts were used to demonstrate repeatable resource creation, inventory filtering, individual resource inspection, and tag-based classification.

The project was completed as a controlled educational exercise. Temporary resources were removed after the validation activities to support responsible cloud use and minimize the risk of unintended consumption.

---

## 2. Executive Summary

The Azure CLI lab provided practical experience with the complete lifecycle of Azure resources through command-line administration. Azure Cloud Shell was opened in Bash mode, the assigned Azure subscription was confirmed, and the built-in command help system was used to investigate Azure CLI command groups and required parameters. Available Azure regions were reviewed before `eastus` was selected as the deployment location.

A resource group named `rg-gp-cli-demo` was created successfully. Two Azure Storage accounts, `stgpclidemo0165722027` and `stgpclidemo0265722027`, were provisioned with the `Standard_LRS` SKU. The resources were then listed, filtered by resource type, and inspected individually. Governance metadata was applied to the resource group, and the portal was used to verify the resulting tag values.

The lab also demonstrated JMESPath-supported inventory analysis. A resource-count query returned `2`, confirming that the resource group contained the two intended storage accounts at that stage. During the tagging activity, shortened storage-account names were used in two commands, which produced `ResourceNotFound` and missing `--ids` errors. Those screenshots are retained in this report as troubleshooting evidence rather than being presented as successful validation. The correct full storage-account names are documented in the remediation procedure.

The final technical outcome was successful creation, inspection, governance validation, and cleanup of the temporary Azure environment. The evidence set demonstrates both successful implementation and the ability to interpret command-line failures accurately.

---

## 3. Objectives

The objectives of the assignment were to:

1. Open and operate Azure Cloud Shell in Bash mode.
2. Confirm the active Azure account and subscription before deployment.
3. Use the Azure CLI help system to discover command groups, subcommands, arguments, and examples.
4. Review supported Azure locations and select a suitable deployment region.
5. Create an Azure resource group as a logical management boundary.
6. Provision two Azure Storage accounts with a defined redundancy SKU.
7. List all resources in the target resource group.
8. Filter the resource inventory by Azure resource type.
9. Inspect the properties of an individual storage account.
10. Apply governance tags to the resource group and storage resources.
11. Use JMESPath expressions to project fields, filter results, and count resources.
12. Compare Azure CLI output with the Azure portal.
13. Identify and resolve errors caused by incorrect resource names.
14. Delete the temporary resource group and verify cleanup.
15. Document the work with evidence that is accurately matched to each task.

---

## 4. Professional Value

This project demonstrates professional value in several areas relevant to cloud administration and cloud security engineering.

### 4.1 Repeatable administration

Command-line operations provide a repeatable and reviewable record of administrative activity. The commands documented in this report can be adapted into scripts, runbooks, and automation pipelines after appropriate parameterization and security review.

### 4.2 Evidence-based validation

Each major task is associated with visible command output or Azure portal evidence. This approach supports technical accountability because the report distinguishes between successful results, partial evidence, and unsuccessful commands.

### 4.3 Governance awareness

The use of tags demonstrates an understanding of metadata-based organization. Tags can support ownership tracking, environment classification, operational grouping, reporting, and cost-management processes when naming conventions are consistently governed.

### 4.4 Troubleshooting discipline

The report does not hide failed commands. The `ResourceNotFound` results are analyzed as evidence of a naming mismatch. This demonstrates the ability to interpret errors, locate the cause, and define a precise corrective action.

### 4.5 Secure documentation

Tenant identifiers, passwords, access tokens, Temporary Access Pass values, keys, and connection strings are excluded from the documentation. This protects lab credentials and keeps the report appropriate for portfolio use.

### 4.6 Cost-conscious cloud practice

The resource group was deleted after validation. Treating cleanup as part of the deployment lifecycle demonstrates responsible use of temporary cloud resources.

---

## 5. Skills Demonstrated

- Azure Cloud Shell navigation in Bash mode
- Azure CLI command discovery and contextual help
- Azure subscription and account verification
- Azure region discovery
- Resource-group lifecycle management
- Azure Storage account provisioning
- Resource inventory listing and filtering
- Individual resource inspection
- Tagging and governance fundamentals
- JMESPath projection, filtering, and counting
- JSON and table-output interpretation
- Azure portal and CLI cross-validation
- Troubleshooting `ResourceNotFound` errors
- Secure handling of lab credentials and identifiers
- Cost-aware cleanup of temporary resources
- Technical evidence analysis and professional reporting

---

## 6. Technologies and Tools Used

| Technology or tool | Use in the lab |
|---|---|
| Microsoft Azure | Cloud platform hosting the assigned lab subscription and resources |
| Azure portal | Graphical interface used to open Cloud Shell and verify resource metadata |
| Azure Cloud Shell | Browser-based command environment used for administrative tasks |
| Bash | Shell selected for command execution |
| Azure CLI | Primary command-line interface used to create, inspect, tag, query, and delete resources |
| Azure Resource Manager | Management layer used for resource groups, storage accounts, tags, and resource identifiers |
| Azure Storage | Service used to provision the two lab storage accounts |
| JMESPath | Query language used through the Azure CLI `--query` parameter |
| Markdown | Format used to create the professional report and evidence register |
| GitHub-compatible repository structure | Recommended structure for storing documentation and screenshot evidence |

> **Version note:** The screenshots do not display the installed Azure CLI version. The report therefore does not claim a specific version. Run `az version` when version evidence is required.

---

## 7. Lab Environment

| Environment component | Recorded configuration |
|---|---|
| Training context | Mentor Pilot Program |
| User role | ICDFA Trainee, Cohort 11, Cloud Security Engineering |
| Access interface | Microsoft Azure portal |
| Command environment | Azure Cloud Shell |
| Shell | Bash |
| Subscription | Assigned lab subscription; identifier intentionally omitted |
| Deployment region | `eastus` |
| Resource group | `rg-gp-cli-demo` |
| Storage account 1 | `stgpclidemo0165722027` |
| Storage account 2 | `stgpclidemo0265722027` |
| Storage SKU | `Standard_LRS` |
| Resource-group tags | `environment=test`, `department=it-ops` |
| Intended storage tags | First account: `environment=test`, `department=development`; second account: `environment=test`, `department=operations` |
| Final state | Temporary lab resource group deleted after validation |

### 7.1 Scope boundary

The assignment focused on management-plane operations. The evidence does not show data-plane activities such as container creation, blob upload, access-key use, shared access signatures, network-rule configuration, or private endpoints.

### 7.2 Sensitive information handling

The screenshots may display tenant or subscription identifiers within terminal output. Before publishing the images in a public repository, redact tenant IDs, subscription IDs, account identifiers, and any other lab-specific values that are not required to prove the task.

---

## 8. Repository Structure

The detailed report should remain separate from the concise project README. A suitable repository structure is:

```text
azure-cli-lab/
├── README.md
├── Documentation_Report.md
├── images/
│   └── evidence/
│       ├── Fig01 Azure CLI Help Overview.png
│       ├── Fig02 Azure Group Command Help.png
│       ├── Fig03 Azure Group Create Help.png
│       ├── Fig04 Azure Subscription Verification.png
│       ├── Fig05 Available Azure Regions.png
│       ├── Fig06 Resource Group Creation and Validation.png
│       ├── Fig07 First Storage Account Provisioning.png
│       ├── Fig08 Second Storage Account Provisioning.png
│       ├── Fig09 Resource Inventory and Storage Inspection.png
│       ├── Fig10 Resource Group Tagging CLI Validation.png
│       ├── Fig11 Resource Group Tags Portal Validation.png
│       ├── Fig12 Resource Count JMESPath Query.png
│       ├── Fig13 First Storage Tagging Error.png
│       ├── Fig14 Second Storage Tagging Error.png
│       ├── Fig15 Resource Group Deletion and Verification.png
│       └── Fig16 Portal Cleanup Verification.png
└── commands/
    └── azure-cli-commands.sh
```

### 8.1 Document separation

- `README.md` should provide a concise repository introduction, key outcomes, and navigation.
- `Documentation_Report.md` should contain the detailed project narrative, methodology, commands, evidence, analysis, troubleshooting, validation, limitations, and conclusions.
- `images/evidence/` should contain only evidence images with filenames that exactly match the report references.
- `commands/azure-cli-commands.sh` may contain sanitized, reusable commands without tenant-specific values.

---

## 9. Architecture and Resource Design

```text
Assigned Azure Subscription
└── Resource Group: rg-gp-cli-demo
    ├── Storage Account: stgpclidemo0165722027
    │   ├── Region: eastus
    │   ├── SKU: Standard_LRS
    │   └── Intended tags:
    │       ├── environment=test
    │       └── department=development
    └── Storage Account: stgpclidemo0265722027
        ├── Region: eastus
        ├── SKU: Standard_LRS
        └── Intended tags:
            ├── environment=test
            └── department=operations
```

The resource group was used as the lifecycle boundary for the lab. Deleting the resource group removed the temporary storage accounts and associated management-plane objects contained within it.

---

## 10. Methodology

The lab was completed using a staged implementation and validation method.

### Phase 1: Environment discovery

1. Open Azure Cloud Shell in Bash mode.
2. Inspect the Azure CLI top-level help output.
3. Inspect the `az group` command group.
4. Inspect the `az group create` command syntax and required arguments.
5. Verify the active Azure account and assigned subscription.
6. Review available Azure regions.

### Phase 2: Resource provisioning

1. Create `rg-gp-cli-demo` in `eastus`.
2. Confirm the resource group with `az group show`.
3. Create the first storage account with `Standard_LRS`.
4. Create the second storage account with `Standard_LRS`.
5. Confirm the successful provisioning state through CLI output.

### Phase 3: Inventory and inspection

1. List all resources in the resource group.
2. Filter resources to `Microsoft.Storage/storageAccounts`.
3. Inspect the first storage account in table format.
4. Confirm names, region, resource type, and provisioning status.

### Phase 4: Governance and query operations

1. Apply `environment=test` and `department=it-ops` to the resource group.
2. Query the resource-group tags from the CLI.
3. Validate the same tags in the Azure portal.
4. Apply distinct department tags to the two storage accounts using their full names.
5. Use JMESPath to display selected fields, filter by department, and count resources.

### Phase 5: Troubleshooting

1. Review command output after storage-account tagging failed.
2. Identify that `stgpclidemo01` and `stgpclidemo02` did not match the full deployed names.
3. Replace the shortened names with `stgpclidemo0165722027` and `stgpclidemo0265722027`.
4. Retrieve the resource ID successfully before invoking the tag operation.
5. Re-run the validation query after correcting the names.

### Phase 6: Cleanup

1. Delete the resource group with `--yes --no-wait`.
2. Query the resource group after deletion.
3. Use `az group exists --name rg-gp-cli-demo` for a clear Boolean cleanup check when required.
4. Review the portal resource-group list to confirm the target lab resource group is no longer present.

---

## 11. Implementation and Evidence Analysis

### 11.1 Azure CLI command discovery

The first activity used the Azure CLI help system to understand the available command groups and navigation method.

```bash
az --help
```

<img width="1086" height="560" alt="Fig01_Azure_CLI_Help_Overview" src="https://github.com/user-attachments/assets/0ac4aef5-f451-4071-8331-a9de8ce94acc" />


**Figure 1 analysis:** The screenshot shows Azure Cloud Shell running Bash and the output of `az --help`. The command output lists Azure CLI command groups and confirms that the environment can execute Azure CLI commands. This evidence supports command discovery, not resource creation.

The resource-group command family was then inspected.

```bash
az group --help
```

<img width="1092" height="563" alt="Fig02_Azure_Group_Command_Help" src="https://github.com/user-attachments/assets/48b7c4ad-d736-4c6c-9a99-b653797c2f0b" />


**Figure 2 analysis:** The screenshot displays the `az group` description, the `lock` subgroup, and commands such as `create`, `delete`, `exists`, `export`, `list`, `show`, `update`, and `wait`. This evidence confirms that the lab used contextual CLI help to identify resource-group operations.

The syntax for resource-group creation was reviewed next.

```bash
az group create --help
```

<img width="1086" height="561" alt="Fig03_Azure_Group_Create_Help" src="https://github.com/user-attachments/assets/d977c511-4b3c-4337-8d64-10c7acbdabc1" />


**Figure 3 analysis:** The screenshot identifies `--location` and `--name` as required arguments and displays global arguments such as `--output`, `--query`, and `--subscription`. This provides direct evidence that the required deployment parameters were reviewed before creating the resource group.

### 11.2 Subscription verification

```bash
az account show --output table
az account list --output table
```

<img width="1090" height="559" alt="Fig04_Azure_Subscription_Verification" src="https://github.com/user-attachments/assets/169bc34e-fdf5-485b-b053-22be84561561" />


**Figure 4 analysis:** The screenshot shows account and subscription information in table format. The assigned subscription is enabled and marked as the default. Identifiers visible in the original screenshot should be redacted before public publication.

### 11.3 Region discovery

```bash
az account list-locations --output table
```

<img width="1085" height="555" alt="Fig05_Available_Azure_Regions" src="https://github.com/user-attachments/assets/e8ade0a7-a222-45e7-9d8c-f47a3b55601c" />


**Figure 5 analysis:** The screenshot presents Azure locations in a table with display names, programmatic names, and regional display names. `eastus` appears in the output and was selected for the lab deployment.

### 11.4 Resource-group creation and validation

```bash
az group create \
  --name rg-gp-cli-demo \
  --location eastus

az group show \
  --name rg-gp-cli-demo \
  --output table
```

<img width="1089" height="288" alt="Fig06_Resource_Group_Creation_and_Validation" src="https://github.com/user-attachments/assets/309639fa-e960-4819-8b66-31b4c1852e2a" />


**Figure 6 analysis:** The JSON output shows the resource group named `rg-gp-cli-demo`, the `eastus` location, and a `Succeeded` provisioning state. The subsequent table output confirms the same resource-group name and location. This is the primary creation evidence for the management boundary.

### 11.5 First storage-account provisioning

```bash
az storage account create \
  --name stgpclidemo0165722027 \
  --resource-group rg-gp-cli-demo \
  --location eastus \
  --sku Standard_LRS
```

<img width="1086" height="561" alt="Fig07_First_Storage_Account_Provisioning" src="https://github.com/user-attachments/assets/f5027657-dbe3-41af-93ab-c0c7faadf910" />


**Figure 7 analysis:** The screenshot shows the creation command for `stgpclidemo0165722027` and the returned storage-account properties. A message indicates that an account with the supplied name was found and would be updated, so the evidence supports successful command execution against an existing or just-created account rather than proving that the name had never existed before. The visible properties include `eastus` placement and HTTPS-only traffic enabled.

### 11.6 Second storage-account provisioning

```bash
az storage account create \
  --name stgpclidemo0265722027 \
  --resource-group rg-gp-cli-demo \
  --location eastus \
  --sku Standard_LRS
```

<img width="1081" height="561" alt="Fig08_Second_Storage_Account_Provisioning" src="https://github.com/user-attachments/assets/d4f84f0d-92c2-42c0-afc8-5dd7a228064c" />


**Figure 8 analysis:** The screenshot displays the creation command and returned JSON properties for `stgpclidemo0265722027`. The output includes the expected storage-account name, creation metadata, and HTTPS-only traffic setting.

### 11.7 Resource inventory, filtering, and inspection

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --output table

az resource list \
  --resource-group rg-gp-cli-demo \
  --resource-type Microsoft.Storage/storageAccounts \
  --output table

az storage account show \
  --name stgpclidemo0165722027 \
  --resource-group rg-gp-cli-demo \
  --output table
```

<img width="1084" height="565" alt="Fig09_Resource_Inventory_and_Storage_Inspection" src="https://github.com/user-attachments/assets/f2a7515a-8921-4e05-9146-bf89de718367" />


**Figure 9 analysis:** The first table lists two storage accounts in `rg-gp-cli-demo`, both in `eastus`, with type `Microsoft.Storage/storageAccounts` and status `Succeeded`. The filtered command returns the same two storage resources. The final command inspects `stgpclidemo0165722027` and shows properties including `StorageV2`, `eastus`, and a successful provisioning state. This is the strongest consolidated evidence of the intended two-resource deployment.

### 11.8 Resource-group tagging through the CLI

```bash
az group update \
  --name rg-gp-cli-demo \
  --tags environment=test department=it-ops

az group show \
  --name rg-gp-cli-demo \
  --query tags
```

<img width="1087" height="555" alt="Fig10_Resource_Group_Tagging_CLI_Validation" src="https://github.com/user-attachments/assets/35e8ec6c-24ad-4346-ad47-f140f4c9c7ef" />


**Figure 10 analysis:** The `az group update` output shows a successful provisioning state and the tags `department: it-ops` and `environment: test`. The subsequent `az group show --query tags` output returns the same two values. This confirms resource-group tag application through the CLI.

### 11.9 Resource-group tagging through the portal

<img width="1087" height="556" alt="Fig11_Resource_Group_Tags_Portal_Validation" src="https://github.com/user-attachments/assets/bf956754-ec72-4336-aeb5-d8b6ee866e9b" />


**Figure 11 analysis:** The Azure portal Tags blade for `rg-gp-cli-demo` displays `department` with value `it-ops` and `environment` with value `test`. This provides graphical cross-validation of the CLI result shown in Figure 10.

### 11.10 JMESPath resource count

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "length([])"
```

> **Correction:** The reusable command should use `length(@)` rather than `length([])`.

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "length(@)"
```

<img width="1088" height="567" alt="Fig12_Resource_Count_JMESPath_Query" src="https://github.com/user-attachments/assets/e637d700-9002-4b3f-a9e0-9fe190201c8e" />


**Figure 12 analysis:** The screenshot shows the resource-list query and output `2`. The result is consistent with the two storage accounts displayed in Figure 9. The report preserves the visible evidence while documenting `length(@)` as the preferred expression for the reusable command.

### 11.11 First storage-account tagging error

The screenshot records an unsuccessful command that used the shortened name `stgpclidemo01`.

<img width="1086" height="292" alt="Fig13_First_Storage_Tagging_Error" src="https://github.com/user-attachments/assets/9f1bcd38-176d-42bf-8d2b-bdd0d7a601fc" />


**Figure 13 analysis:** Azure returned `ResourceNotFound` because `Microsoft.Storage/storageAccounts/stgpclidemo01` was not found in `rg-gp-cli-demo`. The nested resource-ID command therefore returned no ID, and `az resource tag` reported that `--ids` expected at least one argument. This image must be classified as troubleshooting evidence, not successful tagging evidence.

**Corrected command:**

```bash
RESOURCE_ID=$(az storage account show \
  --name stgpclidemo0165722027 \
  --resource-group rg-gp-cli-demo \
  --query id \
  --output tsv)

az tag update \
  --resource-id "$RESOURCE_ID" \
  --operation Merge \
  --tags environment=test department=development
```

### 11.12 Second storage-account tagging error

The screenshot records the same naming problem for the second storage account.

<img width="1091" height="566" alt="Fig14_Second_Storage_Tagging_Error" src="https://github.com/user-attachments/assets/db8d5627-e130-4f8f-a60f-f235efae2362" />


**Figure 14 analysis:** Azure returned `ResourceNotFound` for the shortened name `stgpclidemo02`. Because the resource lookup failed, no value was supplied to `--ids`. The correct command must use `stgpclidemo0265722027`.

**Corrected command:**

```bash
RESOURCE_ID=$(az storage account show \
  --name stgpclidemo0265722027 \
  --resource-group rg-gp-cli-demo \
  --query id \
  --output tsv)

az tag update \
  --resource-id "$RESOURCE_ID" \
  --operation Merge \
  --tags environment=test department=operations
```

### 11.13 Storage-tag validation commands

The supplied screenshot set does not contain successful output for the corrected storage-account tag commands. The following commands should be used to capture that missing validation if the lab environment is recreated:

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "[].{Name:name,Department:tags.department,Environment:tags.environment}" \
  --output table
```

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "[?tags.department=='development'].{Name:name,Type:type}" \
  --output table
```

A new screenshot should only be added after the output visibly confirms the intended values.

### 11.14 Resource-group deletion and CLI verification

```bash
az group delete \
  --name rg-gp-cli-demo \
  --yes \
  --no-wait

az group show \
  --name rg-gp-cli-demo \
  --output table
```

<img width="1083" height="556" alt="Fig15_Resource_Group_Deletion_and_Verification" src="https://github.com/user-attachments/assets/c5e0c5b9-e308-44a6-9597-e67df81fb6b6" />


**Figure 15 analysis:** The screenshot shows the delete command followed by a `group show` query. A table row is still visible, which means the screenshot was captured before asynchronous deletion had fully completed. The image proves that deletion was initiated, but it does not independently prove completed deletion. A definitive CLI check is:

```bash
az group exists --name rg-gp-cli-demo
```

A result of `false` confirms completed deletion.

### 11.15 Portal cleanup verification

<img width="1092" height="557" alt="Fig16_Portal_Cleanup_Verification" src="https://github.com/user-attachments/assets/a2f68dea-1c48-447b-bef5-665051e25d64" />


**Figure 16 analysis:** The Azure portal resource-group list no longer shows `rg-gp-cli-demo`; only another resource group is visible. This supports the final cleanup conclusion. This image is appropriately placed after the deletion command and should not be used as evidence for resource creation.

---

## 12. Validation Summary

| Validation area | Evidence | Assessment |
|---|---|---|
| Azure CLI available in Bash | Figure 1 | Passed |
| Resource-group command discovery | Figures 2 and 3 | Passed |
| Subscription verified | Figure 4 | Passed |
| Region discovery completed | Figure 5 | Passed |
| Resource group created | Figure 6 | Passed |
| First storage account command executed | Figure 7 | Passed with evidence note |
| Second storage account created | Figure 8 | Passed |
| Two storage accounts listed | Figure 9 | Passed |
| Storage resources filtered by type | Figure 9 | Passed |
| Individual storage account inspected | Figure 9 | Passed |
| Resource-group tags applied | Figure 10 | Passed |
| Resource-group tags verified in portal | Figure 11 | Passed |
| Resource count returned two | Figure 12 | Passed |
| First storage-account tag command | Figure 13 | Failed because of shortened name |
| Second storage-account tag command | Figure 14 | Failed because of shortened name |
| Corrected storage-account tag output | Not present in supplied screenshots | Evidence gap |
| Resource-group deletion initiated | Figure 15 | Passed |
| CLI proof of completed deletion | Figure 15 captured too early | Partial evidence |
| Portal cleanup verification | Figure 16 | Passed |

### Validation conclusion

The evidence strongly supports completion of environment discovery, resource provisioning, resource inventory, resource-group tagging, JMESPath counting, and portal cleanup verification. The screenshots do not prove successful storage-account tagging after correction. That distinction is retained to preserve the accuracy and credibility of the report.

---

## 13. Issues Encountered and Resolutions

### 13.1 Shortened storage-account names

**Observed issue:**

```text
ResourceNotFound
argument --ids: expected at least one argument
```

**Cause:** The tagging commands supplied `stgpclidemo01` and `stgpclidemo02`, while the deployed resources were named `stgpclidemo0165722027` and `stgpclidemo0265722027`.

**Resolution:** Use the full deployed resource name, retrieve the resource ID, confirm that the returned variable is not empty, and then apply tags.

```bash
RESOURCE_ID=$(az storage account show \
  --name stgpclidemo0165722027 \
  --resource-group rg-gp-cli-demo \
  --query id \
  --output tsv)

printf '%s\n' "$RESOURCE_ID"
```

The tag command should only run after a valid resource ID is returned.

### 13.2 Asynchronous deletion

**Observed issue:** `az group delete --no-wait` returned control before deletion had completed, so an immediate `az group show` could still return the resource group.

**Resolution:** Use a Boolean existence check until the result becomes `false`.

```bash
az group exists --name rg-gp-cli-demo
```

### 13.3 Evidence completeness

**Observed issue:** No supplied screenshot shows successful storage-account tags after the corrected names were used.

**Resolution:** Do not present the failed screenshots as completion evidence. If the environment is recreated, capture a new screenshot showing the full resource names and the final tags in table output.

---

## 14. Security, Governance, and Cost Considerations

### 14.1 Credential protection

The report excludes passwords, Temporary Access Pass values, access keys, connection strings, and authentication tokens. Credentials should only be obtained from the authorized lab interface and should never be committed to source control.

### 14.2 Identifier redaction

Before public publication, redact subscription IDs, tenant IDs, user principal names, and other lab-specific identifiers visible in terminal output. Resource names may remain when they are non-sensitive and intentionally used as portfolio evidence.

### 14.3 Tag governance

The resource group used `environment=test` and `department=it-ops`. The intended storage tags separated development and operations classifications. In a production environment, tag keys and allowed values should follow an approved organizational convention.

### 14.4 Storage security observations

The screenshots show HTTPS-only traffic enabled for the storage accounts. The screenshots do not prove configuration of public network restrictions, minimum TLS policy beyond the visible output, identity-based data access, private endpoints, or diagnostic settings. Those controls remain outside the demonstrated scope.

### 14.5 Cost management

Deleting the temporary resource group after the exercise reduced the risk of leaving chargeable resources active. Cleanup was treated as an implementation phase rather than an optional afterthought.

---

## 15. Results and Outcomes

The lab produced the following outcomes:

- Azure Cloud Shell was used successfully in Bash mode.
- The Azure CLI help system was used to discover commands and parameters.
- The active subscription was verified before deployment.
- Azure locations were reviewed and `eastus` was selected.
- `rg-gp-cli-demo` was created successfully.
- Two `Standard_LRS` storage accounts were present in the resource group.
- Resource inventory and resource-type filtering returned the expected storage accounts.
- An individual storage account was inspected successfully.
- Resource-group tags were applied and verified through both CLI and portal views.
- A JMESPath resource count returned `2`.
- Storage-account tagging failures were correctly identified as resource-name mismatches.
- Resource-group deletion was initiated, and portal evidence supports final removal of the target group.
- The final report retains an evidence gap for corrected storage-account tag validation rather than overstating completion.

---

## 16. Limitations and Next Steps

### 16.1 Limitations

1. The installed Azure CLI version is not shown in the evidence.
2. Successful storage-account tag output is not included in the supplied screenshots.
3. Figure 15 was captured before asynchronous deletion fully completed.
4. The evidence does not demonstrate storage data-plane operations.
5. The evidence does not demonstrate advanced storage security controls.
6. The screenshots may require redaction before public publication.

### 16.2 Recommended next steps

1. Capture `az version` output for tool-version evidence.
2. Re-run the corrected storage tagging commands with the full names.
3. Capture the JMESPath projection showing each storage account and its final tags.
4. Capture `az group exists --name rg-gp-cli-demo` returning `false` during a future run.
5. Convert repeated commands into a parameterized Bash script.
6. Add input validation that stops the script when a resource ID is empty.
7. Extend the lab with Azure Policy, resource locks, diagnostic settings, and least-privilege RBAC in a separate controlled exercise.
8. Keep `README.md` concise and link to this report for detailed evidence.

---

## 17. Conclusion

The Azure CLI lab demonstrated practical competence in command-line cloud administration. The assignment progressed from command discovery and subscription verification to resource provisioning, inventory inspection, governance tagging, JMESPath querying, troubleshooting, and cleanup.

The strongest evidence confirms creation of the resource group, presence of two storage accounts, successful inventory filtering, individual storage inspection, resource-group tag validation, and a two-resource JMESPath count. The report also documents the storage-account tagging errors accurately and provides corrected commands without misrepresenting the failed screenshots as successful results.

Overall, the project provides a useful portfolio example of Azure administration, governance awareness, troubleshooting discipline, secure documentation, and responsible resource lifecycle management.

---

## 18. Screenshot Renaming Register

Rename each supplied screenshot exactly as shown below before placing the images in `images/evidence/`.

| Original filename | Required new filename | Correct report placement |
|---|---|---|
| `Screenshot 2026-09-30 193913.png` | `Fig01 Azure CLI Help Overview.png` | Section 11.1, top-level Azure CLI help |
| `Screenshot 2026-09-30 194016.png` | `Fig02 Azure Group Command Help.png` | Section 11.1, `az group --help` |
| `Screenshot 2026-09-30 194123.png` | `Fig03 Azure Group Create Help.png` | Section 11.1, `az group create --help` |
| `Screenshot 2026-09-30 195947.png` | `Fig04 Azure Subscription Verification.png` | Section 11.2, account and subscription verification |
| `Screenshot 2026-09-30 194715.png` | `Fig05 Available Azure Regions.png` | Section 11.3, location discovery |
| `Screenshot 2026-09-30 194837.png` | `Fig06 Resource Group Creation and Validation.png` | Section 11.4, resource-group creation |
| `Screenshot 2026-09-30 195336.png` | `Fig07 First Storage Account Provisioning.png` | Section 11.5, first storage account |
| `Screenshot 2026-09-30 195556.png` | `Fig08 Second Storage Account Provisioning.png` | Section 11.6, second storage account |
| `Screenshot 2026-09-30 200211.png` | `Fig09 Resource Inventory and Storage Inspection.png` | Section 11.7, listing, filtering, and inspection |
| `Screenshot 2026-09-30 194209.png` | `Fig10 Resource Group Tagging CLI Validation.png` | Section 11.8, CLI tag validation |
| `Screenshot 2026-09-30 195134.png` | `Fig11 Resource Group Tags Portal Validation.png` | Section 11.9, portal tag validation |
| `Screenshot 2026-09-30 194445.png` | `Fig12 Resource Count JMESPath Query.png` | Section 11.10, count query |
| `Screenshot 2026-09-30 200440.png` | `Fig13 First Storage Tagging Error.png` | Section 11.11, first tagging failure |
| `Screenshot 2026-09-30 200541.png` | `Fig14 Second Storage Tagging Error.png` | Section 11.12, second tagging failure |
| `Screenshot 2026-09-30 195730.png` | `Fig15 Resource Group Deletion and Verification.png` | Section 11.14, deletion initiated and early verification |
| `Screenshot 2026-09-30 195457.png` | `Fig16 Portal Cleanup Verification.png` | Section 11.15, portal cleanup confirmation |

> The sequence is based on the technical workflow rather than screenshot capture time. The two error screenshots are intentionally placed under troubleshooting-related implementation sections.

---

## 19. References

- Microsoft Learn, Azure CLI command reference: `https://learn.microsoft.com/cli/azure/`
- Microsoft Learn, Azure resource command reference: `https://learn.microsoft.com/cli/azure/resource`
- Microsoft Learn, Azure tag command reference: `https://learn.microsoft.com/cli/azure/tag`
- Microsoft Learn, Apply tags with Azure CLI: `https://learn.microsoft.com/azure/azure-resource-manager/management/tag-resources-cli`
- Microsoft Learn, Azure CLI JMESPath query guidance: `https://learn.microsoft.com/cli/azure/query-azure-cli`

---

## 20. Disclaimer

This document is an educational and portfolio record of a guided Microsoft Azure lab. The commands and configurations reflect the documented assignment environment and may require modification before use in another subscription. Tenant-specific credentials, authentication values, passwords, access tokens, subscription identifiers, and other secrets are intentionally excluded.

Azure services, portal interfaces, Azure CLI behavior, and recommended practices may change. Commands should be checked against current Microsoft Learn documentation before reuse. The screenshots should be reviewed and redacted before publication if they expose lab-specific identifiers.

---

**Author:** Wadondera A. Collins  
**Program:** ICDFA Trainee | Cohort 11  
**Professional Focus:** Cloud Security Engineering  
**Project:** Azure CLI Lab  
**Status:** Completed and documented
