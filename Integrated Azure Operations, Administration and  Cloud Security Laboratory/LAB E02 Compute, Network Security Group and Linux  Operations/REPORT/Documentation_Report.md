<div align="center">

# CCSE-102 Laboratory E02
## Compute, Network Security Group and Linux Operations

**Technical Documentation and Evidence Report**

![Course](https://img.shields.io/badge/Course-CCSE--102-17365D?style=for-the-badge)
![Laboratory](https://img.shields.io/badge/Laboratory-E02-C65911?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Simulator](https://img.shields.io/badge/Environment-Offline_Simulator-2F5597?style=for-the-badge)

![Compute](https://img.shields.io/badge/Domain-Compute-0078D4?style=flat-square)
![NSG](https://img.shields.io/badge/Control-NSG-5C2D91?style=flat-square)
![Remediation](https://img.shields.io/badge/Security-Remediation-107C10?style=flat-square)
![HTTP](https://img.shields.io/badge/Service-Localhost_HTTP-9C6500?style=flat-square)

**VM lifecycle administration · Ordered NSG evaluation · SSH exposure remediation · Local Linux service validation**

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
| Laboratory | E02: Compute, Network Security Group and Linux Operations |
| Assessment weighting | 30 marks |
| Student | Wadondera A. Collins |
| Cohort | CCSE Cohort 11, L1/S1 |
| Environment | WSL Ubuntu on a local workstation |
| Simulator | ICDFA `azlocal.py` offline Azure-style simulator, version 1.0 |
| Real service | Python localhost health service on TCP port `8088` |
| Evidence date | 24 November 2026 |
| Document status | Laboratory evidence report |

---

## Executive Summary

Laboratory E02 evaluated simulated compute administration, network security rule behavior, security remediation, and operation of a real Linux localhost service. A simulated Ubuntu VM record named `vm-demo` was created in `rg-icdfa-lab`, started, stopped, and returned to a running state. A simulated Network Security Group named `nsg-demo` was then configured with default-deny behavior and a priority `100` rule allowing SSH only from `192.168.56.0/24`.

Connectivity tests showed that `192.168.56.20` was allowed on TCP port `22`, while `203.0.113.20` was denied by default. A deliberate priority `200` rule allowing SSH from `0.0.0.0/0` changed the external test decision to `allow`. The policy scanner detected the configuration as `ssh-exposure`. Removing priority `200` restored the deny decision, removed the policy finding, and retained only the authorized subnet rule.

A real Python health service was started on `127.0.0.1:8088`. The `/health` endpoint returned HTTP `200 OK` with a healthy JSON response, and `ss` confirmed a localhost-only listener. The final uploaded screenshot, however, still showed the service in `LISTEN` state after the instruction to press `Ctrl+C`. Therefore, port-closure verification is not yet complete and must be repeated before this report is treated as final submission evidence.

---

## 1. Scope and Environment

### 1.1 Simulation boundary

The VM, NSG, rules, policy checks, and inventory states documented in this report are local simulated Azure-style operations. No Microsoft Azure subscription, Azure tenant, Azure CLI session, public cloud VM, or live Azure Network Security Group was used.

The HTTP health service, `curl` request, and TCP socket inspection are real Linux operations performed locally.

### 1.2 E01 continuity

E02 continued from the existing E01 simulator workspace and used the previously created resource group `rg-icdfa-lab`. The simulator was not reset. This retained governance state and allowed E02 resources to be added to the same controlled environment.

---

## 2. Objectives

The laboratory was performed to:

1. Create a simulated Ubuntu VM record.
2. Validate VM start, stop, and restart states.
3. Create an NSG with default-deny behavior.
4. Allow SSH only from an authorized private subnet.
5. Test permitted and denied source addresses.
6. Introduce a controlled insecure SSH rule.
7. Detect the exposure through the policy scanner.
8. Remove the insecure rule and confirm remediation.
9. Start a real local Linux health service.
10. Validate the health endpoint and local-only port binding.
11. Stop the service and verify port closure.

---

## 3. Methodology

The work followed a lifecycle of deployment, validation, negative testing, remediation, and operational verification:

1. Create and operate the simulated VM inventory record.
2. Establish an NSG with an explicit authorized SSH source.
3. Compare an allowed private address against an unmatched external test address.
4. Introduce a deliberately broad SSH rule and observe the changed decision.
5. use the policy scanner to detect the insecure configuration.
6. Remove the insecure rule and repeat the tests.
7. Start the real localhost service, query its health endpoint, and inspect its socket.
8. Attempt service shutdown and validate whether the listener was removed.

The documentation distinguishes observed output from expected behavior. A control is reported as complete only where the supplied evidence visibly confirms success.

---

## 4. Part A: Simulated VM Lifecycle

### 4.1 VM creation

The simulated VM record was created with the following command:

```bash
python3 azlocal.py vm create vm-demo --group rg-icdfa-lab --size B1s
```

The returned record identified `vm-demo`, resource group `rg-icdfa-lab`, size `B1s`, and operating-system label `Ubuntu (simulated record)`. The initial state was `stopped`. The simulator also displayed the notice that VM operations change simulated inventory only.

<img width="546" height="203" alt="Fig01 Simulated VM Creation" src="https://github.com/user-attachments/assets/22102cbd-8798-48f6-b9d9-8cbc182d118e" />


**Figure 1. Simulated VM Creation.** The VM inventory record was created successfully in a stopped state.

### 4.2 VM start operation

The VM was started and the inventory was listed:

```bash
python3 azlocal.py vm start vm-demo
python3 azlocal.py vm list
```

Both command outputs showed `state: running`. This confirmed the transition from the initial stopped state to the running state.

<img width="333" height="268" alt="Fig02 Simulated VM Running State" src="https://github.com/user-attachments/assets/3916177d-8713-425d-bd13-e3686c4c52b5" />



**Figure 2. Simulated VM Running State.** The start operation changed the simulated VM state to `running`.

### 4.3 Stop and restart validation

The lifecycle was tested by stopping, listing, restarting, and listing the VM:

```bash
python3 azlocal.py vm stop vm-demo
python3 azlocal.py vm list
python3 azlocal.py vm start vm-demo
python3 azlocal.py vm list
```

The first operation and listing showed `stopped`. The subsequent start operation and final listing showed `running`. The final E02 compute baseline therefore retained the VM in a running state.

<img width="353" height="500" alt="Fig03 Simulated VM Stop and Restart Validation" src="https://github.com/user-attachments/assets/a19c302a-217f-4fa7-bab2-d2830c63ab36" />


**Figure 3. Simulated VM Stop and Restart Validation.** The complete state transition sequence was successfully demonstrated.

---

## 5. Part B: Network Security Group Validation

### 5.1 NSG creation and default behavior

The simulated NSG was created in the existing resource group:

```bash
python3 azlocal.py nsg create nsg-demo --group rg-icdfa-lab
```

The output showed NSG name `nsg-demo`, group `rg-icdfa-lab`, an empty rule list, and default decision `deny`. This established a restrictive baseline before any allow rule was introduced.

<img width="505" height="158" alt="Fig04 NSG Creation and Default Deny" src="https://github.com/user-attachments/assets/8c543a7e-7fd3-43c9-94cd-5f88583ececa" />


**Figure 4. NSG Creation and Default Deny.** Unmatched traffic is denied by the NSG baseline.

### 5.2 Authorized SSH rule

An allow rule was added for TCP port `22` from the private subnet `192.168.56.0/24`:

```bash
python3 azlocal.py nsg rule nsg-demo \
  --source 192.168.56.0/24 \
  --port 22 \
  --decision allow \
  --priority 100
```

The NSG output showed decision `allow`, port `22`, priority `100`, and the intended source CIDR.

<img width="358" height="249" alt="Fig05 NSG Authorized SSH Rule" src="https://github.com/user-attachments/assets/83714968-6200-4d68-ae1b-71c6336f7c76" />


**Figure 5. NSG Authorized SSH Rule.** SSH was restricted to the designated private source range.

### 5.3 Allowed and denied source tests

The authorized and external test addresses were evaluated:

```bash
python3 azlocal.py nsg test nsg-demo --source 192.168.56.20 --port 22
python3 azlocal.py nsg test nsg-demo --source 203.0.113.20 --port 22
```

The private address `192.168.56.20` matched the priority `100` rule and returned `allow`. The external documentation address `203.0.113.20` matched no rule and returned `deny` with `matched_rule: null`. This confirmed both explicit allowance and default-deny behavior.

<img width="493" height="292" alt="Fig06 NSG Allowed and Denied Tests" src="https://github.com/user-attachments/assets/a4e0584e-bd9c-4c8e-af1e-e9c5bb0dd4e0" />


**Figure 6. NSG Allowed and Denied Tests.** The authorized private address was allowed while the unmatched external address was denied.

---

## 6. Part C: SSH Exposure and Remediation

### 6.1 Deliberate insecure rule and policy detection

A controlled insecure rule was added to allow SSH from every IPv4 source:

```bash
python3 azlocal.py nsg rule nsg-demo \
  --source 0.0.0.0/0 \
  --port 22 \
  --decision allow \
  --priority 200

python3 azlocal.py nsg test nsg-demo --source 203.0.113.20 --port 22
python3 azlocal.py policy
```

The NSG then contained the authorized priority `100` rule and the broad priority `200` rule. The external test address changed from `deny` to `allow` and matched priority `200`. The policy scanner checked two resources and returned one finding: control `ssh-exposure`, finding `SSH allowed from any IPv4 source`, resource `nsg-demo`.

<img width="365" height="627" alt="Fig07 Insecure SSH Exposure Detected" src="https://github.com/user-attachments/assets/42437361-dabb-4748-bc34-595b9a043dee" />


**Figure 7. Insecure SSH Exposure Detected.** The broad rule created a demonstrable exposure that was detected by the policy control.

### 6.2 Remediation and secure-state validation

The insecure rule was removed and the network posture was re-evaluated:

```bash
python3 azlocal.py nsg remove nsg-demo --priority 200
python3 azlocal.py nsg test nsg-demo --source 203.0.113.20 --port 22
python3 azlocal.py policy
python3 azlocal.py nsg list
```

The external address returned to `deny` with no matched rule. The policy result showed `findings_count: 0`. The final NSG listing retained only the priority `100` rule for `192.168.56.0/24`.

<img width="422" height="575" alt="Fig08 SSH Exposure Remediated" src="https://github.com/user-attachments/assets/035e80bf-c118-449e-b0ca-1f8d0b039c8d" />


**Figure 8. SSH Exposure Remediated.** The final simulated network configuration restored default denial for the external address and retained the authorized private-subnet rule.

---

## 7. Part D: Real Linux Localhost Service

### 7.1 Service startup and runtime log

The supplied health service was started with:

```bash
python3 scripts/health_service.py --port 8088
```

The service announced `Local only at http://127.0.0.1:8088/health`. The runtime log also displayed two `GET / HTTP/1.1` requests that returned HTTP `404`. These root-path requests do not show a failure of `/health`; they show that `/` is not the health endpoint.

<img width="371" height="137" alt="Fig09 Local Health Service Runtime Log" src="https://github.com/user-attachments/assets/57c0b245-0f63-4113-aa5f-a9026222b7c7" />


**Figure 9. Local Health Service Runtime Log.** The service started locally. Requests to `/` returned `404`, while the intended endpoint was `/health`.

### 7.2 Health endpoint and local-only binding

The health endpoint and listening socket were tested from another terminal:

```bash
curl -i http://127.0.0.1:8088/health
ss -ltnp | grep 8088
```

The response returned HTTP `200 OK`, content type `application/json`, content length `107`, and a JSON object with `status: healthy`, system `CCSE-102 local linux service`, and a timestamp. The socket output showed Python listening on `127.0.0.1:8088`, which confirmed local-only binding rather than exposure through `0.0.0.0:8088`.

<img width="847" height="210" alt="Fig10 Local Health Endpoint and Port Binding" src="https://github.com/user-attachments/assets/31cc2d71-871d-4e0c-9da5-cd7d4d915cda" />


**Figure 10. Local Health Endpoint and Port Binding.** The real Linux service responded successfully and was restricted to localhost.

### 7.3 Port-closure verification status

The final screenshot included the instruction to return to Terminal 1 and press `Ctrl+C`, followed by:

```bash
ss -ltn | grep 8088 || echo "Port 8088 is no longer listening"
```

However, the visible result still showed:

```text
LISTEN ... 127.0.0.1:8088 ...
```

Therefore, the uploaded evidence does **not** confirm that the service was stopped. The most likely explanation is that `Ctrl+C` was not delivered to the terminal running the Python service, or the closure check was performed before the process ended.

<img width="348" height="77" alt="Fig11 Port Closure Verification Requires Correction" src="https://github.com/user-attachments/assets/ca63aeed-64d1-420d-a5e5-4ec0eeae7fcd" />


**Figure 11. Port Closure Verification Requires Correction.** The listener remained active, so a replacement screenshot is required after the process is stopped correctly.

#### Required corrective validation

1. Return to the exact terminal running `health_service.py`.
2. Press `Ctrl+C` once.
3. Confirm that the Python command exits and the shell prompt returns.
4. In the second terminal, run:

```bash
ss -ltn | grep 8088 || echo "Port 8088 is no longer listening"
```

5. Capture output showing:

```text
Port 8088 is no longer listening
```

6. Replace Figure 11 with the corrected screenshot and rename it:

```text
Fig11 Local HTTP Service Stopped.png
```

Until that replacement is available, the service-shutdown objective remains **partially evidenced**, not passed.

---

## 8. Results Summary

| Control or operation | Expected result | Observed result | Status |
|---|---|---|---|
| VM creation | `vm-demo` created as stopped | Stopped VM record created | Pass |
| VM start | State becomes running | Running shown | Pass |
| VM stop | State becomes stopped | Stopped shown | Pass |
| VM restart | Final state running | Running shown | Pass |
| NSG baseline | Empty rules, default deny | Confirmed | Pass |
| Authorized SSH | Private address allowed | `192.168.56.20` allowed by priority 100 | Pass |
| Unauthorized SSH | External address denied | `203.0.113.20` denied | Pass |
| Deliberate exposure | External address allowed | Allowed by priority 200 | Pass |
| Policy detection | `ssh-exposure` finding | One finding returned | Pass |
| Remediation | External address denied; clean policy | Deny restored; zero findings | Pass |
| Health endpoint | HTTP success and healthy JSON | HTTP 200 and healthy JSON | Pass |
| Local-only binding | Listener on `127.0.0.1:8088` | Confirmed | Pass |
| Service shutdown | Port no longer listening | Listener still visible | **Requires correction** |

---

## 9. Security and Operational Analysis

### 9.1 Compute-state administration

The simulator preserved a clear VM lifecycle record. The state transitioned from stopped to running, back to stopped, and finally to running. This demonstrates administrative control while correctly limiting the claim to simulated inventory.

### 9.2 Default deny and ordered rules

The NSG denied traffic without a matching rule. The private subnet rule at priority `100` allowed the authorized test address. The later broad rule at priority `200` applied only where the priority `100` rule did not match. This demonstrates ordered rule evaluation and the security value of a default-deny baseline.

### 9.3 Exposure detection and remediation

Allowing SSH from `0.0.0.0/0` converted the external test result from deny to allow. The policy scanner detected the condition, and removal of priority `200` restored the secure outcome. The before-and-after evidence demonstrates a complete finding-remediation-validation cycle.

### 9.4 Local service exposure

The health service was bound to `127.0.0.1`, not all interfaces. This limits direct access to the local machine. The successful `/health` request establishes availability, while the two `404` entries for `/` show that endpoint paths matter and that root-path requests are not equivalent to health checks.

### 9.5 Evidence gap in shutdown validation

The last screenshot still showed an active listener. Treating that screenshot as proof of shutdown would be inaccurate. Correct evidence must show either the explicit fallback message or no listener output after the Python process exits.

---

## 10. Risk Register

| Risk ID | Risk | Likelihood | Impact | Control | Evidence/status |
|---|---|---:|---:|---|---|
| E02-R01 | VM service interruption caused by incorrect lifecycle operation | Medium | Medium | Verify state after each operation | Start, stop, and restart outputs captured |
| E02-R02 | SSH exposed to every IPv4 source | High | High | Remove `0.0.0.0/0` rule; retain private CIDR | Policy finding cleared after priority 200 removal |
| E02-R03 | Unauthorized source bypasses network restriction | Medium | High | Default deny plus source-restricted rule | External address denied before and after remediation |
| E02-R04 | Local demonstration service exposed on all interfaces | Medium | High | Bind service to `127.0.0.1` | Local-only listener confirmed |
| E02-R05 | Service left running after testing | Medium | Medium | Stop process and verify socket closure | **Open evidence issue: listener still active in Figure 11** |
| E02-R06 | Incorrect endpoint tested | Medium | Low | Use `/health`, not `/` | `/health` returned 200; `/` returned 404 |

---

## 11. Evidence Register and Exact File Naming

Store the files under `screenshots/E02/` in this exact order:

| Order | Exact filename | Original screenshot | Scenario matched |
|---:|---|---|---|
| 1 | `Fig01 Simulated VM Creation.png` | `Screenshot 2026-11-24 115514.png` | VM created in stopped state |
| 2 | `Fig02 Simulated VM Running State.png` | `Screenshot 2026-11-24 115706.png` | VM start and running listing |
| 3 | `Fig03 Simulated VM Stop and Restart Validation.png` | `Screenshot 2026-11-24 115812.png` | Stop, stopped listing, restart, running listing |
| 4 | `Fig04 NSG Creation and Default Deny.png` | `Screenshot 2026-11-24 115942.png` | NSG created with empty rules and default deny |
| 5 | `Fig05 NSG Authorized SSH Rule.png` | `Screenshot 2026-11-24 120118.png` | Priority 100 private-subnet rule |
| 6 | `Fig06 NSG Allowed and Denied Tests.png` | `Screenshot 2026-11-24 120224.png` | Authorized allow and external default deny |
| 7 | `Fig07 Insecure SSH Exposure Detected.png` | `Screenshot 2026-11-24 120312.png` | Broad rule, external allow, and policy finding |
| 8 | `Fig08 SSH Exposure Remediated.png` | `Screenshot 2026-11-24 120614.png` | Rule removed, external deny, clean policy, final NSG |
| 9 | `Fig09 Local Health Service Runtime Log.png` | `Screenshot 2026-11-24 120812.png` | Local service startup and root-path 404 requests |
| 10 | `Fig10 Local Health Endpoint and Port Binding.png` | `Screenshot 2026-11-24 121044.png` | HTTP 200 healthy response and localhost listener |
| 11 | `Fig11 Port Closure Verification Requires Correction.png` | `Screenshot 2026-11-24 121205.png` | Listener still active; corrective evidence required |

After obtaining corrected shutdown evidence, replace the eleventh file and update its name to:

```text
Fig11 Local HTTP Service Stopped.png
```

---

## 12. Final E02 State

The evidenced final simulated state is:

```text
VM:
  name: vm-demo
  group: rg-icdfa-lab
  size: B1s
  state: running

NSG:
  name: nsg-demo
  default: deny
  retained rule:
    source: 192.168.56.0/24
    port: 22
    decision: allow
    priority: 100

Policy:
  findings_count: 0
```

The real Linux service was healthy and localhost-bound during testing. The service must be stopped and the missing closure evidence corrected before proceeding to a final submission package.

---

## 13. Limitations

1. VM operations modify simulated inventory only.
2. NSG tests model rule evaluation but do not alter the WSL firewall.
3. The test address `203.0.113.20` was evaluated by the simulator; no network connection to that address was attempted.
4. The policy scanner implements controls defined in simulator version 1.0.
5. The Python health service is real and local, but it is not deployed to Microsoft Azure.
6. The uploaded evidence does not yet prove that the local service was stopped.
7. No optional SSH tunnel or second Ubuntu Server VM was used in the supplied evidence.

---

## 14. Recommendations

1. Preserve the final NSG configuration with only the priority `100` private-subnet SSH rule.
2. Do not reintroduce the priority `200` broad rule outside controlled evidence testing.
3. Keep the health service bound to `127.0.0.1`.
4. Use `/health` for service validation and avoid interpreting root-path `404` responses as a service failure.
5. Repeat the shutdown procedure and replace Figure 11 with proof that port `8088` is closed.
6. Review E02 audit logs and export a checksum-protected evidence file before final submission.
7. Do not reset the simulator before E03 because the running VM and cumulative state are required for later recovery testing.

---

## 15. Conclusion

Laboratory E02 successfully demonstrated simulated compute lifecycle administration, restrictive NSG operation, deliberate SSH exposure detection, and remediation. The authorized private address was allowed, the external test address was denied by default, the broad SSH rule created a detectable risk, and removal of that rule restored a zero-finding network posture.

The real Linux health endpoint returned HTTP `200 OK` and was correctly bound to `127.0.0.1:8088`. One evidence item remains incomplete: the final screenshot continued to show the service in `LISTEN` state. The shutdown check must be repeated and Figure 11 replaced before the laboratory is considered fully evidenced.

---

## 16. Academic Integrity and AI Assistance Disclosure

All commands, outputs, screenshots, and conclusions in the final submission must represent laboratory work independently executed and verified by Wadondera A. Collins.

Microsoft Copilot was used to organize this report, inspect the supplied screenshots, align each image with the scenario visibly shown, and identify the unresolved port-closure evidence. Copilot did not execute the student's WSL laboratory session or manufacture terminal results.

---

## 17. Author

**Wadondera A. Collins**  
ICDFA Trainee · Cohort 11 · Cloud Security Engineering  
International Cybersecurity and Digital Forensics Academy

---

<div align="center">

**CCSE-102 Laboratory E02 · Documentation and Evidence Report**  
**Offline Azure-style simulation · Not Microsoft Azure**

</div>
