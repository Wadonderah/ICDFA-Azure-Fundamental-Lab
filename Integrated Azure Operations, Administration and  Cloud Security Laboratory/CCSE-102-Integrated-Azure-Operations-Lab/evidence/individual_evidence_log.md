# CCSE-102 - Individual Laboratory Evidence Log

Student name / registration number: Wadondera A. Collins
Linux distribution and version: Linux; Python 3.14.4
Date: 2026-11-25

## Lab 1 - Governance and access
Evidence IDs: E01-01 through E01-10
Objective: Demonstrate resource-group governance, tagging, role scope, policy, locks, and audit evidence.
Commands: Resource-group, tag, access, NSG, policy, lock, and audit commands recorded in the E01 screenshots and lab guide.
Observed output: `rg-icdfa-lab` was created with cost-centre tags; the analyst Reader role was limited to the resource group.
RBAC denial result: Analyst write operations were denied while permitted reads succeeded.
Lock result: Resource lock stopped unauthorized mutation and the lock was then removed through authorized control.
Screenshots: `screenshots/E01/Fig01` through `screenshots/E01/Fig10`.

## Lab 2 - Compute, virtual network and real Linux service
Evidence IDs: E02-01 through E02-11
Objective: Demonstrate VM lifecycle, NSG decisions, SSH exposure remediation, and localhost-only Linux service behavior.
VM lifecycle: `vm-demo` was created, started, stopped, and restarted as recorded in E02 evidence.
NSG result: The authorized private subnet was allowed; the unauthorized address was denied.
SSH exposure result: The `0.0.0.0/0` rule was removed and the resulting policy finding cleared.
Real service result: The health service was bound to `127.0.0.1:8088`, verified, and stopped; the final listener check showed no listening port.
Screenshots: `screenshots/E02/Fig01` through `screenshots/E02/Fig11`.

## Lab 3 - Storage, integrity and recovery
Evidence IDs: E03-01 through E03-08
Objective: Harden storage, verify file integrity, enforce storage-scoped data access, download the blob, and test simulator backup recovery.
Storage result: Public access was disabled and HTTPS-only access was enabled.
Uploaded file SHA-256: `3fca24dcc7f333d96d247c3c18a4b22cf845ade4b3f462c40abf351c954efd53`
Storage role result: `blob-operator` received `Storage Blob Data Contributor` at `storage:sticdfalab`; blob listing succeeded and a management-plane write was denied.
Recovered file SHA-256: `3fca24dcc7f333d96d247c3c18a4b22cf845ade4b3f462c40abf351c954efd53`; `cmp` confirmed an exact match.
Backup: `known-good`; restore confirmed inventory rollback only.
Screenshots: `screenshots/E03/Fig01` through `screenshots/E03/Fig08`.

## Lab 4 - Monitoring and assurance
Evidence IDs: E04-01 through E04-05
Objective: Configure CPU monitoring, trigger alerts, review cumulative audit evidence, and verify the final assurance report.
Alert threshold and evaluated alerts: 85% threshold; synthetic values of 86% and 94% triggered alerts.
Audit result: Cumulative audit evidence was present and `evidence/outputs/audit-log.json` passed SHA-256 verification.
Final policy result: Three policy checks completed with zero findings.
Final integrity-checked report: `evidence/cloud_operations_report.json` passed SHA-256 verification.
Screenshots: `screenshots/E04/Fig01` through `screenshots/E04/Fig05`.

## Academic integrity
I performed the work using local resources and did not provision or use real Microsoft Azure resources.
AI assistance: AI tools assisted with repository close-out, command verification, and document organization; no simulated result was represented as a genuine Azure result.
