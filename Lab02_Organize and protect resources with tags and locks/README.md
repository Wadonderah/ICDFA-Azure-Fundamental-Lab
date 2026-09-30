<div align="center">

# 🛡️ Azure Resource Governance: Tags and Resource Locks

### Microsoft Learn Guided Project | Skillable Lab | Completed Assignment

**Prepared by:** Wadondera A. Collins  
**Program:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Completion Date:** September 30, 2026  
**Documentation Version:** 1.4

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Resource%20Governance-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Governance](https://img.shields.io/badge/Governance-Tags%20%26%20Locks-6F42C1)](#-skills-demonstrated)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Security](https://img.shields.io/badge/Focus-Cloud%20Security-CB2C30)](#-prerequisites-and-security)

*A hands-on Azure governance project demonstrating resource organization with tags, protection with management locks, enforcement testing, access restoration, validation, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Create Resources and Apply Tags](#-exercise-1-create-resources-and-apply-tags)
- [Exercise 2: Apply Resource Locks](#-exercise-2-apply-resource-locks)
- [Exercise 3: Test Lock Enforcement](#-exercise-3-test-lock-enforcement)
- [Exercise 4: Remove Locks and Clean Up](#-exercise-4-remove-locks-and-clean-up)
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

This repository documents the successful completion of the **Azure Resource Governance: Tags and Resource Locks** guided project. The practical work was completed in a temporary **Skillable Cloud Slice** environment using an Azure subscription provided for the lab session.

The project demonstrated how to organize and protect Azure resources through the following workflow:

1. Create an Azure resource group.
2. Provision two Standard Azure Storage accounts with LRS redundancy.
3. Apply department and environment tags.
4. Find resources with tag-based filters.
5. Apply a `Delete` lock to a storage account.
6. Apply a `Read-only` lock to the resource group.
7. Test blocked modification and deletion operations.
8. Remove both locks.
9. Confirm that normal write access was restored.
10. Remove the temporary validation tag.
11. Delete the resource group and verify cleanup.

> [!NOTE]
> Mentor was available as an optional AI-powered assistant for lab navigation, instruction comprehension, and troubleshooting.

---

## 🎯 Learning Objectives

By completing this project, I demonstrated the ability to:

- Create and manage Azure resource groups and storage accounts.
- Apply key-value metadata at resource-group and resource scope.
- Use consistent tags to classify development and operations resources.
- Filter Azure resources by tag name and value.
- Configure `Delete` and `Read-only` management locks.
- Explain the scope and inherited effect of resource-group locks.
- Validate that locks prevent accidental or unauthorized control-plane changes.
- Remove locks safely through an approved administrative workflow.
- Confirm that write access is restored after lock removal.
- Remove temporary resources to reduce the risk of unintended charges.
- Document governance work without exposing credentials or sensitive information.

---

## 🏗️ Architecture and Resources

```text
Temporary Azure Lab Subscription
└── Resource Group: rg-gp-tags-locks
    ├── Tags
    │   ├── department = development
    │   └── environment = test
    ├── Management Lock: read-only-rg
    │   └── Type: Read-only
    ├── Storage Account: stgptagslock65463711
    │   ├── Performance: Standard
    │   ├── Redundancy: LRS
    │   ├── department = development
    │   ├── environment = test
    │   └── Management Lock: prevent-delete
    │       └── Type: Delete
    └── Storage Account: stgptagsops65463711
        ├── Performance: Standard
        ├── Redundancy: LRS
        ├── department = operations
        └── environment = test
```

| Resource | Name | Governance Configuration | Purpose |
|---|---|---|---|
| Resource group | `rg-gp-tags-locks` | Development and test tags; Read-only lock during testing | Logical container and parent governance scope |
| Storage account 1 | `stgptagslock65463711` | Development and test tags; Delete lock | Protected development storage resource |
| Storage account 2 | `stgptagsops65463711` | Operations and test tags | Operations-classified storage resource |
| Resource-group lock | `read-only-rg` | `Read-only` | Restricted modifications and deletion across the group |
| Resource lock | `prevent-delete` | `Delete` | Prevented deletion of the first storage account |

> [!NOTE]
> **Final state:** Both locks were removed and the resource group was deleted after validation. The architecture represents the deployed lab environment before cleanup.

> [!IMPORTANT]
> A lock applied at a parent scope is inherited by resources below that scope. When multiple locks apply, the most restrictive applicable lock takes precedence.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the assigned Skillable lab environment
- An active temporary Azure lab subscription
- Permission to create and delete resource groups and storage accounts
- Permission to apply tags and management locks
- Access to the Microsoft Azure portal
- Basic familiarity with Azure resources and governance concepts

### Tools and Environment

| Tool or Service | Version or Edition | Purpose |
|---|---|---|
| Microsoft Azure portal | Web service; build not specified | Created and managed Azure resources |
| Azure Resource Manager | Service-managed; API version not specified | Managed resource groups, tags, and locks |
| Azure Storage | Standard performance with LRS | Provided two storage resources for governance testing |
| Skillable Cloud Slice | Version not specified | Hosted the temporary lab environment |
| Mentor | Pilot version; build not specified | Optional lab navigation and troubleshooting support |
| SEA-Dev virtual machine | Operating system version not specified | Provided access to the guided lab environment |

> [!NOTE]
> Product version numbers are not estimated when the lab instructions do not provide them. Azure portal and Azure Resource Manager are continuously updated cloud services.

### Security Notice

Authentication details, passwords, temporary access passes, subscription identifiers, tenant information, access keys, and connection strings are intentionally **not included** in this README.

> [!CAUTION]
> Never store credentials, secrets, personal information, or sensitive business data in Azure tags or public repository files. Tags are organizational metadata, not a secure data store.

Resource locks strengthen governance but do not replace Azure RBAC, Azure Policy, monitoring, change management, or least-privilege access.

---

## 🏷️ Exercise 1: Create Resources and Apply Tags

### 1. Create the Resource Group

1. Sign in to the Microsoft Azure portal through the authorized Skillable lab environment.
2. Search for **Resource groups**.
3. Select **Create**.
4. Enter the resource-group name:

```text
rg-gp-tags-locks
```

5. Choose the assigned subscription and an approved region.
6. Select **Review + create**, then select **Create**.

**Validation:** `rg-gp-tags-locks` appeared in the Azure portal.

### 2. Create the First Storage Account

Create the first storage account with the following configuration:

| Setting | Value |
|---|---|
| Resource group | `rg-gp-tags-locks` |
| Storage account name | `stgptagslock65463711` |
| Performance | Standard |
| Redundancy | Locally Redundant Storage (LRS) |

**Validation:** `stgptagslock65463711` deployed successfully in the assigned region.

### 3. Create the Second Storage Account

Create the second storage account with the following configuration:

| Setting | Value |
|---|---|
| Resource group | `rg-gp-tags-locks` |
| Storage account name | `stgptagsops65463711` |
| Performance | Standard |
| Redundancy | Locally Redundant Storage (LRS) |

**Validation:** `stgptagsops65463711` deployed successfully in the same region.

### 4. Apply Organizational Tags

Apply the following key-value tags:

| Azure Resource | `department` | `environment` |
|---|---|---|
| `rg-gp-tags-locks` | `development` | `test` |
| `stgptagslock65463711` | `development` | `test` |
| `stgptagsops65463711` | `operations` | `test` |

**Validation:** Each resource displayed the intended department and environment values.

### 5. Filter Resources by Tag

Use the Azure portal's tag view or resource filters to test the following pairs:

```text
department = development
department = operations
```

**Validation:** The development filter displayed `stgptagslock65463711`, while the operations filter displayed `stgptagsops65463711`.

> [!TIP]
> A production tagging standard can include approved metadata such as `owner`, `cost-center`, `application`, and `data-classification`, subject to organizational policy.

---

## 🔒 Exercise 2: Apply Resource Locks

### 1. Apply a Delete Lock to the First Storage Account

1. Open `stgptagslock65463711` in the Azure portal.
2. Open the **Locks** pane.
3. Add a lock using the following settings:

| Setting | Value |
|---|---|
| Lock name | `prevent-delete` |
| Lock type | `Delete` |
| Scope | `stgptagslock65463711` |

**Validation:** The `prevent-delete` lock appeared at the storage-account scope.

### 2. Apply a Read-only Lock to the Resource Group

1. Open `rg-gp-tags-locks`.
2. Open the **Locks** pane.
3. Add a lock using the following settings:

| Setting | Value |
|---|---|
| Lock name | `read-only-rg` |
| Lock type | `Read-only` |
| Scope | `rg-gp-tags-locks` |

**Validation:** The `read-only-rg` lock appeared at resource-group scope and applied to resources beneath that scope.

> [!IMPORTANT]
> A `Delete` lock permits authorized reads and modifications but blocks deletion. A `Read-only` lock permits reads while blocking updates and deletion through Azure Resource Manager control-plane operations.

---

## 🧪 Exercise 3: Test Lock Enforcement

### 1. Test the Read-only Lock

Attempt to add or change a tag while `read-only-rg` is active.

**Expected behavior:** The modification is rejected because the resource group is protected by a Read-only lock.

**Validation:** The attempted tag modification failed while the Read-only lock was active.

### 2. Test the Delete Lock

Attempt to delete `stgptagslock65463711` while the applicable locks are active.

**Expected behavior:** Azure blocks the deletion because the resource is protected by management locks.

**Validation:** The protected storage account could not be deleted.

### 3. Review Lock Scope and Inheritance

Review the resource-group Locks pane and the applicable lock information for the storage accounts.

**Validation:** Both locks appeared with their intended names, types, and scopes.

> [!WARNING]
> Lock testing should use temporary lab resources. Do not test destructive operations against production resources without authorization and an approved change plan.

---

## 🧹 Exercise 4: Remove Locks and Clean Up

### 1. Remove the Resource-group Lock

Delete the following lock from the resource-group Locks pane:

```text
read-only-rg
```

**Validation:** The Read-only lock no longer appeared at resource-group scope.

### 2. Remove the Storage-account Lock

Delete the following lock:

```text
prevent-delete
```

**Validation:** No management lock remained on the protected storage account.

### 3. Confirm Write Access Is Restored

Add the following temporary validation tag:

```text
lock-test = passed
```

**Validation:** The temporary tag was saved successfully, confirming that write access had been restored.

Remove the temporary validation tag after testing.

**Validation:** The test tag was removed and the intended organizational tags remained.

### 4. Delete the Resource Group

1. Confirm that no locks remain.
2. Open `rg-gp-tags-locks`.
3. Select **Delete resource group**.
4. Enter the resource-group name when prompted.
5. Confirm deletion.
6. Verify that the resource group and both storage accounts no longer appear in the Azure portal.

**Validation:** The resource group and all contained lab resources were deleted successfully.

> [!WARNING]
> Resource-group deletion is permanent. Always verify the selected resource group and confirm that required locks have been removed before beginning cleanup.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Resource group created | ✅ Passed |
| First storage account created with Standard performance and LRS | ✅ Passed |
| Second storage account created with Standard performance and LRS | ✅ Passed |
| Development and test tags applied to the resource group | ✅ Passed |
| Development and test tags applied to the first storage account | ✅ Passed |
| Operations and test tags applied to the second storage account | ✅ Passed |
| Development tag filter returned the correct resource | ✅ Passed |
| Operations tag filter returned the correct resource | ✅ Passed |
| `prevent-delete` lock applied | ✅ Passed |
| `read-only-rg` lock applied | ✅ Passed |
| Read-only lock blocked tag modification | ✅ Passed |
| Management locks blocked storage-account deletion | ✅ Passed |
| Resource-group lock removed | ✅ Passed |
| Storage-account lock removed | ✅ Passed |
| No locks remained after removal | ✅ Passed |
| `lock-test = passed` confirmed restored write access | ✅ Passed |
| Temporary validation tag removed | ✅ Passed |
| Resource group deleted | ✅ Passed |
| Both storage accounts removed | ✅ Passed |
| Final cleanup verified | ✅ Passed |

---

## 📚 Command Reference

This guided project was completed through the Azure portal. The following table provides a concise portal-navigation reference.

| Goal | Azure Portal Path |
|---|---|
| Create a resource group | **Resource groups** → **Create** |
| Create a storage account | **Storage accounts** → **Create** |
| Add or edit tags | Resource or resource group → **Tags** |
| Find resources by tag | Azure portal → **Tags** or resource-list filters |
| View management locks | Resource or resource group → **Locks** |
| Add a lock | **Locks** → **Add** |
| Remove a lock | **Locks** → Select lock → **Delete** |
| Delete the project environment | Resource group → **Delete resource group** |

### Governance Configuration Reference

```text
Resource group tags:
  department = development
  environment = test

Storage account 1 tags:
  department = development
  environment = test

Storage account 2 tags:
  department = operations
  environment = test

Locks:
  prevent-delete = Delete
  read-only-rg = Read-only
```

---

## 🧰 Troubleshooting

### A tag change is blocked

Check for a `Read-only` lock at the resource, resource-group, or subscription scope. A lock inherited from a parent scope can prevent the requested update.

### A resource cannot be deleted

Review applicable locks at the resource and parent scopes. Remove only the intended lock and only when authorized.

### The resource group cannot be deleted

A lock on a child resource can prevent deletion of the entire resource group. Review the Locks pane and remove approved lab locks before retrying cleanup.

### A tag filter returns no resources

Confirm that:

- The tag key is spelled correctly.
- The tag value matches the assigned value.
- The expected resource has the tag applied directly.
- Capitalization and spacing are consistent with the saved value.

### The lock does not appear where expected

Review the lock at the scope where it was created. A resource-group lock may be inherited by child resources even though it was created at the parent scope.

### Normal write access is not restored

Confirm that all applicable locks have been removed, including locks inherited from parent scopes. Refresh the portal and retry the approved validation change.

### Cleanup still fails after removing a lock

Review the resource group and each child resource for additional locks. Confirm that the correct lab subscription and resource group are selected.

---

## 🧠 Skills Demonstrated

- Microsoft Azure resource provisioning
- Azure Resource Manager governance
- Resource-group lifecycle management
- Azure Storage account deployment
- Key-value resource tagging
- Department and environment classification
- Tag-based resource discovery and filtering
- Azure management-lock configuration
- Delete-lock enforcement validation
- Read-only lock enforcement validation
- Lock scope and inheritance awareness
- Administrative change validation
- Least-privilege and change-management awareness
- Secure handling of cloud information
- Cost-aware resource cleanup

---

## 💡 Key Takeaways

1. **Tags provide operational context.** Consistent key-value metadata improves resource discovery, reporting, governance, and cost-management workflows.
2. **Tagging standards matter.** Approved names and values reduce inconsistent classification and make automation more reliable.
3. **Delete and Read-only locks serve different purposes.** Delete locks block removal, while Read-only locks also block updates.
4. **Scope affects enforcement.** Locks applied at a parent scope are inherited by resources below that scope.
5. **The most restrictive applicable lock takes precedence.** Administrators must review all relevant scopes before troubleshooting blocked operations.
6. **Locks complement access control.** They strengthen protection against accidental changes but do not replace Azure RBAC, Azure Policy, monitoring, or change management.
7. **Validation proves governance controls work.** Testing blocked and restored operations confirms the intended behavior.
8. **Cleanup requires lock awareness.** Approved locks must be removed before temporary lab resources can be deleted successfully.
9. **Tags must not contain secrets.** Governance metadata should never expose credentials, personal data, or sensitive business information.

### Recommended Production Improvements

- Define and maintain an organization-wide naming and tagging standard.
- Approve mandatory tags such as `owner`, `cost-center`, `application`, and `data-classification` where appropriate.
- Use Azure Policy to audit, require, inherit, or remediate mandatory tags.
- Apply locks according to resource criticality and approved change-management procedures.
- Restrict permission to create or remove locks to authorized roles.
- Use Bicep or Terraform for repeatable and reviewable deployments.
- Monitor Azure Activity Log events for important governance changes.
- Review inherited locks before automated deployments and cleanup operations.

---

## ☑️ Completion Checklist

- [x] Accessed the authorized Skillable Azure environment
- [x] Created `rg-gp-tags-locks`
- [x] Created `stgptagslock65463711`
- [x] Created `stgptagsops65463711`
- [x] Configured Standard performance and LRS redundancy
- [x] Applied department and environment tags to the resource group
- [x] Applied development and test tags to the first storage account
- [x] Applied operations and test tags to the second storage account
- [x] Filtered resources by department tag
- [x] Applied the `prevent-delete` Delete lock
- [x] Applied the `read-only-rg` Read-only lock
- [x] Confirmed that the Read-only lock blocked modification
- [x] Confirmed that management locks blocked deletion
- [x] Removed `read-only-rg`
- [x] Removed `prevent-delete`
- [x] Confirmed that no locks remained
- [x] Added `lock-test = passed` to verify restored access
- [x] Removed the temporary validation tag
- [x] Deleted the resource group
- [x] Confirmed removal of both storage accounts
- [x] Verified final cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical cloud-security and Azure-administration portfolio, demonstrating resource governance, metadata management, protective controls, enforcement validation, secure administration, and responsible cleanup.

---

## 🙏 Acknowledgements

This guided project was completed through **Microsoft Learn** and the **Skillable** lab environment. Mentor was available as an optional assistant for lab navigation and troubleshooting.

Official reference material:

- [Guided project: Organize and protect resources with tags and locks](https://learn.microsoft.com/en-us/training/modules/guided-project-organize-resources-tags-locks/)
- [Use tags to organize Azure resources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)
- [Lock Azure resources to protect infrastructure](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources)
- [Define an Azure tagging strategy](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-tagging)
- [Use Azure Policy for tag compliance](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-policies)

---

## ⚖️ Disclaimer

This repository is an educational record of a completed guided project performed in a temporary Microsoft Azure lab environment provided through Skillable. It is not a production-ready architecture and does not replace official Microsoft documentation, organizational governance policies, security standards, or professional cloud architecture guidance.

Resource names and configurations are included as evidence of practical learning. Credentials, access keys, connection strings, subscription identifiers, temporary access information, and other sensitive values are intentionally excluded. Azure services, interfaces, pricing, limits, and behavior may change over time. Validate all procedures against current Microsoft documentation and applicable organizational requirements before reuse in another environment.

---

<div align="center">

### 🎉 Project Completed Successfully

**Azure governance controls: configured, tested, validated, restored, and responsibly cleaned up.**

Made with curiosity, care, and a commitment to responsible cloud engineering.  

**Wadondera A. Collins**  
*ICDFA Trainee | Cohort 11 | Cloud Security Engineering*

</div>
