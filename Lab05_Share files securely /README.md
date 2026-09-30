<div align="center">

# 🔐 Azure Identity and Secure File Exchange: Complete Guide

### Mentor Pilot Program | Completed Assignment Portfolio

**Author:** Wadondera A. Collins  
**Track:** Cloud Security Engineering  
**Status:** Completed

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Security-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Entra ID](https://img.shields.io/badge/Microsoft%20Entra-ID-5E5CE6?logo=microsoft&logoColor=white)](https://www.microsoft.com/security/business/identity-access/microsoft-entra-id)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Learning](https://img.shields.io/badge/Focus-Identity%20and%20Data%20Security-6F42C1)](#-skills-demonstrated)

*A hands-on Azure security portfolio covering group-based least privilege, RBAC validation, private Blob Storage, policy-linked SAS access, revocation, lifecycle management, auditing, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Configure Least-Privilege Access](#-exercise-1-configure-least-privilege-access)
- [Exercise 2: Build a Private File Exchange](#-exercise-2-build-a-private-file-exchange)
- [Exercise 3: Validate, Revoke, Retain, and Clean Up](#-exercise-3-validate-revoke-retain-and-clean-up)
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

This repository documents two completed Microsoft Azure security assignments in the **Mentor Pilot Program**:

1. **Set Up a New Employee with Least-Privilege Access**
2. **Securely Share Files with an External Partner**

The first assignment implemented group-based Azure Role-Based Access Control by assigning the built-in `Reader` role to a Microsoft Entra security group at resource-group scope. A test identity inherited read-only access through group membership. Validation confirmed that the identity could view resources but could not create a storage account.

The second assignment created a private Azure Blob Storage file exchange. A stored access policy controlled a read-only Shared Access Signature for a partner file. The project validated private-by-default access, delegated access through the SAS URL, policy-based revocation, continued data retention after revocation, and automated deletion through lifecycle management.

The portfolio covered the following workflow:

1. Prepare isolated Azure resource groups.
2. Create storage accounts for access and file-exchange testing.
3. Create a Microsoft Entra security group.
4. Add a test identity to the group.
5. Assign `Reader` at resource-group scope.
6. Validate inherited read access and denied write access.
7. Review the role-assignment audit event.
8. Create a private blob container and upload a report.
9. Create a read-only stored access policy.
10. Generate and test a policy-linked SAS URL.
11. Revoke the SAS by deleting the stored access policy.
12. Configure a 30-day lifecycle deletion rule.
13. Remove the temporary resources and identities.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

By completing these assignments, I demonstrated the ability to:

- Administer Microsoft Entra users and security groups.
- Implement group-based Azure permissions.
- Assign a built-in Azure role at resource-group scope.
- Confirm inherited authorization through Access control (IAM).
- Validate least privilege with allowed and denied operations.
- Review access-control activity in the Azure Activity Log.
- Create private Azure Blob Storage containers.
- Upload and manage partner-facing files securely.
- Delegate limited access through a stored access policy and SAS.
- Revoke policy-linked SAS access without deleting the blob.
- Configure lifecycle management for retention cleanup.
- Protect credentials, tokens, and sensitive URLs.
- Remove temporary resources and identity objects after testing.

---

## 🏗️ Architecture and Resources

```text
Azure Subscription
├── Assignment 1: Least-Privilege Access
│   └── Resource Group: rg-gp-access-model
│       └── Storage Account: stgpaccessmodel65662231
│
│   Microsoft Entra ID
│   ├── Test User: Alexgp-65662231
│   └── Security Group: gp-rg-readers65662231
│       └── Azure Reader role at resource-group scope
│
└── Assignment 2: Secure File Exchange
    └── Resource Group: rg-gp-file-exchange
        └── Storage Account: stgpfilexchg65667740
            └── Private Container: partner-drop
                ├── Blob: monthly-report.txt
                ├── Stored Access Policy: partner-read-policy
                └── Lifecycle Rule: delete-shared-files
```

| Resource | Name | Purpose |
|---|---|---|
| Access-model resource group | `rg-gp-access-model` | Isolated RBAC assignment scope |
| Access-validation storage account | `stgpaccessmodel65662231` | Resource used to test read-only access |
| Security group | `gp-rg-readers65662231` | Group assigned the Azure `Reader` role |
| Test identity | `Alexgp-65662231` | Identity used to validate inherited access |
| File-exchange resource group | `rg-gp-file-exchange` | Isolated scope for partner file sharing |
| File-exchange storage account | `stgpfilexchg65667740` | Hosts the private file exchange |
| Blob container | `partner-drop` | Private container for partner files |
| Shared file | `monthly-report.txt` | File used for delegated-access testing |
| Stored access policy | `partner-read-policy` | Controls the policy-linked service SAS |
| Lifecycle rule | `delete-shared-files` | Deletes targeted blobs after 30 days |

> [!NOTE]
> **Final state:** The temporary Azure resources and identity objects were removed after successful validation. The architecture represents the deployed lab environment before cleanup.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An authorized Skillable or Microsoft Learn lab subscription
- Permission to manage the required Azure and Microsoft Entra resources
- Permission to create Azure role assignments at resource-group scope
- A private browser session for independent access testing
- The lab-provided test identity and approved authentication method
- A local copy of `monthly-report.txt`

### Tools and Environment

| Tool or Service | Version or Status | Purpose |
|---|---|---|
| Microsoft Azure portal | Fixed build not provided | Resource, IAM, storage, monitoring, and cleanup |
| Microsoft Entra ID | Fixed build not provided | User, group, and identity management |
| Azure RBAC | API version not exposed | Reader-role assignment and enforcement |
| Azure Blob Storage | API version not recorded | Private file exchange |
| Azure Storage SAS | Policy-linked service SAS | Time-limited delegated read access |
| Lifecycle Management | API version not recorded | Automated retention cleanup |
| Azure Activity Log | Azure Monitor service | Role-assignment audit validation |
| Skillable Cloud Slice | Version not provided | Hosted lab subscription and credentials |
| SEA-Dev virtual machine | Windows build not recorded | Lab access workstation |
| Edge or Chrome | Version not recorded | Portal and private-session validation |
| Temporary Access Pass | Lab authentication method | Temporary test-account sign-in |

> [!NOTE]
> Exact product, browser, operating-system, and API versions were not displayed in the supplied instructions. They are identified as not provided rather than estimated.

### Security Notice

Passwords, usernames, Temporary Access Pass codes, SAS tokens, SAS URLs, subscription identifiers, tenant identifiers, storage keys, and temporary lab credentials are intentionally **not included**.

> [!CAUTION]
> Treat a SAS URL as a secret because possession of the URL can grant the permissions encoded in the signature. Never commit SAS tokens, passwords, access keys, or Temporary Access Pass codes to GitHub.

---

## 🧭 Exercise 1: Configure Least-Privilege Access

### 1. Prepare the Access-Model Resources

Create or open the resource group:

```text
rg-gp-access-model
```

Create the validation storage account:

```text
stgpaccessmodel65662231
```

**Validation:** The resource group and storage account were available for access testing.

### 2. Create the Security Group and Add the User

Create the Microsoft Entra security group:

```text
gp-rg-readers65662231
```

Add the pre-created test identity:

```text
Alexgp-65662231
```

**Validation:** The security group existed and the test identity appeared in its membership list.

### 3. Assign the Reader Role

1. Open `rg-gp-access-model`.
2. Select **Access control (IAM)**.
3. Start a new role assignment.
4. Select the built-in Azure `Reader` role.
5. Select `gp-rg-readers65662231` as the member.
6. Complete the assignment at resource-group scope.

**Validation:** IAM displayed the group-based `Reader` assignment at the intended scope.

### 4. Confirm Inherited Access

Use **Check access** to inspect `Alexgp-65662231`.

**Validation:** The test identity inherited `Reader` through membership in `gp-rg-readers65662231`.

### 5. Test Allowed and Denied Operations

Sign in with the test identity in a private browser session.

- Open the target resource group and storage account.
- Attempt to create a storage account.

**Validation:** Resource viewing was allowed, while resource creation was denied.

### 6. Review the Audit Event

Open the resource group's **Activity log** and review the **Create role assignment** event.

**Validation:** The role-assignment operation appeared in the Azure audit trail.

---

## 📤 Exercise 2: Build a Private File Exchange

### 1. Prepare the File-Exchange Resources

Create the resource group:

```text
rg-gp-file-exchange
```

Create the storage account:

```text
stgpfilexchg65667740
```

Use Standard performance and locally redundant storage as specified by the assignment.

**Validation:** The file-exchange storage account deployed successfully.

### 2. Create the Private Container

Create the blob container:

```text
partner-drop
```

Keep anonymous access disabled.

**Validation:** The container remained private.

### 3. Upload the Partner File

Upload:

```text
monthly-report.txt
```

**Validation:** The report file appeared in `partner-drop`.

### 4. Create the Stored Access Policy

Create the read-only stored access policy:

```text
partner-read-policy
```

Configure the assignment-specified validity period and read permission.

**Validation:** The stored access policy appeared on the private container.

### 5. Generate and Test the SAS URL

Generate a blob SAS URL linked to `partner-read-policy`.

1. Open the direct blob URL without a SAS.
2. Confirm that anonymous access is denied.
3. Open the SAS URL in a private browser session.
4. Confirm that the file can be read through delegated access.

**Validation:** The direct URL denied anonymous access, while the policy-linked SAS URL permitted read access before revocation.

> [!WARNING]
> Do not capture or publish a complete SAS URL. Redact the query string in screenshots and documentation.

---

## 🔄 Exercise 3: Validate, Revoke, Retain, and Clean Up

### 1. Revoke Delegated Access

Delete `partner-read-policy` from the container's stored access policies.

Retest the previously generated SAS URL after the policy change becomes effective.

**Validation:** The policy-linked SAS no longer granted access after revocation.

### 2. Confirm That the Blob Remains Stored

Return to the private container after revoking the SAS.

**Validation:** `monthly-report.txt` remained stored because access revocation did not delete the underlying blob.

### 3. Configure Lifecycle Management

Create the lifecycle rule:

```text
delete-shared-files
```

Configure it to target blobs under:

```text
partner-drop/
```

Set the action to delete targeted blobs when they were last modified more than 30 days ago.

**Validation:** The lifecycle rule targeted the intended path with the assignment-specified retention condition.

### 4. Clean Up the Lab

After completing validation:

1. Delete `rg-gp-access-model`.
2. Remove the test user and security group when required by the lab.
3. Delete `rg-gp-file-exchange`.
4. Confirm that the temporary resources no longer appear.

**Validation:** The project resources and temporary identities were removed.

> [!WARNING]
> Resource-group and identity deletion can be permanent. Verify each selected object before confirming cleanup.

---

## 🖼️ Screenshot Evidence

Add only screenshots captured during the completed lab. Each image must be placed beneath the exact task it supports, and its filename, link, caption, and visible evidence must match.

```markdown
![Security group and membership validation](evidence/Fig01%20Security%20Group%20Membership.png)
![Reader role assignment at resource-group scope](evidence/Fig02%20Reader%20Role%20Assignment.png)
![Inherited access verification](evidence/Fig03%20Inherited%20Reader%20Access.png)
![Least-privilege write denial](evidence/Fig04%20Resource%20Creation%20Denied.png)
![Private blob container](evidence/Fig05%20Private%20Partner%20Container.png)
![Stored access policy](evidence/Fig06%20Stored%20Access%20Policy.png)
![SAS access validation](evidence/Fig07%20SAS%20Access%20Validation.png)
![Revoked SAS access](evidence/Fig08%20SAS%20Access%20Revoked.png)
![Lifecycle management rule](evidence/Fig09%20Lifecycle%20Management%20Rule.png)
![Resource cleanup validation](evidence/Fig10%20Resource%20Cleanup%20Validation.png)
```

> [!IMPORTANT]
> Review every screenshot for credentials, usernames, SAS tokens, SAS URLs, tenant identifiers, subscription identifiers, and other sensitive values before publication.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Security group created | ✅ Passed |
| Test identity added to group | ✅ Passed |
| Reader role assigned at resource-group scope | ✅ Passed |
| Inherited Reader access confirmed | ✅ Passed |
| Role-assignment event reviewed | ✅ Passed |
| Test identity could view resources | ✅ Passed |
| Test identity could not create resources | ✅ Passed |
| Private storage container created | ✅ Passed |
| Partner file uploaded | ✅ Passed |
| Anonymous blob access denied | ✅ Passed |
| Stored access policy created | ✅ Passed |
| Policy-linked SAS access succeeded | ✅ Passed |
| SAS access failed after policy deletion | ✅ Passed |
| Blob remained after access revocation | ✅ Passed |
| 30-day lifecycle rule configured | ✅ Passed |
| Azure resources removed | ✅ Passed |
| Temporary identity objects removed | ✅ Passed |

---

## 📚 Command Reference

These assignments were completed through the Azure portal. The reference below preserves the verified portal workflow.

| Goal | Azure Portal Path |
|---|---|
| Assign an Azure role | Resource group → **Access control (IAM)** → **Add role assignment** |
| Check inherited access | Resource group → **Access control (IAM)** → **Check access** |
| Review the RBAC event | Resource group → **Activity log** |
| Create a private container | Storage account → **Containers** → **Container** |
| Upload the report | `partner-drop` → **Upload** |
| Manage stored access policies | Container → **Access policy** |
| Generate delegated access | Blob → **Generate SAS** |
| Configure lifecycle management | Storage account → **Lifecycle management** |
| Delete project resources | Resource group → **Delete resource group** |

### Repository Structure

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

## 🧰 Troubleshooting

### The test identity does not inherit Reader access

- Confirm the user's group membership.
- Confirm that the role was assigned to the security group.
- Confirm that the role-assignment scope is `rg-gp-access-model`.
- Sign out and sign back in to refresh the test session.

### The test identity can create resources

Review all effective role assignments. A second assignment inherited from a broader scope may grant write access.

### The direct blob URL opens successfully

Review the container access level and storage configuration. The intended lab outcome requires anonymous access to remain disabled.

### The SAS URL does not work before revocation

- Confirm that the SAS is linked to `partner-read-policy`.
- Confirm that read permission is present.
- Confirm that the SAS validity period covers the test time.
- Confirm that the complete URL was copied without alteration.
- Keep the URL private while troubleshooting.

### The SAS URL still works immediately after policy deletion

Stored access policy changes may not be instantaneous. Retest after allowing the policy update to become effective. Do not regenerate the SAS during the revocation test.

### The lifecycle rule does not delete files immediately

Lifecycle management is asynchronous. Confirm that the rule is enabled, the prefix is correct, and the blob meets the age condition.

### Cleanup appears incomplete

Refresh the portal and verify the active tenant and subscription. Confirm deletion from the resource-group, user, and group lists.

---

## 🧠 Skills Demonstrated

- Microsoft Entra identity and group administration
- Azure Role-Based Access Control
- Group-based least-privilege authorization
- Resource-group-scoped role assignment
- Effective-access verification
- Azure Activity Log auditing
- Private Azure Blob Storage configuration
- Stored access policy management
- SAS-based delegated access
- Access revocation and validation
- Storage lifecycle and retention management
- Secure private-session testing
- Protection of credentials and sensitive URLs
- Cloud resource and identity cleanup

---

## 💡 Key Takeaways

1. **Group-based access scales better than repeated direct assignments.** Membership controls who receives the established authorization.
2. **Scope limits exposure.** Resource-group scope constrained the Reader assignment to the required resources.
3. **Least privilege requires negative testing.** Denied resource creation confirmed that read access did not include write permission.
4. **Private storage should remain the default.** External sharing was enabled through a controlled SAS rather than anonymous container access.
5. **A SAS URL is a secret.** Anyone possessing a valid SAS URL may exercise its delegated permissions.
6. **Stored access policies support revocation.** Deleting the policy invalidated the linked SAS without deleting the blob.
7. **Access revocation and data deletion are separate controls.** The shared file remained stored after delegated access was removed.
8. **Lifecycle management supports retention hygiene.** The rule automated deletion of files older than the configured threshold.
9. **Audit and cleanup complete the security lifecycle.** Changes were reviewed and temporary resources were removed after validation.

---

## ☑️ Completion Checklist

### Assignment 1: Least-Privilege Access

- [x] Created `rg-gp-access-model`
- [x] Created `stgpaccessmodel65662231`
- [x] Created `gp-rg-readers65662231`
- [x] Added `Alexgp-65662231` to the group
- [x] Assigned `Reader` at resource-group scope
- [x] Verified inherited access through IAM
- [x] Reviewed the Activity Log event
- [x] Confirmed resource viewing was allowed
- [x] Confirmed resource creation was denied
- [x] Removed the resources and temporary identities

### Assignment 2: Secure File Exchange

- [x] Created `rg-gp-file-exchange`
- [x] Created `stgpfilexchg65667740`
- [x] Created the private `partner-drop` container
- [x] Uploaded `monthly-report.txt`
- [x] Created `partner-read-policy`
- [x] Confirmed anonymous access was denied
- [x] Confirmed policy-linked SAS access succeeded
- [x] Deleted the stored access policy
- [x] Confirmed linked SAS access was revoked
- [x] Confirmed the blob remained stored
- [x] Configured `delete-shared-files`
- [x] Targeted the `partner-drop/` path
- [x] Applied the 30-day condition
- [x] Deleted the project resource group
- [x] Confirmed cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This portfolio project demonstrates practical experience in identity governance, least-privilege authorization, secure delegated storage access, revocation, retention automation, auditing, and responsible cloud cleanup.

---

## 🙏 Acknowledgements

These guided assignments were completed as part of the **Mentor Pilot Program** in a Skillable Azure environment. Mentor supported the learning experience through lab navigation, instruction comprehension, and troubleshooting.

Official reference material:

- [Azure role-based access control overview](https://learn.microsoft.com/azure/role-based-access-control/overview)
- [Temporary Access Pass documentation](https://learn.microsoft.com/entra/identity/authentication/howto-authentication-temporary-access-pass)
- [Azure Storage SAS overview](https://learn.microsoft.com/azure/storage/common/storage-sas-overview)
- [Define a stored access policy](https://learn.microsoft.com/rest/api/storageservices/define-stored-access-policy)
- [Azure Blob Storage lifecycle management](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview)

---

## ⚖️ Disclaimer

This repository is an educational portfolio record of guided lab work completed in a temporary Skillable Azure environment. It is not a production-ready identity or data-sharing architecture and does not replace official Microsoft documentation, organizational policy, or professional security guidance. Resource names and identifiers are included only to document the completed implementation.

Credentials, Temporary Access Pass codes, passwords, SAS tokens, SAS URLs, storage keys, subscription identifiers, tenant identifiers, and other sensitive authentication information are intentionally excluded. Azure services, interfaces, roles, pricing, limits, and features may change. Review current Microsoft documentation and organizational requirements before reproducing the configuration in another environment.

---

<div align="center">

### 🎉 Portfolio Projects Completed Successfully

**Azure identity and secure file exchange: scoped, protected, validated, revoked, retained, and responsibly removed.**

Made with curiosity, care, and a commitment to responsible cloud engineering.  

**Wadondera A. Collins**  
*ICDFA Trainee | Cohort 11 | Cloud Security Engineering*

</div>
