<div align="center">

# Azure Monitoring and Service Health Alerts Documentation Report

## Action Groups, Email Notifications, Testing, and Service Health Alerting

**Prepared by:** Wadondera A. Collins  
**Programme:** ICDFA Trainee | Cohort 11  
**Professional Focus:** Cloud Security Engineering  
**Lab Platform:** Microsoft Azure | Skillable  
**Report Date:** September 30, 2026  
**Project Status:** Completed

</div>

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Executive Summary](#2-executive-summary)
3. [Project Objectives](#3-project-objectives)
4. [Professional Value](#4-professional-value)
5. [Skills Demonstrated](#5-skills-demonstrated)
6. [Technologies and Tools Used](#6-technologies-and-tools-used)
7. [Lab Environment](#7-lab-environment)
8. [Repository Structure](#8-repository-structure)
9. [Methodology](#9-methodology)
10. [Implementation, Evidence, and Analysis](#10-implementation-evidence-and-analysis)
11. [Results and Validation](#11-results-and-validation)
12. [Security and Privacy Notes](#12-security-and-privacy-notes)
13. [Limitations and Next Steps](#13-limitations-and-next-steps)
14. [Conclusion](#14-conclusion)
15. [Disclaimer](#15-disclaimer)
16. [Author](#16-author)

---

## 1. Project Overview

This report documents an Azure monitoring lab focused on establishing a notification workflow for Azure Service Health events. The implementation created a dedicated resource group, configured an Azure Monitor action group with an email notification, tested the action group, created a Service Health alert rule, verified that the alert rule was enabled, and checked the Alert rules page after cleanup.

The screenshots supplied for this project relate to Azure monitoring and alerting. They do not match a cost-governance project involving tags, budgets, or regional policy enforcement. This report therefore uses a corrected project title and evidence structure so that every figure accurately matches its visible Azure task.

---

## 2. Executive Summary

The project established a basic operational-alerting workflow in Microsoft Azure. A resource group named `rg-gp-monitoring-alerts` was configured in East US to organize the monitoring resources. An action group named `ag-gp-ops-email` was present and configured with an email notification named `ops-team-email`. The action group was selected for testing with a sample Service Health alert.

A Service Health quick alert rule named `ar-gp-service-health` was configured for the subscription. The configuration displayed a global region scope, 259 selected services, two selected event types, and use of an existing action group. The Alert rules page then showed the rule with Service health as its signal type and Enabled as its status. A later screenshot showed no alert rules found, which is consistent with cleanup verification after removal or with the current page filters returning no matching rules.

---

## 3. Project Objectives

- Create a dedicated resource group for monitoring and alerting resources.
- Configure an Azure Monitor action group.
- Add an email notification channel to the action group.
- Test the action group using a sample Service Health alert.
- Create an Azure Service Health alert rule.
- Associate the Service Health alert with the existing action group.
- Verify that the alert rule is enabled.
- Review the Alert rules page after cleanup.
- Document the implementation using accurately matched evidence.

---

## 4. Professional Value

This project demonstrates practical observability and incident-notification skills relevant to cloud operations and Cloud Security Engineering. Action groups provide a reusable notification target, while Service Health alerts support awareness of Azure service incidents and platform events affecting a selected subscription.

The project also demonstrates disciplined evidence handling by separating configuration evidence, test evidence, enabled-rule evidence, and cleanup evidence.

---

## 5. Skills Demonstrated

- Azure Portal navigation
- Azure Resource Group configuration
- Azure Monitor action-group configuration
- Email notification-channel setup
- Action-group testing
- Azure Service Health navigation
- Service Health alert-rule configuration
- Alert-rule validation
- Monitoring-resource cleanup verification
- Security-conscious technical documentation

---

## 6. Technologies and Tools Used

| Technology or Tool | Purpose |
|---|---|
| Microsoft Azure Portal | Configure and validate the monitoring workflow |
| Azure Resource Groups | Organize monitoring and alerting resources |
| Azure Monitor | Manage action groups and alert rules |
| Azure Monitor Action Groups | Define reusable notification actions |
| Email notifications | Receive alert notifications through email |
| Azure Service Health | Configure alerts for Azure service events |
| Skillable | Temporary guided-lab environment |
| Markdown | Produce evidence-based project documentation |

---

## 7. Lab Environment

| Environment Item | Visible Configuration |
|---|---|
| Resource group | `rg-gp-monitoring-alerts` |
| Resource-group region | East US |
| Action group | `ag-gp-ops-email` |
| Action-group short name | `OpsEmail` |
| Notification name | `ops-team-email` |
| Notification type | Email |
| Sample test type | Service health alert |
| Alert rule | `ar-gp-service-health` |
| Alert signal type | Service health |
| Alert status | Enabled |
| Alert severity shown | 4, Verbose |
| Service Health region scope shown | Global |

> Personal email information visible in the screenshots should be redacted before the repository is made public.

---

## 8. Repository Structure

```text
Azure-Monitoring-Alerts/
|
+-- Azure_Monitoring_Alerts_Documentation_Report.md
+-- screenshots/
    +-- Fig01 Monitoring Resource Group Configuration.png
    +-- Fig02 Monitoring Resource Group Created.png
    +-- Fig03 Action Group Email Notification.png
    +-- Fig04 Action Group Test Configuration.png
    +-- Fig05 Service Health Alert Configuration.png
    +-- Fig06 Service Health Alert Rule Enabled.png
    +-- Fig07 Alert Rule Cleanup Verification.png
```

The image links below assume the report and images are stored in the same directory. If the images are placed in `screenshots/`, add `screenshots/` to each relative path.

---

## 9. Methodology

1. Configure a dedicated resource group in East US.
2. Confirm that the resource group exists and is available for monitoring resources.
3. Configure an action group with an email notification channel.
4. Select the action group and prepare a Service Health sample test.
5. Configure a Service Health quick alert rule and associate it with the existing action group.
6. Confirm that the Service Health alert rule appears as enabled.
7. Review the Alert rules page after cleanup or removal.
8. Match each screenshot only to the task visibly represented.

---

## 10. Implementation, Evidence, and Analysis

### 10.1 Monitoring Resource Group Configuration

The monitoring workflow began with the configuration of `rg-gp-monitoring-alerts` in East US.

<img width="1094" height="569" alt="Fig01_Monitoring_Resource_Group_Configuration" src="https://github.com/user-attachments/assets/82632c60-6622-42d5-906b-3447a66b7b66" />


*Figure 1: Resource-group configuration for `rg-gp-monitoring-alerts` in East US.*

#### Evidence analysis

The screenshot shows the **Create a resource group** page with the resource-group name and East US region entered. The **Review + create** button is available. This supports the configuration step, but it does not by itself show the final creation notification.

---

### 10.2 Monitoring Resource Group Created

The next screenshot shows `rg-gp-monitoring-alerts` listed in Azure Resource Manager and opened on its Overview page.

<img width="1091" height="574" alt="Fig02_Monitoring_Resource_Group_Created" src="https://github.com/user-attachments/assets/405c6fa4-8614-47e2-bff1-efeb9b1a3b79" />


*Figure 2: The monitoring resource group is present and opened in Azure Resource Manager.*

#### Evidence analysis

The resource group is visible in the Resource groups list and selected in the Azure Portal. The Resources area displays no matching resources under the active filters at the time of capture. This screenshot verifies the resource group's existence but does not prove the presence or absence of resources outside the current filter state.

---

### 10.3 Action Group Email Notification

An email notification named `ops-team-email` was configured in the action-group workflow.

<img width="1094" height="567" alt="Fig03_Action_Group_Email_Notification" src="https://github.com/user-attachments/assets/e0178f2a-5e6c-4625-8e85-691d68e028ed" />


*Figure 3: Action-group notification configuration using the Email notification type.*

#### Evidence analysis

The screenshot shows the **Create action group** workflow on the Notifications tab. The notification type is Email/SMS message/Push/Voice, the notification is named `ops-team-email`, and Email is selected in the configuration panel. The visible personal email address must be redacted before public GitHub publication.

---

### 10.4 Action Group Test Configuration

The action group `ag-gp-ops-email` was selected for testing with a sample Service Health alert.

<img width="1089" height="556" alt="Fig04_Action_Group_Test_Configuration" src="https://github.com/user-attachments/assets/a1aee37e-410b-4e45-858c-411c09891697" />


*Figure 4: Action-group test panel using the Service health alert sample type and the email notification.*

#### Evidence analysis

The screenshot shows `ag-gp-ops-email`, short name `OpsEmail`, and resource group `rg-gp-monitoring-alerts`. The test panel displays **Service health alert** as the sample type and includes the email notification `ops-team-email`. The **Test** button remains visible, so the screenshot verifies test configuration rather than a completed test result.

---

### 10.5 Service Health Alert Configuration

A Service Health quick alert rule was configured and associated with the existing action group.

<img width="1086" height="556" alt="Fig05_Service_Health_Alert_Configuration" src="https://github.com/user-attachments/assets/b416a52b-eacf-4235-ad4f-cc76b284342a" />


*Figure 5: Service Health quick alert configuration for `ar-gp-service-health`.*

#### Evidence analysis

The screenshot shows 259 selected services, Global as the region scope, and two selected event types. The resource group is `rg-gp-monitoring-alerts`, and the alert rule name is `ar-gp-service-health`. **Use an existing action group** is selected. The screenshot captures the configuration state before the final **Create** action is completed.

---

### 10.6 Service Health Alert Rule Enabled

The created Service Health alert rule appears in the Azure Monitor Alert rules list.

<img width="1089" height="566" alt="Fig06_Service_Health_Alert_Rule_Enabled" src="https://github.com/user-attachments/assets/b6754e3a-707f-4e76-a266-25d19cf82cbf" />


*Figure 6: The `ar-gp-service-health` alert rule appears with Service health as its signal type and Enabled status.*

#### Evidence analysis

The Alert rules table directly shows `ar-gp-service-health`. The visible columns show severity 4, subscription target scope, Service health signal type, and an Enabled status. This is final-state evidence that the alert rule existed and was enabled at the time of capture.

---

### 10.7 Alert Rule Cleanup Verification

A later view of the Alert rules page shows no alert rules found.

<img width="1095" height="569" alt="Fig07_Alert_Rule_Cleanup_Verification" src="https://github.com/user-attachments/assets/e6c4304f-5b5f-414a-8d18-5507b6585bbe" />


*Figure 7: Alert rules page showing no alert rules under the displayed subscription and filter state.*

#### Evidence analysis

The page displays **No alert rules found**. This is consistent with cleanup verification after deletion, but the screenshot does not directly display a deletion confirmation. The result could also be affected by the subscription or active filters shown on the page. The most precise claim is that no matching alert rules were visible under the displayed page state.

---

## 11. Results and Validation

| Task | Evidence | Validation Assessment |
|---|---|---|
| Resource-group configuration | Figure 1 | Name and East US region entered |
| Resource group available | Figure 2 | Resource group visible in Azure Resource Manager |
| Email notification configured | Figure 3 | Email channel and notification name visible |
| Action group prepared for testing | Figure 4 | Service Health sample and email notification selected |
| Service Health alert configured | Figure 5 | Rule name, scope settings, and existing action-group option visible |
| Alert rule enabled | Figure 6 | Rule listed with Enabled status |
| No matching rules after cleanup | Figure 7 | Alert rules page shows no results under displayed state |

---

## 12. Security and Privacy Notes

- Redact the personal email address visible in Figures 3 and 4 before publishing the project publicly.
- Review screenshots for subscription identifiers, tenant labels, and account names.
- Do not include lab passwords, Temporary Access Pass tokens, access keys, or other credentials.
- Use approved organizational notification recipients in production.
- Validate an action group before relying on it for operational incident response.
- Use appropriate access control when creating or deleting monitoring resources.

---

## 13. Limitations and Next Steps

### Current limitations

- The action-group screenshots show test preparation, not a completed test-result confirmation.
- No received email notification was included as evidence.
- The final screenshot shows no matching alert rules but does not display the deletion operation itself.
- Personal information remains visible in two screenshots and requires redaction.

### Recommended next steps

1. Capture the completed action-group test result.
2. Capture the received test-notification email with private information redacted.
3. Capture the alert-rule deletion confirmation.
4. Redact personal and tenant-specific information before publishing.
5. Store the evidence in a dedicated `screenshots` folder and update the relative paths.

---

## 14. Conclusion

The project demonstrates a functional Azure monitoring workflow built around a resource group, an action group, email notification settings, action-group testing, and a Service Health alert rule. The strongest completion evidence is the Alert rules view showing `ar-gp-service-health` with an Enabled status.

The screenshots are now ordered and matched to the monitoring tasks they visibly support. They should not be attached to the earlier Cost Governance report because they document a different Azure project.

---

## 15. Disclaimer

This report documents an educational lab performed in a temporary Microsoft Azure Skillable environment. The settings and names are lab-specific and should be reviewed before reuse in another subscription or production environment.

The screenshots may contain account, subscription, tenant, or email information. Redact sensitive or personally identifying information before publishing the repository. This document is an independent educational portfolio report and is not official Microsoft documentation.

---

## 16. Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11  
Cloud Security Engineering

<div align="center">

**Report completed on September 30, 2026**

*Building observable and responsibly managed cloud environments through practical implementation.*

</div>
