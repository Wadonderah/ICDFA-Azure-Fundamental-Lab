<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:071A2B,45:0B5CAD,100:00A4EF&height=230&section=header&text=Monitoring%20%26%20Operational%20Assurance&fontSize=38&fontColor=FFFFFF&fontAlignY=35&desc=Alerting%20%7C%20Audit%20Investigation%20%7C%20Evidence%20Integrity&descSize=18&descAlignY=57&animation=fadeIn" width="100%" alt="CCSE-102 Laboratory E04 monitoring audit and assurance banner" />

# 📊 CCSE-102 Laboratory E04
### Monitoring, Audit and Operational Assurance

<p>
  <img src="https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux platform" />
  <img src="https://img.shields.io/badge/Runtime-Python%203.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.10 or later" />
  <img src="https://img.shields.io/badge/Environment-Offline%20Azure--Style%20Simulator-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Offline Azure-style simulator" />
</p>

<p>
  <img src="https://img.shields.io/badge/Monitoring-CPU%20Thresholds-0B5CAD?style=flat-square&logo=prometheus&logoColor=white" alt="CPU threshold monitoring" />
  <img src="https://img.shields.io/badge/Alerts-Operational%20Detection-C65911?style=flat-square&logo=opsgenie&logoColor=white" alt="Operational alert detection" />
  <img src="https://img.shields.io/badge/Audit-Event%20Traceability-6F42C1?style=flat-square&logo=datadog&logoColor=white" alt="Audit event traceability" />
  <img src="https://img.shields.io/badge/Assurance-SHA--256-2EA44F?style=flat-square&logo=letsencrypt&logoColor=white" alt="SHA-256 evidence assurance" />
  <img src="https://img.shields.io/badge/Project-E04-232F3E?style=flat-square&logo=github&logoColor=white" alt="Laboratory E04" />
</p>

**Threshold-based monitoring · Alert investigation · Cumulative audit review · Final-state assurance · Evidence integrity**

### Wadondera A. Collins
**ICDFA Trainee · Cohort 11 · Cloud Security Engineering**  
International Cybersecurity and Digital Forensics Academy

