<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:071A2B,45:0B5CAD,100:00A4EF&height=240&section=header&text=CCSE-102%20Integrated%20Azure%20Operations&fontSize=38&fontColor=FFFFFF&fontAlignY=34&desc=Administration%20%7C%20Cloud%20Security%20%7C%20Operational%20Assurance&descSize=18&descAlignY=56&animation=fadeIn" width="100%" alt="CCSE-102 Integrated Azure Operations and Cloud Security Laboratory banner" />

# ☁️ Integrated Azure Operations and Cloud Security Laboratory
### Four-Laboratory Cloud Operations, Administration and Security Project

<p>
  <img src="https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux platform" />
  <img src="https://img.shields.io/badge/Runtime-Python%203.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.10 or later" />
  <img src="https://img.shields.io/badge/Environment-Offline%20Azure--Style%20Simulator-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Offline Azure-style simulator" />
</p>

<p>
  <img src="https://img.shields.io/badge/Governance-RBAC%20%26%20Policy-0B5CAD?style=flat-square&logo=auth0&logoColor=white" alt="Governance RBAC and policy" />
  <img src="https://img.shields.io/badge/Network-NSG%20Hardening-C65911?style=flat-square&logo=fortinet&logoColor=white" alt="NSG hardening" />
  <img src="https://img.shields.io/badge/Integrity-SHA--256-6F42C1?style=flat-square&logo=letsencrypt&logoColor=white" alt="SHA-256 integrity verification" />
  <img src="https://img.shields.io/badge/Monitoring-Audit%20Ready-2EA44F?style=flat-square&logo=datadog&logoColor=white" alt="Monitoring and audit readiness" />
  <img src="https://img.shields.io/badge/Status-Four%20Labs%20Completed-181717?style=flat-square&logo=github&logoColor=white" alt="Four laboratories completed" />
</p>

**Governed resources · Least-privilege access · Network remediation · Storage protection · Recovery testing · Operational assurance**

### Wadondera A. Collins
**ICDFA Trainee · Cohort 11 · Cloud Security Engineering**  
International Cybersecurity and Digital Forensics Academy

</div>

---

## Project Overview

This repository documents the **CCSE-102 Integrated Azure Operations, Administration and Cloud Security Laboratory**, a four-part practical focused on resource governance, access control, compute administration, network security, storage protection, integrity verification, recovery, monitoring, and audit assurance.

The project is organized as **one integrated 100-mark assessment containing four separately documented laboratories**. Each laboratory retains its own implementation sequence, evidence, validation results, findings, and limitations, while the repository provides a single reproducible submission package.

### Project outcomes

- Governed an Azure-style resource group with ownership, environment, cost-centre, and governance tags.
- Applied group-scoped and storage-scoped role-based access controls.
- Verified permitted operations and intentional authorization denials.
- Managed a simulated Ubuntu VM through create, start, stop, and restart states.
- Tested ordered NSG rules, default-deny behavior, SSH exposure, and remediation.
- Operated a real Linux HTTP health service on localhost.
- Detected and corrected public-storage and HTTPS misconfigurations.
- Verified uploaded and recovered data with SHA-256.
- Tested a checksummed known-good inventory backup and restoration workflow.
- Configured CPU monitoring, generated alerts, reviewed audit records, and verified assurance evidence.

---

## Offline-Simulation Declaration

> **This project did not provision genuine Microsoft Azure resources.**

The supplied `azlocal.py` application is an offline teaching simulator that reproduces selected Azure-style administration concepts on a local Linux system.

### Simulated cloud-style operations

- Resource groups and tags
- RBAC assignments and authorization decisions
- VM inventory and lifecycle states
- Network Security Groups and ordered rule evaluation
- Storage-account security settings and blob metadata
- Policy findings
- Monitoring rules, metric samples, and alerts
- Inventory backups and restoration
- Audit events and assurance reporting

### Real Linux operations

- Running Python commands
- Operating the localhost health service
- Inspecting TCP sockets with `ss`
- Creating, downloading, and comparing files
- Calculating and verifying SHA-256 hashes
- Creating Git evidence and repository artifacts
- Optional SSH administration or tunnelling where authorized

