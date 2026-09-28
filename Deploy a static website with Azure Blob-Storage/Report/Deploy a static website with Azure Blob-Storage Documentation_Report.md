<div align="center">  
    

# Azure Static Website Hosting

> Deployment, validation, update, and responsible cleanup of a static website hosted with Microsoft Azure Storage.

## Project Information

| Field | Details |
|---|---|
| **Author** | Wadondera A. Collins |
| **Programme** | ICDFA Trainee, Cohort 11 |
| **Specialization** | Cloud Security Engineering |
| **Project** | Azure Static Website Hosting |
| **Project Status** | Completed |
| **Environment** | Microsoft Azure educational lab |  

</div>


---

## 1. Project Overview

This project demonstrates the complete lifecycle of deploying a static website through Microsoft Azure Storage. It covers resource provisioning, storage account configuration, static website hosting, HTML file deployment, endpoint testing, website updating, blob property verification, and resource cleanup.

The solution used an Azure Storage Account to host an `index.html` landing page and a custom `404.html` error page in the automatically created `$web` container. The website was first validated as Version 1 and later updated to display **Version 2 - Landing Page**.

---

## 2. Executive Summary

The project was completed successfully through the Microsoft Azure portal and Azure Blob Storage. A resource group and storage account were created, after which static website hosting was enabled. The `index.html` file was configured as the index document, while `404.html` was configured as the custom error document.

Both files were uploaded to the `$web` container and tested through the generated public website endpoint. The primary endpoint displayed the landing page, while a nonexistent route displayed the custom 404 page. The landing page was then updated from Version 1 to Version 2 and validated through the public endpoint.

Blob properties were reviewed, confirming the `text/html` content type and Hot access tier. After validation, the resource group was deleted to complete the cloud resource lifecycle and prevent unused lab resources from remaining active.

---

## 3. Objectives

- Create and configure an Azure resource group.
- Provision an Azure Storage Account using Standard performance and locally redundant storage.
- Enable static website hosting in Azure Storage.
- Configure `index.html` as the index document.
- Configure `404.html` as the custom error document.
- Upload the website files to the `$web` container.
- Validate the public static website endpoint.
- Test custom error-page behavior using an invalid route.
- Update the deployed landing page from Version 1 to Version 2.
- Verify the content type and access tier of the uploaded blobs.
- Remove the Azure resources after completing the lab.
- Document the implementation with clear, sequential, and sanitized screenshot evidence.

---

## 4. Professional Value

This project provides practical evidence of the ability to deploy cloud-hosted web content and manage the lifecycle of Azure resources. It demonstrates experience in provisioning, configuring, validating, updating, documenting, and removing cloud infrastructure in a controlled lab environment.

From a professional perspective, the project demonstrates:

- Understanding of Azure resource organization.
- Practical familiarity with Azure Storage services.
- Awareness of website availability and error handling.
- Attention to storage configuration and blob properties.
- Recognition of cloud security responsibilities.
- Cost awareness through responsible resource cleanup.
- Ability to document technical work in a structured and verifiable format.

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

- Avoided documenting credentials, access keys, connection strings, and tokens.
- Recognized the importance of least-privilege access.
- Removed unused lab resources to reduce the risk of unintended charges.
- Distinguished an educational deployment from a production-ready architecture.

### Technical Documentation

- Organized evidence using sequential figure labels.
- Connected each screenshot to a specific implementation or validation step.
- Presented the work in a recruiter-friendly GitHub Markdown format.

---

## 6. Technologies and Tools Used

| Technology or Tool | Purpose |
|---|---|
| **Microsoft Azure Portal** | Creation, configuration, management, and deletion of Azure resources |
| **Azure Resource Group** | Logical organization of project resources |
| **Azure Storage Account** | Hosting environment for the static website |
| **Azure Blob Storage** | Storage of the website files |
| **Azure Static Website Hosting** | Publication of HTML content through a public endpoint |
| **HTML5** | Creation of the landing page and custom error page |
| **Web Browser** | Testing the website endpoint and error-page behavior |
| **Local Text Editor** | Creation and modification of the HTML files |
| **GitHub** | Repository hosting and project documentation |
| **Markdown** | Formatting of the project report and screenshot evidence |

