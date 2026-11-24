<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:071A2B,45:0B5CAD,100:00A4EF&height=230&section=header&text=Storage%20Security%20%26%20Recovery&fontSize=40&fontColor=FFFFFF&fontAlignY=35&desc=Integrity%20Validation%20%7C%20Scoped%20Access%20%7C%20Known-Good%20Recovery&descSize=17&descAlignY=57&animation=fadeIn" width="100%" alt="CCSE-102 Laboratory E03 storage security integrity and recovery banner" />

# 🔐 CCSE-102 Laboratory E03
### Storage Security, File Integrity and Recovery

<p>
  <img src="https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux platform" />
  <img src="https://img.shields.io/badge/Runtime-Python%203.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.10 or later" />
  <img src="https://img.shields.io/badge/Environment-Offline%20Azure--Style%20Simulator-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Offline Azure-style simulator" />
</p>

<p>
  <img src="https://img.shields.io/badge/Storage-Private%20%26%20HTTPS--Only-0B5CAD?style=flat-square&logo=files&logoColor=white" alt="Private and HTTPS-only storage" />
  <img src="https://img.shields.io/badge/Integrity-SHA--256-6F42C1?style=flat-square&logo=letsencrypt&logoColor=white" alt="SHA-256 integrity validation" />
  <img src="https://img.shields.io/badge/RBAC-Scoped%20Data%20Access-232F3E?style=flat-square&logo=auth0&logoColor=white" alt="Scoped data access" />
  <img src="https://img.shields.io/badge/Recovery-Known--Good%20Backup-2EA44F?style=flat-square&logo=icloud&logoColor=white" alt="Known-good backup recovery" />
  <img src="https://img.shields.io/badge/Report-Technical%20Assessment-C65911?style=flat-square&logo=readthedocs&logoColor=white" alt="Technical assessment report" />
</p>

**Storage hardening · SHA-256 integrity assurance · Least-privilege data access · Verified inventory recovery**

### Wadondera A. Collins
**ICDFA Trainee · Cohort 11 · Cloud Security Engineering**  
International Cybersecurity and Digital Forensics Academy

</div>

---

## Document Control

| Field | Record |
|---|---|
| Course | CCSE-102: Azure Operations & Administration |
| Practical | Integrated Azure Operations, Administration and Cloud Security Laboratory |
| Laboratory | E03: Storage Security, File Integrity and Recovery |
| Weighting | 25 marks |
| Environment | WSL Ubuntu; ICDFA offline simulator v1.0 |
| Evidence date | 24 November 2026 |
| Report status | Assessment draft with two open corrective actions |

---

## 1. Executive Summary

Laboratory E03 assessed storage hardening, data-integrity verification, scoped storage access, and recovery of simulated inventory. The storage account `sticdfalab` was created with public access disabled and HTTPS-only enabled. Controlled weakening of those settings produced two policy findings: public access enabled and HTTPS not enforced. Reinstating the secure values returned the policy result to zero findings.

A 138-byte local training file was created and assigned the SHA-256 digest `3fca24dcc7f333d96d247c3c18ab422cf845ade4b3f462c40abf351c954efd53`. The file was uploaded as `operations-file`. Its upload record, blob listing, and verification result showed the same digest, and the simulator returned `integrity_ok: true`.

The evidence also exposed two implementation errors. The `blob-operator` role assignment omitted the required storage scope from the executed command, so the positive data-access test failed. The blob-download sequence used invalid argument syntax, so no recovered file was created and no independent comparison was completed. These items are recorded as open corrective actions rather than passed controls.

The recovery test succeeded. A known-good backup was created while `vm-demo` was running and policy compliance was clean. After the VM was stopped, restoring `known-good` returned `verified: true`, restored the VM to `running`, and preserved a zero-finding policy state. The restore applied to simulator inventory only and did not revert blob files.

---

## 2. Scope and Evidence Standard

### 2.1 Scope boundary

The storage account, blob inventory, RBAC assignments, policy findings, VM states, and backups are local Azure-style simulations. No live Microsoft Azure Storage account, Azure Blob container, Azure Policy assignment, Azure Backup vault, or cloud VM was used.

Real Linux activities included creating the training file, calculating SHA-256, executing shell commands, and capturing terminal evidence.

### 2.2 Evidence classification

| Classification | Meaning | Reporting treatment |
|---|---|---|
| Verified | Visible command and output support the required result | Reported as passed |
| Expected denial | A correctly configured control rejects an unauthorized action | Reported as passed |
| Corrective action required | A syntax or sequencing error prevents the intended test | Reported as incomplete |

