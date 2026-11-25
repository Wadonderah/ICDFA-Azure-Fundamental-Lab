<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:071A2B,45:0B5CAD,100:00A4EF&height=230&section=header&text=Monitoring%20%26%20Operational%20Assurance&fontSize=38&fontColor=FFFFFF&fontAlignY=35&desc=Alert%20Validation%20%7C%20Audit%20Traceability%20%7C%20Evidence%20Integrity&descSize=17&descAlignY=57&animation=fadeIn" width="100%" alt="CCSE-102 Laboratory E04 monitoring audit and assurance banner" />

# 📊 CCSE-102 Laboratory E04
### Monitoring, Audit and Operational Assurance

<p>
  <img src="https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux platform" />
  <img src="https://img.shields.io/badge/Runtime-Python%203.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.10 or later" />
  <img src="https://img.shields.io/badge/Environment-Offline%20Azure--Style%20Simulator-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Offline Azure-style simulator" />
</p>

<p>
  <img src="https://img.shields.io/badge/Monitoring-85%25%20CPU%20Threshold-0B5CAD?style=flat-square&logo=prometheus&logoColor=white" alt="85 percent CPU threshold" />
  <img src="https://img.shields.io/badge/Alerts-2%20Validated-C65911?style=flat-square&logo=opsgenie&logoColor=white" alt="Two validated alerts" />
  <img src="https://img.shields.io/badge/Audit-34%20Events-6F42C1?style=flat-square&logo=datadog&logoColor=white" alt="Thirty-four audit events" />
  <img src="https://img.shields.io/badge/Policy-0%20Findings-2EA44F?style=flat-square&logo=checkmarx&logoColor=white" alt="Zero policy findings" />
  <img src="https://img.shields.io/badge/Assurance-SHA--256-232F3E?style=flat-square&logo=letsencrypt&logoColor=white" alt="SHA-256 assurance" />
</p>

**Threshold-based detection · Cumulative audit analysis · Secure-state validation · Checksum-protected assurance evidence**

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
| Laboratory | E04: Monitoring, Audit and Operational Assurance |
| Assessment weighting | 25 marks |
| Student | Wadondera A. Collins |
| Cohort | CCSE Cohort 11, L1/S1 |
| Environment | WSL Ubuntu on a local workstation |
| Simulator | ICDFA `azlocal.py` offline Azure-style simulator, version 1.0 |
| Evidence date | 25 November 2026 |
| Report status | Completed technical assessment report |

---

## 1. Executive Summary

Laboratory E04 assessed operational monitoring, threshold-based alert generation, audit traceability, final-state review, and integrity protection of assurance evidence. A monitoring rule named `high-cpu` was configured for the `cpu_percent` metric at an 85-percent threshold. The simulator generated four deterministic samples: `vm-demo` at 32, 86, and 94 percent, and `storage-demo` at 8 percent. The 86-percent and 94-percent VM readings triggered two alerts, while the 32-percent and 8-percent readings remained below threshold.

The cumulative audit review returned 34 events and visibly included initialization, resource-group creation, tagging, role assignment, and RBAC checks. The output was exported through `tee`, and a SHA-256 checksum file was created. A final operational review confirmed the retained storage object, secure storage settings, known-good backup, two CPU alerts, and a policy result containing zero findings.

The machine-readable cloud operations report was then generated at `evidence/cloud_operations_report.json`. Its SHA-256 digest was recorded and verified with `sha256sum -c`, which returned `OK`. The evidence demonstrates that the final simulated environment was monitored, traceable, policy-compliant, and supported by integrity-verifiable assurance artifacts.

---

## 2. Scope and Evidence Standard

### 2.1 Simulation boundary

The CPU metrics, alert evaluation, audit events, resource inventory, policy checks, and JSON report were produced by the local ICDFA simulator. The evidence does not represent Microsoft Azure Monitor, Log Analytics, Azure Activity Log, Microsoft Sentinel, or a live Azure Policy deployment.

The terminal execution, audit export, SHA-256 calculations, checksum verification, screenshot capture, and report preparation were real local Linux activities.

