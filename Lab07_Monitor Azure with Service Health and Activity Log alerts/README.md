<div align="center">

# Azure Monitoring and Alerting

### Service Health Alerts, Activity Log Alerts, and Reusable Email Notifications

**Author:** Wadondera A. Collins  
**Role:** ICDFA Trainee | Cohort 11 | Cloud Security Engineering  
**Platform:** Microsoft Azure | Skillable Lab Environment  
**Completion Date:** September 30, 2026  
**Project Status:** Completed

</div>

---

## Table of Contents

- [Project Overview](#project-overview)
- [Executive Summary](#executive-summary)
- [Project Objectives](#project-objectives)
- [Professional Value](#professional-value)
- [Skills Demonstrated](#skills-demonstrated)
- [Tools and Azure Services](#tools-and-azure-services)
- [Lab Environment](#lab-environment)
- [Repository Structure](#repository-structure)
- [Implementation Methodology](#implementation-methodology)
  - [Exercise 1: Create and Test an Action Group](#exercise-1-create-and-test-an-action-group)
  - [Exercise 2: Create a Service Health Alert](#exercise-2-create-a-service-health-alert)
  - [Exercise 3: Create an Activity Log Alert](#exercise-3-create-an-activity-log-alert)
  - [Clean-Up and Verification](#clean-up-and-verification)
- [Evidence and Analysis](#evidence-and-analysis)
- [Project Results](#project-results)
- [Validation Checklist](#validation-checklist)
- [Limitations and Next Steps](#limitations-and-next-steps)
- [Security and Operational Notes](#security-and-operational-notes)
- [Conclusion](#conclusion)
- [Disclaimer](#disclaimer)
- [Author](#author)

---

## Project Overview

This completed project demonstrates the implementation of a practical monitoring and notification baseline in Microsoft Azure. The solution combines an Azure Monitor action group, an Azure Service Health alert, and an Activity Log alert to improve awareness of platform events and important administrative changes.

A reusable email notification channel was created and tested before being attached to two alert rules. The first rule monitored Azure service issues and planned maintenance. The second monitored resource-group deletion activity. Both rules were enabled, reviewed, and validated before the project resources were removed.

---

## Executive Summary

Reliable cloud operations depend on timely visibility into service disruptions, planned maintenance, and high-impact administrative actions. In this project, I created a reusable Azure email notification path and connected it to two monitoring scenarios.

The completed solution included:

1. An action group named `ag-gp-ops-email` for reusable email notifications.
2. A Service Health alert named `ar-gp-service-health` for service issues and planned maintenance.
3. An Activity Log alert named `ar-gp-activity-delete` for resource-group deletion events.
4. A dedicated resource group named `rg-gp-monitoring-alerts`.
5. Validation of notification delivery, alert conditions, action-group associations, severity, and enabled state.
6. Complete resource cleanup and post-deletion verification.

This project demonstrates practical Azure monitoring, incident-awareness, cloud administration, and security-conscious documentation skills.

---

## Project Objectives

- Create a dedicated resource group for monitoring resources.
- Configure a reusable action group with email notification delivery.
- Test the action group before attaching it to operational alert rules.
- Review Azure Service Health information.
- Create a Service Health alert for service issues and planned maintenance.
- Create an Activity Log alert for resource-group deletion events.
- Reuse one action group across multiple alert rules.
- Validate each alert rule's condition, action, severity, and enabled state.
- Remove all monitoring resources after completing the lab.
- Verify that cleanup was successful.

---

## Professional Value

This project reflects responsibilities commonly associated with Azure administration, cloud operations, security operations, and Cloud Security Engineering.

It demonstrates the ability to:

- Build reusable notification workflows.
- Test notification channels before operational use.
- Monitor Azure platform incidents and maintenance events.
- Detect high-impact Azure management operations.
- Apply meaningful alert severity.
- Review monitoring configurations for accuracy.
- Protect credentials and personal information in technical documentation.
- Maintain cloud resource hygiene through verified cleanup.

---

## Skills Demonstrated

- Azure Monitor administration
- Azure resource-group management
- Action group creation and testing
- Email notification configuration
- Azure Service Health review
- Service Health alert creation
- Activity Log signal selection
- Alert scope configuration
- Alert severity classification
- Alert-rule validation
- Operational monitoring design
- Resource cleanup and verification
- Professional GitHub documentation

---

## Tools and Azure Services

| Tool or Service | Purpose |
|---|---|
| Microsoft Azure Portal | Configured and validated the monitoring solution |
| Azure Monitor | Managed alerts, alert rules, and action groups |
| Azure Action Groups | Provided a reusable email notification channel |
| Azure Service Health | Supplied service issue and planned maintenance events |
| Azure Activity Log | Supplied Azure management-operation events |
| Azure Alert Rules | Evaluated conditions and triggered notifications |
| Azure Resource Groups | Organized the monitoring resources |
| Skillable Lab Environment | Provided the temporary guided Azure environment |

> Azure services are continuously managed cloud services. Fixed product versions were not shown in the lab instructions, so unsupported version numbers are not listed.

---

## Lab Environment

| Item | Configuration |
|---|---|
| Resource group | `rg-gp-monitoring-alerts` |
| Action group | `ag-gp-ops-email` |
| Display name | `OpsEmail` |
| Action group region | Global |
| Notification name | `ops-team-email` |
| Notification method | Email |
| Service Health alert | `ar-gp-service-health` |
| Service Health event types | Service issue and Planned maintenance |
| Activity Log alert | `ar-gp-activity-delete` |
| Activity Log signal | Delete resource group |
| Activity Log alert severity | `Sev 2 - Warning` |
| Alert state | Enabled upon creation |

> Lab passwords, Temporary Access Pass tokens, usernames, personal email addresses, subscription identifiers, and tenant details are intentionally excluded.

---

## Repository Structure

```text
azure-monitoring-alerts/
|
+-- README.md
+-- screenshots/
|   +-- Fig01 Monitoring Resource Group Created.png
|   +-- Fig02 Action Group Configuration.png
|   +-- Fig03 Action Group Test Success.png
|   +-- Fig04 Azure Test Email Notification.png
|   +-- Fig05 Service Health Review.png
|   +-- Fig06 Service Health Alert Created.png
|   +-- Fig07 Activity Log Delete Condition.png
|   +-- Fig08 Activity Log Alert Created.png
|   +-- Fig09 Alert Rules Validation.png
|   +-- Fig10 Alert Rule Details Reviewed.png
|   +-- Fig11 Monitoring Cleanup Verified.png
+-- LICENSE
```

Only include screenshots that are available and verified. Remove unused placeholders from the final repository.

---

## Implementation Methodology

### Exercise 1: Create and Test an Action Group

#### Task 1: Prepare the environment

1. Signed in to the Azure Portal using the temporary lab account.
2. Opened **Resource groups**.
3. Created `rg-gp-monitoring-alerts`.
4. Selected the preferred Azure region.
5. Identified an authorized email address for notifications.

**Validation:** The monitoring resource group was created successfully.

#### Task 2: Create the action group

1. Opened **Monitor** in the Azure Portal.
2. Selected **Alerts** and then **Action groups**.
3. Started the action-group creation workflow.
4. Selected `rg-gp-monitoring-alerts` as the resource group.
5. Selected **Global** as the region.
6. Entered `ag-gp-ops-email` as the action group name.
7. Entered `OpsEmail` as the display name.
8. Added an **Email/SMS message/Push/Voice** notification.
9. Named the notification `ops-team-email`.
10. Enabled email and entered the authorized notification address.
11. Reviewed and created the action group.

**Validation:** `ag-gp-ops-email` appeared in the action-group list with an email notification configured.

#### Task 3: Test the action group

1. Opened `ag-gp-ops-email`.
2. Selected **Test action group**.
3. Chose **Service Health** as the sample type.
4. Confirmed that `ops-team-email` was selected.
5. Started the test.
6. Confirmed that the test status displayed **Success**.
7. Verified receipt of the Azure test email.

**Validation:** The action-group test succeeded and the notification was received.

---

### Exercise 2: Create a Service Health Alert

#### Task 1: Review Service Health

The following Service Health areas were reviewed:

- **Service issues** for active incidents
- **Planned maintenance** for upcoming maintenance windows
- **Health advisories** for non-critical recommendations
- **Health history** for earlier incidents and resolution information

**Validation:** All four required Service Health areas were reviewed.

#### Task 2: Create the Service Health alert

1. Selected **Create service health alert**.
2. Selected the provided Azure subscription.
3. Retained all services as permitted by the lab.
4. Used the required Global region configuration.
5. Selected **Service issue** and **Planned maintenance**.
6. Attached `ag-gp-ops-email` on the **Actions** tab.
7. Selected `rg-gp-monitoring-alerts` on the **Details** tab.
8. Named the rule `ar-gp-service-health`.
9. Confirmed that the rule was enabled upon creation.
10. Created the alert rule.

**Validation:** `ar-gp-service-health` was created, enabled, and connected to the correct action group.

---

### Exercise 3: Create an Activity Log Alert

#### Task 1: Open alert-rule creation

1. Opened **Monitor**.
2. Selected **Alerts**.
3. Selected **Create** and then **Alert rule**.

#### Task 2: Configure the condition

1. Selected the alert scope.
2. Filtered by the **Resource groups** resource type.
3. Selected `rg-gp-monitoring-alerts`.
4. Opened the **Condition** tab.
5. Selected the **Delete resource group** Activity Log signal.
6. Selected `Sev 2 - Warning`.
7. Retained the remaining default signal settings.

**Validation:** The condition was configured to detect resource-group deletion events.

#### Task 3: Attach the action group and create the rule

1. Opened the **Actions** tab.
2. Selected `ag-gp-ops-email`.
3. Opened the **Details** tab.
4. Selected `rg-gp-monitoring-alerts`.
5. Named the rule `ar-gp-activity-delete`.
6. Confirmed `Sev 2 - Warning` as the severity.
7. Confirmed that the rule was enabled upon creation.
8. Reviewed and created the alert rule.
9. Confirmed that both alert rules appeared in Azure Monitor.

**Validation:** `ar-gp-service-health` and `ar-gp-activity-delete` appeared in the alert-rule list.

#### Task 4: Review the alert rules

The Service Health alert was reviewed to confirm that it:

- Monitored Service issue and Planned maintenance events.
- Used `ag-gp-ops-email`.
- Was enabled.

The Activity Log alert was reviewed to confirm that it:

- Monitored the Delete resource group signal.
- Used `ag-gp-ops-email`.
- Used `Sev 2 - Warning` severity.
- Was enabled.

**Validation:** Both alert rules showed the intended conditions and action-group association.

---

### Clean-Up and Verification

Cleanup was performed in dependency order.

#### Step 1: Delete the alert rules

- Deleted `ar-gp-activity-delete`.
- Deleted `ar-gp-service-health`.
- Confirmed both deletions.

#### Step 2: Delete the action group

- Deleted `ag-gp-ops-email`.
- Confirmed the deletion.

#### Step 3: Delete the resource group

- Deleted `rg-gp-monitoring-alerts`.
- Confirmed the resource-group name when prompted.
- Waited for the successful deletion notification.

#### Step 4: Verify cleanup

Confirmed that:

- `rg-gp-monitoring-alerts` no longer appeared in Resource groups.
- Neither alert rule appeared under **Monitor > Alerts > Alert rules**.
- `ag-gp-ops-email` no longer appeared under **Monitor > Alerts > Action groups**.

---

## Evidence and Analysis

Place each screenshot directly beneath the task it proves. Every filename, Markdown link, caption, and section placement must match the screenshot's visible content.

| Filename | Evidence Required | Analysis |
|---|---|---|
| `Fig01 Monitoring Resource Group Created.png` | `rg-gp-monitoring-alerts` visible after creation | Confirms preparation of the project resource container |
| `Fig02 Action Group Configuration.png` | Action group name, region, and notification configuration | Confirms creation of the reusable notification channel |
| `Fig03 Action Group Test Success.png` | Test result displaying Success | Confirms successful processing of the sample notification |
| `Fig04 Azure Test Email Notification.png` | Received Azure test notification with sensitive details redacted | Confirms end-to-end email delivery |
| `Fig05 Service Health Review.png` | Relevant Service Health interface or reviewed areas | Demonstrates awareness of Azure platform-health information |
| `Fig06 Service Health Alert Created.png` | Enabled `ar-gp-service-health` rule | Confirms creation of the platform-event alert |
| `Fig07 Activity Log Delete Condition.png` | Delete resource group signal and selected scope | Confirms the intended administrative event condition |
| `Fig08 Activity Log Alert Created.png` | Enabled `ar-gp-activity-delete` and severity | Confirms creation and classification of the deletion alert |
| `Fig09 Alert Rules Validation.png` | Both alert rules visible | Confirms both monitoring scenarios were configured |
| `Fig10 Alert Rule Details Reviewed.png` | Correct condition and action group | Confirms configuration review and validation |
| `Fig11 Monitoring Cleanup Verified.png` | Project resources no longer visible | Confirms successful cleanup |

Example image placement:

```markdown
![Fig03 Action Group Test Success](screenshots/Fig03%20Action%20Group%20Test%20Success.png)

*Figure 3: Azure Monitor displays a successful test for the configured action group.*
```

> Do not add a screenshot unless it clearly matches the assigned task. Redact usernames, email addresses, subscription IDs, tenant details, access tokens, and other sensitive information before publication.

---

## Project Results

The project achieved the intended monitoring outcomes:

- A dedicated monitoring resource group was created.
- A reusable email action group was configured and tested.
- The action-group test displayed a successful status.
- The Azure test email was received.
- A Service Health alert was configured for service incidents and planned maintenance.
- An Activity Log alert was configured for resource-group deletion events.
- Both alert rules used the same tested action group.
- The conditions, severity, action group, and enabled state were reviewed.
- All project resources were deleted and cleanup was verified.

---

## Validation Checklist

| Validation Item | Expected Result | Status |
|---|---|---|
| Resource group created | `rg-gp-monitoring-alerts` available | Completed |
| Action group created | `ag-gp-ops-email` available | Completed |
| Email notification configured | `ops-team-email` attached | Completed |
| Action group tested | Test status displayed Success | Completed |
| Test email received | Azure test notification received | Completed |
| Service Health reviewed | Four required areas reviewed | Completed |
| Service Health alert created | Rule created and enabled | Completed |
| Service Health events verified | Service issue and Planned maintenance selected | Completed |
| Activity Log scope configured | Project resource group selected | Completed |
| Deletion signal configured | Delete resource group selected | Completed |
| Activity Log alert created | Rule created and enabled | Completed |
| Severity verified | `Sev 2 - Warning` configured | Completed |
| Action-group association verified | Both rules used `ag-gp-ops-email` | Completed |
| Alert rules deleted | Neither rule remained | Completed |
| Action group deleted | Action group no longer appeared | Completed |
| Resource group deleted | Resource group no longer appeared | Completed |

---

## Limitations and Next Steps

This assignment implemented a focused monitoring baseline in a temporary training environment. Potential future enhancements include:

- Add multiple approved notification recipients.
- Define a documented alert-severity and escalation matrix.
- Monitor additional high-impact administrative events.
- Deploy action groups and alert rules through infrastructure as code.
- Apply standardized naming, tagging, and ownership controls.
- Connect alerts to an approved incident-management process.
- Test notification channels periodically.
- Document response procedures for each monitored event.
- Review alert coverage as the Azure environment changes.

These are recommended extensions and were not part of the completed guided-lab scope.

---

## Security and Operational Notes

- Authentication credentials and access tokens are excluded from this repository.
- The notification channel was tested before operational use.
- One reusable action group supported both alert rules.
- Alert scope and signal selection were validated.
- The deletion alert used an explicit warning severity.
- Both alert rules were enabled and reviewed.
- Temporary resources were removed after the lab.
- Screenshots must be checked and redacted before publication.

In a production environment, notification ownership, escalation paths, severity mappings, alert scope, naming conventions, and incident-response procedures should follow approved organizational standards.

---

## Conclusion

This completed project established a practical Azure monitoring baseline using a tested action group, a Service Health alert, and an Activity Log alert. The solution connected Azure platform and administrative events to a reusable email notification channel, improving awareness of service issues, planned maintenance, and resource-group deletion activity.

The project also reinforced essential cloud-operational practices: test notification delivery, validate alert scope and conditions, assign meaningful severity, protect sensitive information, and remove temporary resources after use.

---

## Disclaimer

This repository documents a completed educational assignment performed in a temporary Skillable Microsoft Azure environment. Resource names, alert rules, severity settings, regions, and notification settings were used for training and may require modification before use in another subscription or production environment.

No passwords, Temporary Access Pass tokens, usernames, email addresses, subscription identifiers, tenant details, or authentication secrets are included. Screenshots should be reviewed and redacted before publication.

Microsoft Azure and related product names are trademarks of Microsoft Corporation. This project is an independent educational portfolio entry and is not an official Microsoft deployment guide.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11  
Cloud Security Engineering  
Focus Areas: Microsoft Azure, Cloud Security, Monitoring, Governance, Identity, and DevOps

---

<div align="center">

**Completed on September 30, 2026**

*Building secure, observable, and resilient cloud environments through practical implementation.*

</div>
