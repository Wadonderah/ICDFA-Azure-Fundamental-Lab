<div align="center">

## Azure Resource Governance: Tags and Resource Locks

**Microsoft Learn Guided Project / Skillable Lab**

**Prepared by:** Wadondera A. Collins  
**Programme:** ICDFA Cloud Security Engineering, Cohort 11  
**Role Focus:** Cloud Security Engineering and Azure Administration  
**Project Status:** Completed  
**Report Version:** 1.1

</div>

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Executive Summary](#executive-summary)
3. [Project Objectives](#project-objectives)
4. [Professional Value](#professional-value)
5. [Skills Demonstrated](#skills-demonstrated)
6. [Technologies and Tools Used](#technologies-and-tools-used)
7. [Lab Environment](#lab-environment)
8. [Repository Structure](#repository-structure)
9. [Methodology](#methodology)
10. [Evidence and Analysis](#evidence-and-analysis)
11. [Results](#results)
12. [Validation Checklist](#validation-checklist)
13. [Limitations and Next Steps](#limitations-and-next-steps)
14. [Security and Privacy Notes](#security-and-privacy-notes)
15. [Conclusion](#conclusion)
16. [Disclaimer](#disclaimer)
17. [Author](#author)

---

## Project Overview

This professional project report documents the implementation and validation of Azure resource governance controls using resource tags and management locks. The completed work covered resource creation, metadata-based organization, tag filtering, lock configuration, enforcement testing, restoration of normal access, and resource cleanup.

The project was completed in a temporary Skillable Cloud Slice environment using a provided Microsoft Azure subscription. A dedicated resource group and two Azure Storage accounts were used to demonstrate how governance controls improve resource visibility and reduce the risk of accidental modification or deletion.

## Executive Summary

The project established a controlled Azure environment containing the `rg-gp-tags-locks` resource group and two Standard StorageV2 accounts. The resources were categorized using `department` and `environment` tags. The first storage account represented a development workload, while the second represented an operations workload. Tag-based filtering was then used to locate resources by department.

Two management-lock scenarios were configured and tested. A Delete lock named `prevent-delete` protected the first storage account from deletion. A Read-only lock named `read-only-rg` prevented modification at the applicable scope. Enforcement was validated through failed tag-modification and deletion attempts. After both locks were removed, the temporary tag `lock-test: passed` confirmed that write access had been restored.

The completed project demonstrates practical capability in Azure resource provisioning, governance, validation, troubleshooting, documentation, and responsible cloud cleanup.

## Project Objectives

- Create a dedicated Azure resource group.
- Deploy two Standard Azure Storage accounts using LRS redundancy.
- Apply consistent organizational tags to the resource group and storage accounts.
- Use tag filters to distinguish development and operations resources.
- Configure Delete and Read-only management locks.
- Validate that the locks block the intended operations.
- Remove the locks through a controlled process.
- Confirm that normal write access is restored after lock removal.
- Remove temporary resources to avoid unintended charges.
- Produce clear evidence suitable for a professional GitHub portfolio.

## Professional Value

This project demonstrates job-relevant skills for cloud security, Azure administration, DevOps, and governance-focused roles. The work shows the ability to:

- Translate governance requirements into Azure configurations.
- Apply metadata standards that support resource discovery and cost-management processes.
- Protect cloud resources from accidental deletion and modification.
- Validate controls through expected-failure testing instead of relying only on configuration status.
- Restore access through authorized lock removal.
- Document technical decisions and outcomes with visual evidence.
- Perform responsible cleanup in a temporary cloud environment.

## Skills Demonstrated

- Azure resource provisioning and lifecycle management
- Resource-group administration
- Azure Storage account deployment
- Organizational tagging with key-value metadata
- Tag-based resource filtering
- Azure management-lock configuration
- Delete-lock testing and validation
- Read-only-lock testing and validation
- Lock scope and inheritance awareness
- Expected-failure testing
- Write-access restoration verification
- Technical evidence collection and analysis
- Cloud cost awareness and resource cleanup
- Security-conscious GitHub documentation

## Technologies and Tools Used

| Technology or Tool | Project Use | Version or Configuration |
|---|---|---|
| Microsoft Azure Portal | Created, tagged, protected, tested, and removed resources | Continuously updated web service; build not specified |
| Azure Resource Manager | Managed the resource group, tags, filters, and management locks | Service-managed; API version not specified |
| Azure Storage | Provided the resources used for governance testing | StorageV2, Standard performance |
| Azure Blob Storage / Azure Data Lake Storage | Storage service option used during deployment | Service version not specified |
| Locally Redundant Storage | Provided the selected redundancy configuration | LRS |
| Azure Resource Tags | Classified resources by department and environment | Key-value metadata |
| Azure Management Locks | Protected resources against deletion and modification | Delete and Read-only |
| Skillable Cloud Slice | Hosted the temporary Azure lab environment | Version not specified |
| Mentor | Provided optional AI-assisted lab guidance | Pilot version; build not specified |
| SEA-Dev virtual machine | Provided access to the lab environment | Operating system version not specified |
| GitHub Markdown | Structured the portfolio report and evidence | Markdown |

> Version numbers are not invented where the lab instructions or screenshots did not provide them.

## Lab Environment

| Component | Configuration |
|---|---|
| Resource group | `rg-gp-tags-locks` |
| Development storage account | `stgptagslock65463711` |
| Operations storage account | `stgptagsops65463711` |
| Region | East US |
| Storage account kind | StorageV2 |
| Performance | Standard |
| Redundancy | Locally Redundant Storage (LRS) |
| Development tags | `department: development`, `environment: test` |
| Operations tags | `department: operations`, `environment: test` |
| Delete lock | `prevent-delete` |
| Read-only lock | `read-only-rg` |
| Restoration validation tag | `lock-test: passed` |
| Subscription | Temporary Azure lab subscription |

## Repository Structure

```text
azure-resource-governance-tags-locks/
├── README.md
├── report/
│   └── Azure-Resource-Governance-Report.md
└── images/
    ├── Fig01 Storage Account Listed.png
    ├── Fig02 Department Tag Filter.png
    ├── Fig03 Read Only Lock Enforcement.png
    ├── Fig04 Development Storage Account Tags.png
    ├── Fig05 Add Read Only Lock.png
    ├── Fig06 Storage Account Configuration.png
    ├── Fig07 Delete Lock Enforcement.png
    ├── Fig08 Add Prevent Delete Lock.png
    ├── Fig09 Write Access Restored.png
    ├── Fig10 Confirmed Prevent Delete Lock.png
    ├── Fig11 Locks Removed.png
    ├── Fig12 Resource Group Tags.png
    ├── Fig13 Operations Storage Account Tags.png
    └── Fig14 Confirmed Read Only Lock.png
```

## Methodology

### 1. Prepare the Environment

A dedicated resource group named `rg-gp-tags-locks` was created in East US. The isolated resource group provided a clear scope for governance testing and simplified final cleanup.

### 2. Provision the Test Resources

Two Standard StorageV2 accounts using LRS redundancy were deployed:

- `stgptagslock65463711` for the development scenario
- `stgptagsops65463711` for the operations scenario

### 3. Apply Organizational Tags

The resource group and development storage account received the following tags:

- `department: development`
- `environment: test`

The operations storage account received:

- `department: operations`
- `environment: test`

### 4. Validate Tag-Based Organization

The `department` tag was used as a filter. The filter demonstrated how consistent key-value metadata supports targeted resource discovery and operational organization.

### 5. Configure Management Locks

A Delete lock named `prevent-delete` was applied to the development storage account. A Read-only lock named `read-only-rg` was configured at the applicable exercise scope.

### 6. Test Lock Enforcement

Two expected-failure tests were performed:

1. A new tag was submitted while the Read-only lock was active. Azure returned a `ScopeLocked` error.
2. The protected storage account was selected for deletion. Azure blocked the operation because the resource scope was locked.

### 7. Remove Locks and Restore Access

Both locks were removed. The Locks pane was checked to confirm that no lock remained on the selected resource. The temporary tag `lock-test: passed` was then saved successfully, verifying that write access had been restored.

### 8. Clean Up Resources

The temporary validation tag and guided-project resources were removed. Cleanup prevented the temporary lab resources from remaining active after validation.

## Evidence and Analysis

> Rename the screenshots exactly as listed below and place them in the repository's `images/` directory. Because this report is stored inside `report/`, each Markdown image path begins with `../images/`.

### Evidence 1: Storage Account Provisioning

![Storage account listed](../images/Fig01%20Storage%20Account%20Listed.png)

**Figure 1: Storage account listed in Azure Storage Center.**

**Analysis:** The Azure Storage Center displays `stgptagslock65463711` as a StorageV2 account in the `rg-gp-tags-locks` resource group and East US region. This provides evidence that the first test resource was provisioned in the intended governance scope.

### Evidence 2: Department Tag Filter

![Department tag filter](../images/Fig02%20Department%20Tag%20Filter.png)

**Figure 2: Filtering resources by the `department` tag.**

**Analysis:** The filter pane shows the `department` key, the Equals operator, and the `development` value. This demonstrates practical use of tags for targeted resource discovery.

### Evidence 3: Read-Only Lock Enforcement

![Read only lock enforcement](../images/Fig03%20Read%20Only%20Lock%20Enforcement.png)

**Figure 3: Tag modification blocked by the active Read-only lock.**

**Analysis:** Azure displays a `ScopeLocked` error after an attempted `test-tag: blocked` update. This is direct evidence that the active control prevented modification as expected.

### Evidence 4: Development Storage Account Tags

![Development storage account tags](../images/Fig04%20Development%20Storage%20Account%20Tags.png)

**Figure 4: Development tags applied to the first storage account.**

**Analysis:** The Tags pane displays `department: development` and `environment: test` on `stgptagslock65463711`. This confirms consistent classification of the development resource.

### Evidence 5: Read-Only Lock Configuration

![Add read only lock](../images/Fig05%20Add%20Read%20Only%20Lock.png)

**Figure 5: Configuration of the `read-only-rg` lock.**

**Analysis:** The Add lock pane shows the `read-only-rg` name and Read-only lock type. This documents the control configuration before enforcement testing.

### Evidence 6: Storage Account Configuration

![Storage account configuration](../images/Fig06%20Storage%20Account%20Configuration.png)

**Figure 6: Review and create settings for the operations storage account.**

**Analysis:** The review page shows the resource group, East US region, `stgptagsops65463711`, Standard performance, and LRS replication. This validates the main deployment settings used for the second account.

### Evidence 7: Delete Lock Enforcement

![Delete lock enforcement](../images/Fig07%20Delete%20Lock%20Enforcement.png)

**Figure 7: Storage account deletion blocked by an active lock.**

**Analysis:** The Azure notification reports that the deletion failed because the scope was locked. This confirms that the management lock protected the selected storage account from removal.

### Evidence 8: Delete Lock Configuration

![Add prevent delete lock](../images/Fig08%20Add%20Prevent%20Delete%20Lock.png)

**Figure 8: Configuration of the `prevent-delete` lock.**

**Analysis:** The Add lock pane shows the `prevent-delete` name, Delete lock type, and a note describing protection against accidental deletion. This demonstrates deliberate implementation of a resource-protection control.

### Evidence 9: Restored Write Access

![Write access restored](../images/Fig09%20Write%20Access%20Restored.png)

**Figure 9: Successful `lock-test: passed` validation tag.**

**Analysis:** The resource displays `lock-test: passed` after lock removal. This verifies that normal write operations were restored and completes the apply, enforce, remove, and retest lifecycle.

### Evidence 10: Delete Lock Confirmation

![Confirmed prevent delete lock](../images/Fig10%20Confirmed%20Prevent%20Delete%20Lock.png)

**Figure 10: Confirmed `prevent-delete` lock on the development storage account.**

**Analysis:** The Locks pane lists `prevent-delete` with the Delete lock type and the storage account as its scope. This confirms successful creation of the deletion-protection control.

### Evidence 11: Lock Removal Verification

![Locks removed](../images/Fig11%20Locks%20Removed.png)

**Figure 11: Selected storage account showing no active locks.**

**Analysis:** The Locks pane states that the selected resource has no locks. This provides evidence that lock removal was completed before restoration testing and cleanup.

### Evidence 12: Resource Group Tags

![Resource group tags](../images/Fig12%20Resource%20Group%20Tags.png)

**Figure 12: Organizational tags applied to `rg-gp-tags-locks`.**

**Analysis:** The resource-group Tags pane displays `department: development` and `environment: test`. This confirms that organizational metadata was applied at resource-group scope.

### Evidence 13: Operations Storage Account Tags

![Operations storage account tags](../images/Fig13%20Operations%20Storage%20Account%20Tags.png)

**Figure 13: Operations tags applied to the second storage account.**

**Analysis:** The Tags pane displays `department: operations` and `environment: test` on `stgptagsops65463711`. This confirms departmental separation while retaining a consistent environment classification.

### Evidence 14: Read-Only Lock Confirmation

![Confirmed read only lock](../images/Fig14%20Confirmed%20Read%20Only%20Lock.png)

**Figure 14: Confirmed `read-only-rg` lock in the Locks pane.**

**Analysis:** The Locks pane displays `read-only-rg` with the Read-only lock type. This confirms that the modification-prevention control was active before validation.

## Results

- The dedicated resource group was created successfully.
- Two Standard StorageV2 accounts using LRS were deployed.
- Department and environment tags were applied consistently.
- Tag-based filtering demonstrated metadata-driven resource discovery.
- Delete and Read-only locks were configured successfully.
- Modification and deletion operations were blocked while the applicable locks were active.
- Lock removal restored normal write access.
- Temporary resources were cleaned up after validation.

## Validation Checklist

### Resource Creation and Tagging

- [x] Created `rg-gp-tags-locks`.
- [x] Created `stgptagslock65463711`.
- [x] Created `stgptagsops65463711`.
- [x] Applied development and test tags to the resource group.
- [x] Applied development and test tags to the first storage account.
- [x] Applied operations and test tags to the second storage account.
- [x] Tested filtering by department.

### Lock Configuration and Enforcement

- [x] Applied the `prevent-delete` Delete lock.
- [x] Applied the `read-only-rg` Read-only lock.
- [x] Confirmed both lock configurations.
- [x] Confirmed that the Read-only lock blocked tag modification.
- [x] Confirmed that the Delete lock blocked storage-account deletion.
- [x] Removed the configured locks.
- [x] Confirmed that no lock remained on the selected resource.
- [x] Added `lock-test: passed` to confirm restored write access.

### Cleanup

- [x] Removed the temporary validation tag.
- [x] Removed applicable resource locks before cleanup.
- [x] Deleted the guided-project resources.

## Limitations and Next Steps

### Limitations

- The project was completed in a temporary training subscription rather than a production environment.
- Configuration was performed primarily through the Azure Portal.
- Azure Policy enforcement, automation, and infrastructure as code were outside the guided lab scope.
- The available screenshots do not include a final portal view showing the deleted resource group.
- Service and API version numbers were not provided and were not invented.

### Recommended Next Steps

- Recreate the deployment with Bicep or Terraform for repeatability.
- Use Azure Policy to enforce and remediate approved tags.
- Extend the tagging model with organization-approved fields such as owner, cost center, application, and data classification.
- Restrict lock-management permissions through least-privilege Azure RBAC.
- Monitor important governance changes using Azure Activity Log alerts.
- Test lock behavior at subscription, resource-group, and individual-resource scopes.
- Add automated validation to a CI/CD workflow.

## Security and Privacy Notes

- No passwords, access tokens, tenant usernames, or other confidential lab credentials are included.
- Azure tags should not contain credentials, secrets, personal data, or other sensitive information.
- Management locks complement, but do not replace, Azure RBAC, Azure Policy, monitoring, and approved change procedures.
- Screenshots should be reviewed before public publication to ensure that no confidential identifiers are exposed.

## Conclusion

This completed project demonstrates an end-to-end Azure governance workflow involving resource creation, classification, protection, enforcement testing, access restoration, and cleanup. The evidence shows practical familiarity with Azure Resource Manager, StorageV2 accounts, organizational tags, and management locks. The work is directly relevant to entry-level cloud security, Azure administration, and DevOps responsibilities.

## Disclaimer

This report documents a completed training exercise performed in a temporary Microsoft Azure lab environment provided through Skillable. The resource names, settings, screenshots, and observations are included as evidence of practical learning. This report is not production implementation guidance. Azure interfaces and service behavior may change, so all configurations should be validated against current Microsoft documentation and organizational policy before production use.

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