This method prevents unsuccessful commands from being described as successful implementation.

---

## 3. Assessment Objectives

1. Establish a secure storage baseline.
2. Detect and remediate public-access and HTTPS weaknesses.
3. Create and hash a non-sensitive local file.
4. Upload, list, and verify a simulated blob.
5. Separate storage data access from resource-management access.
6. Download and compare recovered content with the source.
7. Create a checksummed known-good inventory backup.
8. Change VM state, restore the backup, and verify recovery.

---

## 4. Storage Security Assessment

### 4.1 Secure baseline

The account was created and listed:

```bash
python3 azlocal.py storage create sticdfalab --group rg-icdfa-lab
python3 azlocal.py storage list
```

The account belonged to `rg-icdfa-lab`, contained no blobs, enforced HTTPS, and disabled public access.

<img width="461" height="222" alt="Fig01 Storage Account Secure Baseline" src="https://github.com/user-attachments/assets/d6e27dda-06e1-4ff1-9879-c58873341478" />


**Figure 1. Storage Account Secure Baseline.** `https_only` was `true` and `public_access` was `false`.

### 4.2 Deliberate weakness and detection

```bash
python3 azlocal.py storage set sticdfalab --public-access true --https-only false
python3 azlocal.py policy
```

The scanner checked three resources and returned two findings:

- `storage-private`: Public access enabled
- `storage-https`: HTTPS not enforced

<img width="575" height="350" alt="Fig02 Insecure Storage Policy Findings" src="https://github.com/user-attachments/assets/1f9d991a-0738-450f-8ca9-53d6a616e596" />


**Figure 2. Insecure Storage Policy Findings.** The policy engine detected both exposure and transport weaknesses.

### 4.3 Remediation validation

```bash
python3 azlocal.py storage set sticdfalab --public-access false --https-only true
python3 azlocal.py storage list
python3 azlocal.py policy
```

The secure values were restored and `findings_count` returned to `0`.

<img width="552" height="341" alt="Fig03 Storage Security Remediation" src="https://github.com/user-attachments/assets/1df611b9-0050-4294-997b-ea33dbe06cfe" />


**Figure 3. Storage Security Remediation.** Storage returned to private, HTTPS-only operation.

---

## 5. Integrity Assessment

### 5.1 Source integrity reference

A non-sensitive training file was created. Its original digest was:

```text
3fca24dcc7f333d96d247c3c18ab422cf845ade4b3f462c40abf351c954efd53
```

<img width="511" height="148" alt="Fig04 Source File and Original SHA256" src="https://github.com/user-attachments/assets/2dabca87-56f0-4581-9b5b-c6d03186b101" />


**Figure 4. Source File and Original SHA256.** The digest established the pre-upload integrity reference.

### 5.2 Upload and stored-content verification

```bash
python3 azlocal.py blob upload sticdfalab operations-file --file samples/operations_data.txt
python3 azlocal.py blob list sticdfalab
python3 azlocal.py blob verify sticdfalab operations-file
```

The source, upload record, blob listing, expected value, and actual value used the same digest. The simulator returned `integrity_ok: true`.

<img width="626" height="284" alt="Fig05 Blob Upload and Integrity Verification" src="https://github.com/user-attachments/assets/5a83bee7-c129-420e-b00f-e7f0b02a1d2d" />


**Figure 5. Blob Upload and Integrity Verification.** Upload-time and stored-content integrity were verified.

---

## 6. Access-Control Assessment

### 6.1 Observed result

The intended data-role assignment was entered as two independent shell lines. The first line omitted the mandatory scope; the second line attempted to execute `storage:sticdfalab` as a command. The simulator therefore did not create the assignment. Blob listing as `blob-operator` returned `RBAC DENIED`. The resource-group write attempt was also denied, but successful data access was never established.

<img width="537" height="150" alt="Fig06 Storage Data Role Assignment Requires Correction" src="https://github.com/user-attachments/assets/a54b60c4-52c3-4baa-854d-47fe45b4088d" />


**Figure 6. Storage Data Role Assignment Requires Correction.** This evidence documents an implementation error, not a passed least-privilege test.

### 6.2 Required corrective test

```bash
python3 azlocal.py access assign blob-operator \
  "Storage Blob Data Contributor" \
  storage:sticdfalab
python3 azlocal.py access list
python3 azlocal.py --actor blob-operator blob list sticdfalab
python3 azlocal.py --actor blob-operator group tag rg-icdfa-lab unauthorized test
echo $?
```

