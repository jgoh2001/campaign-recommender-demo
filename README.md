# Campaign Channel Recommender — Public Demo

A standalone, offline, single-file web tool that recommends communications channels
across the campaign funnel. No backend, no build step, no database — `index.html`
runs entirely in the visitor's browser.

This folder is **ready to commit to a GitHub repo and deploy to Azure Static Web Apps.**

---

## Files in this repo

| File | Purpose |
|------|---------|
| `index.html` | The tool itself (self-contained: HTML + CSS + data + logic in one file). |
| `staticwebapp.config.json` | Azure Static Web Apps config (fallback route + basic security headers). |
| `.github/workflows/azure-static-web-apps.yml` | GitHub Action that deploys on every push to `main`. |
| `README.md` | This file. |

---

## Deploy to Azure Static Web Apps

### Option A — Azure Portal wizard (easiest, recommended)

1. Push this folder's contents to a new **GitHub repository** (the `main` branch).
2. In the [Azure Portal](https://portal.azure.com): **Create a resource → Static Web App**.
3. Fill in:
   - **Plan type:** Free
   - **Source:** GitHub → authorize → pick your repo and the `main` branch
   - **Build presets:** Custom
   - **App location:** `/`
   - **Api location:** *(leave blank)*
   - **Output location:** *(leave blank)*
4. Click **Create**. Azure will:
   - add its **own** deployment workflow to your repo automatically, and
   - store the deployment token as a repo secret for you.
5. In ~1–2 minutes your site is live at `https://<name>.azurestaticapps.net`.

> ⚠️ If you use the portal wizard, Azure adds its own workflow file. To avoid two
> workflows deploying at once, **delete `.github/workflows/azure-static-web-apps.yml`**
> from this folder before (or just after) running the wizard. Keep that file only if
> you're wiring the token manually in Option B.

### Option B — Manual (use the workflow in this repo)

1. Create the Static Web App in Azure **without** connecting GitHub (choose "Other" as source).
2. Copy its **deployment token** (Azure Portal → your Static Web App → *Manage deployment token*).
3. In your GitHub repo: **Settings → Secrets and variables → Actions → New repository secret**
   - Name: `AZURE_STATIC_WEB_APPS_API_TOKEN`
   - Value: *(paste the deployment token)*
4. Push to `main`. The included workflow deploys automatically. Pull requests get their
   own temporary **preview URL**, and closing the PR tears the preview down.

---

## Preview locally

Just open `index.html` in any modern browser (double-click). It needs no server.

---

## Custom domain (optional)

In the Static Web App → **Custom domains → Add** and follow the DNS steps. Azure issues
a free TLS certificate automatically.

---

## Scaling later (same platform, no re-host)

Azure Static Web Apps is chosen so the demo and a future production version live on one
platform. When you're ready you can add — without moving hosts:

- **Login** — built-in authentication (Microsoft Entra ID / M365), to gate the tool to
  internal users.
- **An API** — a linked **Azure Functions** backend (the `api/` folder) for things like
  refreshing channel data live from a source system.
- **Environments** — staging/preview slots via pull requests.

---

## ⚠️ Data notice

`index.html` embeds **illustrative sample channel data** with rounded reach figures and
de-identified spokespersons — **but it does retain real owner names and email addresses.**
Because this is a **public** site, those names and emails will be visible to anyone with
the link and may be scraped, cached, and indexed by search engines. Confirm this is
approved before publishing, and switch on **Entra ID authentication** (see *Scaling*
above) if access should be restricted to NTUC staff.