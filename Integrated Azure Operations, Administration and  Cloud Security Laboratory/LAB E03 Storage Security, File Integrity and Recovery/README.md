<div align="center">

# CCSE-102 Laboratory E03
## Storage Security, File Integrity and Recovery

**Offline Azure-Style Storage Administration with Real SHA-256 File Validation**

![Course](https://img.shields.io/badge/Course-CCSE--102-17365D?style=for-the-badge)
![Laboratory](https://img.shields.io/badge/Laboratory-E03-C65911?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)

![Storage](https://img.shields.io/badge/Domain-Storage-0078D4?style=flat-square)
![Integrity](https://img.shields.io/badge/Control-SHA--256-5C2D91?style=flat-square)
![RBAC](https://img.shields.io/badge/Security-Data_Plane_RBAC-107C10?style=flat-square)
![Recovery](https://img.shields.io/badge/Control-Backup_%26_Recovery-9C6500?style=flat-square)

**Storage hardening · Scoped data access · SHA-256 integrity verification · Known-good inventory recovery**

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering

</div>

---

## Table of Contents

1. [Laboratory Overview](#laboratory-overview)
2. [Scope Declaration](#scope-declaration)
3. [Objectives](#objectives)
4. [Start Conditions](#start-conditions)
5. [Laboratory Resources](#laboratory-resources)
6. [Part A: Storage Security](#part-a-storage-security)
7. [Part B: Blob Data, RBAC and SHA-256](#part-b-blob-data-rbac-and-sha-256)
8. [Part C: Backup and Recovery](#part-c-backup-and-recovery)
9. [Evidence Register](#evidence-register)
10. [Security Findings](#security-findings)
11. [Troubleshooting](#troubleshooting)
12. [Completion Checklist](#completion-checklist)
13. [Repository Structure](#repository-structure)
14. [Limitations](#limitations)
15. [Author](#author)

---

## Laboratory Overview

Laboratory E03 is the third compulsory laboratory in the CCSE-102 Integrated Azure Operations, Administration and Cloud Security practical. It assesses storage configuration security, policy-based detection, blob data operations, data-plane access control, SHA-256 integrity validation, and recovery of simulated inventory from a verified backup.

| Item | Detail |
|---|---|
| Laboratory | E03 |
| Title | Storage Security, File Integrity and Recovery |
| Marks | 25 |
| Environment | Linux workstation |
| Simulator | `azlocal.py` version 1.0 |
| Existing resource group | `rg-icdfa-lab` |
| Existing VM | `vm-demo` |
| Storage account | `sticdfalab` |
| Blob name | `operations-file` |
| Data-plane identity | `blob-operator` |
| Backup label | `known-good` |
| Integrity algorithm | SHA-256 |

> **Important:** E03 continues from E01 and E02 in the same simulator workspace. Do not initialize or reset the simulator.

---

## Scope Declaration

E03 combines simulated cloud-style storage controls with real local file and cryptographic-hash operations.

### Simulated operations

- Storage-account creation
- Public-access and HTTPS-only configuration
- Storage policy assessment
- Blob metadata and simulated data-plane authorization
- Inventory backup and restoration

### Real Linux operations

- Creating a non-sensitive local text file
- Calculating SHA-256 hashes
- Copying content to and from the simulator blob directory
- Comparing original and recovered files
- Saving evidence and checksum files

No genuine Microsoft Azure Storage account, Azure Blob container, Recovery Services vault, or cloud backup is created.

---

## Objectives

By completing E03, the student should be able to:

1. Create a simulated storage account with secure defaults.
2. Introduce controlled storage misconfigurations.
3. Detect public-access and transport-security weaknesses.
4. Restore private and HTTPS-only storage settings.
5. Create and hash a non-sensitive local file.
6. Upload the file as a simulated blob.
7. Verify blob integrity through SHA-256 comparison.
8. Assign a storage-scoped data-plane role.
9. Confirm that the data identity cannot administer the resource group.
10. Download the blob and verify that the recovered file matches the original.
11. Create a checksummed known-good simulator backup.
12. Change VM inventory state after the backup.
13. Restore the backup and verify recovery.

---

## Start Conditions

Verify the retained state from E02:

```bash
python3 azlocal.py group list
python3 azlocal.py vm list
python3 azlocal.py nsg list
python3 azlocal.py policy
```

Expected preconditions:

- `rg-icdfa-lab` exists and is unlocked.
- `vm-demo` exists and is running.
- `nsg-demo` retains only the priority `100` SSH rule for `192.168.56.0/24`.
- The policy scanner reports zero findings.

If the resource group is locked, unlock it:

```bash
python3 azlocal.py group unlock rg-icdfa-lab
```

Create E03 evidence directories:

```bash
mkdir -p evidence/E03/outputs screenshots/E03 recovered samples
```

---

## Laboratory Resources

| Resource | Value |
|---|---|
| Resource group | `rg-icdfa-lab` |
| Storage account | `sticdfalab` |
| Initial public access | `false` |
| Initial HTTPS-only setting | `true` |
| Insecure public-access setting | `true` |
| Insecure HTTPS-only setting | `false` |
| Local source file | `samples/operations_data.txt` |
| Blob name | `operations-file` |
| Downloaded file | `recovered/operations_data_recovered.txt` |
| Data identity | `blob-operator` |
| Data role | `Storage Blob Data Contributor` |
| Storage scope | `storage:sticdfalab` |
| Backup label | `known-good` |

---

# Part A: Storage Security

## Step 1: Create the storage account

```bash
python3 azlocal.py storage create sticdfalab --group rg-icdfa-lab
python3 azlocal.py storage list
```

**Expected result:**

- Storage account: `sticdfalab`
- Resource group: `rg-icdfa-lab`
- Public access: `false`
- HTTPS only: `true`
- Blob inventory: empty

**What this proves:** The storage account begins with private access and encrypted-transport enforcement.

**Capture:** `Fig01 Storage Account Secure Baseline.png`

---

## Step 2: Introduce controlled storage weaknesses

```bash
python3 azlocal.py storage set sticdfalab \
  --public-access true \
  --https-only false
```

**Expected result:**

```text
public_access: true
https_only: false
```

> These insecure values are introduced temporarily for controlled assessment. They must not be retained as the final configuration.

**Capture:** `Fig02 Insecure Storage Configuration.png`

---

## Step 3: Detect the storage weaknesses

```bash
python3 azlocal.py policy
```

**Expected findings:**

```text
control: storage-private
finding: Public access enabled
resource: sticdfalab
```

```text
control: storage-https
finding: HTTPS not enforced
resource: sticdfalab
```

**What this proves:** The simulator policy scanner detects both data-exposure and transport-security weaknesses.

**Capture:** `Fig03 Insecure Storage Policy Findings.png`

---

## Step 4: Harden the storage account

```bash
python3 azlocal.py storage set sticdfalab \
  --public-access false \
  --https-only true
```

**Expected result:** Public access is disabled and HTTPS-only enforcement is restored.

---

## Step 5: Validate remediation

```bash
python3 azlocal.py storage list
python3 azlocal.py policy
```

**Expected result:**

- `public_access: false`
- `https_only: true`
- No storage-related policy findings

**What this proves:** The insecure configuration was corrected and the account returned to its secure baseline.

**Capture:** `Fig04 Storage Security Remediation.png`

---

# Part B: Blob Data, RBAC and SHA-256

## Step 6: Prepare a non-sensitive local file

If `samples/operations_data.txt` already exists in the supplied package, inspect and use it. If the file does not exist, create a student-owned training file:

```bash
cat > samples/operations_data.txt <<'DATA'
CCSE-102 operations evidence
Student: Wadondera A. Collins
Purpose: Local storage integrity validation
Classification: Training data only
DATA
```

Display and hash the source file:

```bash
cat samples/operations_data.txt
sha256sum samples/operations_data.txt
```

Record the original SHA-256 digest in the evidence log.

**Capture:** `Fig05 Source File and Original SHA256.png`

---

## Step 7: Upload the file as a simulated blob

```bash
python3 azlocal.py blob upload sticdfalab operations-file \
  --file samples/operations_data.txt
```

**Expected result:** The output displays:

- SHA-256 digest
- File size in bytes
- Upload timestamp

The simulator's educational upload limit is 5 MB.

**Capture:** `Fig06 Blob Upload and Stored Digest.png`

---

## Step 8: List and verify the blob

```bash
python3 azlocal.py blob list sticdfalab
python3 azlocal.py blob verify sticdfalab operations-file
```

**Expected result:**

```text
integrity_ok: true
```

The `expected` and `actual` SHA-256 values must match.

**What this proves:** The current stored content matches the digest recorded at upload time.

**Capture:** `Fig07 Blob Listing and Integrity Verification.png`

---

## Step 9: Assign storage-scoped data access

Because the role name contains spaces, keep the quotation marks:

```bash
python3 azlocal.py access assign blob-operator \
  "Storage Blob Data Contributor" \
  storage:sticdfalab
```

Verify the assignment:

```bash
python3 azlocal.py access list
```

**Expected result:**

```text
user: blob-operator
role: Storage Blob Data Contributor
scope: storage:sticdfalab
```

**What this proves:** Data-plane access can be granted at storage-account scope without assigning resource-group management rights.

**Capture:** `Fig08 Storage Data Role Assignment.png`

---

## Step 10: Validate the data-plane scope

Use the scoped identity to list blobs:

```bash
python3 azlocal.py --actor blob-operator blob list sticdfalab
```

**Expected result:** The blob list operation succeeds.

Attempt to administer the resource group with the same identity:

```bash
python3 azlocal.py --actor blob-operator \
  group tag rg-icdfa-lab unauthorized test
```

Immediately display the exit status:

```bash
echo $?
```

**Expected result:**

- Group administration is denied.
- The command returns RBAC exit status `3`.

**What this proves:** Storage data access does not grant management-plane write access to the resource group.

**Capture:** `Fig09 Storage Data Role Scope Validation.png`

---

## Step 11: Download the blob

The simulator refuses to overwrite an existing destination. Remove only the previous student-owned recovered file if present:

```bash
rm -f recovered/operations_data_recovered.txt
```

Download the blob:

```bash
python3 azlocal.py blob download sticdfalab operations-file \
  --dest recovered/operations_data_recovered.txt
```

**Expected result:** The output displays the destination path and SHA-256 digest.

**Capture:** `Fig10 Blob Download and Recovered Digest.png`

---

## Step 12: Compare original and recovered content

```bash
sha256sum \
  samples/operations_data.txt \
  recovered/operations_data_recovered.txt
```

Run a byte-for-byte comparison:

```bash
cmp --silent \
  samples/operations_data.txt \
  recovered/operations_data_recovered.txt \
  && echo "Recovered file matches original"
```

**Expected result:**

- Both SHA-256 values are identical.
- The terminal prints `Recovered file matches original`.

**What this proves:** The recovered data is identical to the original source file.

**Capture:** `Fig11 Recovered File SHA256 Match.png`

---

# Part C: Backup and Recovery

## Step 13: Establish a known-good inventory state

Ensure the VM is running before taking the backup:

```bash
python3 azlocal.py vm start vm-demo
python3 azlocal.py vm list
python3 azlocal.py policy
```

**Expected result:**

- `vm-demo` state is `running`.
- The policy scanner reports zero findings.

This becomes the known-good state to be recovered later.

**Capture:** `Fig12 Known Good Pre-Backup State.png`

---

## Step 14: Create the backup

```bash
python3 azlocal.py backup create known-good
python3 azlocal.py backup list
```

**Expected result:** The output displays:

- Backup label `known-good`
- Local backup path
- Backup checksum
- `known-good.json` in the backup list

**What this proves:** A checksummed simulator inventory snapshot was created.

**Capture:** `Fig13 Known Good Backup Creation.png`

---

## Step 15: Change the post-backup VM state

```bash
python3 azlocal.py vm stop vm-demo
python3 azlocal.py vm list
```

**Expected result:** `vm-demo` shows `state: stopped`.

This controlled change creates a condition that can be reversed through recovery.

**Capture:** `Fig14 Post Backup VM State Change.png`

---

## Step 16: Demonstrate the restore confirmation safeguard

Run the restore command without confirmation:

```bash
python3 azlocal.py backup restore known-good
```

**Expected result:**

```text
ERROR: Restore requires --confirm because it replaces current simulated inventory.
```

**What this proves:** The simulator requires explicit confirmation before replacing current state.

**Suggested capture:** `Fig15 Restore Confirmation Safeguard.png`

---

## Step 17: Restore the known-good backup

```bash
python3 azlocal.py backup restore known-good --confirm
```

**Expected result:**

```text
restored: known-good
verified: true
```

The output also states that the restoration covers inventory only and does not revert uploaded blob files.

---

## Step 18: Verify recovery

```bash
python3 azlocal.py vm list
python3 azlocal.py policy
```

**Expected result:**

- `vm-demo` returns to the backed-up `running` state.
- The policy scanner reports zero findings.

**What this proves:** The checksummed inventory backup restored the known-good state successfully.

**Capture:** `Fig16 Backup Restore and VM Recovery.png`

> Do not claim that blob files were rolled back. Simulator version 1.0 restores inventory state only.

---

## Step 19: Review E03 audit events

```bash
python3 azlocal.py monitor logs --limit 60
```

Look for:

- Storage creation
- Storage configuration changes
- Blob upload and download
- Role assignment
- Denied authorization for the blob operator
- Backup creation
- VM stop
- Backup restoration

**Capture:** `Fig17 E03 Storage and Recovery Audit Log.png`

---

## Step 20: Save E03 evidence

```bash
{
  echo "=== E03 STORAGE CONFIGURATION ==="
  python3 azlocal.py storage list
  echo
  echo "=== E03 BLOB INVENTORY ==="
  python3 azlocal.py blob list sticdfalab
  echo
  echo "=== E03 ACCESS ASSIGNMENTS ==="
  python3 azlocal.py access list
  echo
  echo "=== E03 BACKUPS ==="
  python3 azlocal.py backup list
  echo
  echo "=== E03 VM STATE ==="
  python3 azlocal.py vm list
  echo
  echo "=== E03 FINAL POLICY ==="
  python3 azlocal.py policy
  echo
  echo "=== E03 AUDIT EVENTS ==="
  python3 azlocal.py monitor logs --limit 60
} | tee evidence/E03/outputs/e03-final-evidence.txt
```

Create and verify the evidence checksum:

```bash
sha256sum evidence/E03/outputs/e03-final-evidence.txt \
  | tee evidence/E03/outputs/e03-final-evidence.sha256

sha256sum -c evidence/E03/outputs/e03-final-evidence.sha256
```

**Expected result:**

```text
evidence/E03/outputs/e03-final-evidence.txt: OK
```

**Capture:** `Fig18 E03 Evidence File and SHA256.png`

---

## Evidence Register

Store E03 screenshots under `screenshots/E03/`. Use exact filenames only after checking that each screenshot visibly supports the stated scenario.

| Figure | Exact filename | Evidence purpose |
|---:|---|---|
| Fig01 | `Fig01 Storage Account Secure Baseline.png` | Private and HTTPS-only storage defaults |
| Fig02 | `Fig02 Insecure Storage Configuration.png` | Public access enabled and HTTPS-only disabled |
| Fig03 | `Fig03 Insecure Storage Policy Findings.png` | Two storage policy findings |
| Fig04 | `Fig04 Storage Security Remediation.png` | Secure settings restored and findings cleared |
| Fig05 | `Fig05 Source File and Original SHA256.png` | Source content and original hash |
| Fig06 | `Fig06 Blob Upload and Stored Digest.png` | Upload metadata and stored SHA-256 |
| Fig07 | `Fig07 Blob Listing and Integrity Verification.png` | Blob inventory and `integrity_ok: true` |
| Fig08 | `Fig08 Storage Data Role Assignment.png` | Storage-scoped data role |
| Fig09 | `Fig09 Storage Data Role Scope Validation.png` | Blob access succeeds; group administration denied |
| Fig10 | `Fig10 Blob Download and Recovered Digest.png` | Download path and recovered digest |
| Fig11 | `Fig11 Recovered File SHA256 Match.png` | Matching hashes and byte comparison |
| Fig12 | `Fig12 Known Good Pre-Backup State.png` | Running VM and clean policy before backup |
| Fig13 | `Fig13 Known Good Backup Creation.png` | Backup label, path, checksum, and listing |
| Fig14 | `Fig14 Post Backup VM State Change.png` | VM stopped after backup |
| Fig15 | `Fig15 Restore Confirmation Safeguard.png` | Restore rejected without `--confirm` |
| Fig16 | `Fig16 Backup Restore and VM Recovery.png` | Verified restore and running VM recovered |
| Fig17 | `Fig17 E03 Storage and Recovery Audit Log.png` | E03 audit events |
| Fig18 | `Fig18 E03 Evidence File and SHA256.png` | Evidence export checksum verification |

---

## Security Findings

### Finding 1: Public storage access creates an exposure risk

When `public_access` was set to `true`, the policy scanner reported `Public access enabled`. Disabling public access restored the private-storage control.

### Finding 2: Disabling HTTPS weakens transport protection

When `https_only` was set to `false`, the scanner reported `HTTPS not enforced`. Restoring `https_only: true` returned the storage configuration to the secure baseline.

### Finding 3: Storage data access should not imply resource administration

The `Storage Blob Data Contributor` assignment allowed `blob-operator` to list data at `storage:sticdfalab`. The same identity was denied when attempting to tag the resource group, demonstrating separation between data-plane and management-plane privileges.

### Finding 4: SHA-256 supports integrity verification

A matching expected and actual SHA-256 digest verified the stored blob. Matching original and recovered hashes, combined with `cmp`, demonstrated content equality after download.

### Finding 5: Recovery must be tested, not merely configured

The known-good backup was followed by a deliberate VM state change and a confirmed restore. The recovered VM state showed that restoration worked for simulated inventory.

---

## Laboratory E03 Troubleshooting

Use the checks below without resetting the simulator. Preserve the shared E01-E03 workspace unless the instructor explicitly requires a restart.


### Error: Storage account already exists

Inspect the current storage state instead of recreating it:

```bash
python3 azlocal.py storage list
```

### Error: Resource group is locked

```bash
python3 azlocal.py group unlock rg-icdfa-lab
```

### Error: Local upload file not found

```bash
pwd
ls -l samples/operations_data.txt
```

Use the correct path from the package directory.

### Error: Educational upload limit exceeded

The simulator limit is 5 MB. Use the small non-sensitive text file specified in this guide.

### Error: RBAC denied for blob data operation

Verify the quoted role and exact scope:

```bash
python3 azlocal.py access list
```

Expected assignment:

```text
blob-operator | Storage Blob Data Contributor | storage:sticdfalab
```

### Error: Destination already exists

The simulator does not overwrite downloads. Remove only the previous student-owned output or choose a new destination:

```bash
rm -f recovered/operations_data_recovered.txt
```

### Error: Backup label already exists

Inspect current backups:

```bash
python3 azlocal.py backup list
```

If `known-good.json` exists from the current valid run, do not recreate it. Continue with the recovery test.

### Restore does not modify blob files

This is expected. Version 1.0 restores simulated inventory only. Blob files are explicitly excluded from restoration.

### Recovered VM remains stopped

Confirm that `vm-demo` was running before the backup was created. Recovery returns the state captured at backup time.

---

## Laboratory E03 Completion Checklist

Complete this checklist only from actual terminal evidence. A failed operation may be marked complete only when failure was the intended security control, such as a management-plane RBAC denial or restore rejection without `--confirm`.


### Part A: Storage security

- [ ] `sticdfalab` created with secure defaults
- [ ] Public access deliberately enabled for testing
- [ ] HTTPS-only deliberately disabled for testing
- [ ] Both policy findings captured
- [ ] Public access disabled
- [ ] HTTPS-only restored
- [ ] Clean policy result captured

### Part B: Data and integrity

- [ ] Non-sensitive source file created or validated
- [ ] Original SHA-256 recorded
- [ ] Blob uploaded
- [ ] Blob inventory listed
- [ ] Blob verification returned `integrity_ok: true`
- [ ] Storage data role assigned at account scope
- [ ] Blob-operator data access succeeded
- [ ] Blob-operator group administration was denied
- [ ] Blob downloaded to a new destination
- [ ] Original and recovered hashes matched
- [ ] Byte comparison confirmed equality

### Part C: Recovery

- [ ] VM confirmed running before backup
- [ ] Policy clean before backup
- [ ] `known-good` backup created
- [ ] Backup checksum recorded
- [ ] VM stopped after backup
- [ ] Restore confirmation safeguard tested
- [ ] Backup restored with `--confirm`
- [ ] Restore returned `verified: true`
- [ ] VM returned to running state
- [ ] Inventory-only restoration limitation documented

### Evidence and documentation

- [ ] E03 audit events reviewed
- [ ] Final evidence file saved
- [ ] Evidence checksum created and verified
- [ ] Screenshots accurately named and stored
- [ ] No sensitive data or `workspace/` state staged for GitHub

---

## Repository Structure

The following is a layout example, not a terminal command:

```text
CCSE-102-Integrated-Azure-Operations-Lab/
├── README.md
├── .gitignore
├── evidence/
│   ├── E01/
│   ├── E02/
│   └── E03/
│       └── outputs/
│           ├── e03-final-evidence.txt
│           └── e03-final-evidence.sha256
├── screenshots/
│   ├── E01/
│   ├── E02/
│   └── E03/
│       ├── Fig01 Storage Account Secure Baseline.png
│       ├── Fig02 Insecure Storage Configuration.png
│       └── ...
├── recovered/
│   └── operations_data_recovered.txt
└── notes/
```

Do not commit the generated `workspace/` directory.

---

## Limitations

- Storage accounts and security settings are simulated locally.
- Blob metadata is recorded in simulator state, while blob content is copied to a local workspace directory.
- SHA-256 verifies content integrity but does not encrypt data or authenticate the file's author.
- The data-plane role is a simplified educational RBAC model.
- The backup contains simulator inventory state and a checksum.
- Restoration does not revert uploaded blob files.
- No Azure Storage redundancy, lifecycle management, soft delete, versioning, immutable storage, or Recovery Services vault is configured.

---

## Academic Integrity and AI Disclosure

All commands, outputs, screenshots, hashes, and interpretations submitted for E03 must come from the student's independently executed laboratory work.

Microsoft Copilot may be disclosed as having assisted with document organization and implementation clarity. Copilot-generated content does not replace execution, evidence capture, checksum verification, recovery testing, or technical interpretation by the student.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Laboratory E03 · Storage Security, File Integrity and Recovery**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
