# Azure Static Website Hosting

> Deployment, validation, update, and resource cleanup of a static website hosted using Microsoft Azure Storage.

## Project Information

| Field | Details |
|---|---|
| **Author** | Wadondera A. Collins |
| **Programme** | ICDFA Trainee, Cohort 11 |
| **Specialization** | Cloud Security Engineering |
| **Project** | Azure Static Website Hosting |
| **Project Status** | Completed |
| **Environment** | Microsoft Azure educational lab |

---

## 1. Project Overview

This project demonstrates the complete lifecycle of deploying a static website through Microsoft Azure Storage. It covers cloud resource provisioning, storage account configuration, static website hosting, HTML file deployment, endpoint testing, website updating, blob property verification, and resource cleanup.

The solution used an Azure Storage Account to host an `index.html` landing page and a custom `404.html` error page in the automatically created `$web` container. The website was initially validated as Version 1 and later updated to display **Version 2 - Landing Page**.

---

## 2. Executive Summary

The project was completed successfully using Microsoft Azure Portal and Azure Blob Storage. A resource group and storage account were created, after which static website hosting was enabled with `index.html` configured as the index document and `404.html` configured as the custom error document.

Both files were uploaded to the `$web` container and tested through the generated public website endpoint. The main endpoint loaded the landing page, while a nonexistent route displayed the custom 404 page. The landing page was subsequently updated from Version 1 to Version 2 and validated through the public endpoint.

The blob properties were reviewed, confirming a `text/html` content type and the Hot access tier. After validation, the resource group was deleted to complete the cloud resource lifecycle and prevent unused lab resources from remaining active.

---

## 3. Objectives

- Create and configure an Azure resource group.
- Create an Azure Storage Account using Standard performance and locally redundant storage.
- Enable static website hosting in Azure Storage.
- Configure `index.html` as the index document.
- Configure `404.html` as the custom error document.
- Upload website files to the `$web` container.
- Validate the public static website endpoint.
- Test custom error page behavior using an invalid route.
- Update the deployed landing page from Version 1 to Version 2.
- Verify the content type and access tier of the uploaded blobs.
- Remove the Azure resources after completing the lab.

---

## 4. Professional Value

This project provides practical evidence of the ability to work with cloud-hosted web content and manage the lifecycle of Azure resources. It demonstrates experience in provisioning, configuring, validating, updating, and removing cloud infrastructure in a controlled lab environment.

From a professional perspective, the project shows:

- An understanding of Azure resource organization.
- Practical familiarity with Azure Storage services.
- Awareness of website availability and error handling.
- Attention to storage configuration and blob properties.
- Recognition of cloud security responsibilities.
- Awareness of cost control through resource cleanup.
- The ability to document technical work in a structured and verifiable format.

---

## 5. Skills Demonstrated

### Cloud Resource Management

- Created and managed an Azure resource group.
- Provisioned and configured an Azure Storage Account.
- Selected Standard performance and locally redundant storage.
- Removed cloud resources after completing validation.

### Azure Storage Administration

- Enabled static website hosting.
- Worked with the `$web` storage container.
- Uploaded and replaced HTML blob files.
- Reviewed blob content type and access tier properties.

### Static Website Deployment

- Published an HTML landing page.
- Configured a custom HTML error page.
- Validated the website through its public endpoint.
- Updated deployed website content and confirmed the change.

### Testing and Validation

- Tested the default index document.
- Tested custom 404 behavior using a nonexistent route.
- Verified that updated content was publicly available.
- Confirmed that the endpoint stopped resolving after resource cleanup.

### Security and Cost Awareness

- Avoided documenting credentials, access keys, connection strings, or tokens.
- Recognized the importance of least privilege access.
- Removed unused lab resources to reduce the risk of unintended charges.
- Distinguished an educational deployment from a production-ready architecture.

---

## 6. Technologies and Tools Used

| Technology or Tool | Purpose |
|---|---|
| **Microsoft Azure Portal** | Creation, configuration, management, and deletion of Azure resources |
| **Azure Resource Group** | Logical organization of project resources |
| **Azure Storage Account** | Hosting environment for the static website |
| **Azure Blob Storage** | Storage of the website files |
| **Azure Static Website Hosting** | Publication of the HTML website through a public endpoint |
| **HTML5** | Creation of the landing page and custom error page |
| **Web Browser** | Testing the website endpoint and error page behavior |
| **Local Text Editor** | Creation and modification of the HTML files |

