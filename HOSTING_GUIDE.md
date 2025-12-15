# GitHub Pages Hosting Guide for Research Pathway

This guide provides step-by-step instructions to host your website on GitHub Pages and connect it to your custom domain (`www.researchpathway.co.nz`).

**Prerequisites:**
- You have a GitHub account.
- You have access to your Domain Registrar (where you bought the domain).
- Your `website` folder is ready (I have already organized it for you).

---

## Phase 1: Upload to GitHub

1.  **Log in to GitHub** and click the **+** icon (top right) -> **New repository**.
2.  **Repository Name**: `research-pathway-website` (or similar).
3.  **Visibility**: Choose **Public** (Required for free hosting).
4.  **Initialize**: Do **not** check any boxes (Add README, etc.). Just click **Create repository**.
5.  **Upload Files**:
    *   On the next screen, look for the link **"uploading an existing file"**.
    *   Drag and drop **ALL** files and folders from your local `website` folder into the browser.
    *   **CRITICAL**: Ensure the file named `CNAME` is included in this upload.
    *   Commit message: "Initial upload".
    *   Click **Commit changes**.

---

## Phase 2: Enable GitHub Pages

1.  Go to your repository **Settings** (tab at the top).
2.  On the left sidebar, click **Pages**.
3.  **Build and deployment**:
    *   **Source**: Select `Deploy from a branch`.
    *   **Branch**: Select `main` (or `master`) and folder `/ (root)`.
    *   Click **Save**.
4.  **Custom domain**:
    *   In the "Custom domain" box, type: `www.researchpathway.co.nz`
    *   Click **Save**.
    *   *Note: If it says "CNAME already exists", that's good! It means it found the file I created for you.*
5.  **Enforce HTTPS**: Check this box (it might take a few minutes to become clickable).

---

## Phase 3: Configure DNS (Connect Your Domain)

**Go to your Domain Registrar's website** (e.g., GoDaddy, Crazy Domains, OnlyDomains) and find the **DNS Management** or **Zone Editor**.

You need to add/edit exactly **two** types of records.

### 1. The "www" Record (CNAME)
This connects `www.researchpathway.co.nz` to your GitHub site.

| Type | Host / Name | Value / Target | TTL |
| :--- | :--- | :--- | :--- |
| **CNAME** | `www` | `[your-github-username].github.io` | 1 Hour / 3600 |

*(Replace `[your-github-username]` with your actual GitHub username. e.g., if your user is `yuqian-zhang`, enter `yuqian-zhang.github.io`)*

### 2. The Root Domain Record (A Record)
This ensures that if someone types `researchpathway.co.nz` (without www), they still find your site.

| Type | Host / Name | Value / Target |
| :--- | :--- | :--- |
| **A** | `@` (or leave blank) | `185.199.108.153` |
| **A** | `@` (or leave blank) | `185.199.109.153` |
| **A** | `@` (or leave blank) | `185.199.110.153` |
| **A** | `@` (or leave blank) | `185.199.111.153` |

*(You only strictly need one A record, but adding all 4 makes it more reliable).*

---

## Phase 4: Troubleshooting "Site Not Showing"

If you have done all the above and the site is not loading or shows an error:

### 1. The "404" Error
*   **Cause**: GitHub doesn't know which file is your homepage.
*   **Fix**: Ensure your main file is named exactly `index.html` (all lowercase). *I have checked your folder, and it is correct.*

### 2. The "Privacy Error" or "Not Secure"
*   **Cause**: The SSL (HTTPS) certificate is still being created.
*   **Fix**: Wait. This process takes anywhere from **15 minutes to 24 hours**. Do not panic. It will resolve itself.

### 3. The "Old Site" or "Blank Page" (Caching)
*   **Cause**: Your browser remembers the old DNS settings.
*   **Fix**:
    *   Try opening the site in an **Incognito/Private** window.
    *   Try accessing it from your **phone** (disconnect from WiFi, use mobile data).

### 4. DNS Propagation Delay
*   **Cause**: DNS changes travel across the internet slowly.
*   **Fix**: This is the most common issue. It can take up to **48 hours**, though usually it's done in 1-2 hours. You can check your status at [whatsmydns.net](https://whatsmydns.net/#CNAME/www.researchpathway.co.nz).

### 5. Check the "CNAME" File in GitHub
*   Go to your GitHub repository "Code" tab.
*   Click on the file named `CNAME`.
*   Does it say **exactly** `www.researchpathway.co.nz`?
*   If it has `http://` or `/` at the end, **edit it** to remove them. It must be just the domain name.
