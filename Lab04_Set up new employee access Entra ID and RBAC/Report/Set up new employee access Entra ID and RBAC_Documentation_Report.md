<div align="center">

# Azure RBAC Least-Privilege Access Model

## Identity and Access Management Technical Report

**Prepared by:** Wadondera A. Collins  
**Programme:** ICDFA Trainee | Cohort 11  
**Specialization:** Cloud Security Engineering  
**Platform:** Microsoft Azure  
**Project Focus:** Microsoft Entra ID, Azure RBAC, Identity Governance, and Least Privilege  
**Assignment Status:** Completed

</div>

---

## Executive Brief

This report documents the implementation and validation of a group-based least-privilege access model in Microsoft Azure. A Microsoft Entra security group was used as the authorization boundary, the built-in Azure `Reader` role was assigned at resource-group scope, and a test identity inherited read-only access through security-group membership.

The model was validated through Azure Access Control (IAM), the Azure Activity Log, and an isolated user session. The test identity could view the protected resources but could not create a new storage account. This positive and negative testing confirmed that read access was granted while write access remained denied.

> **Security notice:** Temporary credentials, passwords, Temporary Access Pass codes, tenant-specific secrets, and other sensitive authentication values are intentionally excluded.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Executive Summary](#executive-summary)
3. [Project Objectives](#project-objectives)
4. [Professional Value](#professional-value)
5. [Skills Demonstrated](#skills-demonstrated)
6. [Technologies and Tools Used](#technologies-and-tools-used)
7. [Lab Environment](#lab-environment)
8. [Access Model Architecture](#access-model-architecture)
9. [Repository Structure](#repository-structure)
10. [Methodology](#methodology)
11. [Implementation Narrative](#implementation-narrative)
12. [Professional Evidence and Analysis](#professional-evidence-and-analysis)
13. [Validation Matrix](#validation-matrix)
14. [Security and Governance Analysis](#security-and-governance-analysis)
15. [Challenges and Lessons Learned](#challenges-and-lessons-learned)
16. [Limitations and Next Steps](#limitations-and-next-steps)
17. [Cleanup and Cost Control](#cleanup-and-cost-control)
18. [Conclusion](#conclusion)
19. [Disclaimer](#disclaimer)
20. [Author](#author)

---

## Project Overview

The project implemented an Azure role-based access control model aligned with the principle of least privilege. The solution used a Microsoft Entra security group to manage authorization instead of assigning the Azure role directly to an individual user.

The security group received the Azure `Reader` role at the `rg-gp-access-model` resource-group scope. The test identity `Alexgp-65662231` inherited the role through membership in `gp-rg-readers65662231`.

The resulting model supported resource visibility without granting resource creation, modification, or deletion permissions. The assignment concluded with access testing, audit review, and removal of the temporary resources and identities.

---

## Executive Summary

A dedicated resource group and test storage account were created to provide a controlled Azure environment for RBAC validation. A Microsoft Entra security group was created and the test identity was added as a member.

The Azure `Reader` role was assigned to the group at resource-group scope. IAM role assignments were reviewed to confirm the selected principal, role, and scope. The **Check access** feature was then used to confirm that the test identity inherited the role through group membership.

The Azure Activity Log provided an audit record of the role-assignment operation. A private browser session was used to test the identity independently from the administrator session. The identity could view resources but could not complete a storage-account creation request.

The outcome demonstrated that authentication alone did not provide unrestricted Azure access. Authorization remained limited by the assigned role and scope.

---

## Project Objectives

1. Create a controlled resource group for RBAC testing.
2. Deploy a test storage account within the resource group.
3. Create a Microsoft Entra security group.
4. Add the test identity to the security group.
5. Assign the Azure `Reader` role to the group.
6. Apply the role assignment at resource-group scope.
7. Verify the assignment in Access Control (IAM).
8. Confirm inherited access through group membership.
9. Review the role-assignment audit event.
10. Validate allowed read access.
11. Validate denied write access.
12. Remove the temporary resources and identities.
13. Document the project without exposing secrets.

---

## Professional Value

### Business Value

- Supports scalable access management through group membership.
- Reduces direct user-level role assignments.
- Restricts access to a defined Azure scope.
- Simplifies onboarding and offboarding.
- Provides auditability for authorization changes.
- Reduces the risk of unauthorized modifications.

### Career Value

The assignment demonstrates practical experience relevant to Cloud Security Engineer, Azure Administrator, Identity and Access Management Analyst, Cloud Engineer, and Governance Specialist roles.

The completed work shows an ability to connect identity management, authorization scope, audit evidence, and practical permission testing into one defensible security control.

---

## Skills Demonstrated

### Identity and Access Management

- Microsoft Entra user administration
- Security-group creation and membership
- Group-based authorization
- Effective-access verification

### Azure Administration

- Resource-group provisioning
- Storage-account deployment
- Access Control (IAM)
- Azure role assignments
- Resource cleanup

### Cloud Security

- Least-privilege design
- RBAC scope selection
- Read-versus-write validation
- Authentication and authorization separation
- Secure handling of temporary access methods

### Governance and Auditing

- Azure Activity Log review
- Role-assignment traceability
- Access-path analysis
- Evidence-based validation

---

## Technologies and Tools Used

| Technology or Service | Project Use |
|---|---|
| Microsoft Azure | Cloud platform |
| Microsoft Entra ID | User, group, and authentication administration |
| Azure RBAC | Role-based authorization |
| Azure Resource Groups | Authorization scope and resource organization |
| Azure Storage Accounts | Test resource and denied-write validation |
| Access Control (IAM) | Role assignment and effective-access checks |
| Azure Activity Log | Audit trail review |
| Temporary Access Pass | Time-limited test-user authentication |
| Private browser session | Isolated permission validation |
| Azure Portal | Administrative and validation interface |

---

## Lab Environment

| Component | Configuration |
|---|---|
| Resource group | `rg-gp-access-model` |
| Test storage account | `stgpaccessmodel65662231` |
| Security group | `gp-rg-readers65662231` |
| Group purpose | Readers for the guided-project resource group |
| Test identity | `Alexgp-65662231` |
| Display name | Alex Guided Project |
| Assigned role | Azure `Reader` |
| Assignment scope | `rg-gp-access-model` |
| Authentication test | Temporary Access Pass in a private session |
| Required read outcome | Allowed |
| Required write outcome | Denied |

---

## Access Model Architecture

```text
Microsoft Entra Test Identity
             |
             | Group membership
             v
Security Group: gp-rg-readers65662231
             |
             | Azure Reader role
             v
Resource Group: rg-gp-access-model
             |
             +------------------------------+
             |                              |
             v                              v
View resources: Allowed          Create resources: Denied
```

The identity was not assigned the role directly. The group received the role, and the identity inherited it through membership. This design supports consistent access administration and limits permission sprawl.

---

## Repository Structure

```text
azure-rbac-least-privilege/
├── README.md
├── REPORT.md
├── images/
│   ├── Fig01 Resource Group Created.png
│   ├── Fig02 Storage Account Deployed.png
│   ├── Fig03 Security Group Created.png
│   ├── Fig04 User Added To Security Group.png
│   ├── Fig05 Reader Role Selected.png
│   ├── Fig06 Reader Role Assignment Verified.png
│   ├── Fig07 Inherited Reader Access.png
│   ├── Fig08 Activity Log Role Assignment.png
│   ├── Fig09 Reader Access Confirmed.png
│   ├── Fig10 Storage Creation Permission Denied.png
│   └── Fig11 Cleanup Verified.png
└── docs/
    └── validation-notes.md
```

The `README.md` should remain concise. This report provides the detailed methodology, evidence framework, validation analysis, governance observations, and improvement recommendations.

---

## Methodology

### Phase 1: Prepare the Environment

- Create the dedicated resource group.
- Deploy the test storage account.
- Confirm that the target resource exists.

### Phase 2: Establish the Identity Foundation

- Create the Microsoft Entra security group.
- Locate the pre-created test identity.
- Add the identity to the group.
- Confirm group membership.

### Phase 3: Configure Authorization

- Open the target resource group.
- Navigate to Access Control (IAM).
- Select the built-in `Reader` role.
- Assign the role to the security group.
- Review the completed role assignment.

### Phase 4: Validate Effective Access

- Use **Check access** for the test identity.
- Confirm inherited access through the group.
- Review the Activity Log for the role-assignment event.

### Phase 5: Test the User Experience

- Sign in through a private browser session.
- Confirm resource visibility.
- Attempt a storage-account creation.
- Confirm that the write action is denied.

### Phase 6: Clean Up

- Delete the resource group.
- Delete the test identity.
- Delete the security group.
- Disable Temporary Access Pass only if enabled specifically for the project.
- Verify removal of the temporary objects.

---

## Implementation Narrative

### Exercise 1: Create User and Group

The resource group `rg-gp-access-model` was created as the project boundary. The storage account `stgpaccessmodel65662231` provided a test resource within that scope.

The security group `gp-rg-readers65662231` was created in Microsoft Entra ID. The test identity `Alexgp-65662231` was added to the group. This completed the identity foundation required for group-based authorization.

### Exercise 2: Assign RBAC Role at Scope

The target resource group was opened in Azure Portal, and the built-in `Reader` role was assigned to the security group through Access Control (IAM).

The assignment was applied at resource-group scope. Role assignments were reviewed to confirm that `gp-rg-readers65662231` appeared with the `Reader` role.

### Exercise 3: Verify the Least-Privilege Model

The **Check access** feature was used to examine the test identity's effective permissions. The access path showed inheritance through the security group.

The Activity Log was reviewed for the `Create role assignment` operation. A separate browser session was then used to sign in as the test identity. The identity could view resources but could not create a new storage account.

This combination of configuration review, inherited-access inspection, audit verification, and hands-on testing provided a complete validation of the access model.

---

## Professional Evidence and Analysis

### Evidence Presentation Standard

Each screenshot should appear directly beneath the task it validates. Every figure should include:

1. A filename in the exact `Fig01 Descriptive Name.png` format.
2. A Markdown image link using the identical filename.
3. A concise caption describing only visible content.
4. An objective evidence analysis.
5. A short security or operational significance statement.

A screenshot must not be used to prove a result that is not visibly present. Configuration pages should not be described as successful deployment unless the image shows a completed state.

---

### Evidence 1: Resource Group Created

```markdown
![Fig01 Resource Group Created](images/Fig01%20Resource%20Group%20Created.png)
```

**Figure 1: The Azure Resource Groups page showing `rg-gp-access-model` as an existing resource group.**

**Visible evidence:** The screenshot should show the resource-group name in an existing-resource view or a completed deployment notification.

**Technical analysis:** The dedicated resource group establishes the Azure scope used for the RBAC assignment. A distinct scope prevents the test permission from applying broadly across the subscription.

**Security significance:** Scope restriction is a core least-privilege control. The smaller the legitimate scope, the lower the potential impact of excessive permissions.

---

### Evidence 2: Storage Account Deployed

```markdown
![Fig02 Storage Account Deployed](images/Fig02%20Storage%20Account%20Deployed.png)
```

**Figure 2: The deployed storage account `stgpaccessmodel65662231` within `rg-gp-access-model`.**

**Visible evidence:** The screenshot should show the storage-account name, deployment state or overview, and association with the correct resource group.

**Technical analysis:** The storage account provides a practical resource against which read and write authorization behavior can be tested.

**Security significance:** Testing against a controlled lab resource avoids applying experimental permissions to unrelated workloads.

---

### Evidence 3: Security Group Created

```markdown
![Fig03 Security Group Created](images/Fig03%20Security%20Group%20Created.png)
```

**Figure 3: Microsoft Entra ID showing the `gp-rg-readers65662231` security group.**

**Visible evidence:** The screenshot should show the exact group name and security-group classification.

**Technical analysis:** The security group operates as the authorization principal for the Azure role assignment.

**Security significance:** Group-based authorization is easier to manage and review than repeated direct assignments to individual users.

---

### Evidence 4: User Added to Security Group

```markdown
![Fig04 User Added To Security Group](images/Fig04%20User%20Added%20To%20Security%20Group.png)
```

**Figure 4: The test identity listed as a member of `gp-rg-readers65662231`.**

**Visible evidence:** The screenshot should show the group-membership view and the test identity.

**Technical analysis:** Group membership creates the inheritance path through which the user receives the Azure role.

**Security significance:** Removing the user from the group would remove the inherited authorization without changing the role assignment itself.

---

### Evidence 5: Reader Role Selected

```markdown
![Fig05 Reader Role Selected](images/Fig05%20Reader%20Role%20Selected.png)
```

**Figure 5: Azure IAM role-assignment workflow with the built-in `Reader` role selected.**

**Visible evidence:** The screenshot should show `Reader` as the selected role and the resource-group IAM context.

**Technical analysis:** The `Reader` role allows resource visibility without granting management operations.

**Security significance:** Selecting the least powerful role that satisfies the business requirement limits unauthorized change.

---

### Evidence 6: Reader Role Assignment Verified

```markdown
![Fig06 Reader Role Assignment Verified](images/Fig06%20Reader%20Role%20Assignment%20Verified.png)
```

**Figure 6: IAM role assignments showing `gp-rg-readers65662231` with the `Reader` role.**

**Visible evidence:** The screenshot should show the principal, role, and resource-group assignment context.

**Technical analysis:** This confirms that the role was assigned to the group rather than directly to the user.

**Security significance:** Principal, role, and scope must all be reviewed because the role name alone does not define the complete authorization model.

---

### Evidence 7: Inherited Reader Access

```markdown
![Fig07 Inherited Reader Access](images/Fig07%20Inherited%20Reader%20Access.png)
```

**Figure 7: IAM Check access showing the test identity inheriting `Reader` through the security group.**

**Visible evidence:** The screenshot should show the test identity, inherited role, and group-based assignment path.

**Technical analysis:** The result demonstrates that Azure evaluates group membership when calculating effective access.

**Security significance:** Effective-access validation confirms the user's practical permissions rather than relying only on configuration assumptions.

---

### Evidence 8: Activity Log Role Assignment

```markdown
![Fig08 Activity Log Role Assignment](images/Fig08%20Activity%20Log%20Role%20Assignment.png)
```

**Figure 8: Azure Activity Log showing the `Create role assignment` event.**

**Visible evidence:** The screenshot should show the operation name, event time, status, and initiating account where visible.

**Technical analysis:** The Activity Log provides a traceable record of the authorization change.

**Security significance:** Audit evidence supports accountability, incident review, governance, and compliance investigations.

---

### Evidence 9: Reader Access Confirmed

```markdown
![Fig09 Reader Access Confirmed](images/Fig09%20Reader%20Access%20Confirmed.png)
```

**Figure 9: The test identity viewing the target resource group or its contained resources.**

**Visible evidence:** The screenshot should show the test-user session and successful resource visibility without exposing authentication secrets.

**Technical analysis:** This positive test confirms that the assigned role supports the required read operation.

**Security significance:** A valid least-privilege design must grant required access, not merely deny unwanted actions.

---

### Evidence 10: Storage Creation Permission Denied

```markdown
![Fig10 Storage Creation Permission Denied](images/Fig10%20Storage%20Creation%20Permission%20Denied.png)
```

**Figure 10: Azure rejecting the test identity's storage-account creation attempt because of insufficient permissions.**

**Visible evidence:** The screenshot should show the permission error or failed authorization result. Temporary authentication information must not be visible.

**Technical analysis:** The failed write attempt demonstrates that the `Reader` role did not grant resource-creation permissions.

**Security significance:** Negative testing provides direct evidence that privilege boundaries are enforced.

---

### Evidence 11: Cleanup Verified

```markdown
![Fig11 Cleanup Verified](images/Fig11%20Cleanup%20Verified.png)
```

**Figure 11: Azure and Microsoft Entra views confirming removal of the temporary project objects.**

**Visible evidence:** Cleanup should show that the resource group, test identity, and security group no longer appear. Use separate figures if one screenshot cannot prove all three results.

**Technical analysis:** Cleanup removes temporary resources, assignments, and identities that are no longer required.

**Security significance:** Orphaned accounts and groups can create unnecessary exposure. Resource cleanup also prevents avoidable cloud charges.

---

## Validation Matrix

| Control Objective | Validation Method | Expected Result | Status |
|---|---|---|---|
| Group exists | Microsoft Entra group review | Security group visible | Completed |
| User belongs to group | Membership review | Test identity listed | Completed |
| Group has `Reader` role | IAM role assignments | Group and role visible | Completed |
| Scope is restricted | IAM scope review | Resource-group scope | Completed |
| User inherits access | Check access | Inherited `Reader` shown | Completed |
| RBAC change is auditable | Activity Log review | Create role assignment event | Completed |
| Read operation succeeds | Private-session test | Target resources visible | Completed |
| Write operation fails | Storage creation test | Permission denied | Completed |
| Temporary objects removed | Cleanup verification | Objects absent | Completed |

---

## Security and Governance Analysis

### Least Privilege

The identity received only the access needed to view the target resources. No write-capable role was assigned.

### Group-Based Authorization

The role assignment targeted a security group. User access could therefore be managed through membership without changing the Azure role assignment.

### Scope Control

The assignment applied at resource-group scope, reducing the access boundary compared with a subscription-level assignment.

### Authentication versus Authorization

Temporary Access Pass allowed the test identity to authenticate. Azure RBAC independently determined the actions available after sign-in.

### Auditability

The Activity Log recorded the role-assignment event, supporting traceability and accountability.

### Defense Through Validation

Configuration review alone was not considered sufficient. Effective-access review, read testing, denied-write testing, and audit review collectively provided stronger assurance.

---

## Challenges and Lessons Learned

- Identity and role changes may require a portal refresh before appearing.
- Role, principal, and scope must be evaluated together.
- Separate-session testing prevents administrator permissions from affecting results.
- Both successful and denied operations should be tested.
- Temporary authentication values must never appear in portfolio evidence.
- Cleanup is part of the security lifecycle, not an optional final step.

---

## Limitations and Next Steps

### Current Limitations

- The project was completed in a temporary lab tenant.
- The implementation used one test identity and one group.
- Screenshots were not supplied with this revision, so the evidence section defines exact attachment requirements rather than claiming visual verification.
- Production access review, alerting, and identity lifecycle automation were outside the assignment scope.

### Recommended Next Steps

- Attach screenshots using the exact filenames defined above.
- Redact sensitive identifiers and all authentication secrets.
- Introduce Microsoft Entra access reviews.
- Evaluate Privileged Identity Management for time-bound elevated access.
- Define RBAC assignments through Bicep or Terraform.
- Configure alerts for sensitive role-assignment changes.
- Document group owners, review frequency, and expiration requirements.

---

## Cleanup and Cost Control

The resource group, test resources, test identity, and security group were removed after validation. Temporary Access Pass should only be disabled if the policy was enabled specifically for this project.

Cleanup reduced unnecessary cloud consumption and removed temporary identity objects that were no longer required.

---

## Conclusion

The project successfully implemented a group-based Azure RBAC model aligned with least-privilege principles. The test identity inherited the `Reader` role through Microsoft Entra security-group membership at resource-group scope.

The user-level validation confirmed that read access worked and write access remained denied. IAM effective-access review and Activity Log analysis added configuration and audit assurance to the practical permission tests.

The assignment demonstrated hands-on capability in Microsoft Entra administration, Azure RBAC, permission inheritance, scope control, audit review, temporary authentication, positive and negative testing, cleanup, and professional evidence design.

This report is intentionally distinct from the GitHub `README.md`. The README introduces the project, while this report provides the full technical narrative, evidence standard, control analysis, validation matrix, governance considerations, limitations, and recommendations.

---

## Disclaimer

This project was completed in a temporary Microsoft Learn or Skillable lab environment for educational and portfolio purposes. Azure interfaces, tenant policies, resource behavior, and available features may differ in other environments.

No passwords, Temporary Access Pass codes, or temporary sign-in credentials should be committed to the repository.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
Azure Identity and Access Management Project Documentation
