<div align="center">

# Azure Identity, Least-Privilege Access, and Secure File Exchange

### Microsoft Azure Guided Project Portfolio

**Author:** Wadondera A. Collins  
**Track:** Cloud Security Engineering  
**Status:** Completed

</div>

---

## Project Overview

This repository documents two completed Microsoft Azure security assignments:

1. **Set Up a New Employee with Least-Privilege Access**
2. **Securely Share Files with an External Partner**

The work demonstrates identity administration, group-based Azure role-based access control (RBAC), least-privilege validation, private Azure Blob Storage, Shared Access Signature (SAS) management, access revocation, lifecycle management, auditing, and secure resource cleanup.

> **Security notice:** Temporary Access Pass tokens, passwords, usernames, SAS URLs, and other lab credentials have been intentionally excluded from this README. Secrets must never be committed to a public GitHub repository.

---

## Assignment 1: Set Up a New Employee with Least-Privilege Access

### Objective

Create a Microsoft Entra ID user and security group, assign the Azure **Reader** role at resource-group scope, and verify that the user can view resources but cannot create or modify them.

### Completed Work

- Created the `rg-gp-access-model` resource group.
- Deployed the `stgpaccessmodel65662231` storage account using Standard performance and locally redundant storage.
- Created the `gp-rg-readers65662231` Microsoft Entra security group.
- Added the pre-created `Alexgp-65662231` user to the security group.
- Assigned the Azure Reader role to the group at resource-group scope.
- Verified inherited access through **Access control (IAM) > Check access**.
- Reviewed the **Create role assignment** record in the Azure Activity Log.
- Tested the user account with a Temporary Access Pass in a private browser session.
- Confirmed that the user could view resources but could not create a storage account.
- Removed the lab resource group, user, and group after validation.

### Security Result

The assignment validated a group-based least-privilege model. Read access was inherited through the security group, while write operations remained denied.

---

## Assignment 2: Securely Share Files with an External Partner

### Objective

Create a private Azure Blob Storage environment, delegate time-limited read access through a stored access policy and SAS URL, revoke that access, and configure automated retention cleanup.

### Completed Work

- Created the `rg-gp-file-exchange` resource group.
- Deployed the `stgpfilexchg65667740` storage account using Standard performance and locally redundant storage.
- Created the private `partner-drop` blob container.
- Uploaded `monthly-report.txt` to the container.
- Created the read-only `partner-read-policy` stored access policy.
- Generated a blob SAS URL linked to the stored access policy.
- Confirmed that the direct blob URL denied anonymous access.
- Confirmed that the SAS URL allowed time-limited read access from a private browser session.
- Deleted the stored access policy and verified that the linked SAS URL was revoked.
- Confirmed that revoking access did not delete the stored file.
- Configured the `delete-shared-files` lifecycle rule to delete blobs under `partner-drop/` when last modified more than 30 days ago.
- Deleted the lab resource group after successful validation.

### Security Result

The assignment demonstrated private-by-default storage, controlled external access, policy-based SAS revocation, data-retention automation, and separation between data deletion and access revocation.

---

## Tools and Environment

| Tool or Service | Version / Status Used | Purpose |
|---|---|---|
| Microsoft Azure Portal | Cloud service; fixed build number not provided by the lab | Resource deployment, IAM, storage, monitoring, and cleanup |
| Microsoft Entra ID | Cloud service; fixed build number not provided by the lab | User, group, authentication method, and identity management |
| Azure RBAC | Azure platform service; API version not exposed in the portal workflow | Reader-role assignment and least-privilege enforcement |
| Azure Storage / Blob Storage | Storage account API version not recorded by the lab | Private container and blob-based file exchange |
| Azure Storage SAS | Service SAS linked to a stored access policy | Time-limited delegated read access |
| Azure Storage Lifecycle Management | Service feature; API version not recorded by the lab | Automatic deletion of older partner files |
| Azure Activity Log | Azure Monitor platform service | Audit verification for role assignment changes |
| Skillable Cloud Slice | Browser-based lab environment; version not provided | Hosted Azure lab subscription and temporary credentials |
| SEA-Dev virtual machine | Windows lab VM; Windows edition/build not recorded | Access workstation for the guided exercises |
| Microsoft Edge or Google Chrome | Browser version not recorded | Azure Portal access and InPrivate/Incognito testing |
| Temporary Access Pass | Microsoft Entra authentication method | Passwordless temporary sign-in for lab accounts |

> Exact product, browser, operating-system, and API version numbers were not displayed in the supplied lab instructions. They are marked as not provided instead of being guessed.

---

## Lab Environment

```text
Azure Subscription
├── Assignment 1: rg-gp-access-model
│   ├── Storage account: stgpaccessmodel65662231
│   ├── Security group: gp-rg-readers65662231
│   ├── Test user: Alexgp-65662231
│   └── RBAC role: Reader at resource-group scope
│
└── Assignment 2: rg-gp-file-exchange
    └── Storage account: stgpfilexchg65667740
        ├── Private container: partner-drop
        ├── Blob: monthly-report.txt
        ├── Stored access policy: partner-read-policy
        └── Lifecycle rule: delete-shared-files
```

