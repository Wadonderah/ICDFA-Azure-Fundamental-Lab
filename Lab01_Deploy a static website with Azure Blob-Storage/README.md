<div align="center">

# 🌐 Azure Static Website Hosting: Complete Guide

### Mentor Pilot Program | Completed Assignment

**Completion Date:** September 30, 2026

[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Blob%20Storage-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![HTML5](https://img.shields.io/badge/HTML-5-E34F26?logo=html5&logoColor=white)](https://html.spec.whatwg.org/)
[![Status](https://img.shields.io/badge/Status-Completed-2EA44F)](#-completion-checklist)
[![Learning](https://img.shields.io/badge/Focus-Static%20Web%20Hosting-6F42C1)](#-skills-demonstrated)

*A hands-on Azure project covering storage provisioning, static website configuration, HTML publishing, custom error handling, content updates, validation, and responsible cleanup.*

</div>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Learning Objectives](#-learning-objectives)
- [Architecture and Resources](#-architecture-and-resources)
- [Prerequisites and Security](#-prerequisites-and-security)
- [Exercise 1: Create the Storage Account and Enable Hosting](#-exercise-1-create-the-storage-account-and-enable-hosting)
- [Exercise 2: Upload and Verify Website Content](#-exercise-2-upload-and-verify-website-content)
- [Exercise 3: Update and Inspect Website Content](#-exercise-3-update-and-inspect-website-content)
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

This repository documents the successful completion of the **Azure Static Website Hosting** guided project in the **Mentor Pilot Program**. The project demonstrated how to publish and maintain a static website with **Azure Blob Storage**, from initial resource provisioning through final validation and cleanup.

The project covered the following workflow:

1. Create an Azure resource group.
2. Provision a Standard Azure Storage account with LRS redundancy.
3. Enable static website hosting.
4. Configure `index.html` as the default document.
5. Configure `404.html` as the custom error document.
6. Upload both files to the `$web` container.
7. Validate the public website endpoint.
8. Test custom error-page behavior with an invalid path.
9. Update the landing page from Version 1 to Version 2.
10. Verify blob content types and access tiers.
11. Delete the resource group and confirm cleanup.

> [!NOTE]
> Mentor was available throughout the lab as an AI-powered assistant for navigating instructions and troubleshooting exercises.

---

## 🎯 Learning Objectives

By completing this project, I demonstrated the ability to:

- Create and manage an Azure resource group.
- Provision an Azure Storage account through the Azure portal.
- Configure Standard performance and locally-redundant storage.
- Enable static website hosting in Azure Storage.
- Configure default index and custom error documents.
- Upload and overwrite HTML blobs in the `$web` container.
- Validate a publicly accessible static website endpoint.
- Test and confirm custom 404-page behavior.
- Inspect blob metadata, content type, and access tier.
- Update deployed website content without rebuilding the hosting environment.
- Remove temporary Azure resources after successful validation.
- Document cloud work without exposing credentials or tenant-specific information.

---

## 🏗️ Architecture and Resources

```text
Local Workstation
├── index.html
└── 404.html
        │
        │ Upload through Azure portal
        ▼
Azure Subscription
└── Resource Group: rg-gp-static-website
    └── Storage Account: stgpstaticsite65475541
        ├── Performance: Standard
        ├── Redundancy: LRS
        ├── Static Website Hosting: Enabled
        └── Container: $web
            ├── index.html
            └── 404.html
                    │
                    ▼
           Public Website Endpoint
```

| Resource | Name or Setting | Purpose |
|---|---|---|
| Resource group | `rg-gp-static-website` | Logical container for project resources |
| Storage account | `stgpstaticsite65475541` | Hosts the static website and HTML blobs |
| Performance | `Standard` | Storage performance tier used by the lab |
| Redundancy | `Locally-redundant storage (LRS)` | Stores local redundant copies of the data |
| Website container | `$web` | Stores publicly served static website files |
| Index document | `index.html` | Default website landing page |
| Error document | `404.html` | Custom page for invalid paths |
| Blob content type | `text/html` | Identifies both uploaded files as HTML content |
| Blob access tier | `Hot` | Access tier confirmed during validation |

> [!NOTE]
> **Final state:** The resource group and all project resources were deleted after validation. The architecture above represents the deployed environment before cleanup.

> [!IMPORTANT]
> Azure Storage account names must be globally unique and use only lowercase letters and numbers. Replace the sample storage account name if it is unavailable in another subscription.

---

## 🔐 Prerequisites and Security

### Prerequisites

- Access to the [Azure portal](https://portal.azure.com/)
- An Azure subscription or authorized lab environment
- Permission to create and delete resource groups and storage accounts
- A local text editor for creating HTML files
- A modern web browser for endpoint validation
- Basic familiarity with HTML and Azure portal navigation

### Tools and Environment

| Tool or Service | Version | Purpose |
|---|---|---|
| Microsoft Azure portal | Not specified | Resource provisioning and configuration |
| Azure Storage account | Service/API version not specified | Static website hosting |
| Azure Blob Storage | Service/API version not specified | Storage for website files |
| HTML | HTML5 | Landing page and custom error page |
| Web browser | Not specified | Website and error-page validation |
| Local text editor | Not specified | HTML file creation and revision |
| Operating system | Not specified | Local working environment |

> [!NOTE]
> Exact portal, browser, editor, operating-system, and Azure service versions were not provided in the assignment. They are intentionally listed as not specified rather than estimated.

### Security Notice

Passwords, temporary access passes, storage access keys, connection strings, subscription identifiers, tenant details, and lab-specific sign-in information are intentionally **not included** in this README.

> [!CAUTION]
> Never commit credentials, access keys, shared access signatures, connection strings, or other secrets to GitHub. If a secret is exposed, revoke or rotate it immediately through the appropriate Azure or identity-management process.

Use only the authorized lab account, apply least-privilege access, and verify resource names carefully before deletion.

---

## 🛠️ Exercise 1: Create the Storage Account and Enable Hosting

### 1. Create the Resource Group

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for **Resource groups**.
3. Select **Create**.
4. Enter the following resource-group name:

```text
rg-gp-static-website
```

5. Select the assigned subscription and an approved region.
6. Select **Review + create**, then select **Create**.

**Validation:** The resource group `rg-gp-static-website` appeared in the Azure portal.

### 2. Create the Storage Account

1. Search for **Storage accounts** in the Azure portal.
2. Select **Create**.
3. Configure the account with the following values:

| Setting | Value |
|---|---|
| Resource group | `rg-gp-static-website` |
| Storage account name | `stgpstaticsite65475541` |
| Region | Same region as the resource group |
| Preferred storage type | Azure Blob Storage or Azure Data Lake Storage |
| Performance | Standard |
| Redundancy | Locally-redundant storage (LRS) |

4. Select **Review + create**.
5. After validation passes, select **Create**.
6. When deployment completes, select **Go to resource**.

**Validation:** The storage account deployed successfully with Standard performance and LRS redundancy.

### 3. Enable Static Website Hosting

1. In the storage account menu, under **Data management**, select **Static website**.
2. Set **Static website** to **Enabled**.
3. Enter the following document names:

```text
Index document name: index.html
Error document path: 404.html
```

4. Select **Save**.
5. Record the generated primary endpoint for temporary validation use.

**Validation:** Static website hosting showed **Enabled**, a primary endpoint was generated, and the `$web` container was created.

> [!TIP]
> Keep endpoint details out of public documentation when the assignment does not require them. Document the validation result instead.

---

## 📤 Exercise 2: Upload and Verify Website Content

### 1. Create the Version 1 Landing Page

Create a local file named `index.html` with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Landing Page</title>
</head>
<body>
  <h1>Version 1 - Landing Page</h1>
  <p>Welcome to our product page. This is the initial published version.</p>
</body>
</html>
```

**Validation:** The file was saved locally as `index.html`.

### 2. Upload the Landing Page

1. In the storage account, under **Data storage**, select **Containers**.
2. Open the `$web` container.
3. Select **Upload**.
4. Browse to and select `index.html`.
5. Complete the upload.

**Validation:** `index.html` appeared in the `$web` container.

### 3. Create and Upload the Custom Error Page

Create a local file named `404.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Not Found</title>
</head>
<body>
  <h1>404 - Page Not Found</h1>
  <p>The page you requested does not exist. Return to the <a href="/">home page</a>.</p>
</body>
</html>
```

Upload `404.html` to the `$web` container using the same portal upload process.

**Validation:** The `$web` container listed both `index.html` and `404.html`.

### 4. Verify the Live Website

1. Return to the storage account's **Static website** page.
2. Open the primary endpoint in a web browser.
3. Confirm that the page displays:

```text
Version 1 - Landing Page
```

**Validation:** The public endpoint loaded the Version 1 landing page successfully.

### 5. Verify the Custom Error Page

Append a nonexistent path to the primary endpoint, such as:

```text
/fakepage
```

Confirm that the browser displays:

```text
404 - Page Not Found
```

Select the home-page link and verify that it returns to the landing page.

**Validation:** An invalid path displayed the custom 404 page, and the home-page link returned to the website root.

---

## 🔄 Exercise 3: Update and Inspect Website Content

### 1. Update the Landing Page to Version 2

Replace the local `index.html` content with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Landing Page</title>
</head>
<body>
  <h1>Version 2 - Landing Page</h1>
  <p>Welcome to our updated product page with the latest information.</p>
</body>
</html>
```

**Validation:** The revised file was saved as `index.html`, replacing the local Version 1 file.

### 2. Upload and Overwrite the Existing Blob

1. Open the `$web` container.
2. Select **Upload**.
3. Select the updated `index.html`.
4. Enable **Overwrite if files already exist**.
5. Complete the upload.

**Validation:** The existing `index.html` blob was replaced successfully.

### 3. Verify the Updated Website

Refresh the static website endpoint in the browser. If necessary, perform a hard refresh to bypass cached content.

Confirm that the page displays:

```text
Version 2 - Landing Page
```

**Validation:** The live website displayed the Version 2 heading and updated message.

### 4. Review Blob Properties

Inspect both `index.html` and `404.html` in the `$web` container.

Confirm the following properties:

| Property | Expected Value |
|---|---|
| Content type | `text/html` |
| Access tier | `Hot` |

Review the raw content of `index.html` and confirm that it matches the Version 2 HTML.

**Validation:** Both blobs used the `text/html` content type and Hot access tier, and `index.html` contained the Version 2 source.

### 5. Delete the Resource Group

1. Search for **Resource groups** in the Azure portal.
2. Open `rg-gp-static-website`.
3. Select **Delete resource group**.
4. Enter the resource-group name when prompted.
5. Confirm the deletion.
6. Wait for the deletion notification.

Verify that `rg-gp-static-website` no longer appears in the resource-group list. Confirm that the saved static website endpoint no longer resolves after cleanup completes.

**Validation:** The resource group and all contained project resources were removed successfully.

> [!WARNING]
> Resource-group deletion is permanent and removes every resource inside the group. Always verify the selected resource group before confirming deletion.

---

## ✅ Validation Results

| Check | Result |
|---|---|
| Resource group created | ✅ Passed |
| Storage account deployed | ✅ Passed |
| Standard performance configured | ✅ Passed |
| LRS redundancy configured | ✅ Passed |
| Static website hosting enabled | ✅ Passed |
| Primary endpoint generated | ✅ Passed |
| `$web` container created | ✅ Passed |
| `index.html` uploaded | ✅ Passed |
| `404.html` uploaded | ✅ Passed |
| Version 1 landing page displayed | ✅ Passed |
| Custom 404 page displayed | ✅ Passed |
| Home-page link returned to the site root | ✅ Passed |
| `index.html` updated with overwrite enabled | ✅ Passed |
| Version 2 landing page displayed | ✅ Passed |
| `text/html` content type confirmed | ✅ Passed |
| Hot access tier confirmed | ✅ Passed |
| Resource group deleted | ✅ Passed |
| Final cleanup verified | ✅ Passed |

---

## 📚 Command Reference

This project was completed through the Azure portal. The following table provides a concise portal-navigation reference rather than introducing unverified CLI steps.

| Goal | Azure Portal Path |
|---|---|
| Create a resource group | **Resource groups** → **Create** |
| Create a storage account | **Storage accounts** → **Create** |
| Enable static website hosting | Storage account → **Data management** → **Static website** |
| Open the website container | Storage account → **Data storage** → **Containers** → `$web` |
| Upload an HTML file | `$web` container → **Upload** |
| Overwrite `index.html` | `$web` container → **Upload** → **Overwrite if files already exist** |
| Inspect blob properties | `$web` container → Select blob → **Overview** |
| Delete the project | Resource group → **Delete resource group** |

### Project File Reference

```text
.
├── index.html
├── 404.html
└── README.md
```

---

## 🧰 Troubleshooting

### Storage account name is unavailable

Azure Storage account names must be globally unique. Choose a different lowercase alphanumeric suffix and retry the deployment.

### The `$web` container is missing

Confirm that static website hosting is enabled and that the configuration was saved. Azure creates the `$web` container when the static website feature is enabled.

### The landing page does not load

Confirm that:

- The file is named exactly `index.html`.
- `index.html` is in the `$web` container.
- The index document setting uses the same spelling and capitalization.
- The primary endpoint, rather than a blob-management URL, is being opened.

### The custom error page does not appear

Confirm that:

- The error document path is set to `404.html`.
- `404.html` exists in the `$web` container.
- The filename and configured path use matching capitalization.
- The test URL contains a path that does not exist.

### Version 1 still appears after the update

- Refresh the page.
- Perform a hard refresh or open a private browsing window.
- Confirm that overwrite was enabled during upload.
- Open the blob's edit view and verify that it contains the Version 2 source.

### The browser downloads the HTML file

Inspect the blob properties and confirm that the content type is:

```text
text/html
```

### The website endpoint still works after deletion

Resource-group deletion can take time to complete. Confirm that the resource group no longer appears in the portal, then test the endpoint again after the deletion operation finishes.

### A path returns an unexpected 404 response

Azure static website filenames and URL paths are case-sensitive. Confirm that the requested path matches the stored filename exactly.

---

## 🧠 Skills Demonstrated

- Microsoft Azure fundamentals
- Azure portal navigation
- Azure resource-group management
- Azure Storage account provisioning
- Locally-redundant storage configuration
- Azure Blob Storage management
- Static website hosting configuration
- HTML5 document creation
- `$web` container content management
- Blob upload and overwrite operations
- Custom 404-page configuration
- Public endpoint validation
- Blob property inspection
- Browser-based troubleshooting
- Secure handling of cloud credentials
- Cost-aware Azure resource cleanup

---

## 💡 Key Takeaways

1. **Azure Storage can host static content directly.** HTML files can be delivered through the storage account's public static website endpoint.
2. **The `$web` container is central to deployment.** Website files must be uploaded there to be served by the static website feature.
3. **Exact filenames matter.** Index, error-page, and URL path names must match the configured values and capitalization.
4. **Content type affects browser behavior.** HTML files should use `text/html` so browsers render them correctly.
5. **Website updates can be simple.** Replacing `index.html` with overwrite enabled publishes revised content without recreating the hosting environment.
6. **Validation should cover normal and error paths.** A complete test checks the landing page, invalid routes, links, and blob properties.
7. **Cleanup is part of responsible cloud practice.** Temporary resources should be removed and deletion should be verified.
8. **Secrets do not belong in source control.** Public documentation should describe the process without exposing credentials or tenant-specific identifiers.

---

## ☑️ Completion Checklist

- [x] Signed in to the authorized Azure environment
- [x] Created `rg-gp-static-website`
- [x] Created `stgpstaticsite65475541`
- [x] Configured Standard performance
- [x] Configured locally-redundant storage
- [x] Enabled static website hosting
- [x] Configured `index.html` as the index document
- [x] Configured `404.html` as the error document
- [x] Uploaded both files to the `$web` container
- [x] Verified the Version 1 landing page
- [x] Verified the custom 404 page
- [x] Confirmed the home-page link worked
- [x] Updated `index.html` to Version 2
- [x] Uploaded the revised file with overwrite enabled
- [x] Verified the Version 2 landing page
- [x] Confirmed `text/html` for both blobs
- [x] Confirmed the Hot access tier
- [x] Deleted the resource group
- [x] Confirmed cleanup

---

## 👤 Author

**Wadondera A. Collins**  
ICDFA Trainee | Cohort 11 | Cloud Security Engineering

This project forms part of my practical cloud-security and Azure-administration portfolio, demonstrating static content deployment, storage configuration, validation, troubleshooting, and responsible resource cleanup.

---

## 🙏 Acknowledgements

This guided project was completed as part of the **Mentor Pilot Program**. Mentor supported the learning experience by helping with lab navigation, instruction comprehension, and troubleshooting.

Official reference material: [Static website hosting in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website) and [Host a static website in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to).

---

## ⚖️ Disclaimer

This repository is an educational record of a completed guided project. It is not a production-ready architecture and does not replace official Microsoft documentation, organizational security policies, or professional cloud architecture guidance. Azure services, interfaces, pricing, limits, and features may change over time. Resource names and configuration values shown here are lab-specific examples and should be reviewed before reuse.

Passwords, access keys, connection strings, shared access signatures, subscription identifiers, tenant information, and other secrets are intentionally excluded. The documented environment used anonymous public read access for static website content. Production scenarios may require additional review for authentication, authorization, network controls, custom domains, certificates, monitoring, logging, availability, and content delivery. Always validate current requirements before deploying a public workload.

---

<div align="center">

### 🎉 Project Completed Successfully

**Azure static website hosting: configured, published, updated, validated, and responsibly removed.**

Made with curiosity, care, and a commitment to responsible cloud engineering.

</div>
