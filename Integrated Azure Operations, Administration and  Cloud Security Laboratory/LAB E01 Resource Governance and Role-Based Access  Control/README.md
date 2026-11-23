<div align="center">

# CCSE-102 Laboratory E01
## Resource Governance and Role-Based Access Control

**Offline Azure-Style Administration Simulation**

![Course](https://img.shields.io/badge/Course-CCSE--102-17365D?style=for-the-badge)
![Laboratory](https://img.shields.io/badge/Laboratory-E01-C65911?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)

![Governance](https://img.shields.io/badge/Control-Resource_Governance-2F5597?style=flat-square)
![RBAC](https://img.shields.io/badge/Control-RBAC-0078D4?style=flat-square)
![Least Privilege](https://img.shields.io/badge/Security-Least_Privilege-107C10?style=flat-square)
![Audit](https://img.shields.io/badge/Evidence-Audit_Logs-5C2D91?style=flat-square)

**Resource-group governance, mandatory tagging, scoped Reader access, authorization testing, lock enforcement, and audit validation**

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering

</div>

---

## Table of Contents

1. [Laboratory Overview](#laboratory-overview)
2. [Important Scope Declaration](#important-scope-declaration)
3. [Objectives](#objectives)
4. [Prerequisites](#prerequisites)
5. [Laboratory Resources](#laboratory-resources)
6. [Implementation Procedure](#implementation-procedure)
7. [Evidence Register](#evidence-register)
8. [Expected Security Findings](#expected-security-findings)
9. [Troubleshooting](#troubleshooting)
10. [Completion Checklist](#completion-checklist)
11. [Repository Structure](#repository-structure)
12. [Limitations](#limitations)
13. [Author](#author)

---

## Laboratory Overview

Laboratory E01 is the first of four compulsory laboratories in the CCSE-102 Integrated Azure Operations, Administration and Cloud Security practical. It focuses on resource governance and role-based access control using the ICDFA offline Azure-style simulator.

| Item | Detail |
|---|---|
| Laboratory | E01 |
| Title | Resource Governance and Role-Based Access Control |
| Marks | 20 |
| Environment | Linux workstation |
| Runtime | Python 3.10 or later |
| Simulator | `azlocal.py` version 1.0 |
| Subscription | `ICDFA-SIM-001` |
| Administrator identity | `student-admin` |
| Test identity | `analyst` |
| Resource group | `rg-icdfa-lab` |

> **Execution rule:** Complete the common preparation before beginning E01. Initialize the simulator only once and do not reset it between E01, E02, E03, and E04.

---

## Important Scope Declaration

This laboratory does **not** create resources in Microsoft Azure. It uses a locally controlled, offline teaching simulator that reproduces selected Azure-style administration concepts.

### Simulated operations

- Resource-group creation and management
- Resource tagging
- Role assignments
- Permission evaluation
- Resource locking
- Audit events

### Real Linux operations

- Running Python commands
- Reading and writing local files
- Creating evidence directories
- Capturing terminal output and screenshots

No Microsoft Azure tenant, Azure CLI session, Azure credit, or live cloud subscription is used.

---

## Objectives

By completing Laboratory E01, the student should be able to:

1. Confirm the Linux and Python laboratory environment.
2. Initialize the offline simulator safely.
3. Create a simulated resource group.
4. Apply owner, environment, cost-centre, and governance tags.
5. Assign a group-scoped Reader role to a fictional analyst.
6. verify that Reader access permits reading but denies writing.
7. Demonstrate an actual RBAC-denied operation.
8. Apply a simulated resource-group lock.
9. Verify that the lock prevents configuration changes.
10. Remove the lock using an authorized identity.
11. Review the audit trail for governance and authorization events.

---

## Prerequisites

Before starting E01, confirm that the extracted package contains:

```text
azlocal.py
scripts/
guides/
templates/
```

Confirm Python:

```bash
python3 --version
```

The version must be Python 3.10 or later.

Validate the supplied simulator:

```bash
python3 -m py_compile azlocal.py
```

No output means the Python syntax check passed.

> Use the original `azlocal.py` supplied in the laboratory package. Do not reconstruct the simulator from HTML-formatted code copied from a webpage.

---

## Laboratory Resources

The following names are used consistently throughout E01:

| Resource | Value |
|---|---|
| Resource group | `rg-icdfa-lab` |
| Owner tag | `Wadondera-A-Collins` |
| Environment tag | `training` |
| Cost-centre tag | `CCSE102` |
| Governance tag | `controlled` |
| Reader identity | `analyst` |
| Reader scope | `group:rg-icdfa-lab` |
| Deliberately denied VM name | `denied-demo` |

---

# Implementation Procedure

## Phase 0: Common Preparation

Perform this phase only if the simulator has not already been initialized. If the simulator was initialized previously and contains valid progress, do not run `init` again.

### Step 0.1: Open the package directory

Replace the example path with the actual extracted package path:

```bash
cd /your/real/path/to/the/extracted-package
pwd
ls -la
```

**Expected result:**

- The terminal displays the package directory.
- `azlocal.py`, `scripts/`, `guides/`, and `templates/` are visible.

**Capture:** `Fig01 Extracted Laboratory Package.png`

---

### Step 0.2: Confirm Linux and Python

```bash
cat /etc/os-release
python3 --version
which python3
```

**Expected result:** Python 3.10 or later is available.

**Capture:** `Fig02 Linux and Python Version.png`

---

### Step 0.3: Create evidence directories

```bash
mkdir -p evidence/E01/outputs screenshots/E01 notes
```

These directories will store E01 command outputs, screenshots, and notes.

---

### Step 0.4: Create `.gitignore`

```bash
cat > .gitignore <<'GITIGNORE'
workspace/
.env
*.pem
*.key
id_rsa*
__pycache__/
*.pyc
GITIGNORE

cat .gitignore
```

**Expected result:** The exclusion patterns are displayed. The generated `workspace/` directory and common secret-bearing files will be excluded from Git commits.

---

### Step 0.5: Review simulator help

```bash
python3 azlocal.py --help
```

Optional E01-specific help:

```bash
python3 azlocal.py group --help
python3 azlocal.py access --help
python3 azlocal.py monitor --help
```

**Capture:** `Fig03 Simulator Help Menu.png`

---

### Step 0.6: Initialize the simulator once

```bash
python3 azlocal.py init
```

**Expected result:**

```json
{
  "notice": "Offline simulation; NOT Microsoft Azure",
  "result": "ready",
  "subscription": "ICDFA-SIM-001"
}
```

The exact workspace path will depend on the extracted package location.

**Capture:** `Fig04 Simulator Initialization.png`

> **Do not run** `python3 azlocal.py init --reset --confirm` during the normal implementation. That command deletes the existing simulated state.

---

### Step 0.7: Verify the clean initial state

```bash
python3 azlocal.py status
python3 azlocal.py access list
```

**Expected status before resource creation:**

- No resource groups
- Zero VM records
- Zero NSGs
- Zero storage accounts
- Zero monitoring rules
- Subscription `ICDFA-SIM-001`

**Expected initial role assignments:**

- `student-admin` has `Owner` at `subscription` scope.
- `auditor` has `Reader` at `subscription` scope.

**Capture:** `Fig05 Initial Status and RBAC.png`

---

# Laboratory E01: Resource Governance and RBAC

## Step 1: Create the resource group

Run:

```bash
python3 azlocal.py group create rg-icdfa-lab \
  --owner Wadondera-A-Collins \
  --environment training
```

**Expected result:**

```json
{
  "group": "rg-icdfa-lab",
  "location": "local-linux",
  "locked": false,
  "tags": {
    "environment": "training",
    "owner": "Wadondera-A-Collins"
  }
}
```

**What this proves:**

- The resource group was created successfully.
- Mandatory owner and environment tags were applied.
- The resource group begins in an unlocked state.

**Capture:** `Fig06 Resource Group Creation.png`

---

## Step 2: Verify the governance baseline

Run the commands separately:

```bash
python3 azlocal.py group list
```

```bash
python3 azlocal.py policy
```

**Expected result:**

- `group list` displays `rg-icdfa-lab` and its tags.
- The policy check reports `findings_count: 0` because both required tags are populated.
- The policy output reports `simulation: true`.

**What this proves:** The new resource group satisfies the simulator's required-tag governance control.

**Capture:** `Fig07 Resource Group Tags and Baseline Policy.png`

---

## Step 3: Add a cost-centre tag

```bash
python3 azlocal.py group tag rg-icdfa-lab cost-centre CCSE102
```

Verify the change:

```bash
python3 azlocal.py group list
```

**Expected result:** The resource group contains the additional tag:

```text
cost-centre: CCSE102
```

**What this proves:** Resource metadata can be updated for cost allocation and administrative organization.

**Suggested capture:** `Fig08 Cost Centre Governance Tag.png`

---

## Step 4: Assign group-scoped Reader access

```bash
python3 azlocal.py access assign analyst Reader group:rg-icdfa-lab
```

Verify all assignments:

```bash
python3 azlocal.py access list
```

**Expected assignment:**

```json
{
  "role": "Reader",
  "scope": "group:rg-icdfa-lab",
  "user": "analyst"
}
```

**What this proves:** The fictional analyst receives read-only access limited to `rg-icdfa-lab`, rather than broad subscription-level access.

**Capture:** `Fig09 Analyst Reader Assignment.png`

---

## Step 5: Test permitted read access

```bash
python3 azlocal.py access check analyst read group:rg-icdfa-lab
```

**Expected result:**

```json
{
  "action": "read",
  "permitted": true,
  "scope": "group:rg-icdfa-lab",
  "user": "analyst"
}
```

**What this proves:** The Reader role permits read operations at the assigned scope.

---

## Step 6: Test denied write access

```bash
python3 azlocal.py access check analyst write group:rg-icdfa-lab
```

**Expected result:**

```json
{
  "action": "write",
  "permitted": false,
  "scope": "group:rg-icdfa-lab",
  "user": "analyst"
}
```

**What this proves:** The Reader role does not grant resource modification rights.

**Capture:** `Fig10 Reader Permission Validation.png`

---

## Step 7: Prove RBAC enforcement with an actual denied operation

The global `--actor` option must appear before the `vm` command:

```bash
python3 azlocal.py --actor analyst vm create denied-demo --group rg-icdfa-lab
```

Immediately display the exit status:

```bash
echo $?
```

**Expected result:**

```text
ERROR: RBAC DENIED: analyst lacks permission write on group:rg-icdfa-lab
```

Expected exit status:

```text
3
```

**What this proves:** RBAC is enforced during an actual attempted administrative operation, not merely reported by a permission-check command.

> The failed VM creation is an expected and successful security-control test. The `denied-demo` VM must not appear in the VM inventory.

**Capture:** `Fig11 RBAC Denied VM Creation.png`

---

## Step 8: Apply a resource-group lock

```bash
python3 azlocal.py group lock rg-icdfa-lab
```

**Expected result:**

```text
locked: true
```

**What this proves:** An authorized Owner can place the simulated resource group into a protected state.

---

## Step 9: Test lock enforcement

Attempt to add a tag while the group is locked:

```bash
python3 azlocal.py group tag rg-icdfa-lab test locked-change
```

**Expected result:**

```text
ERROR: Resource group rg-icdfa-lab has a simulated delete/read-only lock. Unlock before changes.
```

**What this proves:** The resource lock prevents changes even when the current identity normally has write permission.

**Capture:** `Fig12 Resource Lock Enforcement.png`

---

## Step 10: Unlock the resource group

```bash
python3 azlocal.py group unlock rg-icdfa-lab
```

**Expected result:**

```text
locked: false
```

---

## Step 11: Verify an authorized post-unlock change

```bash
python3 azlocal.py group tag rg-icdfa-lab governance controlled
```

Verify the complete group state:

```bash
python3 azlocal.py group list
```

**Expected result:**

- The group is unlocked.
- `governance: controlled` is present.
- Owner, environment, and cost-centre tags remain present.

**What this proves:** Authorized changes resume successfully after the lock is removed.

**Capture:** `Fig13 Resource Unlock and Governance Tag.png`

---

## Step 12: Re-run the policy assessment

```bash
python3 azlocal.py policy
```

**Expected result:**

```text
findings_count: 0
```

**What this proves:** The final E01 governance configuration remains compliant with the simulator's required-tag policy.

**Capture:** `Fig14 Final E01 Policy Validation.png`

---

## Step 13: Review the E01 audit trail

```bash
python3 azlocal.py monitor logs --limit 30
```

Look for the following events:

- `init`
- `group-create`
- `group-tag`
- `rbac-assign`
- `rbac-check`
- `authorisation` with outcome `denied`
- `group-lock`
- `group-unlock`

**What this proves:** Governance and authorization activity is traceable through the simulator's audit log.

**Capture:** `Fig15 E01 Governance Audit Log.png`

---

## Step 14: Save E01 outputs

Save important output to a student-owned evidence file:

```bash
{
  echo "=== E01 FINAL GROUP STATE ==="
  python3 azlocal.py group list
  echo
  echo "=== E01 ACCESS ASSIGNMENTS ==="
  python3 azlocal.py access list
  echo
  echo "=== E01 FINAL POLICY ==="
  python3 azlocal.py policy
  echo
  echo "=== E01 AUDIT EVENTS ==="
  python3 azlocal.py monitor logs --limit 30
} | tee evidence/E01/outputs/e01-final-evidence.txt
```

Create a SHA-256 checksum:

```bash
sha256sum evidence/E01/outputs/e01-final-evidence.txt \
  | tee evidence/E01/outputs/e01-final-evidence.sha256
```

Verify the checksum:

```bash
sha256sum -c evidence/E01/outputs/e01-final-evidence.sha256
```

**Expected result:**

```text
evidence/E01/outputs/e01-final-evidence.txt: OK
```

**Capture:** `Fig16 E01 Evidence File and SHA256.png`

---

## Evidence Register

Rename screenshots only after confirming that each image visibly supports the stated evidence.

| Figure | Filename | Evidence shown |
|---|---|---|
| Fig01 | `Fig01 Extracted Laboratory Package.png` | Package directory and supplied files |
| Fig02 | `Fig02 Linux and Python Version.png` | Linux distribution and Python 3.10+ |
| Fig03 | `Fig03 Simulator Help Menu.png` | Simulator command interface |
| Fig04 | `Fig04 Simulator Initialization.png` | Initialization and offline-simulation notice |
| Fig05 | `Fig05 Initial Status and RBAC.png` | Clean state and initial identities |
| Fig06 | `Fig06 Resource Group Creation.png` | Resource group, tags, location, and unlocked state |
| Fig07 | `Fig07 Resource Group Tags and Baseline Policy.png` | Group listing and zero baseline findings |
| Fig08 | `Fig08 Cost Centre Governance Tag.png` | Added cost-centre tag |
| Fig09 | `Fig09 Analyst Reader Assignment.png` | Reader assignment at group scope |
| Fig10 | `Fig10 Reader Permission Validation.png` | Read true and write false |
| Fig11 | `Fig11 RBAC Denied VM Creation.png` | Actual denied operation and exit status 3 |
| Fig12 | `Fig12 Resource Lock Enforcement.png` | Locked group rejecting a tag change |
| Fig13 | `Fig13 Resource Unlock and Governance Tag.png` | Authorized unlock and successful governance tag |
| Fig14 | `Fig14 Final E01 Policy Validation.png` | Final zero-finding policy result |
| Fig15 | `Fig15 E01 Governance Audit Log.png` | E01 audit events |
| Fig16 | `Fig16 E01 Evidence File and SHA256.png` | Evidence export and checksum verification |

---

## Expected Security Findings

### Finding 1: Reader access correctly limits administrative operations

The fictional `analyst` identity can read `rg-icdfa-lab` but cannot perform write operations. The unsuccessful VM-creation attempt confirms that the assignment follows least-privilege principles.

### Finding 2: Resource locks protect configuration integrity

The group lock prevents tag modification until an authorized Owner removes the lock. The test demonstrates administrative protection against unintended changes.

### Finding 3: Required tags support governance

The `owner` and `environment` tags satisfy the simulator's required-tag policy. The additional `cost-centre` and `governance` tags improve resource organization and accountability.

### Finding 4: Audit logs support traceability

The audit log records resource creation, tag changes, role assignment, permission checks, denied authorization, lock, and unlock activities.

---

## Troubleshooting

### Error: Lab not initialized

```text
ERROR: Lab not initialised. Run: python3 azlocal.py init
```

Run the initialization command only if this is the first laboratory session:

```bash
python3 azlocal.py init
```

### Error: Resource group already exists

Do not recreate it. Verify the existing state:

```bash
python3 azlocal.py group list
```

### Error: RBAC DENIED while using `student-admin`

Check that `--actor` was not accidentally set to another identity. List assignments:

```bash
python3 azlocal.py access list
```

### Error: Group remains locked

Unlock it as the default Owner identity:

```bash
python3 azlocal.py group unlock rg-icdfa-lab
```

### `echo $?` does not return 3

Run `echo $?` immediately after the denied VM-creation command. Running another command first replaces the recorded exit status.

### Policy reports a missing tag

Review the group:

```bash
python3 azlocal.py group list
```

Restore the required tag if it is empty:

```bash
python3 azlocal.py group tag rg-icdfa-lab owner Wadondera-A-Collins
python3 azlocal.py group tag rg-icdfa-lab environment training
```

---

## Completion Checklist

- [ ] Original simulator syntax validated
- [ ] Simulator initialized once
- [ ] Initial status and role assignments recorded
- [ ] `rg-icdfa-lab` created
- [ ] Owner and environment tags applied
- [ ] Baseline policy returned zero findings
- [ ] Cost-centre tag added
- [ ] `analyst` assigned Reader at group scope
- [ ] Analyst read check returned `true`
- [ ] Analyst write check returned `false`
- [ ] Actual analyst VM-creation attempt was denied
- [ ] Denied command returned exit status `3`
- [ ] Group lock applied
- [ ] Locked change was rejected
- [ ] Group unlocked by an authorized identity
- [ ] Governance tag added after unlock
- [ ] Final policy validation returned zero findings
- [ ] E01 audit events reviewed
- [ ] Evidence output saved and hashed
- [ ] Screenshots accurately named and stored
- [ ] No secrets or `workspace/` content staged for GitHub

---

## Repository Structure

The following is a layout example, not a terminal command:

```text
CCSE-102-Integrated-Azure-Operations-Lab/
├── README.md
├── .gitignore
├── evidence/
│   └── E01/
│       └── outputs/
│           ├── e01-final-evidence.txt
│           └── e01-final-evidence.sha256
├── screenshots/
│   └── E01/
│       ├── Fig01 Extracted Laboratory Package.png
│       ├── Fig02 Linux and Python Version.png
│       └── ...
└── notes/
```

Do not commit the generated `workspace/` directory.

---

## Limitations

- Resource groups and RBAC assignments are simulated locally.
- The deliberately denied VM operation does not contact Microsoft Azure.
- Resource locks affect simulator state only.
- The policy check evaluates controls implemented in simulator version 1.0.
- Audit events are stored in the local simulator workspace.
- This laboratory does not demonstrate Azure Entra ID, Azure Resource Manager, or live Azure Policy enforcement.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

## Academic Integrity and AI Disclosure

All commands, outputs, screenshots, interpretations, and validation results submitted for this laboratory must come from the student's independently executed laboratory work.

Microsoft Copilot may be disclosed as having assisted with document organization and clarity. Copilot-generated text does not replace execution, verification, interpretation, or evidence collection by the student.

---

<div align="center">

**CCSE-102 Laboratory E01 · Resource Governance and RBAC**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