### 2.2 Evidence assessment criteria

| Classification | Meaning | Treatment in this report |
|---|---|---|
| Verified | Visible command and output demonstrate the required result | Reported as passed |
| Contextually verified | A combined screenshot contains multiple commands whose visible output supports the scenario | Reported with precise boundaries |
| Not evidenced | The output is not visible or does not prove the stated control | Not claimed as completed |

All five supplied screenshots were reviewed against their visible commands and outputs before naming and placement.

---

## 3. Assessment Objectives

1. Configure an enabled CPU-threshold monitoring rule.
2. Generate operational metric samples.
3. Validate alerts at or above the configured threshold.
4. Review the cumulative audit trail across the integrated practical.
5. Export audit evidence and create a checksum record.
6. Review the final resource and security posture.
7. Confirm that deliberate security weaknesses remained remediated.
8. Generate a machine-readable operational-assurance report.
9. Verify the assurance report with SHA-256.

---

## 4. Monitoring-Control Assessment

### 4.1 CPU-threshold rule

The rule was created with:

```bash
python3 azlocal.py monitor rule high-cpu --threshold 85
```

The output identified rule `high-cpu`, metric `cpu_percent`, threshold `85`, and `enabled: true`.

<img width="491" height="132" alt="Fig01 High CPU Monitoring Rule" src="https://github.com/user-attachments/assets/94111347-6e6c-49b9-92e1-937ddf5140fe" />


**Figure 1. High CPU Monitoring Rule.** The threshold control was enabled successfully at 85 percent.

### 4.2 Metric generation and alert evaluation

The sample and alert commands were executed together:

```bash
python3 azlocal.py monitor sample
python3 azlocal.py monitor alerts
```

Four samples were added:

| Resource | CPU reading | Threshold outcome |
|---|---:|---|
| `vm-demo` | 32% | Below threshold |
| `vm-demo` | 86% | Alert triggered |
| `vm-demo` | 94% | Alert triggered |
| `storage-demo` | 8% | Below threshold |

The alert output returned `count: 2`. Both alerts referenced `vm-demo`, rule `high-cpu`, threshold `85`, and values `86` and `94`.

<img width="332" height="583" alt="Fig02 Operational Metrics and Triggered Alerts" src="https://github.com/user-attachments/assets/127b7d52-8cbf-4372-97f5-78c95fa26a61" />


**Figure 2. Operational Metrics and Triggered Alerts.** The threshold logic correctly included the two readings above 85 percent and excluded the readings below the threshold.

### 4.3 Monitoring interpretation

The results demonstrate deterministic threshold evaluation rather than predictive analytics. The rule evaluated stored samples and generated an alert for every value greater than or equal to 85. The screenshot shows one sampling run, so the expected alert count remained two.

The `storage-demo` label is a hard-coded metric resource in simulator version 1.0. The label is not the storage account `sticdfalab`.

---

## 5. Audit and Traceability Assessment

### 5.1 Cumulative audit review

The audit trail was reviewed and exported:

```bash
python3 azlocal.py monitor logs --limit 100
python3 azlocal.py monitor logs --limit 100 | tee evidence/outputs/audit-log.json
sha256sum evidence/outputs/audit-log.json | tee evidence/outputs/audit-log.sha256
```

The visible output returned `count: 34`. Representative events included:

- `init` by `student-admin`
- `group-create` for `rg-icdfa-lab`
- `group-tag`
- `rbac-assign` for the group-scoped analyst Reader role
- `rbac-check` showing analyst read permitted

The audit records visibly contained `action`, `actor`, `detail`, `outcome`, and UTC `time` fields. The sequence demonstrates cumulative traceability from the earlier laboratories into E04.

<img width="476" height="637" alt="Fig03 Cumulative Audit Log and Integrity Evidence" src="https://github.com/user-attachments/assets/f4b69bd9-66a9-4ad7-8301-117bb2d77662" />


**Figure 3. Cumulative Audit Log and Integrity Evidence.** The audit trail preserved attributed and time-stamped evidence across the integrated laboratory.

### 5.2 Audit-integrity interpretation

The visible command created `evidence/outputs/audit-log.sha256`. The screenshot does not show a subsequent `sha256sum -c` result for the audit export. Therefore, the report confirms checksum creation but does not claim that audit-checksum verification was visibly demonstrated in this figure.

Recommended final verification:

```bash
sha256sum -c evidence/outputs/audit-log.sha256
```

Expected result:

```text
evidence/outputs/audit-log.json: OK
```

---

## 6. Final-State Assurance Assessment

The final state was reviewed using status, group, access, VM, NSG, storage, backup, alert, and policy commands. The supplied screenshot visibly shows the later portion of the combined output.

Visible final-state evidence included:

- Storage account `sticdfalab`
- Blob `operations-file`
- Blob size `138` bytes
- Blob SHA-256 `3fca24dcc7f333d96d247c3c18ab422cf845ade4b3f462c40abf351c954efd53`
- `https_only: true`
- `public_access: false`
- Backup `known-good.json`
- Two `high-cpu` alerts at 86 and 94 percent
- Policy `findings_count: 0`
- `simulation: true`

<img width="457" height="634" alt="Fig04 Final Secure Inventory and Policy Review" src="https://github.com/user-attachments/assets/cc47a4e2-704d-4989-b526-1d2c0223d679" />


**Figure 4. Final Secure Inventory and Policy Review.** The visible final configuration retained secure storage settings, recovery evidence, expected alerts, and a zero-finding policy result.

### 6.1 Assurance conclusion from the final state

The final policy result confirms that the deliberate SSH and storage weaknesses introduced during E02 and E03 were no longer active. The storage account remained private and HTTPS-only, and the known-good backup remained available. The screenshot also confirms that the uploaded operations file remained registered after inventory restoration, which is consistent with the simulator's inventory-only restore limitation.

---

## 7. Machine-Readable Assurance Artifact

### 7.1 Report generation

The final report was generated with:

```bash
python3 azlocal.py report --output evidence/cloud_operations_report.json
```

The simulator returned:

```text
report: /home/wadon/lab/evidence/cloud_operations_report.json
sha256: 05cf5aba7217004a37df732dffb2d4b3b6c73aae560d5de6eea23d7274769903
```

### 7.2 Independent checksum record and verification

The corresponding shell commands were:

```bash
sha256sum evidence/cloud_operations_report.json \
  | tee evidence/cloud_operations_report.sha256

sha256sum -c evidence/cloud_operations_report.sha256
```

The separately calculated digest matched the digest returned by the simulator. Verification returned:

```text
evidence/cloud_operations_report.json: OK
```

<img width="562" height="155" alt="Fig05 Assurance Report SHA256 Verification" src="https://github.com/user-attachments/assets/05f22d66-d6ab-4ac4-9773-a9538df69c1b" />


**Figure 5. Assurance Report SHA256 Verification.** The machine-readable report was generated and independently verified without modification.

---

## 8. Findings Register

### E04-F01: CPU threshold breaches detected

- **Condition:** `vm-demo` recorded 86% and 94% CPU samples.
- **Threshold:** 85%.
- **Detection:** Two `high-cpu` alerts were generated.
- **Operational significance:** Elevated utilization was identified for investigation.
- **Status:** Verified.

### E04-F02: Low samples correctly excluded

- **Condition:** `vm-demo` recorded 32%; `storage-demo` recorded 8%.
- **Detection:** Neither reading appeared in the alert list.
- **Operational significance:** The rule did not generate alerts for values below the threshold.
- **Status:** Verified.

### E04-F03: Cumulative audit traceability available

- **Condition:** The audit query returned 34 events.
- **Evidence:** Governance, tagging, RBAC assignment, and permission-check entries were visible.
- **Operational significance:** Administrative activity remained attributable and time-stamped.
- **Status:** Verified.

### E04-F04: Final policy posture clean

- **Condition:** Previous deliberate network and storage weaknesses had been remediated.
- **Evidence:** `findings_count: 0`.
- **Operational significance:** The final simulator state passed all implemented policy checks.
- **Status:** Verified.

### E04-F05: Assurance report integrity validated

- **Condition:** The JSON assurance report was generated and hashed.
- **Evidence:** Simulator and shell digests matched; `sha256sum -c` returned `OK`.
- **Operational significance:** Subsequent report modification can be detected.
- **Status:** Verified.

### E04-F06: Audit checksum verification not visible

- **Condition:** The audit checksum creation command is visible, but its `-c` verification result is not shown.
- **Operational significance:** Checksum creation is evidenced; independent verification should be captured separately if required.
- **Status:** Advisory evidence gap.

---

## 9. Results Matrix

| Assessment item | Expected outcome | Observed outcome | Status |
|---|---|---|---|
| Monitoring rule | Enabled at 85% | Enabled, threshold 85 | Pass |
| Metric samples | Four deterministic readings | 32, 86, 94, and 8 | Pass |
| Alert evaluation | Alerts for 86 and 94 | Two alerts returned | Pass |
| Low-value exclusion | No alerts for 32 and 8 | Excluded from alerts | Pass |
| Audit review | Cumulative events available | 34 events returned | Pass |
| Audit export | Local JSON evidence created | Export command visible | Pass |
| Audit checksum creation | Digest file created | Creation command visible | Pass |
| Audit checksum verification | `OK` result | Not visible | Advisory |
| Final storage state | Private and HTTPS-only | Confirmed | Pass |
| Backup continuity | `known-good.json` retained | Confirmed | Pass |
| Final policy | Zero findings | Confirmed | Pass |
| JSON assurance report | Generated successfully | Path and digest returned | Pass |
| Report SHA-256 verification | Verification returns `OK` | Confirmed | Pass |

---

## 10. Risk Register

| Risk ID | Risk | Likelihood | Impact | Control | Evidence/status |
|---|---|---:|---:|---|---|
| E04-R01 | High CPU condition is not detected | Medium | High | 85% `high-cpu` rule | Controlled; two breaches detected |
| E04-R02 | Repeated sampling creates duplicate alerts | Medium | Medium | Run sample once and record sample count | One run evidenced; alert count two |
| E04-R03 | Administrative actions are not traceable | Medium | High | Cumulative audit log | 34 events returned |
| E04-R04 | Prior security weaknesses remain active | Medium | High | Final policy scan | Zero findings |
| E04-R05 | Assurance report is modified after generation | Medium | High | SHA-256 checksum and `-c` verification | Controlled; `OK` shown |
| E04-R06 | Audit export is modified without detection | Medium | High | Audit SHA-256 file | Checksum created; verification screenshot recommended |

---

## 11. Evidence Register and Exact File Naming

Store the files under `screenshots/E04/` in this exact order:

| Order | Exact filename | Original screenshot | Scenario matched |
|---:|---|---|---|
| 1 | `Fig01 High CPU Monitoring Rule.png` | `Screenshot 2026-11-25 081326.png` | Enabled 85% CPU rule |
| 2 | `Fig02 Operational Metrics and Triggered Alerts.png` | `Screenshot 2026-11-25 081447.png` | Four samples and two threshold alerts |
| 3 | `Fig03 Cumulative Audit Log and Integrity Evidence.png` | `Screenshot 2026-11-25 082239.png` | 34 audit events, export, and checksum creation |
| 4 | `Fig04 Final Secure Inventory and Policy Review.png` | `Screenshot 2026-11-25 082645.png` | Storage, backup, alerts, and zero findings |
| 5 | `Fig05 Assurance Report SHA256 Verification.png` | `Screenshot 2026-11-25 082838.png` | Report generation, matching digest, and `OK` verification |

### Optional additional evidence

If audit checksum verification is captured separately, add:

```text
Fig06 Audit Log SHA256 Verification.png
```

Do not create Figure 6 unless the screenshot visibly shows:

```text
evidence/outputs/audit-log.json: OK
```

---

## 12. Troubleshooting Record