Successful replacement evidence must show the assignment, successful blob listing, denied group write, and exit code `3`.

**Replacement filename:** `Fig06 Storage Data Role Scope Validation.png`

---

## 7. Recovery-File Verification

### 7.1 Observed result

The download evidence used invalid syntax. No recovered file was produced; `sha256sum` and `cmp` consequently reported missing files. The text `Recovered file matches original` was typed as a command rather than produced by a successful conditional comparison.

The lower part of the same screenshot contains valid known-good backup evidence, but it does not repair the missing file-recovery proof.

<img width="499" height="624" alt="Fig07 Blob Recovery Commands Require Correction and Backup Creation" src="https://github.com/user-attachments/assets/b09d3028-5e05-4ec2-8c85-f1839fe4090a" />


**Figure 7. Blob Recovery Commands Require Correction and Backup Creation.** Download verification is incomplete; backup creation is valid.

### 7.2 Required corrective test

```bash
mkdir -p recovered
rm -f recovered/operations_data_recovered.txt
python3 azlocal.py blob download sticdfalab operations-file \
  --dest recovered/operations_data_recovered.txt
sha256sum samples/operations_data.txt recovered/operations_data_recovered.txt
cmp --silent samples/operations_data.txt recovered/operations_data_recovered.txt \
  && echo "Recovered file matches original"
```

Successful evidence must show the download path, matching hashes, and the `cmp` success message.

**Replacement filename:** `Fig07 Recovered File SHA256 Match.png`

---

## 8. Backup and Recovery Assessment

### 8.1 Known-good backup

Before backup creation, `vm-demo` was `running` and the policy scan returned zero findings. Backup `known-good` was created and listed as `known-good.json`.

Recorded checksum:

```text
5f5dfef49dcc2cc27aed8e028ac10180914fdae0057cdd71b9f185a1361afa63
```

### 8.2 Recovery validation

```bash
python3 azlocal.py vm stop vm-demo
python3 azlocal.py vm list
python3 azlocal.py backup restore known-good --confirm
python3 azlocal.py vm list
python3 azlocal.py policy
```

The controlled state change showed the VM as stopped. Restore returned `verified: true`; the VM then returned to running, and policy remained clean.

<img width="426" height="545" alt="Fig08 Backup Restore and VM Recovery" src="https://github.com/user-attachments/assets/d2a51835-a0a2-404a-811b-76466214e6d2" />


**Figure 8. Backup Restore and VM Recovery.** The known-good simulator inventory was restored successfully.

The output explicitly states that restoration is inventory-only and does not revert uploaded blob files.

---

## 9. Findings Register

### E03-F01: Public storage exposure

- **Condition:** `public_access: true`
- **Risk:** Unrestricted content exposure
- **Detection:** `storage-private` policy finding
- **Treatment:** Set public access to `false`
- **Residual status:** Closed

### E03-F02: HTTPS enforcement disabled

- **Condition:** `https_only: false`
- **Risk:** Insecure transport permitted by configuration
- **Detection:** `storage-https` policy finding
- **Treatment:** Set HTTPS-only to `true`
- **Residual status:** Closed

### E03-F03: Data-role assignment incomplete

- **Condition:** Scope omitted from the executed assignment
- **Impact:** Positive data-access test could not be completed
- **Treatment:** Re-run the complete scoped assignment
- **Residual status:** Open pending replacement Figure 6

### E03-F04: Independent download comparison incomplete

- **Condition:** Invalid download arguments prevented output creation
- **Impact:** Recovered-file equality was not demonstrated
- **Treatment:** Re-run download, SHA-256, and `cmp`
- **Residual status:** Open pending replacement Figure 7

---

## 10. Results Matrix

| Assessment item | Evidence outcome | Status |
|---|---|---|
| Secure storage baseline | Private and HTTPS-only | Pass |
| Weakness detection | Two findings | Pass |
| Storage remediation | Zero findings | Pass |
| Original digest | Recorded | Pass |
| Blob upload and verification | `integrity_ok: true` | Pass |
| Scoped data-role assignment | Missing scope | Open |
| Positive data access | Denied because assignment failed | Open |
| Management write denial | Denied | Repeat after corrected assignment |
| Blob download | File not created | Open |
| Independent hash comparison | Not completed | Open |
| Known-good backup | Checksum and file recorded | Pass |
| Inventory restore | `verified: true`; VM running | Pass |
| Post-restore policy | Zero findings | Pass |

---

## 11. Risk Register