> Tool and software versions not provided in the source report have not been estimated or invented.

---

## 7. Lab Environment

| Resource or Setting | Configuration |
|---|---|
| **Resource Group** | `rg-gp-static-website` |
| **Storage Account** | `stgpstaticsite65475541` |
| **Performance Tier** | Standard |
| **Redundancy** | Locally redundant storage, LRS |
| **Static Website Hosting** | Enabled |
| **Website Container** | `$web` |
| **Index Document** | `index.html` |
| **Error Document** | `404.html` |
| **Blob Access Tier** | Hot |
| **Content Type** | `text/html` |
| **Project Status** | Completed and cleaned up |

---

## 8. Repository Structure

```text
azure-static-website-hosting/
├── README.md
├── index.html
├── 404.html
├── screenshots/
│   ├── Fig01 resource-group-created.png
│   ├── Fig02 storage-account-created.png
│   ├── Fig03 static-website-enabled.png
│   ├── Fig04 web-container-files.png
│   ├── Fig05 version-one-landing-page.png
│   ├── Fig06 custom-404-page.png
│   ├── Fig07 version-two-landing-page.png
│   ├── Fig08 index-blob-properties.png
│   ├── Fig09 error-blob-properties.png
│   └── Fig10 resource-cleanup-confirmation.png
└── docs/
    └── Azure_Static_Website_Hosting_Report.docx
```

> Rename each screenshot according to the evidence it contains and preserve the sequential naming format from `Fig01` to `Fig10`.

---

## 9. Methodology

### Step 1: Provision the Azure Resource Group

The project began by creating the `rg-gp-static-website` resource group. This provided a logical container for the storage resources used during the lab.

**Screenshot:** `Fig01 resource-group-created.png`

```markdown
"C:\Users\wadon\OneDrive\Pictures\Screenshots\linux-week2\Fig01 resource-group-created.png"
```

### Step 2: Create the Storage Account

The storage account `stgpstaticsite65475541` was created using Standard performance and locally redundant storage.

**Screenshot:** `Fig02 storage-account-created.png`

```markdown
![Fig02 Storage account created](screenshots/Fig02%20storage-account-created.png)
```

### Step 3: Enable Static Website Hosting

Static website hosting was enabled on the storage account. The index document was configured as `index.html`, while the error document was configured as `404.html`.

**Screenshot:** `Fig03 static-website-enabled.png`

```markdown
![Fig03 Static website enabled](screenshots/Fig03%20static-website-enabled.png)
```

### Step 4: Upload Website Files

The `index.html` and `404.html` files were uploaded to the `$web` container created for static website content.

**Screenshot:** `Fig04 web-container-files.png`

```markdown
![Fig04 Web container files](screenshots/Fig04%20web-container-files.png)
```

### Step 5: Validate the Version 1 Landing Page

The public static website endpoint was opened in a browser to confirm that the original landing page loaded correctly.

**Screenshot:** `Fig05 version-one-landing-page.png`

```markdown
![Fig05 Version one landing page](screenshots/Fig05%20version-one-landing-page.png)
```

### Step 6: Validate the Custom 404 Page

A nonexistent website path was entered to test error handling. The configured custom 404 page was displayed successfully.

**Screenshot:** `Fig06 custom-404-page.png`

```markdown
![Fig06 Custom 404 page](screenshots/Fig06%20custom-404-page.png)
```

### Step 7: Update the Website

The `index.html` file was revised from Version 1 to Version 2 and uploaded with overwrite enabled. After refreshing the public endpoint, the website displayed **Version 2 - Landing Page**.

**Screenshot:** `Fig07 version-two-landing-page.png`

```markdown
![Fig07 Version two landing page](screenshots/Fig07%20version-two-landing-page.png)
```

### Step 8: Review the Index Blob Properties

The properties of `index.html` were reviewed. The content type was `text/html` and the access tier was Hot.

**Screenshot:** `Fig08 index-blob-properties.png`

```markdown
![Fig08 Index blob properties](screenshots/Fig08%20index-blob-properties.png)
```

### Step 9: Review the Error Blob Properties

The properties of `404.html` were reviewed. The content type was `text/html` and the access tier was Hot.

