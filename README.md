# Cloud Resume Challenge — Frontend

[![Deploy Frontend](https://github.com/Dinku143/cloud-resume-frontend/actions/workflows/deploy-frontend.yml/badge.svg)](https://github.com/Dinku143/cloud-resume-frontend/actions/workflows/deploy-frontend.yml)

The frontend of my [Cloud Resume Challenge](https://cloudresumechallenge.dev/docs/the-challenge/azure/) — a single-page resume website hosted on Azure Blob Storage, served globally via Azure Front Door with HTTPS and a custom domain.

**Live site:** [https://www.dinkisaworku.com](https://www.dinkisaworku.com)  
**Blog post:** [How I Built My Cloud Resume on Azure](https://dev.to/dinku143/how-i-built-my-cloud-resume-on-azure-with-terraform-github-actions-54no)  
**Backend repo:** [cloud-resume-backend-infra](https://github.com/Dinku143/cloud-resume-backend-infra)

---

## What It Is

A hand-coded HTML/CSS resume website with:

- Dark cyberpunk design with animated blobs and scroll reveal effects
- Custom animated cursor
- Live visitor counter powered by an Azure Function API
- Fully responsive layout
- Deployed automatically via GitHub Actions on every push to `main`

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 |
| Styling | CSS3 (custom properties, grid, animations) |
| Fonts | Bebas Neue · DM Mono · Syne (Google Fonts) |
| Hosting | Azure Blob Storage (Static Website) |
| CDN & HTTPS | Azure Front Door Standard |
| DNS | Cloudflare |
| CI/CD | GitHub Actions |

---

## Project Structure

```
cloud-resume-frontend/
├── frontend/
│   ├── my_resume.html     ← single-page resume
│   └── my_resume.css      ← all styles
└── .github/
    └── workflows/
        └── deploy-frontend.yml  ← CI/CD pipeline
```

---

## CI/CD Pipeline

Every push to `main` automatically:

```
Push to main
     ↓
Login to Azure
     ↓
Upload HTML + CSS to Azure Blob Storage ($web container)
     ↓
Purge Azure Front Door cache
     ↓
www.dinkisaworku.com is updated live
```

### Required GitHub Secrets

| Secret | Description |
|---|---|
| `AZURE_CREDENTIALS` | Service Principal JSON from `az ad sp create-for-rbac` |
| `STORAGE_ACCOUNT_KEY` | Azure Storage Account access key |

---

## Local Development

No build tools needed. Just open the file directly:

```bash
# Clone the repo
git clone https://github.com/Dinku143/cloud-resume-frontend.git
cd cloud-resume-frontend

# Open in browser
open frontend/my_resume.html

# Or open in VS Code
code frontend/my_resume.html
```

---

## Deployment

Deployment is fully automated via GitHub Actions. To deploy manually:

```bash
az storage blob upload-batch \
  --account-name dinkisacvstorage \
  --destination '$web' \
  --source frontend/ \
  --overwrite \
  --auth-mode key \
  --account-key YOUR_STORAGE_KEY
```

---

## Author

**Dinkisa Demeke Worku**  
Azure Cloud & Infrastructure Engineer  
[dinkisaworku.com](https://www.dinkisaworku.com) · [LinkedIn](https://www.linkedin.com/in/dinkisa-worku-a43b68253/) · [GitHub](https://github.com/Dinku143)