| ID | Risk | Impact | Control | Status |
|---|---|---:|---|---|
| R01 | Public storage exposure | High | Disable public access | Controlled |
| R02 | HTTPS not enforced | High | Require HTTPS-only | Controlled |
| R03 | Incorrect role scope | Medium | Exact storage-scoped assignment | Open |
| R04 | Invalid download syntax | High | Parser-supported `--dest` option | Open |
| R05 | Undetected content change | High | SHA-256 before upload and after download | Partial |
| R06 | Inventory loss | High | Checksummed backup and tested restore | Controlled |

---

## 12. Evidence Register

| Order | Exact filename | Original screenshot | Status |
|---:|---|---|---|
| 1 | `Fig01 Storage Account Secure Baseline.png` | `Screenshot 2026-11-24 130919.png` | Valid |
| 2 | `Fig02 Insecure Storage Policy Findings.png` | `Screenshot 2026-11-24 130954.png` | Valid |
| 3 | `Fig03 Storage Security Remediation.png` | `Screenshot 2026-11-24 131335.png` | Valid |
| 4 | `Fig04 Source File and Original SHA256.png` | `Screenshot 2026-11-24 131452.png` | Valid |
| 5 | `Fig05 Blob Upload and Integrity Verification.png` | `Screenshot 2026-11-24 131556.png` | Valid |
| 6 | `Fig06 Storage Data Role Assignment Requires Correction.png` | `Screenshot 2026-11-24 131726.png` | Replace |
| 7 | `Fig07 Blob Recovery Commands Require Correction and Backup Creation.png` | `Screenshot 2026-11-24 131946.png` | Replace download portion |
| 8 | `Fig08 Backup Restore and VM Recovery.png` | `Screenshot 2026-11-24 132043.png` | Valid |

---

## 13. Troubleshooting Record

| Symptom | Cause | Corrective action |
|---|---|---|
| Missing `scope` error | Scope entered on a separate line | Include scope in the assignment command |
| Blob access denied | Role assignment was not created | Correct assignment, verify, then retry |
| Download rejects command | Unsupported argument form | Use `--dest <path>` |
| Recovered file missing | Download failed | Complete download before hash comparison |
| Success text treated as command | Text entered directly | Use `cmp ... && echo ...` |
| Blob files unchanged after restore | Inventory-only backup design | Record limitation; do not claim blob rollback |

---

## 14. Corrective Action and Completion Status

### Verified

- [x] Secure storage baseline
- [x] Two storage findings detected
- [x] Storage remediated
- [x] Source digest recorded
- [x] Blob upload and integrity verified
- [x] Known-good backup created
- [x] VM state changed and restored
- [x] Restore verified
- [x] Final policy clean

### Outstanding

- [ ] Correct storage data-role assignment
- [ ] Successful blob listing as `blob-operator`
- [ ] Management denial after correct assignment
- [ ] Successful blob download
- [ ] Matching original and recovered hashes
- [ ] Successful byte comparison
- [ ] Replace Figures 6 and 7
- [ ] Capture E03 audit log if required
- [ ] Export and hash final E03 evidence

---

## 15. Limitations

1. Storage and recovery controls are simulated locally.
2. Blob data resides in the simulator workspace.
3. SHA-256 verifies integrity but does not encrypt data or authenticate authorship.
4. Backup restoration covers inventory only.
5. Current evidence does not prove scoped data access or downloaded-file equality.
6. Azure redundancy, soft delete, versioning, immutability, and Recovery Services were not configured.

---

## 16. Recommendations

1. Keep `sticdfalab` private and HTTPS-only.
2. Re-run the data-role and download procedures exactly as documented.
3. Replace Figures 6 and 7 rather than presenting errors as successful evidence.
4. Preserve `known-good` and do not reset before E04.
5. Exclude `workspace/` from GitHub.

---

## 17. Conclusion

E03 successfully demonstrated storage hardening, policy detection, upload-integrity verification, and tested inventory recovery. The backup restored `vm-demo` from stopped to running with verification and a clean policy result.

The data-role assignment and independent downloaded-file comparison remain incomplete. The report therefore records two open corrective actions and does not claim unsupported completion.

---

## 18. Academic Integrity and AI Assistance Disclosure

All final commands, outputs, screenshots, hashes, and conclusions must represent laboratory work independently executed and verified by Wadondera A. Collins.

Microsoft Copilot was used to organize this report, match screenshots to visible evidence, and identify command failures requiring correction. Copilot did not execute the WSL session or manufacture results.

---

## 19. Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy
