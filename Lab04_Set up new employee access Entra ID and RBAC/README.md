<div align="center">

# Azure RBAC Least-Privilege Access Model

### Microsoft Entra ID • Azure RBAC • Identity Governance • Access Validation

**Completed Mentor Pilot Program Assignment**

**Author:** Wadondera A. Collins  
**Programme:** ICDFA Trainee | Cohort 11  
**Specialization:** Cloud Security Engineering  
**Platform:** Microsoft Azure

</div>

---

## Project Overview

This project demonstrates the implementation and validation of a least-privilege access model in Microsoft Azure. The completed assignment focused on creating an identity and security group in Microsoft Entra ID, assigning the Azure `Reader` role at resource-group scope, validating inherited access, testing permitted and denied actions, reviewing the RBAC audit trail, and removing the lab resources and identities after completion.

The access model was designed around group-based authorization. Instead of assigning permissions directly to an individual account, the `Reader` role was assigned to a security group. The test user inherited read-only access through group membership, demonstrating a scalable and manageable approach to Azure access control.

> **Security notice:** Temporary credentials, passwords, Temporary Access Pass codes, subscription identifiers, and other sensitive lab values are intentionally excluded from this repository.

---

## Project Goal

Build and verify an Azure role-based access control model in which a test user can view resources inside a designated resource group but cannot create or modify resources.

```text
Test User
    |
    | Member of
    v
Security Group
    |
    | Reader role assignment
    v
Azure Resource Group
    |
    +--> View resources: Allowed
    |
    +--> Create resources: Denied
```

---

## Assignment Exercises

### 1. Create User and Group

- Prepared a dedicated Azure resource group.
- Created a test storage account to provide a resource for access validation.
- Created a Microsoft Entra security group.
- Used the pre-created test user account.
- Added the test user to the security group.

### 2. Assign RBAC Role at Scope

- Opened the target resource group.
- Assigned the Azure `Reader` role to the security group.
- Applied the assignment at resource-group scope.
- Verified the assignment through **Access control (IAM)**.

### 3. Verify the Least-Privilege Model

- Checked the test user's effective access.
- Confirmed that the `Reader` role was inherited through group membership.
- Reviewed the role-assignment event in the Azure Activity Log.
- Signed in using the test identity.
- Confirmed that resource viewing was allowed.
- Confirmed that resource creation was denied.
- Removed the lab resources and identities after validation.

---

## Objectives

- Create a controlled Azure environment for RBAC testing.
- Implement group-based permission management in Microsoft Entra ID.
- Assign the `Reader` role at the correct Azure scope.
- Confirm that permissions are inherited through security-group membership.
- Validate allowed and denied actions using a test identity.
- Review the Azure audit trail for the role assignment.
- Demonstrate the principle of least privilege.
- Remove temporary resources and identities after completing the assignment.

---

## Key Resources

| Resource | Purpose |
|---|---|
| `rg-gp-access-model` | Isolated resource group used as the RBAC assignment scope |
| `stgpaccessmodel65662231` | Test storage account used for access validation |
| `gp-rg-readers65662231` | Security group assigned the `Reader` role |
| `Alexgp-65662231` | Test identity used to validate inherited access |
| Azure `Reader` role | Grants read access without resource-management permissions |

---

## Technologies and Services

- Microsoft Azure
- Microsoft Entra ID
- Azure Role-Based Access Control
- Azure Resource Groups
- Azure Storage Accounts
- Azure Access Control (IAM)
- Azure Activity Log
- Temporary Access Pass authentication
- InPrivate or Incognito browser testing

---

## Skills Demonstrated

### Identity and Access Management

- Microsoft Entra user and group administration
- Security-group membership management
- Group-based permission assignment
- Effective-access verification

### Azure Administration

- Resource-group administration
- Storage-account provisioning
- Role assignment at resource-group scope
- Azure portal navigation

### Cloud Security

- Least-privilege implementation
- RBAC scope selection
- Separation of identity and authorization
- Read-versus-write permission validation
- Authentication-method awareness

### Governance and Auditing

- Azure Activity Log review
- Role-assignment verification
- Access-path documentation
- Resource and identity cleanup

---

## Implementation Summary

### Identity Foundation

A Microsoft Entra security group was created to act as the permission-management boundary. The test user was added to the group so that access could be managed through membership rather than through a direct user-level role assignment.

### Scoped Role Assignment

The built-in `Reader` role was assigned to the security group at the `rg-gp-access-model` resource-group scope. This limited the assignment to resources within the selected resource group and avoided unnecessary subscription-wide access.

### Access Verification

The Azure **Check access** feature was used to confirm that the test user inherited the `Reader` role through the security group. The Activity Log was reviewed to verify that Azure recorded the role-assignment operation.

### Least-Privilege Testing

The test identity was used in a separate browser session. The identity could view the resource group and its resources but could not create a new storage account. This behavior validated the intended read-only access model.

### Cleanup

The project resource group, test user, and security group were removed after validation. Temporary Access Pass configuration was only to be disabled if it had been enabled specifically for the project.

---

## Access Model

| Validation Scenario | Expected Result | Project Result |
|---|---|---|
| View the target resource group | Allowed | Confirmed |
| View resources inside the resource group | Allowed | Confirmed |
| Inherit access through security-group membership | Allowed | Confirmed |
| Create a storage account in the resource group | Denied | Confirmed |
| Modify or delete protected resources | Not granted by `Reader` | Least-privilege model maintained |

---

## Security Design Decisions

### Group-Based Access

Assigning permissions to a group simplifies onboarding and offboarding. Access can be granted or removed by changing group membership without recreating the RBAC assignment.

### Resource-Group Scope

The role was assigned at resource-group scope rather than subscription scope. This reduced the access boundary to the resources required for the assignment.

### Read-Only Role

The `Reader` role supported visibility without granting resource-creation or modification permissions. The denied storage-account creation test demonstrated that the test identity did not receive write access.

### Separate Test Session

A private browser session was used to validate the test identity independently from the administrator session. This prevented the administrator's permissions from affecting the access test.

---

## Validation Checklist

- [x] Dedicated resource group prepared
- [x] Test storage account created
- [x] Microsoft Entra security group created
- [x] Test user added to the security group
- [x] Azure `Reader` role assigned to the group
- [x] Role assignment scoped to the resource group
- [x] Group role assignment verified in IAM
- [x] User access checked through IAM
- [x] Inherited group access confirmed
- [x] Role-assignment activity reviewed
- [x] Test identity could view resources
- [x] Test identity could not create resources
- [x] Resource group removed
- [x] Test identity removed
- [x] Security group removed

---

## Project Results

The completed project established a working least-privilege access model in Azure. The test identity received read-only access through security-group membership at resource-group scope. Access validation showed that the identity could inspect the target resources while resource creation remained blocked.

This outcome demonstrated that:

- Group membership can be used to manage Azure permissions at scale.
- RBAC scope determines where access applies.
- The `Reader` role supports visibility without management permissions.
- Effective access can be verified through IAM.
- Role-assignment activity can be reviewed through Azure logging.
- Least privilege should be validated through both allowed and denied actions.

---

## Repository Structure

```text
azure-rbac-least-privilege/
├── README.md
├── REPORT.md
├── images/
│   └── project-evidence-screenshots.png
└── docs/
    └── validation-notes.md
```

> Screenshot evidence should be documented in the detailed `REPORT.md` and placed directly beneath the task supported by the visible content. Sensitive authentication values must be redacted before publication.

---

## Lessons Learned

- Azure permissions are easier to manage through security groups than through direct user assignments.
- Scope selection is central to least-privilege design.
- A successful sign-in does not imply unrestricted Azure access.
- Effective-access checks and real user testing provide complementary validation.
- Audit logs are essential for reviewing access-control changes.
- Cleanup is part of responsible cloud resource management.

---

## Recommended Improvements

For a production implementation, consider:

- Microsoft Entra Privileged Identity Management for time-bound privileged access
- Access reviews for recurring membership validation
- Administrative units for delegated identity administration
- Azure Policy for governance enforcement
- Diagnostic settings and centralized log retention
- Infrastructure as Code for repeatable RBAC deployment
- Clear naming, ownership, and expiration standards for security groups

These recommendations extend beyond the completed lab scope.

---

## Disclaimer

This project was completed in a temporary Microsoft Learn or Skillable lab environment for educational and portfolio-development purposes. Resource names, tenant settings, interface labels, and available features may differ in other Azure environments.

No passwords, Temporary Access Pass codes, function keys, or temporary lab sign-in credentials should be committed to this repository.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering
