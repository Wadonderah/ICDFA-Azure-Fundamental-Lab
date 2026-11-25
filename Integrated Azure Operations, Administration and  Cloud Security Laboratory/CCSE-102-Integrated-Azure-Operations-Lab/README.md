# CCSE-102 Integrated Azure Operations and Cloud Security Laboratory

**Student:** Wadondera A. Collins

This repository contains evidence for four separately documented ICDFA laboratories: governance and RBAC, compute and network operations, storage integrity and recovery, and monitoring and operational assurance.

## Offline-simulation declaration

The supplied `azlocal.py` simulator reproduces selected Azure-style administration concepts locally. No genuine Microsoft Azure resources were provisioned. VM inventory, RBAC assignments, NSGs, storage settings, monitoring rules, backups, and policy results are simulated. Linux process, file, SSH, and SHA-256 operations are real local operations.

## Laboratory map

- **E01:** Resource governance and role-based access control
- **E02:** Compute lifecycle, NSG testing, Linux operations, and SSH exposure remediation
- **E03:** Storage hardening, integrity verification, scoped RBAC, backup, and recovery
- **E04:** CPU monitoring, cumulative audit review, policy assurance, and integrity verification

## Technologies

- Linux
- Python 3
- SHA-256
- The ICDFA offline Azure-style simulator
- Local HTTP service and socket inspection

## Repository structure

- `evidence/`: Completed evidence log, risk register, assurance report, audit evidence, and checksums
- `screenshots/E01/` through `screenshots/E04/`: Laboratory screenshots
- `recovered/`: Recovered and SHA-256-validated operations file
- `notes/`: Implementation notes
- `guides/`: Original laboratory guides
- `templates/`: Original evidence templates
- `Documentation_Report.pdf`: Professional consolidated report

## Reproduction

```bash
python3 azlocal.py init
python3 azlocal.py status
python3 azlocal.py policy
python3 azlocal.py blob verify sticdfalab operations-file
sha256sum -c evidence/cloud_operations_report.sha256
sha256sum -c evidence/outputs/audit-log.sha256
```

The local health service can be tested on port 8088 and stopped after evidence collection:

```bash
python3 scripts/health_service.py --port 8088
curl http://127.0.0.1:8088/health
ss -ltn | grep 8088
```

## Results summary

The final policy review returned zero findings. The storage role was scoped to `storage:sticdfalab`, an unauthorized group write was denied, the original and recovered files had matching SHA-256 hashes, and CPU alerts fired at 86% and 94% against an 85% threshold. The E02 localhost service was stopped and port 8088 was no longer listening.

## Evidence limitations

The recovery exercises restore simulator inventory only; they do not restore real Azure VM disks or storage infrastructure. Alert metrics and resource records are synthetic. The official report should retain the individual E01-E04 sections and clearly identify this offline context.

## Deliverables

- [Professional report](Documentation_Report.pdf)
- [Individual evidence log](evidence/individual_evidence_log.md)
- [Risk register](evidence/risk_register.csv)
- [Assurance report](evidence/cloud_operations_report.json)
- [Audit export](evidence/outputs/audit-log.json)
