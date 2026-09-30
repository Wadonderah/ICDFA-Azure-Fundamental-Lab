<div align="center">

# ☁️ Azure CLI Lab: Complete Guide

### Mentor Pilot Program | Completed Assignment

**Completion Date:** September 30, 2026

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-CLI-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#completion-checklist)
[![Learning](https://img.shields.io/badge/Focus-Cloud%20Administration-6F42C1)](#skills-demonstrated)

*A hands-on journey through Azure Cloud Shell, resource provisioning, tagging, JMESPath queries, validation, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Explore Azure Cloud Shell](#-exercise-1-explore-azure-cloud-shell)
- [Exercise 2: Create and Inspect Resources](#-exercise-2-create-and-inspect-resources)
- [Exercise 3: Tag, Query, and Clean Up](#-exercise-3-tag-query-and-clean-up)
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

This repository documents the successful completion of the **Azure CLI Lab** in the **Mentor Pilot Program**. The lab introduced practical Azure administration through **Azure Cloud Shell** and the **Azure CLI**, progressing from environment discovery to complete resource lifecycle management.

The project covered the following workflow:

1. Launch Azure Cloud Shell in Bash mode.
2. Verify the active Azure account and subscription.
3. Explore built-in Azure CLI help.
4. Identify an available deployment region.
5. Create a resource group.
6. Provision two Azure Storage accounts.
7. List, filter, and inspect resources.
8. Apply governance tags.
9. Query resource data with JMESPath.
10. Compare CLI results with the Azure portal.
11. Delete the lab resources and verify cleanup.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

By completing this lab, I demonstrated the ability to:

- Navigate Azure Cloud Shell in Bash mode.
- Verify and switch Azure subscriptions from the command line.
- Discover Azure CLI commands with the built-in help system.
- Deploy Azure resources using repeatable CLI commands.
- Format command output as tables, JSON, TSV, YAML, and colorized JSON.
- Filter Azure inventories by resource type.
- Apply tags for organization, governance, and cost-management scenarios.
- Use JMESPath to select, reshape, filter, and count JSON results.
- Validate that the Azure portal and CLI expose the same underlying resources.
- Remove temporary resources to prevent unintended consumption and charges.

---

## 🏗️ Architecture and Resources

```text
Azure Subscription
└── Resource Group: rg-gp-cli-demo
    ├── Storage Account: stgpclidemo0165722027
    │   ├── SKU: Standard_LRS
    │   └── Tags: environment=test, department=development
    └── Storage Account: stgpclidemo0265722027
        ├── SKU: Standard_LRS
        └── Tags: environment=test, department=operations
```

| Resource | Name | Region | Purpose |
|---|---|---|---|
| Resource group | `rg-gp-cli-demo` | `eastus` | Logical container for lab resources |
| Storage account | `stgpclidemo0165722027` | `eastus` | First managed storage resource |
| Storage account | `stgpclidemo0265722027` | `eastus` | Second managed storage resource |

> [!NOTE]
> **Final state:** All temporary resources shown above were deleted after validation. The diagram represents the deployed lab environment before cleanup.

> [!IMPORTANT]
> Azure Storage account names must be globally unique, contain only lowercase letters and numbers, and use 3 to 24 characters. Replace the sample names if they are unavailable in another subscription.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An Azure subscription with permission to create and delete resources
- Azure Cloud Shell configured in **Bash** mode
- A selected target region, such as `eastus`

### Security Notice

Authentication values, temporary access passes, passwords, tenant-specific usernames, and subscription identifiers are intentionally **not included** in this README.

> [!CAUTION]
> Never commit passwords, Temporary Access Pass tokens, access keys, connection strings, or other secrets to GitHub. If a credential has been exposed, rotate or revoke it immediately using the appropriate identity-management process.

The lab credentials should be retrieved only from the authorized lab interface and used only for the assigned environment.

---

## 🧭 Exercise 1: Explore Azure Cloud Shell

### 1. Launch Cloud Shell

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Select the **Cloud Shell** icon in the portal toolbar.
3. Choose **Bash** when prompted.
4. Complete the storage-mount setup if Cloud Shell is being opened for the first time.
5. Confirm that a Bash prompt appears.

**Validation:** Cloud Shell opened successfully in Bash mode.

### 2. Verify the Account and Subscription

```bash
az account show --output table
```

If multiple subscriptions are available, list them before selecting the intended subscription:

```bash
az account list --output table
```

To switch subscriptions when necessary:

```bash
az account set --subscription "<subscription-name-or-id>"
```

**Validation:** The active subscription name and ID matched the assigned lab subscription.

### 3. Explore the CLI Help System

```bash
az --help
az group --help
az group create --help
```

These commands revealed top-level groups, resource-group operations, and required parameters such as `--name` and `--location`.

**Validation:** The CLI help system was used to discover commands, subcommands, and parameters.

### 4. List Available Azure Regions

```bash
az account list-locations --output table
```

The selected deployment location for this lab was:

```text
eastus
```

**Validation:** A supported target region was identified before resource deployment.

---

## 🛠️ Exercise 2: Create and Inspect Resources

### 1. Create the Resource Group

```bash
az group create \
  --name rg-gp-cli-demo \
  --location eastus
```

Verify the result:

```bash
az group show \
  --name rg-gp-cli-demo \
  --output table
```

**Validation:** `rg-gp-cli-demo` was created and returned a successful provisioning state.

### 2. Create the First Storage Account

```bash
az storage account create \
  --name stgpclidemo0165722027 \
  --resource-group rg-gp-cli-demo \
  --location eastus \
  --sku Standard_LRS
```

**Validation:** The first storage account completed provisioning successfully.

### 3. Create the Second Storage Account

```bash
az storage account create \
  --name stgpclidemo0265722027 \
  --resource-group rg-gp-cli-demo \
  --location eastus \
  --sku Standard_LRS
```

**Validation:** The second storage account completed provisioning successfully.

### 4. List All Resources

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --output table
```

### 5. Filter by Resource Type

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --resource-type Microsoft.Storage/storageAccounts \
  --output table
```

**Validation:** The resource-type filter isolated the two storage accounts.

### 6. Inspect a Specific Storage Account

```bash
az storage account show \
  --name stgpclidemo0165722027 \
  --resource-group rg-gp-cli-demo \
  --output table
```

**Validation:** The CLI returned the selected account's name, location, kind, and SKU details.

### Output Formats Explored

```bash
--output table
--output json
--output jsonc
--output tsv
--output yaml
```

---

## 🏷️ Exercise 3: Tag, Query, and Clean Up

### 1. Tag the Resource Group

```bash
az group update \
  --name rg-gp-cli-demo \
  --tags environment=test department=it-ops
```

Verify the tags:

```bash
az group show \
  --name rg-gp-cli-demo \
  --query tags
```

**Validation:** The resource group displayed the `environment` and `department` tags.

### 2. Tag the First Storage Account

> [!NOTE]
> **Lab-instruction alignment:** The supplied guide used `department=operations` in both storage-account tagging commands, but its later JMESPath exercise expected one resource tagged `department=development`. This README uses `development` for the first account and `operations` for the second so the commands and validation outcome are consistent.

```bash
az resource tag \
  --tags environment=test department=development \
  --ids "$(az storage account show \
    --name stgpclidemo0165722027 \
    --resource-group rg-gp-cli-demo \
    --query id \
    --output tsv)"
```

### 3. Tag the Second Storage Account

```bash
az resource tag \
  --tags environment=test department=operations \
  --ids "$(az storage account show \
    --name stgpclidemo0265722027 \
    --resource-group rg-gp-cli-demo \
    --query id \
    --output tsv)"
```

**Validation:** Both storage accounts received an environment tag and distinct department values.

> [!TIP]
> The lab command `az resource tag` is preserved because it reflects the completed exercise. For automation where existing tags must be retained, a current alternative is `az tag update --operation Merge --resource-id <resource-id> --tags key=value`.

### 4. Display Names and Tags with JMESPath

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "[].{Name:name, Department:tags.department, Environment:tags.environment}" \
  --output table
```

### 5. Filter by Department

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "[?tags.department=='development'].{Name:name, Type:type}" \
  --output table
```

**Validation:** The filter returned only the resource tagged with `department=development`.

### 6. Count Resources

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "length(@)"
```

**Expected result:** `2`

### 7. Compare CLI Results with the Portal

The resource group, storage accounts, locations, and tags were reviewed in the Azure portal and compared with the CLI output.

**Validation:** The portal and CLI displayed matching resource metadata.

### 8. Delete the Resource Group

```bash
az group delete \
  --name rg-gp-cli-demo \
  --yes \
  --no-wait
```

Check whether the resource group still exists:

```bash
az group show \
  --name rg-gp-cli-demo \
  --output table
```

A `ResourceGroupNotFound` or equivalent not-found response confirms that deletion has completed.

> [!WARNING]
> Deleting a resource group permanently removes the resources inside it. Always verify the target name before running a delete command.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Cloud Shell opened in Bash mode | ✅ Passed |
| Correct subscription verified | ✅ Passed |
| CLI help system explored | ✅ Passed |
| Deployment region identified | ✅ Passed |
| Resource group created | ✅ Passed |
| First storage account created | ✅ Passed |
| Second storage account created | ✅ Passed |
| Resource listing and filtering completed | ✅ Passed |
| Resource group tags applied | ✅ Passed |
| Storage account tags applied | ✅ Passed |
| JMESPath projection completed | ✅ Passed |
| JMESPath filtering completed | ✅ Passed |
| Resource count confirmed | ✅ Passed |
| Portal and CLI compared | ✅ Passed |
| Resource group deleted | ✅ Passed |
| Final cleanup verified | ✅ Passed |

---

## 📚 Command Reference

| Goal | Command |
|---|---|
| Show the active subscription | `az account show --output table` |
| List subscriptions | `az account list --output table` |
| List regions | `az account list-locations --output table` |
| Create a resource group | `az group create --name <name> --location <region>` |
| Show a resource group | `az group show --name <name> --output table` |
| Create a storage account | `az storage account create --name <name> --resource-group <group> --location <region> --sku Standard_LRS` |
| List resources | `az resource list --resource-group <group> --output table` |
| Apply resource-group tags | `az group update --name <group> --tags key=value` |
| Delete a resource group | `az group delete --name <group> --yes --no-wait` |

---

## 🧰 Troubleshooting

### Storage account name is unavailable

Storage account names are globally unique. Change the numeric suffix and retry.

```bash
az storage account check-name \
  --name <proposed-storage-account-name>
```

### Wrong subscription is active

```bash
az account list --output table
az account set --subscription "<subscription-name-or-id>"
az account show --output table
```

### Resource deployment fails

Request the resource details in JSON to inspect the returned state and error information:

```bash
az group show \
  --name rg-gp-cli-demo \
  --output jsonc
```

### Deletion is still in progress

Because `--no-wait` returns control immediately, query the resource group again after the deletion operation has progressed:

```bash
az group exists --name rg-gp-cli-demo
```

A result of `false` confirms that the resource group no longer exists.

### JMESPath output is empty

Confirm that tags are present and that spelling and capitalization match the filter:

```bash
az resource list \
  --resource-group rg-gp-cli-demo \
  --query "[].{Name:name, Tags:tags}" \
  --output table
```

---

## 🧠 Skills Demonstrated

- Microsoft Azure fundamentals
- Azure Cloud Shell navigation
- Azure CLI command discovery
- Bash multiline command construction
- Resource-group lifecycle management
- Azure Storage account provisioning
- Resource inventory and filtering
- Tagging and governance fundamentals
- JMESPath projections and filters
- Portal-to-CLI validation
- Secure handling of credentials
- Cost-aware resource cleanup

---

## 💡 Key Takeaways

1. **The CLI improves repeatability.** Commands can be reviewed, reused, documented, and adapted for automation.
2. **Validation prevents cascading errors.** Confirming each resource before continuing makes troubleshooting easier.
3. **Tags create useful context.** Consistent metadata supports organization, governance, reporting, and cost analysis.
4. **JMESPath turns raw JSON into answers.** Queries can extract exactly the fields needed without external tools.
5. **Cleanup is part of deployment.** Responsible cloud administration includes verifying that temporary resources are removed.
6. **Secrets do not belong in source control.** Documentation should explain authentication without exposing credentials.

---

## ☑️ Completion Checklist

- [x] Signed in to the authorized lab environment
- [x] Opened Azure Cloud Shell in Bash mode
- [x] Verified the active account and subscription
- [x] Explored Azure CLI help
- [x] Listed and selected an Azure region
- [x] Created `rg-gp-cli-demo`
- [x] Created two storage accounts
- [x] Listed and filtered Azure resources
- [x] Applied resource-group and resource-level tags
- [x] Queried resources with JMESPath
- [x] Compared CLI results with the Azure portal
- [x] Deleted the resource group
- [x] Confirmed cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical cloud-security and Azure-administration portfolio, demonstrating command-line resource management, validation, governance, and secure cleanup practices.

---

## 🙏 Acknowledgements

This guided project was completed as part of the **Mentor Pilot Program**. Mentor supported the learning experience by helping with lab navigation, instruction comprehension, and troubleshooting.

---

## ⚖️ Disclaimer

This repository is an educational record of a completed guided lab. Resource names, commands, and configurations are documented for learning and portfolio purposes. Tenant-specific credentials, passwords, access tokens, subscription identifiers, and other secrets are intentionally excluded. Azure interfaces and CLI behavior may change over time, so commands should be checked against current Microsoft documentation before reuse in another environment.

---

<div align="center">

### 🎉 Lab Completed Successfully

**Azure CLI skills: practiced, validated, and ready for the next challenge.**

Made with curiosity, care, and a commitment to responsible cloud engineering.

</div>