| Symptom | Likely cause | Corrective action |
|---|---|---|
| Alert count exceeds two | `monitor sample` was run more than once | Record the number of sample runs; do not reset solely to reduce the count |
| No alerts appear | Rule or sample was not created | Run the rule, sample once, then evaluate alerts |
| Early E01 events are missing | Audit limit is too low | Increase `--limit` to 100 or 200 |
| Policy shows SSH exposure | Priority 200 rule remains | Remove priority 200 and re-run policy |
| Policy shows storage findings | Public access or HTTPS setting is insecure | Set public access false and HTTPS-only true |
| Checksum verification fails | Evidence changed after hashing | Investigate the change, then regenerate the checksum deliberately |
| JSON cannot be parsed | File was edited or generated incorrectly | Regenerate with `azlocal.py report`; do not repair manually |
| `storage-demo` seems unfamiliar | Hard-coded monitoring label | Record it as simulator sample data, not `sticdfalab` |

---

## 13. Completion Checklist

### Monitoring

- [x] `high-cpu` rule created
- [x] Threshold set to 85%
- [x] Rule enabled
- [x] Four samples generated
- [x] 86% and 94% alerts identified
- [x] 32% and 8% readings excluded

### Audit and traceability

- [x] Cumulative audit log reviewed
- [x] Audit count recorded as 34
- [x] Governance and RBAC events identified
- [x] Audit output exported
- [x] Audit checksum creation command executed
- [ ] Optional audit checksum `-c` verification screenshot captured

### Final-state assurance

- [x] Storage inventory reviewed
- [x] Storage remained private and HTTPS-only
- [x] Known-good backup retained
- [x] Two alerts retained
- [x] Final policy returned zero findings
- [x] Simulation status visibly identified

### Assurance artifact

- [x] JSON report generated
- [x] Report path recorded
- [x] Simulator digest recorded
- [x] Independent SHA-256 digest matched
- [x] `sha256sum -c` returned `OK`
- [x] Screenshots named and matched correctly

---

## 14. Limitations

1. Monitoring samples are deterministic educational values, not live telemetry.
2. Alerts are evaluated from stored samples and do not send notifications.
3. `storage-demo` is a hard-coded sample label, not the actual `sticdfalab` account.
4. Audit events are local simulator records rather than Azure Activity Log events.
5. The JSON report summarizes selected inventory fields and is not an enterprise compliance report.
6. The policy scanner evaluates only the controls implemented in simulator version 1.0.
7. SHA-256 detects changes but does not encrypt evidence or prove authorship.
8. Audit checksum creation is visible, but a separate `sha256sum -c` result for the audit export was not supplied.

---

## 15. Recommendations

1. Preserve the final zero-finding policy state when packaging the project.
2. Do not generate additional monitoring samples unless a repeat test is explicitly required.
3. Capture the optional audit checksum verification to complete the evidence chain.
4. Store the JSON report and checksum together in the repository.
5. Retain the original screenshots and use the exact renamed copies under `screenshots/E04/`.
6. Exclude `workspace/` because it contains local simulator state and audit records.
7. Explain explicitly in the final PDF that monitoring and auditing were simulated locally.

---

## 16. Conclusion

Laboratory E04 successfully demonstrated threshold-based monitoring, alert evaluation, cumulative audit traceability, final security-posture validation, and checksum-protected assurance reporting. The 85-percent CPU rule detected exactly two qualifying VM readings. The audit query returned 34 attributed events, and the final policy assessment returned zero findings.

The machine-readable cloud operations report was generated and independently verified with SHA-256. Together, the evidence shows that the final simulated environment was operationally monitored, auditable, securely configured, and supported by integrity-verifiable artifacts. A separate audit checksum verification screenshot is recommended but does not alter the validated report-checksum result.

---

## 17. Academic Integrity and AI Assistance Disclosure

All commands, outputs, screenshots, alert counts, audit findings, and checksums in the final submission must represent laboratory work independently executed and verified by Wadondera A. Collins.

Microsoft Copilot was used to organize this report, inspect the supplied screenshots, match each image to the visible technical scenario, and distinguish verified results from the optional audit-checksum evidence gap. Copilot did not execute the WSL laboratory or manufacture terminal evidence.

---

## 18. Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Laboratory E04 · Technical Documentation and Evidence Report**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
