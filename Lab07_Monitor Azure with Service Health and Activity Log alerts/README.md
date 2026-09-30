<div align="center">

# 🔔 Azure Monitoring and Alerting: Complete Guide

### Mentor Pilot Program | Completed Assignment

**Author:** Wadondera A. Collins  
**Role:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Completion Date:** September 30, 2026

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Monitor-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Alerts](https://img.shields.io/badge/Focus-Alerting%20and%20Notifications-6F42C1)](#-skills-demonstrated)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Service Health](https://img.shields.io/badge/Azure-Service%20Health-00A4EF)](#-exercise-2-create-a-service-health-alert)

*A hands-on Azure monitoring lab covering reusable action groups, email notification testing, Service Health alerts, Activity Log alerts, configuration validation, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Create and Test an Action Group](#-exercise-1-create-and-test-an-action-group)
- [Exercise 2: Create a Service Health Alert](#-exercise-2-create-a-service-health-alert)
- [Exercise 3: Create an Activity Log Alert](#-exercise-3-create-an-activity-log-alert)
- [Exercise 4: Clean Up and Verify](#-exercise-4-clean-up-and-verify)
- [Screenshot Evidence](#-screenshot-evidence)
- [Validation Results](#-validation-results)
- [Command Reference](#-command-reference)
- [Troubleshooting](#-troubleshooting)
- [Skills Demonstrated](#-skills-demonstrated)
- [Key Takeaways](#-key-takeaways)
- [Completion Checklist](#-completion-checklist)
- [Author](#-author)
- [Acknowledgements](#-acknowledgements)
- [Disclaimer](#-disclaimer)

---

## 🚀 Project Overview

This repository documents the successful completion of the **Azure Monitoring and Alerting** lab in the **Mentor Pilot Program**. The project established a reusable email notification path and connected it to two operational monitoring scenarios.

The solution included:

1. An action group named `ag-gp-ops-email`.
2. A tested email notification named `ops-team-email`.
3. A Service Health alert named `ar-gp-service-health`.
4. An Activity Log alert named `ar-gp-activity-delete`.
5. A dedicated resource group named `rg-gp-monitoring-alerts`.
6. Validation of alert conditions, severity, action-group association, and enabled state.
7. Ordered cleanup and post-deletion verification.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

By completing this lab, I demonstrated the ability to:

- Create a dedicated Azure monitoring resource group.
- Configure a reusable Azure Monitor action group.
- Configure and test email notification delivery.
- Review Azure Service Health information.
- Create a Service Health alert for incidents and planned maintenance.
- Create an Activity Log alert for resource-group deletion.
- Reuse one action group across multiple alert rules.
- Assign and verify alert severity.
- Review alert conditions, actions, and enabled state.
- Remove temporary monitoring resources and verify cleanup.

---

## 🏗️ Architecture and Resources

```text
Azure Subscription
└── Resource Group: rg-gp-monitoring-alerts
    ├── Action Group: ag-gp-ops-email
    │   ├── Display Name: OpsEmail
    │   ├── Region: Global
    │   └── Email Notification: ops-team-email
    ├── Service Health Alert: ar-gp-service-health
    │   ├── Service issue
    │   ├── Planned maintenance
    │   └── Action: ag-gp-ops-email
    └── Activity Log Alert: ar-gp-activity-delete
        ├── Signal: Delete resource group
        ├── Severity: Sev 2 - Warning
        └── Action: ag-gp-ops-email
```

| Resource | Name or Setting | Purpose |
|---|---|---|
| Resource group | `rg-gp-monitoring-alerts` | Monitoring resource boundary |
| Action group | `ag-gp-ops-email` | Reusable notification channel |
| Display name | `OpsEmail` | Short action-group display name |
| Notification | `ops-team-email` | Authorized email receiver |
| Service Health alert | `ar-gp-service-health` | Platform incident and maintenance awareness |
| Activity Log alert | `ar-gp-activity-delete` | Resource-group deletion detection |
| Severity | `Sev 2 - Warning` | Activity Log alert classification |

> [!NOTE]
> **Final state:** The alert rules, action group, and resource group were deleted after validation.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An authorized Skillable Azure lab subscription
- Permission to create resource groups, action groups, and alert rules
- Read access to the selected monitoring scope
- An authorized email address for notification testing

### Tools and Environment

| Tool or Service | Version or Status | Purpose |
|---|---|---|
| Microsoft Azure portal | Version not provided | Monitoring configuration and validation |
| Azure Monitor | Managed Azure service | Alerts, rules, and action groups |
| Azure Action Groups | Managed Azure feature | Reusable notifications |
| Azure Service Health | Managed Azure service | Platform health notifications |
| Azure Activity Log | Managed Azure service | Management-operation events |
| Skillable Lab Environment | Version not provided | Guided educational subscription |

> [!NOTE]
> Fixed product versions were not displayed in the lab instructions and are not estimated here.

### Security Notice

Passwords, Temporary Access Pass codes, usernames, email addresses, subscription identifiers, tenant information, and authentication secrets are intentionally **not included**.

> [!CAUTION]
> Review screenshots before publication and redact email addresses, usernames, subscription IDs, tenant IDs, and access tokens.

---

## 📧 Exercise 1: Create and Test an Action Group

### 1. Prepare the Environment

1. Sign in to the Azure portal with the authorized lab account.
2. Open **Resource groups**.
3. Create `rg-gp-monitoring-alerts` in the selected region.
4. Identify an authorized notification address without publishing it.

**Validation:** The monitoring resource group was created successfully.

### 2. Create the Action Group

Configure the action group with the following values:

| Setting | Value |
|---|---|
| Resource group | `rg-gp-monitoring-alerts` |
| Region | Global |
| Action group name | `ag-gp-ops-email` |
| Display name | `OpsEmail` |
| Notification type | Email/SMS message/Push/Voice |
| Notification name | `ops-team-email` |
| Notification method | Email |

**Validation:** `ag-gp-ops-email` appeared in the action-group list with the email notification configured.

### 3. Test the Action Group

1. Open `ag-gp-ops-email`.
2. Select **Test action group**.
3. Choose **Service Health** as the sample type.
4. Confirm `ops-team-email` is selected.
5. Start the test.
6. Verify the test status and notification delivery.

**Validation:** The test displayed **Success**, and the authorized mailbox received the Azure test email.

---

## 🩺 Exercise 2: Create a Service Health Alert

### 1. Review Service Health

Review the following areas:

- Service issues
- Planned maintenance
- Health advisories
- Health history

**Validation:** All four Service Health areas were reviewed.

### 2. Configure the Service Health Alert

1. Select **Create service health alert**.
2. Select the lab subscription.
3. Retain the services permitted by the lab.
4. Use the required Global configuration.
5. Select **Service issue** and **Planned maintenance**.
6. Attach `ag-gp-ops-email`.
7. Select `rg-gp-monitoring-alerts` for the rule.
8. Name the rule `ar-gp-service-health`.
9. Confirm the rule is enabled upon creation.
10. Create the rule.

**Validation:** `ar-gp-service-health` was created, enabled, and connected to the correct action group.

---

## ⚠️ Exercise 3: Create an Activity Log Alert

### 1. Configure the Scope and Condition

1. Open **Monitor** → **Alerts**.
2. Select **Create** → **Alert rule**.
3. Filter the scope by the **Resource groups** type.
4. Select `rg-gp-monitoring-alerts`.
5. Open **Condition**.
6. Select the **Delete resource group** Activity Log signal.
7. Select `Sev 2 - Warning`.

**Validation:** The condition was configured to detect resource-group deletion events.

### 2. Attach the Action Group and Create the Rule

1. Open **Actions**.
2. Select `ag-gp-ops-email`.
3. Open **Details**.
4. Select `rg-gp-monitoring-alerts`.
5. Name the rule `ar-gp-activity-delete`.
6. Confirm `Sev 2 - Warning`.
7. Confirm the rule is enabled.
8. Review and create the rule.

**Validation:** Both alert rules appeared in Azure Monitor.

### 3. Review Both Rules

Confirm that the Service Health alert:

- Monitors Service issue and Planned maintenance events.
- Uses `ag-gp-ops-email`.
- Is enabled.

Confirm that the Activity Log alert:

- Monitors the Delete resource group signal.
- Uses `ag-gp-ops-email`.
- Uses `Sev 2 - Warning`.
- Is enabled.

**Validation:** Both rules showed the intended conditions and action-group association.

---

## 🧹 Exercise 4: Clean Up and Verify

### 1. Delete the Alert Rules

Delete `ar-gp-activity-delete` and `ar-gp-service-health`.

**Validation:** Neither alert rule remained in the alert-rule list.

### 2. Delete the Action Group

Delete `ag-gp-ops-email`.

**Validation:** The action group no longer appeared in Azure Monitor.

### 3. Delete the Resource Group

Delete `rg-gp-monitoring-alerts` and confirm the resource-group name when prompted.

**Validation:** The resource group no longer appeared under Resource groups.

> [!WARNING]
> Resource deletion can be permanent. Verify each selected object before confirming cleanup.

---

## 🖼️ Screenshot Evidence

| Filename | Required Evidence | Placement |
|---|---|---|
| `Fig01 Monitoring Resource Group Created.png` | Monitoring resource group | Exercise 1, Prepare the Environment |
| `Fig02 Action Group Configuration.png` | Action group and notification settings | Exercise 1, Create the Action Group |
| `Fig03 Action Group Test Success.png` | Successful action-group test | Exercise 1, Test the Action Group |
| `Fig04 Azure Test Email Notification.png` | Received test notification with sensitive data redacted | Exercise 1, Test the Action Group |
| `Fig05 Service Health Review.png` | Service Health areas reviewed | Exercise 2, Review Service Health |
| `Fig06 Service Health Alert Created.png` | Enabled Service Health alert | Exercise 2, Configure the Alert |
| `Fig07 Activity Log Delete Condition.png` | Deletion signal and scope | Exercise 3, Configure Scope and Condition |
| `Fig08 Activity Log Alert Created.png` | Enabled deletion alert and severity | Exercise 3, Create the Rule |
| `Fig09 Alert Rules Validation.png` | Both rules visible | Exercise 3, Review Both Rules |
| `Fig10 Alert Rule Details Reviewed.png` | Correct condition and action group | Exercise 3, Review Both Rules |
| `Fig11 Monitoring Cleanup Verified.png` | Final cleanup evidence | Exercise 4, Clean Up and Verify |

```markdown
![Fig03 Action Group Test Success](screenshots/Fig03%20Action%20Group%20Test%20Success.png)

*Figure 3: Azure Monitor displays a successful test for the configured action group.*
```

> [!IMPORTANT]
> Include only screenshots that visibly prove the assigned task. Ensure each filename, Markdown link, caption, and placement matches its image exactly.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Monitoring resource group created | ✅ Passed |
| Action group created | ✅ Passed |
| Email notification configured | ✅ Passed |
| Action group test succeeded | ✅ Passed |
| Azure test email received | ✅ Passed |
| Service Health areas reviewed | ✅ Passed |
| Service Health alert created | ✅ Passed |
| Service issue selected | ✅ Passed |
| Planned maintenance selected | ✅ Passed |
| Activity Log scope configured | ✅ Passed |
| Delete resource group signal selected | ✅ Passed |
| Activity Log alert created | ✅ Passed |
| `Sev 2 - Warning` configured | ✅ Passed |
| Both rules used the action group | ✅ Passed |
| Both rules were enabled | ✅ Passed |
| Alert rules deleted | ✅ Passed |
| Action group deleted | ✅ Passed |
| Resource group deleted | ✅ Passed |
| Final cleanup verified | ✅ Passed |

---

## 📚 Command Reference

This assignment was completed through the Azure portal.

| Goal | Azure Portal Path |
|---|---|
| Create the resource group | **Resource groups** → **Create** |
| Create an action group | **Monitor** → **Alerts** → **Action groups** → **Create** |
| Test an action group | Action group → **Test action group** |
| Review Service Health | **Service Health** |
| Create a Service Health alert | **Service Health** → **Create service health alert** |
| Create an Activity Log alert | **Monitor** → **Alerts** → **Create** → **Alert rule** |
| Review alert rules | **Monitor** → **Alerts** → **Alert rules** |
| Delete the action group | **Monitor** → **Alerts** → **Action groups** |
| Delete the project | Resource group → **Delete resource group** |

### Repository Structure

```text
azure-monitoring-alerts/
├── README.md
├── screenshots/
│   ├── Fig01 Monitoring Resource Group Created.png
│   ├── Fig02 Action Group Configuration.png
│   ├── Fig03 Action Group Test Success.png
│   ├── Fig04 Azure Test Email Notification.png
│   ├── Fig05 Service Health Review.png
│   ├── Fig06 Service Health Alert Created.png
│   ├── Fig07 Activity Log Delete Condition.png
│   ├── Fig08 Activity Log Alert Created.png
│   ├── Fig09 Alert Rules Validation.png
│   ├── Fig10 Alert Rule Details Reviewed.png
│   └── Fig11 Monitoring Cleanup Verified.png
└── LICENSE
```

---

## 🧰 Troubleshooting

### The test email is not received

- Confirm the email address is correct.
- Review the action-group test result.
- Check the mailbox's junk or filtered folders.
- Confirm the email notification is enabled.

### The Service Health alert cannot use the action group

Confirm that the action group region is **Global** and that the signed-in identity can read the action group.

### The deletion signal is unavailable

Confirm that the alert scope is a resource group and search the available Activity Log signals for **Delete resource group**.

### Both alert rules do not appear

Verify the active subscription and selected resource group. Refresh the Alert rules view after creation.

### The alert rule is disabled

Open the rule details, review its state, and enable it if the lab requires the rule to be active.

### Cleanup appears incomplete

Independently check Alert rules, Action groups, and Resource groups in the active subscription.

---

## 🧠 Skills Demonstrated

- Azure Monitor administration
- Azure resource-group management
- Action-group creation and testing
- Email notification configuration
- Azure Service Health review
- Service Health alert creation
- Activity Log signal selection
- Alert scope configuration
- Alert severity classification
- Reusable notification design
- Alert-rule validation
- Monitoring cleanup and verification
- Professional technical documentation

---

## 💡 Key Takeaways

1. **Reusable action groups simplify notification management.** One tested notification channel supported both alert rules.
2. **Notification paths should be tested before operational use.** The successful test and received email validated delivery.
3. **Service Health alerts improve platform awareness.** The rule covered service issues and planned maintenance.
4. **Activity Log alerts provide visibility into administrative actions.** The deletion rule targeted a high-impact management event.
5. **Scope, condition, action, severity, and state all require review.** A rule is only useful when its complete configuration matches the monitoring objective.
6. **Severity communicates operational importance.** The deletion event used `Sev 2 - Warning` as required by the lab.
7. **Cleanup completes the monitoring lifecycle.** Rules, notification resources, and the project resource group were removed and verified.

---

## ☑️ Completion Checklist

- [x] Created `rg-gp-monitoring-alerts`
- [x] Created `ag-gp-ops-email`
- [x] Configured `OpsEmail`
- [x] Added `ops-team-email`
- [x] Tested the action group
- [x] Confirmed successful email delivery
- [x] Reviewed Service Health
- [x] Created `ar-gp-service-health`
- [x] Selected Service issue
- [x] Selected Planned maintenance
- [x] Created `ar-gp-activity-delete`
- [x] Selected Delete resource group
- [x] Configured `Sev 2 - Warning`
- [x] Attached the reusable action group to both rules
- [x] Confirmed both rules were enabled
- [x] Reviewed both rules
- [x] Deleted both alert rules
- [x] Deleted the action group
- [x] Deleted the resource group
- [x] Confirmed cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical Azure monitoring and cloud-security portfolio, demonstrating reusable notifications, platform-health awareness, administrative-event detection, validation, and responsible cleanup.

---

## 🙏 Acknowledgements

This guided project was completed as part of the **Mentor Pilot Program** in a Skillable Azure environment. Mentor supported the learning experience through lab navigation, instruction comprehension, and troubleshooting.

Official reference material:

- [Create and manage Azure Monitor action groups](https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/action-groups)
- [Create activity log and Service Health alert rules](https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-create-activity-log-alert-rule)
- [Create Service Health alerts](https://learn.microsoft.com/en-us/azure/service-health/alerts-activity-log-service-notifications-portal)
- [Monitor Azure with Service Health and Activity Log alerts](https://learn.microsoft.com/en-us/training/modules/guided-project-monitor-service-health-activity-alerts/)

---

## ⚖️ Disclaimer

This repository documents a completed educational assignment performed in a temporary Skillable Microsoft Azure environment. It is not a production-ready monitoring design and does not replace official Microsoft documentation, organizational monitoring standards, or professional security guidance. Resource names, alert conditions, severity mappings, notification recipients, regions, and escalation procedures require review before reuse.

Passwords, Temporary Access Pass codes, usernames, email addresses, subscription identifiers, tenant information, access tokens, and authentication secrets are intentionally excluded. Screenshots must be reviewed and redacted before publication. Azure services, interfaces, roles, limits, and features may change over time.

---

<div align="center">

### 🎉 Lab Completed Successfully

**Azure monitoring: configured, tested, connected, validated, and responsibly removed.**

Made with curiosity, care, and a commitment to secure, observable, and resilient cloud engineering.  

**Wadondera A. Collins**  
*ICDFA Trainee | Cohort 11 | Cloud Security Engineering*

</div>
