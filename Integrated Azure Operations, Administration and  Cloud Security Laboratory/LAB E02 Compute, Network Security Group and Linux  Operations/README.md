<div align="center">

# CCSE-102 Laboratory E02
## Compute, Network Security Group and Linux Operations

**Offline Azure-Style Administration Simulation with Real Local Linux Service Validation**

![Course](https://img.shields.io/badge/Course-CCSE--102-17365D?style=for-the-badge)
![Laboratory](https://img.shields.io/badge/Laboratory-E02-C65911?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)

![Compute](https://img.shields.io/badge/Domain-Compute-0078D4?style=flat-square)
![NSG](https://img.shields.io/badge/Control-NSG-5C2D91?style=flat-square)
![Remediation](https://img.shields.io/badge/Security-Remediation-107C10?style=flat-square)
![HTTP](https://img.shields.io/badge/Service-Localhost_HTTP-9C6500?style=flat-square)

**Simulated VM lifecycle · Ordered NSG evaluation · SSH exposure detection and remediation · Localhost HTTP validation**

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
6. [Part A: Simulated VM Lifecycle](#part-a-simulated-vm-lifecycle)
7. [Part B: NSG Allow and Deny Tests](#part-b-nsg-allow-and-deny-tests)
8. [Part C: SSH Exposure and Remediation](#part-c-ssh-exposure-and-remediation)
9. [Part D: Real Linux Localhost Service](#part-d-real-linux-localhost-service)
10. [Evidence Register](#evidence-register)
11. [Security Findings](#security-findings)
12. [Troubleshooting](#troubleshooting)
13. [Completion Checklist](#completion-checklist)
14. [Repository Structure](#repository-structure)
15. [Limitations](#limitations)
16. [Author](#author)

---

## Laboratory Overview

Laboratory E02 is the second compulsory laboratory in the CCSE-102 Integrated Azure Operations, Administration and Cloud Security practical. E02 covers simulated compute administration, Network Security Group rule evaluation, deliberate SSH exposure, remediation, and operation of a real local Linux HTTP health service.

| Item | Detail |
|---|---|
| Laboratory | E02 |
| Title | Compute, Network Security Group and Linux Operations |
| Marks | 30 |
| Environment | Linux workstation |
| Runtime | Python 3.10 or later |
| Simulator | `azlocal.py` version 1.0 |
| Existing resource group | `rg-icdfa-lab` |
| Simulated VM | `vm-demo` |
| Simulated NSG | `nsg-demo` |
| Real local service | Health endpoint on `127.0.0.1:8088` |

> **Important:** E02 continues from E01 in the same simulator workspace. Do not run `python3 azlocal.py init` and do not reset the simulator.

---

## Scope Declaration

E02 deliberately combines simulated cloud-style operations and real Linux operations.

### Simulated operations

- Creating a VM inventory record
- Starting and stopping a VM record
- Creating an NSG
- Adding and removing NSG rules
- Testing NSG decisions
- Detecting a broad SSH rule with the policy scanner
- Recording simulator audit events

### Real Linux operations

- Starting `scripts/health_service.py`
- Testing the service with `curl`
- Inspecting the listening TCP socket with `ss`
- Stopping the process with `Ctrl+C`

The VM and NSG operations do not create genuine Microsoft Azure resources and do not configure the Linux host firewall. The health service is a real process running locally on the Linux workstation.

---

## Objectives

By completing E02, the student should be able to:

1. Confirm that the governed resource group created in E01 remains available.
2. Create and administer a simulated VM record.
3. Validate VM start, stop, and restart states.
4. Create a simulated NSG with default-deny behavior.
5. Permit SSH from an authorized private subnet.
6. Verify allowed and denied connection decisions.
7. Introduce an intentionally insecure SSH rule.
8. Detect the insecure rule through the policy scanner.
9. Remove the insecure rule and verify remediation.
10. Start and test a real local Linux HTTP service.
11. Confirm that the HTTP service listens only on localhost.
12. Stop the service and verify that port `8088` is closed.

---

## Start Conditions

Before beginning E02, run:

```bash
python3 azlocal.py group list
```

The retained E01 state should include:

```text
Resource group: rg-icdfa-lab
Location: local-linux
Locked: false
Tags:
  owner: Wadondera-A-Collins
  environment: training
  cost-centre: CCSE102
  governance: controlled
```

If `locked` is `true`, unlock the group before continuing:

```bash
python3 azlocal.py group unlock rg-icdfa-lab
```

Create E02 evidence directories:

```bash
mkdir -p evidence/E02/outputs screenshots/E02
```

---

## Laboratory Resources

| Resource | Value |
|---|---|
| Resource group | `rg-icdfa-lab` |
| VM name | `vm-demo` |
| VM size | `B1s` |
| VM operating system label | `Ubuntu (simulated record)` |
| NSG name | `nsg-demo` |
| Authorized SSH subnet | `192.168.56.0/24` |
| Authorized test address | `192.168.56.20` |
| Unauthorized test address | `203.0.113.20` |
| SSH port | `22/TCP` |
| Authorized rule priority | `100` |
| Deliberately insecure rule | `0.0.0.0/0`, port `22`, priority `200` |
| Local health endpoint | `http://127.0.0.1:8088/health` |

---

# Part A: Simulated VM Lifecycle

## Step 1: Verify the E01 resource group

```bash
python3 azlocal.py group list
```

**Expected result:** `rg-icdfa-lab` exists, is unlocked, and retains the E01 tags.

**Capture:** `Fig01 E01 Resource Group Continuity.png`

---

## Step 2: Create the simulated VM record

```bash
python3 azlocal.py vm create vm-demo \
  --group rg-icdfa-lab \
  --size B1s
```

**Expected result:**

- Name: `vm-demo`
- Group: `rg-icdfa-lab`
- Size: `B1s`
- State: `stopped`
- OS: `Ubuntu (simulated record)`
- Notice: VM operations change simulated inventory only

**What this proves:** The simulator can create a governed compute inventory record inside the existing resource group.

**Capture:** `Fig02 Simulated VM Creation.png`

---

## Step 3: Start the VM

```bash
python3 azlocal.py vm start vm-demo
python3 azlocal.py vm list
```

**Expected result:** `vm-demo` shows `state: running`.

**What this proves:** The simulated VM lifecycle supports a transition from stopped to running.

**Capture:** `Fig03 Simulated VM Running State.png`

---

## Step 4: Stop the VM

```bash
python3 azlocal.py vm stop vm-demo
python3 azlocal.py vm list
```

**Expected result:** `vm-demo` shows `state: stopped`.

**Capture:** `Fig04 Simulated VM Stopped State.png`

---

## Step 5: Restart the VM for the operational baseline

```bash
python3 azlocal.py vm start vm-demo
python3 azlocal.py vm list
```

**Expected result:** The final E02 compute baseline shows `state: running`.

**Capture:** `Fig05 Simulated VM Restart Validation.png`

---

# Part B: NSG Allow and Deny Tests

## Step 6: Create the NSG

```bash
python3 azlocal.py nsg create nsg-demo --group rg-icdfa-lab
```

**Expected result:**

- NSG name: `nsg-demo`
- Group: `rg-icdfa-lab`
- Rules: empty
- Default decision: `deny`

**What this proves:** Traffic without a matching allow rule is denied by default.

**Capture:** `Fig06 NSG Creation and Default Deny.png`

---

## Step 7: Add the authorized SSH rule

```bash
python3 azlocal.py nsg rule nsg-demo \
  --source 192.168.56.0/24 \
  --port 22 \
  --decision allow \
  --priority 100
```

**Expected result:** The NSG contains an allow rule for TCP port `22` from `192.168.56.0/24` at priority `100`.

**What this proves:** SSH can be limited to an authorized private source range.

**Capture:** `Fig07 NSG Authorized SSH Rule.png`

---

## Step 8: Test the authorized address

```bash
python3 azlocal.py nsg test nsg-demo \
  --source 192.168.56.20 \
  --port 22
```

**Expected result:**

```text
decision: allow
matched rule priority: 100
```

**Capture:** `Fig08 NSG Authorized Address Allowed.png`

---

## Step 9: Test the unauthorized address

```bash
python3 azlocal.py nsg test nsg-demo \
  --source 203.0.113.20 \
  --port 22
```

**Expected result:**

```text
decision: deny
matched_rule: null
```

The request is denied because no rule matches and the NSG default is deny.

**Capture:** `Fig09 NSG Unauthorized Address Denied.png`

---

# Part C: SSH Exposure and Remediation

## Step 10: Introduce the insecure SSH rule

```bash
python3 azlocal.py nsg rule nsg-demo \
  --source 0.0.0.0/0 \
  --port 22 \
  --decision allow \
  --priority 200
```

**Expected result:** The NSG now contains an additional rule that permits SSH from every IPv4 address.

> This configuration is introduced only for controlled security testing. Do not use it as the final configuration.

---

## Step 11: Confirm the exposure

```bash
python3 azlocal.py nsg test nsg-demo \
  --source 203.0.113.20 \
  --port 22
```

**Expected result:**

```text
decision: allow
matched rule priority: 200
```

**What this proves:** The broad rule changes the previously denied address to an allowed decision.

**Capture:** `Fig10 Broad SSH Rule Allows External Address.png`

---

## Step 12: Detect the insecure rule

```bash
python3 azlocal.py policy
```

**Expected finding:**

```text
control: ssh-exposure
finding: SSH allowed from any IPv4 source
resource: nsg-demo
```

**What this proves:** The policy scanner detects an NSG rule allowing SSH from `0.0.0.0/0`.

**Capture:** `Fig11 Insecure SSH Exposure Detected.png`

---

## Step 13: Remove the insecure rule

```bash
python3 azlocal.py nsg remove nsg-demo --priority 200
```

**Expected result:** The priority `200` rule is removed. The authorized priority `100` rule remains.

---

## Step 14: Verify remediation

Run the following separately:

```bash
python3 azlocal.py nsg test nsg-demo \
  --source 203.0.113.20 \
  --port 22
```

```bash
python3 azlocal.py policy
```

```bash
python3 azlocal.py nsg list
```

**Expected result:**

- The external address is denied again.
- The `ssh-exposure` finding is absent.
- Only the authorized `192.168.56.0/24` SSH rule remains.

**What this proves:** The insecure rule was removed and the restrictive network posture was restored.

**Capture:** `Fig12 SSH Exposure Remediated.png`

---

# Part D: Real Linux Localhost Service

This section uses a real Linux process rather than a simulated cloud resource.

## Step 15: Start the health service in Terminal 1

From the package directory, open the first terminal and run:

```bash
python3 scripts/health_service.py --port 8088
```

Leave Terminal 1 running while performing the next tests.

**Expected result:** The supplied service starts on port `8088` and remains active until interrupted.

---

## Step 16: Test the health endpoint from Terminal 2

Open a second terminal in the package directory:

```bash
curl -i http://127.0.0.1:8088/health
```

**Expected result:**

- An HTTP success response
- A health response from the supplied service

Use the actual body returned by the script in the final report. Do not replace it with an assumed response.

**Capture:** `Fig13 Local HTTP Health Endpoint Response.png`

---

## Step 17: Confirm local-only TCP binding

```bash
ss -ltnp | grep 8088
```

If process details require additional permission, use:

```bash
ss -ltn | grep 8088
```

**Expected result:** The listening address shows:

```text
127.0.0.1:8088
```

The service must not be listening on `0.0.0.0:8088` or `[::]:8088`.

**What this proves:** The service is available locally without being exposed on all network interfaces.

**Capture:** `Fig14 Localhost Port Binding Validation.png`

---

## Step 18: Stop the health service

Return to Terminal 1 and press:

```text
Ctrl+C
```

`Ctrl+C` is a keyboard action, not a command to type.

---

## Step 19: Confirm port closure

In Terminal 2, run:

```bash
ss -ltn | grep 8088 || echo "Port 8088 is no longer listening"
```

**Expected result:**

```text
Port 8088 is no longer listening
```

**Capture:** `Fig15 Local HTTP Service Stopped.png`

---

## Step 20: Review E02 audit events

```bash
python3 azlocal.py monitor logs --limit 40
```

Look for:

- VM creation
- VM start and stop events
- NSG creation
- NSG rule additions
- NSG tests
- Insecure-rule removal

The real HTTP service does not use `azlocal.py`; therefore, its `curl`, `ss`, and process events are not expected in the simulator audit log.

**Capture:** `Fig16 E02 Compute and NSG Audit Log.png`

---

## Step 21: Save E02 simulator evidence

```bash
{
  echo "=== E02 VM INVENTORY ==="
  python3 azlocal.py vm list
  echo
  echo "=== E02 NSG CONFIGURATION ==="
  python3 azlocal.py nsg list
  echo
  echo "=== E02 FINAL POLICY ==="
  python3 azlocal.py policy
  echo
  echo "=== E02 AUDIT EVENTS ==="
  python3 azlocal.py monitor logs --limit 40
} | tee evidence/E02/outputs/e02-final-evidence.txt
```

Create and verify a checksum:

```bash
sha256sum evidence/E02/outputs/e02-final-evidence.txt \
  | tee evidence/E02/outputs/e02-final-evidence.sha256

sha256sum -c evidence/E02/outputs/e02-final-evidence.sha256
```

**Expected result:**

```text
evidence/E02/outputs/e02-final-evidence.txt: OK
```

**Capture:** `Fig17 E02 Evidence File and SHA256.png`

---

## Evidence Register

Store E02 screenshots under `screenshots/E02/` using exact names that match visible content.

| Figure | Exact filename | Evidence purpose |
|---:|---|---|
| Fig01 | `Fig01 E01 Resource Group Continuity.png` | Existing unlocked resource group and retained tags |
| Fig02 | `Fig02 Simulated VM Creation.png` | VM record created in stopped state |
| Fig03 | `Fig03 Simulated VM Running State.png` | VM started and listed as running |
| Fig04 | `Fig04 Simulated VM Stopped State.png` | VM stopped and listed as stopped |
| Fig05 | `Fig05 Simulated VM Restart Validation.png` | VM restarted to running baseline |
| Fig06 | `Fig06 NSG Creation and Default Deny.png` | NSG created with empty rules and default deny |
| Fig07 | `Fig07 NSG Authorized SSH Rule.png` | Private-subnet SSH allow rule |
| Fig08 | `Fig08 NSG Authorized Address Allowed.png` | Authorized address allowed by priority 100 |
| Fig09 | `Fig09 NSG Unauthorized Address Denied.png` | External address denied by default |
| Fig10 | `Fig10 Broad SSH Rule Allows External Address.png` | External address allowed after insecure rule |
| Fig11 | `Fig11 Insecure SSH Exposure Detected.png` | Policy finding for SSH from any IPv4 source |
| Fig12 | `Fig12 SSH Exposure Remediated.png` | Denied re-test, clean policy, final NSG rules |
| Fig13 | `Fig13 Local HTTP Health Endpoint Response.png` | Real HTTP response from localhost service |
| Fig14 | `Fig14 Localhost Port Binding Validation.png` | Listener restricted to `127.0.0.1:8088` |
| Fig15 | `Fig15 Local HTTP Service Stopped.png` | Port no longer listening after shutdown |
| Fig16 | `Fig16 E02 Compute and NSG Audit Log.png` | E02 simulator audit events |
| Fig17 | `Fig17 E02 Evidence File and SHA256.png` | Evidence export and checksum verification |

> Rename screenshots only after checking their visible content. Do not force a screenshot into a figure number if the screenshot does not prove the stated activity.

---

## Security Findings

### Finding 1: Default-deny behavior restricts unmatched traffic

The NSG begins with a default decision of `deny`. An address outside the authorized subnet is denied when no rule matches.

### Finding 2: Source-restricted SSH supports least exposure

The priority `100` rule permits SSH only from `192.168.56.0/24`. The test address `192.168.56.20` is allowed because it belongs to that subnet.

### Finding 3: Broad SSH access creates an avoidable attack path

The deliberately insecure `0.0.0.0/0` rule permits SSH from any IPv4 address. The policy scanner identifies this as `ssh-exposure`.

### Finding 4: Rule removal restores the secure posture

Removing priority `200` causes the external test address to return to the default-deny decision while preserving the authorized private-subnet rule.

### Finding 5: Localhost binding minimizes service exposure

The real health service is tested through `127.0.0.1:8088`. A localhost-only listener prevents direct access through other host interfaces unless an explicitly authorized tunnel is used.

---

## Troubleshooting

### Error: Resource group not found

Confirm the E01 state:

```bash
python3 azlocal.py group list
```

Do not reset the simulator. If E01 state is genuinely missing, restore or repeat E01 before creating E02 resources.

### Error: Resource group is locked

```bash
python3 azlocal.py group unlock rg-icdfa-lab
```

### Error: VM record already exists

Do not recreate it. Inspect its state:

```bash
python3 azlocal.py vm list
```

Continue with the required lifecycle operation.

### Error: NSG priority already exists

```bash
python3 azlocal.py nsg list
```

The simulator requires unique priorities. Remove the unwanted conflicting rule before adding the intended rule.

### Authorized address unexpectedly denied

Verify all three values:

- Source CIDR: `192.168.56.0/24`
- Test address: `192.168.56.20`
- Port: `22`

Then inspect:

```bash
python3 azlocal.py nsg list
```

### External address remains allowed after remediation

Confirm that priority `200` was removed:

```bash
python3 azlocal.py nsg list
```

If the rule remains, run:

```bash
python3 azlocal.py nsg remove nsg-demo --priority 200
```

### `curl` reports connection refused

Confirm that Terminal 1 is still running:

```bash
python3 scripts/health_service.py --port 8088
```

Then test again in Terminal 2.

### Port `8088` is already in use

Identify the current listener:

```bash
ss -ltnp | grep 8088
```

Stop only the process known to belong to the laboratory. Do not terminate unrelated system services.

### Service listens on `0.0.0.0:8088`

Stop the service immediately with `Ctrl+C`. Use the ICDFA-provided script as instructed. Do not expose port `8088` publicly.

---

## Completion Checklist

### Part A: Compute

- [ ] E01 resource group continuity verified
- [ ] `vm-demo` created in stopped state
- [ ] VM started and running state verified
- [ ] VM stopped and stopped state verified
- [ ] VM restarted to final running baseline

### Part B: NSG validation

- [ ] `nsg-demo` created with default deny
- [ ] Authorized SSH rule added for `192.168.56.0/24`
- [ ] `192.168.56.20` allowed on port `22`
- [ ] `203.0.113.20` denied before insecure rule

### Part C: Remediation

- [ ] Broad `0.0.0.0/0` SSH rule added for controlled testing
- [ ] External address changed to allow
- [ ] Policy scanner reported `ssh-exposure`
- [ ] Priority `200` rule removed
- [ ] External address returned to deny
- [ ] Final policy no longer reports SSH exposure
- [ ] Authorized priority `100` rule remains

### Part D: Real Linux service

- [ ] Health service started in Terminal 1
- [ ] Health endpoint tested with `curl`
- [ ] Listener confirmed as `127.0.0.1:8088`
- [ ] Service stopped with `Ctrl+C`
- [ ] Port closure verified

### Evidence and documentation

- [ ] E02 audit events reviewed
- [ ] Final evidence file saved
- [ ] SHA-256 checksum created and verified
- [ ] Screenshots accurately named and stored
- [ ] Simulated and real operations clearly distinguished
- [ ] No secrets or `workspace/` state staged for GitHub

---

## Repository Structure

The following is a layout example, not a command:

```text
CCSE-102-Integrated-Azure-Operations-Lab/
├── README.md
├── .gitignore
├── evidence/
│   ├── E01/
│   └── E02/
│       └── outputs/
│           ├── e02-final-evidence.txt
│           └── e02-final-evidence.sha256
├── screenshots/
│   ├── E01/
│   └── E02/
│       ├── Fig01 E01 Resource Group Continuity.png
│       ├── Fig02 Simulated VM Creation.png
│       └── ...
└── notes/
```

Do not commit the generated `workspace/` directory.

---

## Limitations

- VM operations change simulated inventory only.
- NSG tests model ordered rule evaluation but do not alter the Linux firewall.
- `203.0.113.20` is used as a controlled documentation test address in the simulator, not as a contacted external system.
- The policy scanner checks controls implemented in simulator version 1.0.
- The health endpoint is a real local Linux service, but it is not an Azure-hosted application.
- The localhost service must not be exposed publicly.
- An additional Ubuntu Server VM and SSH tunnel are optional, not required for the core single-workstation implementation.

---

## Academic Integrity and AI Disclosure

All commands, outputs, screenshots, and interpretations submitted for E02 must come from the student's independently executed laboratory work.

Microsoft Copilot may be disclosed as having assisted with document organization and implementation clarity. Copilot-generated content does not replace command execution, evidence capture, validation, or technical interpretation by the student.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Laboratory E02 · Compute, NSG and Linux Operations**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