> Tool and software versions not provided in the source material have not been estimated or invented.

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

> Place each screenshot inside the `screenshots` folder and preserve the sequential naming format from `Fig01` to `Fig10`.

---

## 9. Methodology

### Step 1: Provision the Azure Resource Group

The project began by creating the `rg-gp-static-website` resource group. This provided a logical container for the Azure resources used during the lab.

<img width="666" height="559" alt="Fig01 resource-group-created" src="https://github.com/user-attachments/assets/c8fe5fde-ce84-4150-b29a-9693578d1d69" />


*Fig01: Successful creation of the Azure resource group.*

### Step 2: Create the Storage Account

The storage account `stgpstaticsite65475541` was created using Standard performance and locally redundant storage.

<img width="1087" height="607" alt="Fig02 storage-account-created" src="https://github.com/user-attachments/assets/940a12c3-50b8-45c4-8632-abeb491dce00" />


*Fig02: Successful creation of the Azure Storage Account using the selected configuration.*

### Step 3: Enable Static Website Hosting

Static website hosting was enabled on the storage account. The index document was configured as `index.html`, while the custom error document was configured as `404.html`.

<img width="1086" height="375" alt="Fig03 static-website-enabled" src="https://github.com/user-attachments/assets/80bb5f9d-9ece-4f11-8e96-826dcb22a88c" />


*Fig03: Static website hosting enabled with the index and custom error documents configured.*

### Step 4: Upload the Website Files

The `index.html` and `404.html` files were uploaded to the automatically created `$web` container.

<img width="1091" height="354" alt="Fig04 web-container-files" src="https://github.com/user-attachments/assets/c6626ad2-00cd-4a2b-8b06-9dbe3254fd0c" />


*Fig04: The `index.html` and `404.html` files uploaded to the `$web` container.*

### Step 5: Validate the Version 1 Landing Page

The public static website endpoint was opened in a web browser to confirm that the original landing page loaded correctly.

<img width="1088" height="299" alt="Fig05 version-one-landing-page" src="https://github.com/user-attachments/assets/338b90a7-c120-4444-a8dd-6ace9228acf0" />


*Fig05: Successful validation of the Version 1 landing page through the public endpoint.*

### Step 6: Validate the Custom 404 Page

A nonexistent website path was entered to test error handling. The configured custom 404 page was displayed successfully.

<img width="1087" height="295" alt="Fig06 custom-404-page" src="https://github.com/user-attachments/assets/0e270ce9-4ec0-4d01-9a68-519d85b43a5a" />


*Fig06: Successful validation of the custom 404 page using a nonexistent route.*

### Step 7: Update the Website

The `index.html` file was revised from Version 1 to Version 2 and uploaded with overwrite enabled. After the public endpoint was refreshed, the website displayed **Version 2 - Landing Page**.

![Fig07 Version 2 landing page](screenshots/Fig07%20version-two-landing-page.png)

*Fig07: Successful publication and validation of the updated Version 2 landing page.*

### Step 8: Review the Index Blob Properties

The properties of `index.html` were reviewed. The file had a `text/html` content type and used the Hot access tier.

![Fig08 Index blob properties](screenshots/Fig08%20index-blob-properties.png)

*Fig08: Blob properties of `index.html`, including its content type and access tier.*

### Step 9: Review the Error Blob Properties

The properties of `404.html` were reviewed. The file had a `text/html` content type and used the Hot access tier.

![Fig09 Error blob properties](screenshots/Fig09%20error-blob-properties.png)

*Fig09: Blob properties of `404.html`, including its content type and access tier.*

### Step 10: Remove the Lab Resources

After completing the required validation, the `rg-gp-static-website` resource group was deleted. The cleanup check confirmed that the resource group was no longer available and that the saved website endpoint no longer resolved.

![Fig10 Resource cleanup confirmation](screenshots/Fig10%20resource-cleanup-confirmation.png)

*Fig10: Confirmation that the Azure lab resources were successfully removed.*

---

## 10. Evidence and Analysis

