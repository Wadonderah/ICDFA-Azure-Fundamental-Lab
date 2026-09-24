# Azure Static Website Hosting

A completed hands-on project demonstrating how to host and update a static website using Azure Blob Storage.

## What I Completed

- Created an Azure resource group and storage account
- Enabled static website hosting
- Uploaded `index.html` and a custom `404.html` page to the `$web` container
- Verified the public website and error page
- Updated the landing page from Version 1 to Version 2
- Confirmed the blobs used the `text/html` content type and Hot access tier
- Deleted the resource group after completing the lab

## Tools and Environment

- Microsoft Azure Portal
- Azure Blob Storage
- HTML5
- Web browser
- Local text editor

> Exact portal, browser, editor, operating-system, and Azure service versions were not provided in the assignment.

## Azure Configuration

- **Resource group:** `rg-gp-static-website`
- **Storage account:** `stgpstaticsite65475541`
- **Performance:** Standard
- **Redundancy:** Locally-redundant storage (LRS)
- **Index document:** `index.html`
- **Error document:** `404.html`
- **Container:** `$web`

## Result

The final website successfully displayed **Version 2 - Landing Page**, and invalid paths returned the custom 404 page.

## Disclaimer

This project was completed for educational purposes. It is not a production-ready architecture. Azure features, pricing, and interfaces may change. Do not publish credentials, access keys, connection strings, or other sensitive information in a public repository.

## Author

**Wadondera A. Collins**  
ICDFA Trainee, Cohort 11 | Cloud Security Engineering