**Screenshot:** `Fig09 error-blob-properties.png`

```markdown
![Fig09 Error blob properties](screenshots/Fig09%20error-blob-properties.png)
```

### Step 10: Remove the Lab Resources

After completing the required validation, the `rg-gp-static-website` resource group was deleted. The cleanup check confirmed that the resource group was no longer available and that the saved endpoint no longer resolved.

**Screenshot:** `Fig10 resource-cleanup-confirmation.png`

```markdown
![Fig10 Resource cleanup confirmation](screenshots/Fig10%20resource-cleanup-confirmation.png)
```

---

## 10. Evidence and Analysis

| Evidence | Validation Performed | Analysis |
|---|---|---|
| `Fig01 resource-group-created.png` | Resource group creation | Demonstrates the logical organization of Azure project resources |
| `Fig02 storage-account-created.png` | Storage account provisioning | Confirms that the hosting resource was created with the selected configuration |
| `Fig03 static-website-enabled.png` | Static website configuration | Confirms that the index and error documents were assigned |
| `Fig04 web-container-files.png` | File upload | Confirms the presence of `index.html` and `404.html` in the `$web` container |
| `Fig05 version-one-landing-page.png` | Initial endpoint test | Demonstrates that the original landing page was publicly accessible |
| `Fig06 custom-404-page.png` | Invalid route test | Confirms that the custom error document handled nonexistent paths |
| `Fig07 version-two-landing-page.png` | Website update test | Demonstrates successful replacement and publication of the revised index file |
| `Fig08 index-blob-properties.png` | Index blob inspection | Provides evidence of the configured content type and access tier |
| `Fig09 error-blob-properties.png` | Error blob inspection | Provides evidence of the configured content type and access tier |
| `Fig10 resource-cleanup-confirmation.png` | Resource deletion | Demonstrates responsible cleanup of the educational lab environment |

The documented results confirm that static website hosting was enabled, the required HTML files were stored in the `$web` container, the main endpoint and custom error page operated correctly, Version 2 was published successfully, and the resources were removed after validation.

---

## 11. Key Results

- Azure static website hosting was enabled successfully.
- The `$web` container contained `index.html` and `404.html`.
- The public endpoint displayed the landing page.
- Invalid routes displayed the custom 404 page.
- The updated endpoint displayed **Version 2 - Landing Page**.
- Both HTML blobs used the `text/html` content type.
- Both HTML blobs used the Hot access tier.
- The project resources were deleted after completion.

---

## 12. Security and Cost Considerations

- Credentials, access keys, connection strings, and tokens must not be committed to a public GitHub repository.
- Least privilege access should be used when managing Azure resources.
- Sensitive Azure account information should be removed or obscured in screenshots before publication.
- Unused lab resources should be deleted to reduce the risk of unintended charges.
- A production deployment would require further review of monitoring, logging, HTTPS, custom domains, and applicable organizational security requirements.

---

## 13. Limitations and Next Steps

This project demonstrates a basic educational implementation and is not presented as a production-ready architecture. The source report does not specify the local operating system, browser version, text editor version, or Azure service/API version.

Potential future improvements include:

- Connecting a custom domain.
- Reviewing HTTPS and secure content delivery requirements.
- Introducing deployment automation through a controlled CI/CD workflow.
- Adding monitoring and logging.
- Applying formal access control and least privilege policies.
- Expanding the website with CSS and JavaScript.
- Documenting a production-focused security review.

> The items above are recommended future enhancements and were not represented as completed project activities.

---

## 14. Conclusion

This project demonstrated the full lifecycle of deploying a static website through Azure Storage. It included cloud resource provisioning, static website configuration, HTML content publication, endpoint validation, custom error page testing, content updating, blob property inspection, and resource cleanup.

The successful display of the Version 2 landing page and the custom 404 page confirmed that the website configuration operated as intended. The final deletion of the lab resources also demonstrated responsible cloud resource and cost management.

---

## 15. Disclaimer

This project is provided for educational and portfolio demonstration purposes only. The documented configuration is not a production-ready architecture and does not replace official Microsoft Azure documentation, organizational policies, or professional cloud security guidance.

Azure credentials, access keys, tokens, connection strings, subscription identifiers, and other sensitive information must not be published in this repository. Screenshots should be reviewed and redacted before being committed publicly.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