This distinction is maintained throughout the laboratory reports to avoid representing simulated inventory as a live Microsoft Azure deployment.

---

## Laboratory Map

| Laboratory | Title | Marks | Core capabilities demonstrated |
|---|---|---:|---|
| **E01** | Resource Governance and Role-Based Access Control | 20 | Resource groups, tags, policy checks, Reader access, RBAC denial, locks, audit events |
| **E02** | Compute, Network Security Group and Linux Operations | 30 | VM lifecycle, default-deny NSG behavior, SSH testing, exposure remediation, localhost service |
| **E03** | Storage Security, File Integrity and Recovery | 25 | Storage hardening, scoped data access, SHA-256 verification, backup and recovery |
| **E04** | Monitoring, Audit and Operational Assurance | 25 | CPU alerts, cumulative audit analysis, final policy assurance, checksum-protected reporting |

### E01: Governance and RBAC

The first laboratory established `rg-icdfa-lab`, applied governance metadata, assigned a group-scoped Reader role to `analyst`, and proved that read access succeeded while write access was denied. A simulated resource lock prevented configuration changes until an authorized unlock occurred.

### E02: Compute, networking, and Linux operations

The second laboratory managed the `vm-demo` lifecycle and configured `nsg-demo` with default-deny behavior. SSH access was restricted to `192.168.56.0/24`; deliberate exposure through `0.0.0.0/0` was detected and remediated. A real HTTP health service was tested on `127.0.0.1:8088` and stopped after evidence collection.

### E03: Storage, integrity, and recovery

The third laboratory created `sticdfalab`, detected public-access and HTTPS weaknesses, and restored private HTTPS-only settings. The `operations-file` blob was verified with SHA-256, storage access was scoped to `storage:sticdfalab`, an unauthorized group write was denied, and a known-good backup restored simulated inventory.

### E04: Monitoring, audit, and assurance

The fourth laboratory configured an 85% CPU threshold. Samples at 86% and 94% generated two alerts, while lower readings did not. The cumulative audit trail was reviewed, the final policy returned zero findings, and the machine-readable assurance report was protected and verified with SHA-256.

---

## Security Control Coverage

| Security objective | Control implemented | Validation method |
|---|---|---|
| Resource accountability | Owner, environment, cost-centre, and governance tags | Resource-group listing and zero-finding policy result |
| Least privilege | Group-scoped Reader and storage-scoped data role | Permitted read/data access and denied management writes |
| Change protection | Simulated resource-group lock | Configuration change rejected while locked |
| Network restriction | Default deny and authorized SSH CIDR | Allowed private address and denied external address |
| Exposure remediation | Removal of `0.0.0.0/0` SSH rule | External test returned to deny; policy finding cleared |
| Storage confidentiality | Public access disabled | Storage listing and policy verification |
| Transport protection | HTTPS-only enabled | Storage listing and zero policy findings |
| Data integrity | SHA-256 verification | Matching source, blob, and recovered-file hashes |
| Recovery assurance | Checksummed known-good backup | VM state restored from stopped to running |
| Operational detection | 85% CPU alert rule | Alerts generated at 86% and 94% |
| Traceability | Simulator audit log | Attributed and time-stamped events across E01–E04 |
| Evidence integrity | SHA-256 checksum files | `sha256sum -c` returned `OK` |

---

## Technologies and Tools

### Core environment

- **Linux / WSL Ubuntu** for terminal-based laboratory execution
- **Python 3.10 or later** for the ICDFA simulator and local health service
- **ICDFA `azlocal.py` simulator v1.0** for Azure-style administration records
- **Git and GitHub** for version control, reproducibility, and final evidence publication

### Administration and assurance utilities

- `curl` for HTTP health-endpoint testing
- `ss` for TCP listener inspection
- `sha256sum` for evidence and file-integrity validation
- `cmp` for byte-for-byte recovered-file comparison
- `tee` for saving command output while retaining terminal visibility
- Markdown and PDF for technical documentation

---

## Repository Structure

