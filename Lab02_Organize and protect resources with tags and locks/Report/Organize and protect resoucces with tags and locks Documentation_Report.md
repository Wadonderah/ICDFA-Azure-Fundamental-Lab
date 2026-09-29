<div align="center">

# Azure Resource Governance

## Tags and Resource Locks

**Microsoft Learn Guided Project / Skillable Lab**

**Author:** Wadondera A. Collins  
**Programme:** ICDFA Cloud Security Engineering, Cohort 11  
**Role Focus:** Cloud Security Engineering and Azure Administration  
**Status:** Completed

</div>

---

## Project Overview

This completed guided project demonstrates how to organize and protect Microsoft Azure resources using resource tags and management locks. The work covered resource creation, tag-based organization, tag filtering, Delete and Read-only lock configuration, lock-enforcement testing, access restoration, and resource cleanup.

## Project Objectives

- Create a dedicated Azure resource group and two storage accounts.
- Apply consistent department and environment tags.
- Filter resources using organizational tag values.
- Configure Delete and Read-only management locks.
- Validate that the locks block modification and deletion.
- Remove the locks and confirm that normal access is restored.
- Clean up the temporary Azure resources.

## Technologies and Environment

| Component | Configuration |
|---|---|
| Microsoft Azure Portal | Continuously updated web service; build not specified |
| Azure Resource Manager | Resource groups, tags, filters, and management locks |
| Azure Storage | StorageV2, Standard performance |
| Redundancy | Locally Redundant Storage (LRS) |
| Resource group | `rg-gp-tags-locks` |
| Development storage account | `stgptagslock65463711` |
| Operations storage account | `stgptagsops65463711` |
| Region | East US |
| Lab platform | Skillable Cloud Slice |

## Methodology

1. Created `rg-gp-tags-locks` in East US.
2. Configured and deployed two Standard StorageV2 accounts using LRS.
3. Applied resource-group and storage-account tags.
4. Filtered resources by the `department` tag.
5. Applied the `prevent-delete` Delete lock.
6. Applied the `read-only-rg` Read-only lock.
7. Tested Read-only and Delete lock enforcement.
8. Removed the locks.
9. Confirmed restored write access with `lock-test: passed`.
10. Cleaned up the temporary resources.

## Evidence and Analysis

> Place all screenshots in an `images/` folder. Filenames, headings, image links, and evidence statements below match the visible Azure Portal content exactly.

### Resource Creation

#### Fig01 Storage Account Configuration.png

<img width="1052" height="603" alt="Fig01 Storage Account Configuration" src="https://github.com/user-attachments/assets/2d0bac8b-35a6-49c0-afd5-bc2e346bcf34" />


**Visible evidence:** The **Create a storage account** Review + create page shows resource group `rg-gp-tags-locks`, location **East US**, storage account `stgptagsops65463711`, primary service **Azure Blob Storage or Azure Data Lake Storage**, Standard performance, and LRS replication.

#### Fig02 Storage Account Listed.png

<img width="1052" height="494" alt="Fig02 Storage Account Listed" src="https://github.com/user-attachments/assets/e44057cc-d6b0-4734-b8cf-c2ad3da6d6fc" />


**Visible evidence:** Azure Storage Center lists `stgptagslock65463711` as a **Storage account**, kind **StorageV2**, in `rg-gp-tags-locks`, located in **East US**.

### Resource Tagging and Filtering

#### Fig03 Resource Group Tags.png

<img width="1056" height="641" alt="Fig03 Resource Group Tags" src="https://github.com/user-attachments/assets/538efe7e-2fd5-4dfc-b264-0858414abdc6" />


**Visible evidence:** The Tags pane for `rg-gp-tags-locks` shows `department: development` and `environment: test`.

#### Fig04 Development Storage Account Tags.png

<img width="1052" height="626" alt="Fig04 Development Storage Account Tags" src="https://github.com/user-attachments/assets/3070efe7-71a6-49f6-888c-0cc2b15da45a" />


**Visible evidence:** The Tags pane for `stgptagslock65463711` shows `department: development` and `environment: test`.

#### Fig05 Operations Storage Account Tags.png

<img width="1050" height="603" alt="Fig05 Operations Storage Account Tags" src="https://github.com/user-attachments/assets/aec36f75-ceff-483e-9294-f4221b966dce" />


**Visible evidence:** The Tags pane for `stgptagsops65463711` shows `department: operations` and `environment: test`.

#### Fig06 Department Tag Filter.png

<img width="1055" height="528" alt="Fig06 Department Tag Filter" src="https://github.com/user-attachments/assets/e428f390-001f-48a9-90b0-04b6447b3ea7" />


