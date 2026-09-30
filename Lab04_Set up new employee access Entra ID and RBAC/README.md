<div align="center">

# 🔐 Azure RBAC Lab: Least-Privilege Access Model

### Mentor Pilot Program | Completed Assignment

**Author:** Wadondera A. Collins  
**Completion Date:** September 30, 2026

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-RBAC-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Entra ID](https://img.shields.io/badge/Microsoft%20Entra-ID-5E5CE6?logo=microsoft&logoColor=white)](https://www.microsoft.com/security/business/identity-access/microsoft-entra-id)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Learning](https://img.shields.io/badge/Focus-Identity%20Governance-6F42C1)](#-skills-demonstrated)

*A hands-on journey through Microsoft Entra ID, group-based Azure RBAC, resource-group scope, access validation, audit review, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Prepare Identities and Resources](#-exercise-1-prepare-identities-and-resources)
- [Exercise 2: Assign RBAC at Resource-Group Scope](#-exercise-2-assign-rbac-at-resource-group-scope)
- [Exercise 3: Validate Access, Audit, and Clean Up](#-exercise-3-validate-access-audit-and-clean-up)
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

This repository documents the successful completion of the **Azure RBAC Least-Privilege Access Model** lab in the **Mentor Pilot Program**. The project used group-based authorization by assigning the built-in Azure `Reader` role to a Microsoft Entra security group at resource-group scope.

The test identity inherited read-only access through group membership. Validation confirmed that the identity could view the target resource group and storage account but could not create Azure resources. The role-assignment event was reviewed in the Azure Activity Log before the temporary resources and identities were removed.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

- Manage Microsoft Entra security groups and membership.
- Implement group-based Azure authorization.
- Assign a built-in Azure role at resource-group scope.
- Verify assignments and inherited effective access through IAM.
- Validate permitted and denied actions using a test identity.
- Review role-assignment activity in the Azure Activity Log.
- Apply least privilege and perform responsible cleanup.

---

## 🏗️ Architecture and Resources

```text
Microsoft Entra ID
├── Test User: Alexgp-65662231
│   └── Member of
└── Security Group: gp-rg-readers65662231
        │
        │ Azure Reader role
        ▼
Azure Resource Group: rg-gp-access-model
└── Storage Account: stgpaccessmodel65662231

View resources: Allowed
Create or modify resources: Denied
```

| Resource | Name | Purpose |
|---|---|---|
| Resource group | `rg-gp-access-model` | Isolated RBAC assignment scope |
| Storage account | `stgpaccessmodel65662231` | Read-access validation resource |
| Security group | `gp-rg-readers65662231` | Group assigned the `Reader` role |
| Test identity | `Alexgp-65662231` | Identity used to test inherited access |
| Azure role | `Reader` | View resources without making changes |

> [!NOTE]
> **Final state:** The project resource group, test identity, and security group were removed after validation.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An authorized Azure subscription or lab environment
- Permission to manage project resources and required Microsoft Entra objects
- Permission to create role assignments at resource-group scope
- A private browser session for test-identity validation

### Security Notice

Passwords, Temporary Access Pass codes, tokens, subscription identifiers, tenant identifiers, and temporary sign-in details are intentionally **not included**.

> [!CAUTION]
> Never commit authentication values or cloud secrets to GitHub. Revoke or rotate any exposed credential immediately.

---

## 🧭 Exercise 1: Prepare Identities and Resources

### 1. Prepare the Resource Group

Create or open `rg-gp-access-model`.

**Validation:** The resource group was available as the intended authorization scope.

### 2. Create the Test Storage Account

Create `stgpaccessmodel65662231` inside the project resource group.

**Validation:** The storage account deployed successfully.

### 3. Create the Security Group

Create the Microsoft Entra security group `gp-rg-readers65662231`.

**Validation:** The security group was available for role assignment.

### 4. Add the Test Identity

Add `Alexgp-65662231` to the security group.

**Validation:** The identity appeared in the group membership list.

---

## 🛡️ Exercise 2: Assign RBAC at Resource-Group Scope

### 1. Open Access Control

Open `rg-gp-access-model`, select **Access control (IAM)**, and start a new role assignment.

### 2. Select the Reader Role

Select the built-in Azure `Reader` role.

### 3. Assign the Role to the Group

Select `gp-rg-readers65662231` as the member and complete the assignment.

**Validation:** The group received `Reader` at `rg-gp-access-model` scope.

### 4. Verify the Assignment

| Field | Expected Value |
|---|---|
| Role | `Reader` |
| Member | `gp-rg-readers65662231` |
| Member type | Group |
| Scope | `rg-gp-access-model` |

**Validation:** IAM displayed the expected group-based assignment.

---

## ✅ Exercise 3: Validate Access, Audit, and Clean Up

### 1. Check Effective Access

Use **Check access** and search for `Alexgp-65662231`.

**Validation:** The identity inherited `Reader` through group membership.

### 2. Review the Audit Event

Open the resource group's **Activity log** and locate the role-assignment operation.

**Validation:** The successful role-assignment event was available for review.

### 3. Test Allowed Access

Sign in as the test identity in a separate private browser session and open the resource group and storage account.

**Validation:** Resource viewing was allowed.

### 4. Test Denied Access

Attempt to create a storage account in the resource group.

**Validation:** Resource creation was denied, confirming that write access was not granted.

### 5. Clean Up

Delete the project resource group, test identity, and security group after validation.

**Validation:** The temporary resources and identity objects were removed.

> [!WARNING]
> Resource and identity deletion can be permanent. Verify each selected object before confirming cleanup.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Resource group prepared | ✅ Passed |
| Test storage account created | ✅ Passed |
| Security group created | ✅ Passed |
| Test identity added to group | ✅ Passed |
| Reader role assigned to group | ✅ Passed |
| Assignment limited to resource-group scope | ✅ Passed |
| Assignment verified in IAM | ✅ Passed |
| Inherited access confirmed | ✅ Passed |
| Activity Log event reviewed | ✅ Passed |
| Resource viewing allowed | ✅ Passed |
| Resource creation denied | ✅ Passed |
| Resources and identities removed | ✅ Passed |

---

## 📚 Command Reference

This assignment was completed through the Azure portal.

| Goal | Azure Portal Path |
|---|---|
| Create a resource group | **Resource groups** → **Create** |
| Create a storage account | **Storage accounts** → **Create** |
| Create a security group | **Microsoft Entra ID** → **Groups** → **New group** |
| Add a group member | Security group → **Members** → **Add members** |
| Assign an Azure role | Resource group → **Access control (IAM)** → **Add role assignment** |
| Check effective access | Resource group → **Access control (IAM)** → **Check access** |
| Review audit activity | Resource group → **Activity log** |
| Delete resources | Resource group → **Delete resource group** |

---

## 🧰 Troubleshooting

### Add role assignment is unavailable

Confirm that the administrator identity can create role assignments at the selected scope.

### The group does not appear

Verify the active Microsoft Entra tenant, confirm the group exists, and search its exact name.

### Inherited access is missing

Confirm the user's membership, the assigned group, and the role-assignment scope. Sign out and sign back in to refresh the test session.

### The test identity can create resources

Review all effective assignments. Another role inherited from a broader scope may grant write access.

### The Activity Log event is difficult to locate

Filter by the relevant time, resource group, operation, and status without publishing tenant-specific identifiers.

---

## 🧠 Skills Demonstrated

- Microsoft Entra identity administration
- Security-group membership management
- Azure Role-Based Access Control
- Group-based authorization
- Resource-group-scoped role assignment
- Effective-access verification
- Inherited permission analysis
- Allowed-versus-denied testing
- Azure Activity Log review
- Least-privilege security design
- Secure credential handling
- Resource and identity cleanup

---

## 💡 Key Takeaways

1. **Group-based access improves manageability.** Membership changes can grant or remove access without rebuilding the RBAC assignment.
2. **Scope defines the authorization boundary.** Resource-group scope limited access to the required project resources.
3. **Reader enables visibility without management rights.** The test identity could inspect resources but could not create them.
4. **Authentication and authorization are separate.** Signing in did not grant unrestricted Azure permissions.
5. **IAM checks and user testing complement each other.** The access path and actual behavior were both validated.
6. **Audit records support accountability.** The Activity Log recorded the role-assignment operation.
7. **Cleanup includes identities and groups.** Temporary authorization objects should be removed with cloud resources.

---

## ☑️ Completion Checklist

- [x] Prepared `rg-gp-access-model`
- [x] Created `stgpaccessmodel65662231`
- [x] Created `gp-rg-readers65662231`
- [x] Added `Alexgp-65662231` to the group
- [x] Assigned `Reader` at resource-group scope
- [x] Verified the assignment in IAM
- [x] Confirmed inherited effective access
- [x] Reviewed the Activity Log event
- [x] Tested resource viewing
- [x] Confirmed resource creation was denied
- [x] Removed the project resources and identities
- [x] Confirmed cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical cloud-security and Azure-administration portfolio, demonstrating identity governance, scoped authorization, least-privilege validation, auditing, and responsible cleanup.

---

## 🙏 Acknowledgements

This guided project was completed as part of the **Mentor Pilot Program**. Mentor supported the learning experience by helping with lab navigation, instruction comprehension, and troubleshooting.

Official references:

- [Azure RBAC overview](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)
- [Understand Azure RBAC scope](https://learn.microsoft.com/en-us/azure/role-based-access-control/scope-overview)
- [Azure built-in roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)
- [Assign Azure roles using the portal](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal)

---

## ⚖️ Disclaimer

This repository is an educational record of a completed guided lab in a temporary Microsoft Learn or Skillable environment. It is not a production-ready identity architecture and does not replace official Microsoft documentation, organizational policy, or professional security guidance. Azure services, interfaces, roles, pricing, limits, and features may change.

Passwords, Temporary Access Pass codes, access tokens, keys, subscription identifiers, tenant identifiers, and temporary credentials are intentionally excluded. Production implementations require additional review for privileged access, access reviews, monitoring, log retention, group ownership, expiration, separation of duties, and automation.

---

<div align="center">

### 🎉 Lab Completed Successfully

**Azure least privilege: scoped, inherited, audited, tested, and responsibly removed.**

Made with curiosity, care, and a commitment to responsible cloud engineering.  

**Wadondera A. Collins**

</div>