```text
CCSE-102-Integrated-Azure-Operations-Lab/
├── README.md
├── Documentation_Report.pdf
├── .gitignore
├── evidence/
│   ├── individual_evidence_log.md
│   ├── risk_register.csv
│   ├── cloud_operations_report.json
│   ├── cloud_operations_report.sha256
│   ├── Documentation_Report.sha256
│   ├── E01/
│   │   └── outputs/
│   ├── E02/
│   │   └── outputs/
│   ├── E03/
│   │   └── outputs/
│   └── E04/
│       └── outputs/
│           ├── audit-log.json
│           ├── audit-log.sha256
│           ├── final-summary.txt
│           └── final-summary.sha256
├── screenshots/
│   ├── E01/
│   ├── E02/
│   ├── E03/
│   └── E04/
├── recovered/
│   └── operations_data_recovered.txt
├── guides/
├── templates/
└── notes/
    └── implementation_notes.md
```

### Directory purpose

| Path | Purpose |
|---|---|
| `evidence/` | Completed evidence log, risk register, assurance report, audit outputs, summaries, and checksum files |
| `screenshots/E01/`–`screenshots/E04/` | Laboratory-specific terminal and validation screenshots |
| `recovered/` | Downloaded file used for independent SHA-256 and byte-comparison validation |
| `guides/` | Original laboratory instructions supplied with the package |
| `templates/` | Original evidence-log and risk-register templates |
| `notes/` | Student-created implementation and troubleshooting notes |
| `Documentation_Report.pdf` | Formal consolidated technical assessment and evidence report |

> The generated `workspace/` directory is intentionally excluded from GitHub because the directory contains local simulator state, audit records, blobs, and backups.

---

## Reproduction and Validation

### Prerequisites

```bash
python3 --version
python3 -m py_compile azlocal.py
```

Python must be version 3.10 or later. Run subsequent commands from the directory containing `azlocal.py`.

### Initial setup

Use this only when starting a new simulator workspace:

```bash
python3 azlocal.py init
python3 azlocal.py status
```

> Do not run `init --reset --confirm` when reproducing an existing evidence set. Resetting deletes accumulated simulator state.

### Review final simulated state

```bash
python3 azlocal.py status
python3 azlocal.py group list
python3 azlocal.py access list
python3 azlocal.py vm list
python3 azlocal.py nsg list
python3 azlocal.py storage list
python3 azlocal.py backup list
python3 azlocal.py monitor alerts
python3 azlocal.py policy
```

### Revalidate blob integrity

```bash
python3 azlocal.py blob verify sticdfalab operations-file
```

Expected final field:

```text
integrity_ok: true
```

### Revalidate recovered-file integrity

```bash
sha256sum \
  samples/operations_data.txt \
  recovered/operations_data_recovered.txt

cmp --silent \
  samples/operations_data.txt \
  recovered/operations_data_recovered.txt \
  && echo "Recovered file matches original"
```

### Verify assurance evidence

```bash
sha256sum -c evidence/cloud_operations_report.sha256
sha256sum -c evidence/E04/outputs/audit-log.sha256
sha256sum -c evidence/Documentation_Report.sha256
```

Every applicable verification should return `OK`.

---

## Local HTTP Service Validation

Start the supplied service in Terminal 1:

```bash
python3 scripts/health_service.py --port 8088
```

Test the endpoint from Terminal 2:

```bash
curl http://127.0.0.1:8088/health
ss -ltn | grep 8088
```

The service should respond through `127.0.0.1:8088`. The service must not be exposed through `0.0.0.0:8088`.

After evidence collection, return to Terminal 1 and press `Ctrl+C`. Confirm closure from Terminal 2:

```bash
ss -ltn | grep 8088 || echo "Port 8088 is no longer listening"
```

Expected final result:

```text
Port 8088 is no longer listening
```

---

## Results Summary