| Evidence | Validation Performed | Analysis |
|---|---|---|
| `Fig01 resource-group-created.png` | Resource group creation | Demonstrates the logical organization of Azure project resources |
| `Fig02 storage-account-created.png` | Storage account provisioning | Confirms that the hosting resource was created with the selected configuration |
| `Fig03 static-website-enabled.png` | Static website configuration | Confirms that the index and error documents were assigned |
| `Fig04 web-container-files.png` | File upload | Confirms the presence of `index.html` and `404.html` in the `$web` container |
| `Fig05 version-one-landing-page.png` | Initial endpoint test | Demonstrates that the original landing page was publicly accessible |
| `Fig06 custom-404-page.png` | Invalid-route test | Confirms that the custom error document handled nonexistent paths |
| `Fig07 version-two-landing-page.png` | Website update test | Demonstrates successful replacement and publication of the revised index file |
| `Fig08 index-blob-properties.png` | Index blob inspection | Provides evidence of the configured content type and access tier |
| `Fig09 error-blob-properties.png` | Error blob inspection | Provides evidence of the configured content type and access tier |
| `Fig10 resource-cleanup-confirmation.png` | Resource deletion | Demonstrates responsible cleanup of the educational lab environment |

The documented results confirm that static website hosting was enabled, the required HTML files were stored in the `$web` container, the primary endpoint and custom error page operated correctly, Version 2 was published successfully, and the resources were removed after validation.

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
- Least-privilege access should be used when managing Azure resources.
- Subscription identifiers, tenant information, email addresses, and other sensitive data should be obscured in screenshots before publication.
- Unused lab resources should be deleted to reduce the risk of unintended charges.
- A production deployment would require further review of monitoring, logging, HTTPS, custom domains, identity, authorization, and organizational security requirements.
- Repository history should be reviewed if sensitive material is committed accidentally, because deleting a file from the latest version alone may not remove it from earlier commits.

---

## 13. Limitations and Next Steps

This project demonstrates an educational implementation and is not presented as a production-ready architecture. The source material does not specify the local operating system, browser version, text editor version, or Azure service/API version.

Potential future improvements include:

- Connect a custom domain.
- Review HTTPS and secure content-delivery requirements.
- Introduce deployment automation through a controlled CI/CD workflow.
- Add monitoring and logging.
- Apply formal access-control and least-privilege policies.
- Expand the website with CSS and JavaScript.
- Add an architecture diagram to improve technical communication.
- Include a deployment checklist and rollback procedure.
- Evaluate Azure Static Web Apps when authentication, authorization, configurable headers, or managed GitHub-based CI/CD is required.

> The items above are recommended future enhancements and are not represented as completed project activities.

---

## 14. Screenshot Attachment Guide

To make the screenshots display correctly on GitHub:

1. Create a folder named `screenshots` in the repository root.
2. Rename the screenshots exactly as listed in the repository structure.
3. Upload all ten image files to the `screenshots` folder.
4. Keep `README.md` in the repository root.
5. Commit the README and screenshots to the same branch.
6. Verify every image in GitHub's rendered README view.
7. Match capitalization, spacing, and the `.png` extension exactly.
8. Do not place image Markdown inside triple-backtick code blocks.
9. Do not use a local path such as `C:\Users\...`.
10. Review and redact every screenshot before publishing the repository.

If a screenshot does not display, verify that its filename and path match the corresponding Markdown image reference exactly.

---

## 15. Conclusion

This project demonstrated the full lifecycle of deploying a static website through Azure Storage. It included cloud resource provisioning, static website configuration, HTML content publication, endpoint validation, custom error-page testing, content updating, blob property inspection, technical documentation, and resource cleanup.

The successful display of the Version 2 landing page and custom 404 page confirmed that the website configuration operated as intended. The final deletion of the lab resources also demonstrated responsible cloud-resource and cost management.

---

## 16. References

- [Microsoft Learn: Static website hosting in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website)
- [Microsoft Learn: Host a static website in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to)

---

## 17. Disclaimer

This project is provided for educational and portfolio-demonstration purposes only. The documented configuration is not a production-ready architecture and does not replace official Microsoft Azure documentation, organizational policies, or professional cloud-security guidance.

Azure credentials, access keys, tokens, connection strings, subscription identifiers, and other sensitive information must not be published in this repository. Screenshots should be reviewed and redacted before being committed publicly.

---

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11  
Cloud Security Engineering