---

## Skills Demonstrated

- Microsoft Entra identity and group administration
- Azure RBAC and role assignment at scope
- Group-based access management
- Least-privilege design and permission testing
- Azure Activity Log auditing
- Private Azure Blob Storage configuration
- Stored access policies and SAS-based delegation
- Access revocation and validation
- Storage lifecycle and retention management
- Secure use of private browser sessions
- Cloud resource cleanup and cost awareness
- Protection of credentials, tokens, and sensitive URLs

---

## Validation Summary

### Assignment 1

- [x] Security group existed in Microsoft Entra ID.
- [x] Test user was a member of the group.
- [x] Reader role was assigned at resource-group scope.
- [x] IAM showed the inherited Reader role.
- [x] Activity Log recorded the role assignment.
- [x] The test user could view resources.
- [x] The test user could not create new resources.
- [x] Resources and identities were removed after testing.

### Assignment 2

- [x] Storage account deployed successfully.
- [x] Blob container remained private.
- [x] Report file uploaded successfully.
- [x] Direct anonymous access was denied.
- [x] Policy-linked SAS access succeeded before revocation.
- [x] SAS access failed after policy deletion.
- [x] The blob remained stored after access revocation.
- [x] The 30-day lifecycle deletion rule targeted `partner-drop/`.
- [x] Lab resources were removed after testing.

---

## Screenshot Evidence

Add only screenshots captured during the completed lab. Ensure every image name and caption accurately matches the visible evidence.

```markdown
![Security group and membership validation](evidence/Fig01 Security Group Membership.png)
![Reader role assignment at resource-group scope](evidence/Fig02 Reader Role Assignment.png)
![Inherited access verification](evidence/Fig03 Inherited Reader Access.png)
![Least-privilege write denial](evidence/Fig04 Resource Creation Denied.png)
![Private blob container](evidence/Fig05 Private Partner Container.png)
![Stored access policy](evidence/Fig06 Stored Access Policy.png)
![SAS access validation](evidence/Fig07 SAS Access Validation.png)
![Revoked SAS access](evidence/Fig08 SAS Access Revoked.png)
![Lifecycle management rule](evidence/Fig09 Lifecycle Management Rule.png)
![Resource cleanup validation](evidence/Fig10 Resource Cleanup Validation.png)
```

---

## Repository Structure

```text
azure-identity-secure-file-exchange/
├── README.md
├── evidence/
│   ├── Fig01 Security Group Membership.png
│   ├── Fig02 Reader Role Assignment.png
│   ├── Fig03 Inherited Reader Access.png
│   ├── Fig04 Resource Creation Denied.png
│   ├── Fig05 Private Partner Container.png
│   ├── Fig06 Stored Access Policy.png
│   ├── Fig07 SAS Access Validation.png
│   ├── Fig08 SAS Access Revoked.png
│   ├── Fig09 Lifecycle Management Rule.png
│   └── Fig10 Resource Cleanup Validation.png
└── sample-files/
    └── monthly-report.txt
```

---

## Security Notes

- Do not publish passwords, Temporary Access Pass codes, SAS tokens, tenant credentials, or lab sign-in details.
- Treat a SAS URL as a secret because it grants access according to its embedded permissions and validity rules.
- Use groups for scalable access administration instead of assigning recurring permissions directly to individual users.
- Apply permissions at the narrowest practical scope.
- Validate both allowed and denied operations when testing least privilege.
- Review audit logs after access-control changes.
- Delete temporary resources and test identities when they are no longer required.

---

## References

- [Azure role-based access control documentation](https://learn.microsoft.com/azure/role-based-access-control/overview)
- [Microsoft Entra Temporary Access Pass documentation](https://learn.microsoft.com/entra/identity/authentication/howto-authentication-temporary-access-pass)
- [Azure Storage shared access signature overview](https://learn.microsoft.com/azure/storage/common/storage-sas-overview)
- [Define a stored access policy](https://learn.microsoft.com/rest/api/storageservices/define-stored-access-policy)
- [Azure Blob Storage lifecycle management](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview)

---

## Conclusion

These assignments established practical experience in Azure identity security and protected data sharing. The completed work combined Microsoft Entra ID, Azure RBAC, audit validation, private Blob Storage, policy-controlled SAS access, immediate revocation, and lifecycle management to enforce least privilege throughout the resource lifecycle.

---

## Disclaimer

This repository is an educational portfolio record of guided lab work completed in a temporary Skillable Azure environment. Resource names and identifiers are included only to document the implementation. Credentials, Temporary Access Pass codes, SAS URLs, passwords, and other sensitive authentication information have been removed. Azure services and portal interfaces may change over time. Always consult current Microsoft documentation before applying the same configuration in a production environment.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