**Visible evidence:** The Resource groups filter pane shows the `department` tag, the **Equals** operator, and the `development` value.

### Resource Lock Configuration

#### Fig07 Add Prevent Delete Lock.png

<img width="1054" height="622" alt="Fig07 Add Prevent Delete Lock" src="https://github.com/user-attachments/assets/76205012-5491-4758-a018-e7fadf0c4ea9" />


**Visible evidence:** The Add lock pane for `stgptagslock65463711` shows lock name `prevent-delete`, lock type **Delete**, and the note **Prevents accidental deletion of test storage account**.

#### Fig08 Confirmed Prevent Delete Lock.png

<img width="679" height="516" alt="Fig08 Confirmed Prevent Delete Lock" src="https://github.com/user-attachments/assets/ffeb3fbf-8797-42ef-9e27-107f56d1898d" />


**Visible evidence:** The Locks pane for `stgptagslock65463711` lists `prevent-delete` with lock type **Delete**.

#### Fig09 Add Read Only Lock.png

<img width="1053" height="559" alt="Fig09 Add Read Only Lock" src="https://github.com/user-attachments/assets/2efe553c-d9f4-4361-9721-b761bf858874" />


**Visible evidence:** The Add lock pane for `stgptagsops65463711` shows lock name `read-only-rg` and lock type **Read-only**.

#### Fig10 Confirmed Read Only Lock.png

<img width="673" height="496" alt="Fig10 Confirmed Read Only Lock" src="https://github.com/user-attachments/assets/4982cb52-3949-4dd2-b66f-fd22ee74d9c4" />


**Visible evidence:** The Locks pane for `stgptagsops65463711` lists `read-only-rg` with a Read-only lock type.

### Lock-Enforcement Testing

#### Fig11 Read Only Lock Enforcement.png

<img width="1051" height="604" alt="Fig11 Read Only Lock Enforcement" src="https://github.com/user-attachments/assets/80278348-9f99-4070-8ecc-6a26255368bb" />


**Visible evidence:** The Tags pane for `stgptagsops65463711` shows an attempted `test-tag: blocked` update and the error **Could not save the tags** with error code `ScopeLocked`.

#### Fig12 Delete Lock Enforcement.png

<img width="1055" height="642" alt="Fig12 Delete Lock Enforcement" src="https://github.com/user-attachments/assets/0114c1bf-4ced-4c33-925d-d29f9b458a9b" />


**Visible evidence:** Azure Storage Center shows that the delete command for `stgptagslock65463711` failed because the scope was locked.

### Lock Removal and Access Restoration

#### Fig13 Locks Removed.png

<img width="1053" height="604" alt="Fig13 Locks Removed" src="https://github.com/user-attachments/assets/2ec29d0b-55d6-4834-bef9-ceed945c0a19" />


**Visible evidence:** The Locks pane for `stgptagsops65463711` displays **This resource has no locks**.

#### Fig14 Write Access Restored.png

<img width="862" height="544" alt="Fig14 Write Access Restored" src="https://github.com/user-attachments/assets/10073ccf-3092-47b6-b6ce-fb1afc0ba261" />


**Visible evidence:** The Tags pane for `stgptagsops65463711` displays `lock-test: passed`, confirming that the tag was saved after lock removal.

## Validation Checklist

- [x] Created the resource group and two storage accounts.
- [x] Applied the correct resource-group and storage-account tags.
- [x] Tested filtering with the `department` tag.
- [x] Applied and confirmed the Delete lock.
- [x] Applied and confirmed the Read-only lock.
- [x] Confirmed that tag modification was blocked.
- [x] Confirmed that storage-account deletion was blocked.
- [x] Removed the configured locks.
- [x] Confirmed that no lock remained on the selected resource.
- [x] Confirmed restored write access with `lock-test: passed`.
- [x] Cleaned up the temporary lab resources.

## Skills Demonstrated

- Azure resource provisioning and lifecycle management
- Azure resource tagging and filtering
- Delete and Read-only lock configuration
- Governance-control testing and validation
- Access-restoration verification
- Cloud cleanup and cost awareness
- Professional technical documentation

## Security Notes

- No passwords, access tokens, or confidential lab credentials are included.
- Azure tags should not contain credentials, secrets, personal data, or other sensitive values.
- Management locks complement Azure RBAC, Azure Policy, monitoring, and approved change-management processes.

## Disclaimer

This repository documents a completed training exercise performed in a temporary Microsoft Azure lab environment provided through Skillable. Resource settings and screenshots are included as evidence of practical learning. Azure interfaces and service behavior may change, so production configurations should be validated against current Microsoft documentation and organizational policy.

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