| Validation area | Final result |
|---|---|
| Governance policy | Required tags present; final policy returned zero findings |
| Group RBAC | Analyst read allowed; analyst write and VM creation denied |
| Resource lock | Change rejected while locked; authorized change succeeded after unlock |
| VM lifecycle | Create, start, stop, and restart states validated |
| NSG security | Authorized private source allowed; external source denied after remediation |
| SSH exposure | `0.0.0.0/0` rule detected and removed |
| Linux service | Health endpoint returned successfully; service bound to localhost and later stopped |
| Storage security | Public access disabled; HTTPS-only enabled |
| Storage RBAC | Data access scoped to `storage:sticdfalab`; group write denied |
| File integrity | Original, stored, and recovered SHA-256 values matched |
| Recovery | Known-good inventory backup restored `vm-demo` to the backed-up state |
| Monitoring | Alerts triggered at 86% and 94% against an 85% threshold |
| Audit assurance | Cumulative events exported and protected by SHA-256 |
| Final assurance report | JSON report generated and checksum verification returned `OK` |

---

## Evidence Index

### Core assessment artifacts

- [Professional consolidated report](Documentation_Report.pdf)
- [Individual evidence log](evidence/individual_evidence_log.md)
- [Risk register](evidence/risk_register.csv)
- [Machine-readable assurance report](evidence/cloud_operations_report.json)
- [Assurance-report checksum](evidence/cloud_operations_report.sha256)
- [Audit export](evidence/E04/outputs/audit-log.json)
- [Audit checksum](evidence/E04/outputs/audit-log.sha256)

### Laboratory screenshots

- [E01: Governance and RBAC evidence](screenshots/E01/)
- [E02: Compute, NSG and Linux evidence](screenshots/E02/)
- [E03: Storage, integrity and recovery evidence](screenshots/E03/)
- [E04: Monitoring, audit and assurance evidence](screenshots/E04/)

---

## Risk and Security Considerations

The final risk register addresses:

1. SSH exposure through `0.0.0.0/0`
2. Public storage access
3. HTTPS-only enforcement disabled
4. Excessive or incorrectly scoped permissions
5. Missing monitoring and delayed detection
6. File tampering or corruption
7. Simulated inventory loss
8. Local-service exposure
9. Secrets or simulator state committed to GitHub

The complete likelihood, impact, treatment, ownership, and verification records are maintained in [`evidence/risk_register.csv`](evidence/risk_register.csv).

---

## Evidence Integrity and Repository Safety

The repository excludes common secret-bearing and simulator-state paths:

```gitignore
workspace/
.env
*.pem
*.key
id_rsa*
__pycache__/
*.pyc
```

Before publication, staged files should be reviewed with:

```bash
git status
git diff --cached --name-only
git ls-files
```

The final evidence files should be validated with their accompanying SHA-256 records before submission.

---

## Limitations

- The cloud-style resource operations are simulated and do not represent a production Microsoft Azure deployment.
- VM lifecycle actions modify local inventory records rather than real virtual machines.
- NSG tests model ordered rule evaluation but do not configure the Linux host firewall.
- Storage security settings and blob metadata are maintained by the local simulator.
- Backup restoration covers simulator inventory only and does not restore real VM disks or roll back blob files.
- Monitoring samples are deterministic educational values rather than live telemetry.
- Audit records are local simulator events rather than Microsoft Azure Activity Log entries.
- SHA-256 detects content changes but does not encrypt evidence or prove authorship.
- The localhost health service is a real Linux process but is not hosted in Microsoft Azure.

---

## Professional Report

The formal report provides the full evidence-driven assessment, including:

- Document control and executive summary
- Methodology and simulation boundary
- Separate E01–E04 implementation sections
- Screenshot analysis and findings
- Consolidated results matrix
- Risk register and security-control assessment
- Limitations and recommendations
- AI-assistance disclosure
- Final submission close-out and demonstration controls

➡️ **[Open the consolidated Documentation Report](Documentation_Report.pdf)**

---

## Academic Integrity and AI Assistance Disclosure

All commands, outputs, screenshots, hashes, interpretations, and conclusions in this repository must represent laboratory work independently executed and verified by Wadondera A. Collins.

Microsoft Copilot was used to support document organization, improve presentation, examine supplied screenshots, and align evidence with the relevant laboratory scenarios. Copilot did not execute the WSL laboratory session or manufacture terminal evidence. Final validation, evidence ownership, and submission responsibility remain with the student.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Integrated Azure Operations and Cloud Security Laboratory**  
**Four laboratories · One consolidated assessment · Evidence-driven cloud operations and security**

**Offline Azure-style simulation · Not Microsoft Azure**

</div>
