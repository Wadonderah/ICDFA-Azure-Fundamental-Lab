<div align="center">

# Secure External File Exchange with Azure Blob Storage

## Lab Documentation Report

**Prepared by:** Wadondera A. Collins  
**Programme:** ICDFA, Cloud Security Engineering, Cohort 11  
**Environment:** Microsoft Azure through Skillable Cloud Slice  
**Completion date:** 29 September 2026  
**Document type:** Technical implementation and validation report

</div>

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Executive Summary](#2-executive-summary)
3. [Objectives](#3-objectives)
4. [Professional Value](#4-professional-value)
5. [Skills Demonstrated](#5-skills-demonstrated)
6. [Tools and Environment](#6-tools-and-environment)
7. [Lab Architecture](#7-lab-architecture)
8. [Implementation Methodology](#8-implementation-methodology)
9. [Evidence and Technical Analysis](#9-evidence-and-technical-analysis)
10. [Results and Validation](#10-results-and-validation)
11. [Security Observations](#11-security-observations)
12. [Limitations and Next Steps](#12-limitations-and-next-steps)
13. [Resource Cleanup](#13-resource-cleanup)
14. [Conclusion](#14-conclusion)
15. [Disclaimer](#15-disclaimer)

---

## 1. Project Overview

This project implemented a controlled external file-sharing workflow with Azure Blob Storage. A private blob container was used to hold a partner report. Temporary read access was granted through a Shared Access Signature (SAS), validated from an unauthenticated InPrivate browser session, and then revoked. A lifecycle management rule was also enabled to support automated deletion of aging files.

The implementation focused on four security principles:

- **Private by default:** the blob could not be accessed anonymously.
- **Limited delegation:** external access was restricted to a time-bound read operation.
- **Revocable access:** the stored access policy was removed when partner access was no longer required.
- **Lifecycle governance:** a storage rule was enabled to manage older shared files automatically.

---

## 2. Executive Summary

The lab successfully demonstrated a secure partner file-exchange pattern in Microsoft Azure. The `monthly-report.txt` object was stored in the private `partner-drop` container within the `stgpfilexchg65667740` storage account. Direct access to the blob returned the `PublicAccessNotPermitted` error, confirming that anonymous public access was unavailable.

A read-only SAS was then generated and tested. The SAS URL displayed the expected report contents in an InPrivate browser without an interactive Azure sign-in. Following validation, the stored access policy was deleted, and the Azure portal showed no remaining stored access policies. The `delete-shared-files` lifecycle management rule was enabled for block blobs. Finally, the `rg-gp-file-exchange` resource group was deleted, completing the cleanup process.

The evidence collectively demonstrates secure storage configuration, delegated access testing, policy revocation, lifecycle governance, and responsible resource cleanup.

---

## 3. Objectives

The project objectives were to:

1. Create an Azure storage environment for external file exchange.
2. Configure a private container that blocks anonymous access.
3. Upload a sample partner report to Azure Blob Storage.
4. Create a stored access policy for controlled read access.
5. Generate and test a SAS URL.
6. Compare unauthorized direct access with authorized SAS access.
7. Revoke delegated access by deleting the stored access policy.
8. Configure a lifecycle management rule for older files.
9. Remove all project resources after validation.

---

## 4. Professional Value

This project reflects tasks commonly associated with cloud security engineering and Azure administration. The implementation shows the ability to protect cloud-hosted data, validate access boundaries, apply temporary authorization, revoke external access, retain audit-ready evidence, and clean up temporary resources.

The strongest portfolio value is the end-to-end validation. The report does not only record configuration screens. The evidence shows both sides of the security control: unauthorized access was denied, while the approved SAS-based access path displayed the intended file.

---

## 5. Skills Demonstrated

- Azure Storage account administration
- Azure Blob Storage container management
- Private object storage configuration
- Shared Access Signature generation and testing
- Stored access policy administration
- Access revocation
- InPrivate browser security testing
- Azure lifecycle management configuration
- Resource-group cleanup
- Least-exposure and time-bound access principles
- Screenshot-based technical evidence collection
- Security-focused documentation

---

## 6. Tools and Environment

| Component | Version or Configuration | Use in the Project |
|---|---|---|
| Microsoft Azure Portal | Cloud service; build number not visible in the evidence | Created and managed storage, policies, lifecycle rules, and cleanup |
| Azure Storage | Storage account `stgpfilexchg65667740` | Hosted the blob container and report file |
| Azure Blob Storage | Block blob in private container | Stored `monthly-report.txt` |
| Azure SAS | Read permission; HTTPS selected in the visible generation screen | Provided delegated access to the report |
| Stored Access Policy | `partner-read-policy` | Controlled the delegated access configuration |
| Lifecycle Management | Enabled rule `delete-shared-files` | Applied automated data-lifecycle governance |
| Microsoft Edge | InPrivate browsing; version not visible | Tested direct and SAS-based access |
| Skillable Cloud Slice | Version not provided | Supplied the temporary Azure lab environment |
| SEA-Dev Lab VM | Windows environment; edition/build not visible | Accessed the portal and browser testing session |

> Version numbers not shown by the lab or screenshots are recorded as **not provided** rather than estimated.

---

## 7. Lab Architecture

```text
Resource group: rg-gp-file-exchange
└── Storage account: stgpfilexchg65667740
    ├── Blob container: partner-drop
    │   └── Blob: monthly-report.txt
    ├── Stored access policy: partner-read-policy
    ├── SAS-based read access
    └── Lifecycle rule: delete-shared-files
```

### Access Flow

```text
Unauthenticated direct URL
        │
        └── Denied: PublicAccessNotPermitted

Approved SAS URL
        │
        └── Read access to monthly-report.txt

Stored access policy removed
        │
        └── Policy-controlled access path revoked
```

---

## 8. Implementation Methodology

### Phase 1: Storage Preparation

A dedicated Azure resource group and storage account were used to isolate the lab. The `partner-drop` container was configured for private file exchange, and `monthly-report.txt` was uploaded as a block blob.

### Phase 2: Delegated Access Configuration

The `partner-read-policy` stored access policy was configured for time-bound access. A SAS token and blob SAS URL were generated for `monthly-report.txt`, with read permission and HTTPS selected in the visible configuration.

### Phase 3: Positive and Negative Testing

The blob was tested from an InPrivate browser session:

- The direct URL without SAS authorization returned an access error.
- The SAS URL displayed the report content successfully.

This paired test confirmed that access depended on the delegated authorization path rather than public container exposure.

### Phase 4: Access Revocation

The stored access policy was deleted from the container. The resulting Access policy page displayed no stored access policy entries, providing configuration-level evidence of policy removal.

### Phase 5: Lifecycle Governance

The `delete-shared-files` lifecycle management rule was enabled for block blobs. This established an automated storage-governance control for the file-exchange workflow.

### Phase 6: Cleanup

The `rg-gp-file-exchange` resource group was deleted. The portal notification confirmed the deletion, and the resource-group list showed no resource groups to display in the temporary lab subscription view.

---

## 9. Evidence and Technical Analysis

### 9.1 Private Container and Uploaded Report

<img width="1094" height="565" alt="Fig01_Private_Partner_Container" src="https://github.com/user-attachments/assets/67e3399e-bae6-4d0e-981b-c32fd83c01b4" />


**Figure 1: Private partner container with `monthly-report.txt`.**

The screenshot shows the `partner-drop` container in the `stgpfilexchg65667740` storage account. The container contains one object, `monthly-report.txt`, shown as a block blob with a visible size of 136 B and an available lease state. This evidence confirms that the report file was uploaded and remained present in the container.

### 9.2 Stored Access Policy Configuration

<img width="1091" height="560" alt="Fig02_Stored_Access_Policy" src="https://github.com/user-attachments/assets/9703a6db-539b-4fcc-8fb7-3e0fdfbf68dd" />


**Figure 2: Stored access policy configured for the partner container.**

The Access policy page shows a stored policy entry whose identifier is visibly truncated as `partner-rea...`. The row displays a start time, an expiry time, and the available policy actions. The open options menu includes **Edit** and **Delete**, confirming that the stored policy existed and could be administered before revocation.

### 9.3 SAS Token and URL Generation

<img width="1093" height="555" alt="Fig03_Direct_Access_Denied" src="https://github.com/user-attachments/assets/60f4d50a-a71d-4532-8fe7-26c5c402fe74" />


**Figure 3: SAS configuration and generated access URL for `monthly-report.txt`.**

The screenshot shows the SAS generation interface for `monthly-report.txt`. Visible settings include **Read** permission and **HTTPS only**. The interface also displays generated token and URL fields, confirming that a delegated link was produced for the blob.

> **Required redaction:** The original screenshot exposes a SAS token and full SAS URL. Before publishing the evidence to GitHub, blur or cover both generated-value fields. A SAS URL must be treated as a secret while valid.

### 9.4 Direct Access Denied

<img width="1094" height="612" alt="Fig04_SAS_Access_Validation" src="https://github.com/user-attachments/assets/0b3ddd6d-1630-479f-accf-bca6d206d730" />


**Figure 4: Anonymous direct access blocked by the storage account.**

The InPrivate browser displays an XML error response with the code `PublicAccessNotPermitted` and the message `Public access is not permitted on this storage account.` The address bar shows the direct blob path without a visible SAS query string. This is strong negative-test evidence that the report was not publicly accessible.

### 9.5 SAS Access Validation

<img width="1095" height="644" alt="Fig05_Stored_Access_Policy_Deleted" src="https://github.com/user-attachments/assets/dd10ba93-052d-4b3e-a3a6-05e650a7187c" />


**Figure 5: Successful read access through the SAS URL.**

The InPrivate browser displays the contents of `monthly-report.txt`, including the report heading and the expected operational fields. A SAS query string is visible in the address bar. This confirms that the delegated URL provided read access to the private blob without requiring an interactive Azure portal session.

> **Required redaction:** Blur the SAS query string in the browser address bar before publishing this screenshot.

### 9.6 Stored Access Policy Deleted

<img width="1093" height="432" alt="Fig06_Lifecycle_Management_Rule" src="https://github.com/user-attachments/assets/b83ff6cb-bd90-415c-ab5d-9bfbe56d7e3e" />


**Figure 6: Access policy page after stored policy removal.**

The `partner-drop | Access policy` page shows **No results** under Stored access policies. This confirms that no stored policy entry remained visible after the deletion action. The absence of a stored policy is the configuration evidence for the access-revocation stage.

### 9.7 Lifecycle Management Rule

<img width="1093" height="563" alt="Fig07_Resource_Group_Deletion" src="https://github.com/user-attachments/assets/9dd1d58c-8ab7-4b83-8f64-144c9459781e" />


**Figure 7: Enabled `delete-shared-files` lifecycle rule.**

The Lifecycle management page for `stgpfilexchg65667740` lists the `delete-shared-files` rule with status **Enabled** and blob type **Block**. This confirms that an automated lifecycle control was configured for block-blob data.

### 9.8 Resource Group Deletion and Cleanup

<img width="1095" height="556" alt="Fig08_Resource_Cleanup_Validation" src="https://github.com/user-attachments/assets/0b99f8a6-d5b6-4bb3-a9e8-03b359899a5f" />


**Figure 8: Deletion confirmation for `rg-gp-file-exchange`.**

The Azure portal notification states that the `rg-gp-file-exchange` resource group was deleted. The Resource groups view simultaneously shows **No resource groups to display**, while the selected resource-group pane contains no matching resources. This provides final evidence that the temporary project environment was removed.

---

## 10. Results and Validation

| Validation Requirement | Evidence | Result |
|---|---|---|
| Partner report exists in the private container | Figure 1 | Passed |
| Stored access policy was created | Figure 2 | Passed |
| SAS token and URL were generated | Figure 3 | Passed |
| Direct anonymous access was blocked | Figure 4 | Passed |
| SAS-based read access displayed the report | Figure 5 | Passed |
| Stored access policy was removed | Figure 6 | Passed |
| Lifecycle rule was enabled | Figure 7 | Passed |
| Resource group was deleted | Figure 8 | Passed |

### Final Validation Checklist

- [x] `partner-drop` contained `monthly-report.txt`.
- [x] A stored access policy was visible before revocation.
- [x] A read-only SAS access path was generated.
- [x] Direct blob access returned `PublicAccessNotPermitted`.
- [x] The SAS URL displayed the expected report contents.
- [x] The stored access policy list showed no results after deletion.
- [x] The lifecycle rule was enabled for block blobs.
- [x] Azure confirmed deletion of `rg-gp-file-exchange`.

---

## 11. Security Observations

### Effective Controls

- The direct URL was denied, which verified that the blob was not anonymously public.
- Delegated access was limited to the SAS path rather than opening the container publicly.
- HTTPS-only access was selected in the SAS generation interface.
- Policy removal provided a controlled revocation step.
- Lifecycle management introduced automated data-governance capability.
- Resource cleanup reduced unnecessary cloud-resource exposure and cost risk.

### Evidence-Handling Risk

Two screenshots contain sensitive authorization material:

1. The SAS generation screenshot exposes the generated token and URL.
2. The successful access screenshot exposes the SAS query string in the address bar.

Both screenshots must be redacted before the repository is made public. The redaction should cover only the secret values while preserving the settings and validation evidence.

---

## 12. Limitations and Next Steps

### Limitations

- The screenshots do not display exact Azure Portal, browser, Skillable, or Windows version numbers.
- The lifecycle screenshot confirms that the rule is enabled but does not display the detailed prefix and age conditions.
- The policy-deletion screenshot proves that the stored policy is absent, but a separate post-deletion browser error is not included.
- The SAS generation screenshot shows `Stored access policy: None`; therefore, that specific screenshot demonstrates SAS generation but does not independently prove that the generated SAS was bound to `partner-read-policy`.

### Recommended Next Steps

- Capture the lifecycle-rule details showing the `partner-drop/` prefix, age condition, and delete action.
- Capture the browser authorization error after stored-policy deletion to provide direct revocation evidence.
- Capture SAS generation with `partner-read-policy` visibly selected if policy-linked SAS generation is an assessment requirement.
- Redact all tokens, signatures, account identifiers, and temporary credentials before publication.
- In a production design, evaluate Microsoft Entra-backed user delegation SAS and centralized monitoring requirements.

---

## 13. Resource Cleanup

Cleanup was completed by deleting the `rg-gp-file-exchange` resource group. The Azure portal displayed a successful deletion notification, and no resource groups remained visible in the lab subscription view. This action removed the temporary storage environment created for the exercise.

Cleanup is an important closeout activity because temporary cloud resources can create avoidable cost, security exposure, and administrative clutter if left active.

---

## 14. Conclusion

The project successfully implemented and validated a secure Azure Blob Storage file-exchange workflow. The captured evidence proves that the report existed in a private container, anonymous direct access was rejected, delegated SAS access succeeded, the stored access policy was removed, lifecycle management was enabled, and the temporary Azure resource group was deleted.

The completed work demonstrates practical cloud-security skills in data protection, temporary access delegation, negative and positive access testing, revocation, lifecycle governance, evidence handling, and environment cleanup.

---

## 15. Disclaimer

This document records work completed in a temporary educational Azure lab environment. The configuration and evidence are intended for training and portfolio purposes and should not be treated as a production deployment standard without additional organizational review.

Passwords, Temporary Access Pass codes, SAS tokens, SAS URLs, tenant credentials, and other secrets must not be committed to a public repository. Screenshots that expose authorization material must be redacted before publication. Product interfaces and service behavior may change, so current Microsoft documentation should be reviewed before implementing a similar solution in a live environment.

---

## Evidence Filename Map

Rename and arrange the uploaded screenshots according to their visible contents before adding the report to GitHub:

```text
evidence/
├── Fig01 Private Partner Container.png
├── Fig02 Stored Access Policy.png
├── Fig03 SAS Token And URL Generated.png
├── Fig04 Direct Access Denied.png
├── Fig05 SAS Access Validation.png
├── Fig06 Stored Access Policy Deleted.png
├── Fig07 Lifecycle Management Rule.png
└── Fig08 Resource Group Deletion And Cleanup.png
```

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
