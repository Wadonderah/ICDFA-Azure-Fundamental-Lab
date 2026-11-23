<div align="center">

# CCSE-102 Laboratory E01
## Resource Governance and Role-Based Access Control

**Technical Documentation and Evidence Report**

![Course](https://img.shields.io/badge/Course-CCSE--102-17365D?style=for-the-badge)
![Laboratory](https://img.shields.io/badge/Laboratory-E01-C65911?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Simulator](https://img.shields.io/badge/Environment-Offline_Simulator-2F5597?style=for-the-badge)

![Governance](https://img.shields.io/badge/Control-Resource_Governance-0078D4?style=flat-square)
![RBAC](https://img.shields.io/badge/Control-RBAC-5C2D91?style=flat-square)
![Least Privilege](https://img.shields.io/badge/Security-Least_Privilege-107C10?style=flat-square)
![Audit](https://img.shields.io/badge/Evidence-Audit_Trail-9C6500?style=flat-square)

**Governance configuration · Scoped access control · Denial validation · Change protection · Audit traceability**

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

</div>

---

## Document Control

| Field | Value |
|---|---|
| Course | CCSE-102: Azure Operations & Administration |
| Practical | Integrated Azure Operations, Administration and Cloud Security Laboratory |
| Laboratory | E01: Resource Governance and Role-Based Access Control |
| Assessment weighting | 20 marks |
| Student | Wadondera A. Collins |
| Cohort | CCSE Cohort 11, L1/S1 |
| Environment | WSL Ubuntu on Linux-compatible workstation |
| Runtime | Python 3.10 or later |
| Simulator | ICDFA `azlocal.py` offline Azure-style simulator, version 1.0 |
| Evidence date | 23 November 2026 |
| Document status | Laboratory evidence report |

---

## Executive Summary

Laboratory E01 evaluated resource governance and role-based access control using the ICDFA offline Azure-style administration simulator. The implementation created the simulated resource group `rg-icdfa-lab`, applied mandatory ownership and environment metadata, added a cost-centre tag, and confirmed a zero-finding governance baseline. A fictional `analyst` identity was then assigned the `Reader` role at the resource-group scope.

Permission testing showed that the analyst could perform a read check but could not perform a write check. Enforcement was validated through an actual attempted VM creation, which was denied with exit code `3`. A simulated resource lock was subsequently applied and shown to prevent a tag modification. After an authorized unlock, the governance tag was successfully added. The audit log recorded the permission checks, denied authorization, lock, unlock, and post-unlock tag operation.

The results demonstrate least-privilege access, administrative change protection, governance metadata control, and operational traceability. All cloud-style resources documented in this report are local simulated records rather than resources provisioned in Microsoft Azure.

---

## 1. Scope and Environment

### 1.1 Scope declaration

This laboratory was completed with the ICDFA-provided offline simulator. No Microsoft Azure tenant, Azure subscription, Azure credit, Azure CLI session, or Microsoft-hosted lab was used.

The following activities were simulated:

- Resource-group creation and management
- Resource tags and governance checks
- Role-based access assignments
- Permission decisions
- VM-creation authorization enforcement
- Resource locking and unlocking
- Audit-log generation

The following activities were real local operations:

- Executing Python commands in WSL Ubuntu
- Reading and writing simulator state on the local filesystem
- Capturing terminal evidence
- Preparing this documentation report

### 1.2 Laboratory package

The laboratory package was opened in Visual Studio Code through WSL Ubuntu. The visible package structure contained the required `guides`, `samples`, `scripts`, and `templates` directories together with `azlocal.py`, `START_HERE.md`, and `SYSTEM_REQUIREMENTS.txt`.

<img width="189" height="698" alt="Fig01 Laboratory Package Structure" src="https://github.com/user-attachments/assets/83b418df-980d-4027-b8b7-650e420c116d" />


**Figure 1. Laboratory Package Structure.** The extracted package contains the simulator and supporting laboratory directories required for implementation.

---

## 2. Objectives

Laboratory E01 was performed to:

1. Create a governed resource group with required tags.
2. Validate the required-tag policy baseline.
3. Add administrative metadata for cost allocation.
4. Assign Reader access at resource-group scope.
5. Validate permitted read and denied write decisions.
6. Prove RBAC enforcement through an actual denied operation.
7. Apply a resource lock and verify change prevention.
8. Remove the lock through an authorized action.
9. Verify an authorized post-unlock change.
10. Examine the audit trail for governance and authorization events.

---

## 3. Methodology

The laboratory followed a controlled sequence of configuration, validation, negative testing, remediation, and audit review:

1. Establish the resource group and required metadata.
2. Confirm initial governance compliance.
3. Extend governance metadata with a cost-centre tag.
4. Assign least-privilege Reader access.
5. Test expected access decisions.
6. Attempt an operation that the Reader role must not perform.
7. Apply a resource lock and attempt a prohibited change.
8. Unlock the resource and confirm normal administration resumes.
9. Review logged events to establish traceability.

Negative tests were treated as successful evidence when the security control produced the expected denial.

---

## 4. Implementation and Evidence

### 4.1 Resource-group creation

The resource group was created with the required owner and environment tags:

```bash
python3 azlocal.py group create rg-icdfa-lab \
  --owner Wadondera-A-Collins \
  --environment training
```

The simulator returned the resource group name `rg-icdfa-lab`, location `local-linux`, lock state `false`, environment `training`, and owner `Wadondera-A-Collins`. This confirmed successful creation and correct initial governance metadata.

<img width="411" height="195" alt="Fig02 Resource Group Creation" src="https://github.com/user-attachments/assets/f63ebf69-420d-4f72-9657-42c7d8d25975" />


**Figure 2. Resource Group Creation.** The resource group was created with both mandatory tags and began in an unlocked state.

### 4.2 Governance baseline validation

The group configuration and policy status were reviewed:

```bash
python3 azlocal.py group list
python3 azlocal.py policy
```

The group listing retained the correct owner and environment values. The policy result showed one checked resource, zero findings, and `simulation: true`. The absence of findings confirmed that the mandatory governance tags were present.

<img width="384" height="257" alt="Fig03 Resource Group Tags and Baseline Policy" src="https://github.com/user-attachments/assets/cb564f63-71aa-44f8-b338-88f0a4cde9b8" />


**Figure 3. Resource Group Tags and Baseline Policy.** The required-tag control passed with `findings_count` equal to `0`.

### 4.3 Additional cost-centre metadata

A cost-centre tag was added to improve administrative classification:

```bash
python3 azlocal.py group tag rg-icdfa-lab cost-centre CCSE102
python3 azlocal.py group list
```

The updated state displayed `cost-centre: CCSE102` while preserving the owner and environment tags. The result demonstrates that the resource group can be categorized for training cost allocation or organizational reporting.

<img width="463" height="320" alt="Fig04 Cost Centre Governance Tag" src="https://github.com/user-attachments/assets/d478faeb-865b-4fa3-8bd4-92d223880dd8" />


**Figure 4. Cost Centre Governance Tag.** The additional `cost-centre` metadata was applied without altering the existing mandatory tags.

### 4.4 Group-scoped Reader role assignment

The fictional analyst received the Reader role only at the target resource-group scope:

```bash
python3 azlocal.py access assign analyst Reader group:rg-icdfa-lab
python3 azlocal.py access list
```

The assignment output showed `analyst`, role `Reader`, and scope `group:rg-icdfa-lab`. The complete list also retained the default subscription-level assignments for `student-admin` and `auditor`.

<img width="488" height="318" alt="Fig05 Analyst Reader Role Assignment" src="https://github.com/user-attachments/assets/bd7b2363-d421-4481-b32b-60dfe6dae118" />


**Figure 5. Analyst Reader Role Assignment.** The analyst was restricted to Reader access for `rg-icdfa-lab` rather than receiving subscription-wide privileges.

### 4.5 Permission validation

The assigned permissions were tested directly:

```bash
python3 azlocal.py access check analyst read group:rg-icdfa-lab
python3 azlocal.py access check analyst write group:rg-icdfa-lab
```

The read decision returned `permitted: true`; the write decision returned `permitted: false`. The paired result validates that Reader access supports observation without configuration modification.

<img width="532" height="225" alt="Fig06 Reader Permission Validation" src="https://github.com/user-attachments/assets/5e88eb93-04dd-4ca2-b189-7af7980d23e7" />


**Figure 6. Reader Permission Validation.** The permission checks demonstrate least privilege at the assigned resource-group scope.

### 4.6 Enforced denial of an administrative operation

A real simulated administration attempt was performed under the analyst identity:

```bash
python3 azlocal.py --actor analyst vm create denied-demo --group rg-icdfa-lab
echo $?
```

The simulator returned `RBAC DENIED`, stating that the analyst lacked write permission on `group:rg-icdfa-lab`. The shell returned exit code `3`. This negative test confirms that the authorization decision was enforced during an attempted resource operation rather than existing only as a reported check.

<img width="557" height="91" alt="Fig07 RBAC Denied VM Creation" src="https://github.com/user-attachments/assets/0d36f0b8-8f70-4379-ab82-5770bf200cd9" />


**Figure 7. RBAC Denied VM Creation.** The expected failure demonstrates effective Reader-role enforcement. No `denied-demo` VM record was created.

### 4.7 Resource-lock enforcement

A resource-group lock was applied and then tested by attempting a tag change:

```bash
python3 azlocal.py group lock rg-icdfa-lab
python3 azlocal.py group tag rg-icdfa-lab test locked-change
```

The first operation set `locked: true`. The second operation failed with an error explaining that the simulated delete/read-only lock must be removed before changes. The existing cost-centre, environment, and owner tags remained visible.

<img width="540" height="213" alt="Fig08 Resource Lock Enforcement" src="https://github.com/user-attachments/assets/f11b4f45-d564-4bfd-a4f9-7272ecd693b5" />


**Figure 8. Resource Lock Enforcement.** The resource lock prevented configuration modification even though the default identity normally has write permission.

### 4.8 Authorized unlock and post-lock change

The group was unlocked, a governance tag was added, and the final group state was listed:

```bash
python3 azlocal.py group unlock rg-icdfa-lab
python3 azlocal.py group tag rg-icdfa-lab governance controlled
python3 azlocal.py group list
```

The output first changed the lock state to `false`. The subsequent tag command succeeded and added `governance: controlled`. The final listing retained `cost-centre: CCSE102`, `environment: training`, and `owner: Wadondera-A-Collins`.

<img width="382" height="489" alt="Fig09 Resource Unlock and Governance Tag" src="https://github.com/user-attachments/assets/892412da-40c2-4a30-a93e-e67b2a9af98a" />


**Figure 9. Resource Unlock and Governance Tag.** Normal authorized administration resumed only after the lock was removed.

### 4.9 Audit-log review

The most recent audit events were reviewed:

```bash
python3 azlocal.py monitor logs --limit 25
```

The visible events included:

- A successful analyst read permission check
- A successfully evaluated analyst write check with `permitted: false`
- A denied analyst authorization event for `write on group:rg-icdfa-lab`
- A successful `group-lock` event by `student-admin`
- A successful `group-unlock` event by `student-admin`
- A successful post-unlock `group-tag` event by `student-admin`

<img width="377" height="641" alt="Fig10 E01 Governance and RBAC Audit Log" src="https://github.com/user-attachments/assets/7480d700-927b-4a8b-b3eb-22f47cd5e17a" />


**Figure 10. E01 Governance and RBAC Audit Log.** The audit trail provides time-stamped attribution and outcomes for governance and authorization activities.

---

## 5. Results Summary

| Test | Expected outcome | Observed outcome | Status |
|---|---|---|---|
| Resource-group creation | Group created with owner and environment tags | `rg-icdfa-lab` created with correct tags | Pass |
| Baseline policy | No missing required-tag findings | `findings_count: 0` | Pass |
| Cost-centre tag | `CCSE102` added | Tag shown in group listing | Pass |
| Reader assignment | Analyst receives group-scoped Reader role | Assignment listed at `group:rg-icdfa-lab` | Pass |
| Read permission | Reader may read | `permitted: true` | Pass |
| Write permission | Reader may not write | `permitted: false` | Pass |
| Unauthorized VM creation | Operation denied | RBAC denial, exit code `3` | Pass |
| Lock enforcement | Configuration change blocked | Tag change rejected | Pass |
| Authorized unlock | Lock removed | `locked: false` | Pass |
| Post-unlock change | Governance tag accepted | `governance: controlled` | Pass |
| Audit review | Relevant activities recorded | Checks, denial, lock, unlock, and tag visible | Pass |

---

## 6. Security and Operational Analysis

### 6.1 Least privilege

The analyst was assigned Reader at the narrowest required scope, `group:rg-icdfa-lab`. The identity could read the group but could not write to it. This reduces the likelihood that a user requiring visibility could change resource configuration.

### 6.2 Defense against unauthorized administration

The denied VM-creation attempt shows enforcement at operation time. The shell exit code `3` provides additional technical evidence that the command failed because of authorization rather than because of an unrelated syntax or resource error.

### 6.3 Governance metadata

The owner and environment tags satisfied the simulator's required-tag policy. The cost-centre tag added administrative classification, while the governance tag documented the controlled final state. Consistent metadata supports ownership, reporting, accountability, and later automation.

### 6.4 Change protection

The resource lock blocked a tag update until an authorized unlock occurred. This demonstrates a control for preventing accidental or unauthorized configuration changes during protected periods.

### 6.5 Traceability

The audit log associated each event with a timestamp, actor, action, outcome, and detail. The evidence distinguishes permission evaluation from enforcement: the write check was evaluated successfully but contained `permitted: false`, while the attempted VM creation generated a separate denied authorization event.

---

## 7. Risks and Controls

| Risk ID | Risk | Likelihood | Impact | Control applied | Verification |
|---|---|---:|---:|---|---|
| E01-R01 | Excessive permissions could allow unauthorized changes | Medium | High | Group-scoped Reader role | Read true, write false, VM creation denied |
| E01-R02 | Missing ownership metadata could weaken accountability | Medium | Medium | Mandatory owner tag | Owner shown as `Wadondera-A-Collins` |
| E01-R03 | Missing environment classification could cause management errors | Medium | Medium | Mandatory environment tag | Environment shown as `training` |
| E01-R04 | Unprotected resources could be changed accidentally | Medium | High | Simulated resource-group lock | Locked tag change rejected |
| E01-R05 | Administrative actions could lack traceability | Medium | High | Local audit logging | RBAC, denial, lock, unlock, and tag events visible |

---

## 8. Evidence Register and File Naming

The screenshots should be stored under `screenshots/E01/` using these exact filenames and this exact order:

| Order | Exact filename | Source screenshot | Evidence purpose |
|---:|---|---|---|
| 1 | `Fig01 Laboratory Package Structure.png` | `Screenshot 2026-11-23 161046.png` | Package and simulator structure |
| 2 | `Fig02 Resource Group Creation.png` | `Screenshot 2026-11-23 165008.png` | Step 1 resource-group creation |
| 3 | `Fig03 Resource Group Tags and Baseline Policy.png` | `Screenshot 2026-11-23 165201.png` | Step 2 group listing and zero findings |
| 4 | `Fig04 Cost Centre Governance Tag.png` | `Screenshot 2026-11-23 171248.png` | Step 3 additional governance tag |
| 5 | `Fig05 Analyst Reader Role Assignment.png` | `Screenshot 2026-11-23 171403.png` | Step 4 Reader assignment |
| 6 | `Fig06 Reader Permission Validation.png` | `Screenshot 2026-11-23 173350.png` | Step 5 read/write decisions |
| 7 | `Fig07 RBAC Denied VM Creation.png` | `Screenshot 2026-11-23 180130.png` | Step 6 denial and exit code 3 |
| 8 | `Fig08 Resource Lock Enforcement.png` | `Screenshot 2026-11-23 180352.png` | Step 7 lock enforcement |
| 9 | `Fig09 Resource Unlock and Governance Tag.png` | `Screenshot 2026-11-23 180454.png` | Step 8 authorized change |
| 10 | `Fig10 E01 Governance and RBAC Audit Log.png` | `Screenshot 2026-11-23 180624.png` | Step 9 cumulative audit evidence |

### Evidence quality note

`Screenshot 2026-11-23 180119.png` was not used because the supplied file is only **1 × 5 pixels** and contains no readable laboratory evidence. Including it would weaken the evidence record and create a figure with no verifiable content. The remaining ten screenshots cover the complete E01 sequence, including the package structure and Steps 1 through 9.

---

## 9. Final E01 State

At the end of Laboratory E01, the expected retained state is:

```text
Resource group: rg-icdfa-lab
Location: local-linux
Locked: false
Tags:
  owner: Wadondera-A-Collins
  environment: training
  cost-centre: CCSE102
  governance: controlled

RBAC assignment:
  user: analyst
  role: Reader
  scope: group:rg-icdfa-lab
```

This state should remain available for the later laboratories. The simulator must not be reset before E02.

---

## 10. Limitations

1. The simulator models selected Azure-style concepts but is not Microsoft Azure.
2. The VM creation denial affects simulated inventory only.
3. The resource-group lock is a simulator control, not an Azure Resource Manager lock.
4. The policy engine checks controls implemented in simulator version 1.0.
5. Audit events are written to the local simulator workspace.
6. The laboratory does not test Microsoft Entra ID, Azure Policy assignments, Azure Activity Log, or live Azure RBAC propagation.
7. The screenshots verify the commands and visible outputs supplied for E01; no unsupported Azure deployment claim is made.

---

## 11. Recommendations

1. Retain group-scoped Reader access for identities that need visibility but not modification rights.
2. Review role assignments periodically and remove access that is no longer required.
3. Preserve owner, environment, cost-centre, and governance metadata throughout later laboratories.
4. Apply locks before high-risk maintenance or assessment checkpoints and remove them only through controlled procedures.
5. Export and hash evidence logs before final submission to strengthen integrity assurance.
6. Keep the generated `workspace/` directory out of the public GitHub repository because it may contain local state or personal details.

---

## 12. Conclusion

Laboratory E01 successfully established a governed simulated resource group and demonstrated least-privilege access control. Required tags produced a clean policy baseline, the additional cost-centre tag improved classification, and the analyst Reader assignment allowed observation while denying modification. The actual denied VM-creation attempt confirmed enforcement with exit code `3`. Resource locking protected the group from change, while an authorized unlock restored normal administration. Finally, the audit log provided traceable evidence of permission checks, denial, locking, unlocking, and tagging.

The final E01 state is suitable for continuation into Laboratory E02 without resetting the simulator.

---

## 13. Academic Integrity and AI Assistance Disclosure

All commands, results, screenshots, and interpretations in the final submission must represent laboratory work independently executed and verified by Wadondera A. Collins.

Microsoft Copilot was used to organize the report, improve clarity, and align the supplied screenshots with the visible command evidence. Copilot did not execute the student's WSL laboratory session or manufacture the terminal results. Final verification, evidence ownership, and submission responsibility remain with the student.

---

## 14. Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Laboratory E01 · Documentation and Evidence Report**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
