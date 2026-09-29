# Azure Resource Governance: Tags and Resource Locks

> **Status:** Completed  
> **Project Type:** Microsoft Learn Guided Project / Skillable Lab  
> **Role Focus:** Cloud Security Engineering and Azure Administration  
> **Documentation Version:** 1.4  
> **Author:** Wadondera A. Collins

## Project Overview

This completed guided project demonstrates how to organize and protect Microsoft Azure resources using resource tags and management locks. The practical work covered resource creation, tag-based organization, lock enforcement testing, restoration of normal access, and final resource cleanup.

The lab was completed in a temporary Skillable Cloud Slice environment with an Azure subscription provided for the session.

## Objectives

- Create an Azure resource group and two storage accounts.
- Apply organizational tags at resource-group and resource level.
- Filter resources by tag values.
- Configure `Delete` and `Read-only` management locks.
- Validate that the locks blocked unauthorized or accidental operations.
- Remove the locks and confirm that normal write access was restored.
- Delete the lab resources to prevent unintended charges.

## Tools, Services, and Environment

| Tool or Service | Purpose | Version / Edition |
|---|---|---|
| Microsoft Azure Portal | Created and managed the Azure resources | Web service; portal build not specified in the lab |
| Azure Resource Manager | Managed resource groups, tags, and resource locks | Service-managed; API version not specified in the lab |
| Azure Storage | Provisioned two standard storage accounts | Standard performance, Locally Redundant Storage (LRS); API version not specified |
| Azure Blob Storage / Azure Data Lake Storage | Preferred storage type offered during deployment | Service version not specified in the lab |
| Skillable Cloud Slice | Hosted the temporary lab environment and Azure subscription | Version not specified |
| Mentor | Optional AI-powered lab navigation and troubleshooting assistant | Pilot version; build number not specified |
| SEA-Dev virtual machine | Provided access to the guided lab environment | Operating system version not specified |

> Product version numbers are not invented where the lab instructions did not provide them. Azure Portal and Azure Resource Manager are continuously updated cloud services.

## Lab Environment

- **Resource group:** `rg-gp-tags-locks`
- **Storage account 1:** `stgptagslock65463711`
- **Storage account 2:** `stgptagsops65463711`
- **Performance tier:** Standard
- **Redundancy:** Locally Redundant Storage (LRS)
- **Subscription:** Temporary Azure lab subscription

## Key Governance Lessons

- Tags provide searchable key-value metadata for organizing Azure resources and supporting operational or cost-management requirements.
- Consistent tag names and values improve filtering, reporting, and governance.
- A Delete lock permits reads and modifications while preventing deletion.
- A Read-only lock prevents modifications and deletion at the applicable scope.
- Parent-scope locks are inherited by resources below that scope, and the most restrictive applicable lock takes precedence.
- Management locks protect control-plane operations and complement Azure RBAC, policy, monitoring, and change management.

## Recommended Production Improvements

The following recommendations extend beyond the guided lab and would strengthen a production implementation:

- Define and document an organization-wide resource naming and tagging standard.
- Add approved governance tags such as `owner`, `cost-center`, `application`, and `data-classification` where required.
- Use Azure Policy to audit, require, inherit, or remediate mandatory tags.
- Apply locks according to resource criticality and an approved change-management process.
- Restrict permission to create or remove locks to authorized roles.
- Use Bicep or Terraform to make deployments repeatable and reviewable.
- Configure Azure Activity Log monitoring and alerts for important governance changes.
- Review inherited locks before automated deployments or cleanup operations.
- Never place credentials, secrets, personal data, or other sensitive values in tags or repository files.

## Completed Assignments

### Assignment 1: Create Resources and Apply Tags

**Assignment documentation version:** 1.0

Created the `rg-gp-tags-locks` resource group and deployed two storage accounts in the same region. Organizational tags were then applied as follows:

| Azure resource | `department` tag | `environment` tag |
|---|---|---|
| `rg-gp-tags-locks` | `development` | `test` |
| `stgptagslock65463711` | `development` | `test` |
| `stgptagsops65463711` | `operations` | `test` |

Tag filters were tested using the `department` key. Filtering by `development` displayed the development storage account, while filtering by `operations` displayed the operations storage account.

**Result:** Resources were successfully created, categorized, and located through tag-based filtering.

### Assignment 2: Apply Resource Locks

**Assignment documentation version:** 1.0

Configured two Azure management locks:

- Applied a `Delete` lock named `prevent-delete` to the first storage account.
- Applied a `Read-only` lock named `read-only-rg` to the resource group.

The lock configuration demonstrated protection at different scopes. The storage-account lock protected the selected resource from deletion, while the resource-group lock restricted modifications across the group.

**Result:** Both locks appeared in the resource group Locks pane with their appropriate scopes.

### Assignment 3: Test Lock Enforcement

**Assignment documentation version:** 1.0

Validated the configured governance controls by attempting operations that should be blocked:

1. Attempted to add a tag while the resource group had a `Read-only` lock.
2. Confirmed that the modification failed because the resource was locked.
3. Attempted to delete the protected storage account.
4. Confirmed that deletion was blocked by the management lock.
5. Removed both locks from the resource group Locks pane.
6. Added the temporary tag `lock-test: passed` to verify that write permissions had been restored.
7. Removed the temporary validation tag after testing.

**Result:** The locks enforced the expected restrictions, and removing them restored normal resource-management operations.

### Assignment 4: Resource Cleanup

**Assignment documentation version:** 1.0

Confirmed that no locks remained before deleting `rg-gp-tags-locks`. Deleting the resource group also removed its two storage accounts and associated tags. The Azure Portal was checked afterward to confirm that the lab resources no longer appeared.

**Result:** Lab resources were removed to avoid unintended Azure charges.

## Validation Checklist

### Resource Creation and Tagging

- [x] Created the `rg-gp-tags-locks` resource group.
- [x] Created `stgptagslock65463711` using Standard performance and LRS redundancy.
- [x] Created `stgptagsops65463711` using Standard performance and LRS redundancy.
- [x] Applied `department: development` and `environment: test` to the resource group.
- [x] Applied `department: development` and `environment: test` to the first storage account.
- [x] Applied `department: operations` and `environment: test` to the second storage account.
- [x] Confirmed that filtering by `department: development` displayed the correct storage account.
- [x] Confirmed that filtering by `department: operations` displayed the correct storage account.

### Resource Lock Configuration

- [x] Applied the `prevent-delete` Delete lock to the first storage account.
- [x] Applied the `read-only-rg` Read-only lock to the resource group.
- [x] Confirmed that both locks appeared with the correct scopes in the Locks pane.

### Lock Enforcement Testing

- [x] Confirmed that the Read-only lock blocked a tag modification.
- [x] Confirmed that the Delete lock blocked storage-account deletion.
- [x] Removed the `read-only-rg` lock.
- [x] Removed the `prevent-delete` lock.
- [x] Confirmed that no locks remained on the resource group or storage accounts.
- [x] Added `lock-test: passed` to confirm that write access was restored.
- [x] Removed the temporary `lock-test` tag after validation.

### Cleanup

- [x] Deleted the `rg-gp-tags-locks` resource group.
- [x] Confirmed that both storage accounts were removed.
- [x] Confirmed that the resource group no longer appeared in the Azure Portal.

## Skills Demonstrated

- Azure resource provisioning and lifecycle management
- Cloud resource organization using key-value tags
- Department and environment classification
- Tag-based resource discovery and filtering
- Azure management lock configuration
- Delete and read-only control validation
- Lock scope and inheritance awareness
- Operational validation and cloud cost hygiene
- Azure resource cleanup

## Project Outcome

The project was completed successfully. It demonstrated a full Azure governance workflow: provisioning resources, applying consistent metadata, protecting resources against accidental changes or deletion, testing enforcement, removing controls when appropriate, restoring access, and cleaning up the environment.

## Security Notes

- Resource tags should contain only appropriate organizational metadata.
- Resource locks support governance but do not replace role-based access control, monitoring, or security policies.

## Disclaimer

This repository documents a completed training exercise performed in a temporary Microsoft Azure lab environment provided through Skillable. Resource names and configurations are included only as evidence of practical learning. No confidential lab access information is included. Azure interfaces and service behavior may change over time, and the steps in this README should be validated against current Microsoft documentation before use in a production environment.

## References

- [Guided project: Organize and protect resources with tags and locks](https://learn.microsoft.com/en-us/training/modules/guided-project-organize-resources-tags-locks/)
- [Use tags to organize Azure resources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)
- [Lock Azure resources to protect infrastructure](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources)
- [Define an Azure tagging strategy](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-tagging)
- [Use Azure Policy for tag compliance](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-policies)

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