</div>

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Simulation Boundary](#simulation-boundary)
3. [Security and Operations Objectives](#security-and-operations-objectives)
4. [Prerequisites and Start Conditions](#prerequisites-and-start-conditions)
5. [Laboratory Resources](#laboratory-resources)
6. [Part A: Monitoring and Alerting](#part-a-monitoring-and-alerting)
7. [Part B: Audit Investigation](#part-b-audit-investigation)
8. [Part C: Final-State Assurance](#part-c-final-state-assurance)
9. [Part D: Assurance Report and SHA-256](#part-d-assurance-report-and-sha-256)
10. [Evidence Register](#evidence-register)
11. [Operational Findings](#operational-findings)
12. [Troubleshooting](#troubleshooting)
13. [Completion Checklist](#completion-checklist)
14. [Repository Structure](#repository-structure)
15. [Limitations](#limitations)
16. [Author](#author)

---

## Project Overview

Laboratory E04 is the fourth compulsory laboratory in the CCSE-102 Integrated Azure Operations, Administration and Cloud Security practical. E04 builds on the cumulative simulator state created in E01, E02, and E03. The laboratory configures threshold-based monitoring, evaluates generated alerts, investigates the audit trail, validates the final secure configuration, and produces a checksum-protected assurance report.

| Item | Detail |
|---|---|
| Laboratory | E04 |
| Title | Monitoring, Audit and Operational Assurance |
| Marks | 25 |
| Platform | Linux workstation |
| Runtime | Python 3.10 or later |
| Simulator | `azlocal.py` version 1.0 |
| Alert rule | `high-cpu` |
| Metric | `cpu_percent` |
| Threshold | `85` percent |
| Expected qualifying readings | `86` and `94` percent |
| Assurance report | `evidence/E04/cloud_operations_report.json` |
| Integrity algorithm | SHA-256 |

> **Critical continuity rule:** Continue using the existing simulator workspace. Do not initialize or reset the simulator. The E04 audit review depends on events accumulated during E01, E02, and E03.

---

## Simulation Boundary

### Simulated operations

- CPU monitoring-rule creation
- Deterministic metric generation
- Threshold-based alert evaluation
- Audit-log investigation
- Resource inventory review
- Final policy assessment
- JSON assurance-report generation

### Real Linux operations

- Saving audit output with `tee`
- Calculating SHA-256 checksums
- Validating checksum files with `sha256sum -c`
- Organizing evidence and screenshots
- Reviewing JSON files locally

The monitoring samples are educational simulator data, not live telemetry from Microsoft Azure Monitor. The audit log is local simulator evidence, not the Azure Activity Log.

---

## Security and Operations Objectives

By completing E04, the student should be able to:

1. Create a CPU-threshold monitoring rule.
2. Generate deterministic operational metrics.
3. Identify readings that exceed the configured threshold.
4. Explain why specific readings generate alerts.
5. Investigate governance, RBAC, compute, NSG, storage, backup, and monitoring events.
6. Export and hash the audit log.
7. Review the final simulator inventory.
8. Confirm remediation of deliberate security weaknesses.
9. Generate a machine-readable assurance report.
10. Protect the report with a verifiable SHA-256 checksum.
11. Prepare final evidence for the professional PDF report and GitHub repository.

---

## Prerequisites and Start Conditions

### 1. Confirm the shared workspace

Run:

```bash
python3 azlocal.py status
```

Expected continuity indicators include:

- Resource group `rg-icdfa-lab`
- VM inventory containing `vm-demo`
- NSG inventory containing `nsg-demo`
- Storage inventory containing `sticdfalab`
- Existing E01-E03 audit events

### 2. Review the final E03 state

```bash
python3 azlocal.py group list
python3 azlocal.py vm list
python3 azlocal.py nsg list
python3 azlocal.py storage list
python3 azlocal.py backup list
python3 azlocal.py policy
```

Expected secure baseline:

- `rg-icdfa-lab` retains governance tags.
- `vm-demo` is present.
- `nsg-demo` retains only the authorized SSH rule.
- `sticdfalab` has public access disabled and HTTPS-only enabled.
- Backup `known-good.json` is present.
- Policy reports zero findings.

### 3. Create E04 evidence directories

```bash
mkdir -p evidence/E04/outputs screenshots/E04
```

---

## Laboratory Resources

| Resource | Value |
|---|---|
| Monitoring rule | `high-cpu` |
| Metric | `cpu_percent` |
| Threshold | `85` |
| Sample 1 | `vm-demo`, 32 percent |
| Sample 2 | `vm-demo`, 86 percent |
| Sample 3 | `vm-demo`, 94 percent |
| Sample 4 | `storage-demo`, 8 percent |
| Audit export | `evidence/E04/outputs/e04-audit-log.json` |
| Audit checksum | `evidence/E04/outputs/e04-audit-log.sha256` |
| Assurance report | `evidence/E04/cloud_operations_report.json` |
| Report checksum | `evidence/E04/cloud_operations_report.sha256` |

> The hard-coded metric label `storage-demo` is part of simulator version 1.0. It is not the storage-account name `sticdfalab`.

---

# Part A: Monitoring and Alerting

## Step 1: Create the high-CPU monitoring rule

```bash
python3 azlocal.py monitor rule high-cpu --threshold 85
```

**Expected result:**

```text
metric: cpu_percent
threshold: 85
enabled: true
```

**What this proves:** A threshold rule exists to detect CPU readings at or above 85 percent.

**Capture:** `Fig01 High CPU Monitoring Rule.png`

---

## Step 2: Generate the metric sample once

```bash
python3 azlocal.py monitor sample
```

Simulator version 1.0 adds four readings:

| Resource | CPU percentage | Expected threshold result |
|---|---:|---|
| `vm-demo` | 32 | Below threshold |
| `vm-demo` | 86 | Alert |
| `vm-demo` | 94 | Alert |
| `storage-demo` | 8 | Below threshold |

**Expected result:** The output reports that four samples were added.

**Capture:** `Fig02 Operational Metric Samples.png`

> Run `monitor sample` only once. Every invocation appends four more readings and creates repeated qualifying alerts.

---

## Step 3: Evaluate generated alerts

```bash
python3 azlocal.py monitor alerts
```

**Expected result after one sample run:**

- Alert count: `2`
- `vm-demo` at `86` percent
- `vm-demo` at `94` percent
- Rule: `high-cpu`
- Threshold: `85`

The 32-percent and 8-percent readings should not generate alerts.

**What this proves:** The rule identifies values equal to or above its defined threshold.

**Capture:** `Fig03 High CPU Alerts Triggered.png`

---

## Step 4: Record the monitoring interpretation

Document the following in the individual evidence log:

```text
The high-cpu rule evaluated cpu_percent readings against an 85 percent threshold.
The 86 percent and 94 percent vm-demo readings triggered alerts.
The 32 percent vm-demo and 8 percent storage-demo readings remained below threshold.
```

This interpretation belongs in the evidence log or report, not in the terminal.

---

# Part B: Audit Investigation

## Step 5: Review the cumulative audit trail

```bash
python3 azlocal.py monitor logs --limit 100
```

Identify representative events from all four laboratories:

### Governance and RBAC

- `group-create`
- `group-tag`
- `rbac-assign`
- `rbac-check`
- Denied `authorisation`
- `group-lock`
- `group-unlock`

### Compute and networking

- `vm-create`
- `vm-start`
- `vm-stop`
- `nsg-create`
- `nsg-rule`
- `nsg-test`
- `nsg-remove`

### Storage and recovery

- `storage-create`
- `storage-set`
- `blob-upload`
- `blob-download`, if completed successfully
- `backup-create`
- `backup-restore`

### Monitoring

- `monitor-rule`
- `monitor-sample`

**What this proves:** The simulator provides attribution, timestamps, outcomes, and details across the integrated practical.

**Capture:** `Fig04 Cumulative Audit Log Investigation.png`

---

## Step 6: Export the audit log

```bash
python3 azlocal.py monitor logs --limit 100 \
  | tee evidence/E04/outputs/e04-audit-log.json
```

Verify that the file exists:

```bash
ls -lh evidence/E04/outputs/e04-audit-log.json
```

**Capture:** `Fig05 Audit Log Export.png`

---

## Step 7: Hash and verify the audit export

```bash
sha256sum evidence/E04/outputs/e04-audit-log.json \
  | tee evidence/E04/outputs/e04-audit-log.sha256

sha256sum -c evidence/E04/outputs/e04-audit-log.sha256
```

**Expected result:**

```text
evidence/E04/outputs/e04-audit-log.json: OK
```

**What this proves:** The exported audit evidence can be checked for subsequent modification.

**Capture:** `Fig06 Audit Log SHA256 Verification.png`

---

# Part C: Final-State Assurance

## Step 8: Review the complete simulator status

Run the following commands separately so their outputs remain readable:

```bash
python3 azlocal.py status
```

```bash
python3 azlocal.py group list
```

```bash
python3 azlocal.py access list
```

```bash
python3 azlocal.py vm list
```

```bash
python3 azlocal.py nsg list
```

```bash
python3 azlocal.py storage list
```

```bash
python3 azlocal.py backup list
```

```bash
python3 azlocal.py monitor alerts
```

```bash
python3 azlocal.py policy
```

### Expected final posture

| Area | Expected secure state |
|---|---|
| Governance | `rg-icdfa-lab` has owner, environment, cost-centre, and governance tags |
| RBAC | Analyst remains Reader; storage data role is correctly scoped if E03 correction was completed |
| Compute | `vm-demo` exists in the recovered operational state |
| NSG | Only the authorized `192.168.56.0/24` SSH rule remains |
| Storage | Public access false; HTTPS-only true |
| Backup | `known-good.json` exists |
| Monitoring | Two expected CPU alerts after one sample run |
| Policy | Zero findings |

**Capture:** `Fig07 Final Secure Inventory Review.png`

---

## Step 9: Investigate any non-zero policy result

If `policy` reports findings, do not proceed directly to the final report. Identify the resource and remediate it.

### SSH exposure

```bash
python3 azlocal.py nsg list
python3 azlocal.py nsg remove nsg-demo --priority 200
```

### Public storage or HTTPS disabled

```bash
python3 azlocal.py storage set sticdfalab \
  --public-access false \
  --https-only true
```

### Missing required tags

```bash
python3 azlocal.py group tag rg-icdfa-lab owner Wadondera-A-Collins
python3 azlocal.py group tag rg-icdfa-lab environment training
```

Re-run:

```bash
python3 azlocal.py policy
```

Proceed only when the expected deliberate findings have been remediated.

**Capture when remediation was needed:** `Fig08 Final Policy Remediation.png`

---

# Part D: Assurance Report and SHA-256

## Step 10: Generate the machine-readable assurance report

```bash
python3 azlocal.py report \
  --output evidence/E04/cloud_operations_report.json
```

**Expected result:** The command displays:

- Absolute report path
- SHA-256 digest

The report contains:

- Generation timestamp
- Course identifier
- Offline-simulation notice
- Resource-group count
- VM records
- NSG configuration
- Storage account summaries and blob counts
- Access assignments
- Alert definitions

> The JSON assurance report is supporting machine-readable evidence. It does not replace the required professional PDF report.

**Capture:** `Fig09 Assurance Report Generation.png`

---

## Step 11: Inspect the generated JSON

```bash
python3 -m json.tool evidence/E04/cloud_operations_report.json
```

Alternatively:

```bash
cat evidence/E04/cloud_operations_report.json
```

Review the report for expected inventory and the notice that it concerns local simulated resources only.

**Capture:** `Fig10 Assurance Report Contents.png`

---

## Step 12: Create the report checksum

```bash
sha256sum evidence/E04/cloud_operations_report.json \
  | tee evidence/E04/cloud_operations_report.sha256
```

---

## Step 13: Verify the report checksum

```bash
sha256sum -c evidence/E04/cloud_operations_report.sha256
```

**Expected result:**

```text
evidence/E04/cloud_operations_report.json: OK
```

**What this proves:** The final machine-readable assurance artifact can be checked for integrity.

**Capture:** `Fig11 Assurance Report SHA256 Verification.png`

---

## Step 14: Save the final E04 summary

```bash
{
  echo "=== E04 STATUS ==="
  python3 azlocal.py status
  echo
  echo "=== E04 ALERTS ==="
  python3 azlocal.py monitor alerts
  echo
  echo "=== E04 FINAL POLICY ==="
  python3 azlocal.py policy
  echo
  echo "=== E04 BACKUPS ==="
  python3 azlocal.py backup list
} | tee evidence/E04/outputs/e04-final-summary.txt
```

Hash and verify the summary:

```bash
sha256sum evidence/E04/outputs/e04-final-summary.txt \
  | tee evidence/E04/outputs/e04-final-summary.sha256

sha256sum -c evidence/E04/outputs/e04-final-summary.sha256
```

**Expected result:**

```text
evidence/E04/outputs/e04-final-summary.txt: OK
```

**Capture:** `Fig12 Final E04 Summary and SHA256.png`

---

## Evidence Register

Store E04 screenshots under `screenshots/E04/`. Rename each image only after confirming that its visible content supports the stated scenario.

| Figure | Exact filename | Evidence purpose |
|---:|---|---|
| Fig01 | `Fig01 High CPU Monitoring Rule.png` | Rule `high-cpu`, threshold 85, enabled |
| Fig02 | `Fig02 Operational Metric Samples.png` | Four deterministic metric readings |
| Fig03 | `Fig03 High CPU Alerts Triggered.png` | Alerts at 86 and 94 percent |
| Fig04 | `Fig04 Cumulative Audit Log Investigation.png` | Cross-laboratory event review |
| Fig05 | `Fig05 Audit Log Export.png` | Audit output saved to E04 evidence directory |
| Fig06 | `Fig06 Audit Log SHA256 Verification.png` | Audit checksum and `OK` verification |
| Fig07 | `Fig07 Final Secure Inventory Review.png` | Final resource, access, backup, alert, and policy state |
| Fig08 | `Fig08 Final Policy Remediation.png` | Optional remediation if a final finding exists |
| Fig09 | `Fig09 Assurance Report Generation.png` | JSON output path and generated digest |
| Fig10 | `Fig10 Assurance Report Contents.png` | Machine-readable inventory and simulation notice |
| Fig11 | `Fig11 Assurance Report SHA256 Verification.png` | Report checksum verification |
| Fig12 | `Fig12 Final E04 Summary and SHA256.png` | Final summary export and integrity check |

> If no final remediation is required, omit Figure 8 and continue sequentially without inventing evidence. Use filenames that match the actual screenshots you capture.

---

## Operational Findings

### Finding 1: Threshold monitoring identifies elevated CPU samples

The 85-percent rule should detect the 86-percent and 94-percent VM readings while excluding the 32-percent VM and 8-percent storage readings.

### Finding 2: Repeated sample generation duplicates alerts

Every `monitor sample` invocation appends another set of four readings. Repeated execution increases the alert count without representing new real telemetry. Record the number of sample runs when interpreting results.

### Finding 3: Audit logs provide end-to-end traceability

The cumulative log links actors, actions, outcomes, details, and timestamps across governance, access control, compute, networking, storage, recovery, and monitoring activities.

### Finding 4: Final policy review validates remediation persistence

A zero-finding final scan confirms that deliberately insecure SSH and storage settings were removed and that mandatory resource-group tags remain present.

### Finding 5: Checksums strengthen evidence assurance

SHA-256 files allow the audit export, JSON assurance report, and final summary to be checked for changes after generation.

---

## Troubleshooting

### Unexpected alert count greater than two

Cause: `monitor sample` was run more than once. Each run appends another 86-percent and 94-percent reading.

Check the alert output:

```bash
python3 azlocal.py monitor alerts
```

Do not reset the simulator merely to reduce the count. Record how many sample runs occurred and explain the duplicate alerts accurately.

### No alerts appear

Confirm that the rule and samples were created:

```bash
python3 azlocal.py monitor rule high-cpu --threshold 85
python3 azlocal.py monitor sample
python3 azlocal.py monitor alerts
```

Do not recreate the rule repeatedly unless the initial rule command failed.

### Audit output does not show early E01 events

The `--limit` value returns only the most recent events. Increase it:

```bash
python3 azlocal.py monitor logs --limit 200
```

### Policy reports SSH exposure

```bash
python3 azlocal.py nsg list
python3 azlocal.py nsg remove nsg-demo --priority 200
python3 azlocal.py policy
```

### Policy reports storage findings

```bash
python3 azlocal.py storage set sticdfalab \
  --public-access false \
  --https-only true
python3 azlocal.py policy
```

### Audit or report checksum returns FAILED

The evidence file changed after the checksum was created. Review the file, then deliberately regenerate the checksum:

```bash
sha256sum <evidence-file> | tee <checksum-file>
sha256sum -c <checksum-file>
```

Do not overwrite a checksum merely to conceal an unexplained modification.

### Report directory does not exist

```bash
mkdir -p evidence/E04
```

Then rerun the report command.

### Generated JSON cannot be parsed

Validate it:

```bash
python3 -m json.tool evidence/E04/cloud_operations_report.json
```

If parsing fails, regenerate the file through `azlocal.py report` rather than editing the JSON manually.

---

## Completion Checklist

### Monitoring and alerts

- [ ] `high-cpu` rule created at threshold 85
- [ ] Rule shown as enabled
- [ ] Metric sample generated
- [ ] 32, 86, 94, and 8 percent readings recorded
- [ ] Alerts evaluated
- [ ] 86 and 94 percent alerts identified
- [ ] Number of sample runs documented

### Audit investigation

- [ ] Cumulative audit log reviewed
- [ ] Governance and RBAC events identified
- [ ] VM and NSG events identified
- [ ] Storage and recovery events identified
- [ ] Monitoring events identified
- [ ] Audit output exported
- [ ] Audit SHA-256 created and verified

### Final-state assurance

- [ ] Resource-group tags reviewed
- [ ] Access assignments reviewed
- [ ] VM inventory reviewed
- [ ] NSG final rules reviewed
- [ ] Storage final settings reviewed
- [ ] Known-good backup listed
- [ ] Alerts reviewed
- [ ] Final policy scan completed
- [ ] Deliberate security findings fully remediated

### Assurance artifacts

- [ ] JSON assurance report generated
- [ ] Simulation notice confirmed in the JSON
- [ ] Assurance-report checksum created
- [ ] Assurance-report checksum verified as `OK`
- [ ] Final E04 summary exported
- [ ] Final-summary checksum verified
- [ ] Screenshots accurately named and stored
- [ ] Risk register updated
- [ ] Individual evidence log updated
- [ ] No `workspace/`, keys, tokens, or credentials staged for GitHub

---

## Repository Structure

The following is a layout example, not a terminal command:

```text
CCSE-102-Integrated-Azure-Operations-Lab/
├── README.md
├── Documentation_Report.pdf
├── .gitignore
├── evidence/
│   ├── E01/
│   ├── E02/
│   ├── E03/
│   └── E04/
│       ├── cloud_operations_report.json
│       ├── cloud_operations_report.sha256
│       └── outputs/
│           ├── e04-audit-log.json
│           ├── e04-audit-log.sha256
│           ├── e04-final-summary.txt
│           └── e04-final-summary.sha256
├── screenshots/
│   ├── E01/
│   ├── E02/
│   ├── E03/
│   └── E04/
│       ├── Fig01 High CPU Monitoring Rule.png
│       ├── Fig02 Operational Metric Samples.png
│       └── ...
├── recovered/
└── notes/
```

Do not commit the generated `workspace/` directory.

---

## Limitations

- Monitoring samples are deterministic educational values, not live telemetry.
- `storage-demo` is a hard-coded metric label and not the created `sticdfalab` account.
- Alerts are generated by scanning stored samples; the simulator does not send notifications.
- Audit events are stored locally in `workspace/audit.jsonl`.
- The JSON report summarizes selected inventory fields and is not a full enterprise compliance assessment.
- The policy scanner evaluates only the controls implemented in simulator version 1.0.
- SHA-256 provides integrity verification but does not encrypt evidence or prove authorship.
- No Microsoft Azure Monitor, Log Analytics workspace, Azure Activity Log, Microsoft Sentinel, or Azure Policy service is used.

---

## Academic Integrity and AI Disclosure

All commands, outputs, screenshots, alert counts, audit findings, and checksums submitted for E04 must come from the student's independently executed laboratory work.

Microsoft Copilot may be disclosed as having assisted with document organization and implementation clarity. Copilot-generated content does not replace command execution, evidence capture, audit investigation, checksum verification, or technical interpretation by the student.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Laboratory E04 · Monitoring, Audit and Operational Assurance**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
