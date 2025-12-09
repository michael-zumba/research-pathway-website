# How to Host Your Website for Free with Your Custom Domain

Since you have your own domain (**www.researchpathway.co.nz**), **Netlify** is the best "Free & Easy" choice. It handles the SSL certificate (HTTPS) for you automatically.

---

## Step 1: Upload Your Site to Netlify (Drag & Drop)

1.  **Prepare Your Folder**:
    *   Use the main `website` folder (the one containing `index.html` and `style.css`).
    *   *Do NOT use the `google_sites_deploy` folder.*
2.  **Upload**:
    *   Go to [app.netlify.com/drop](https://app.netlify.com/drop).
    *   Drag your `website` folder onto the browser window.
    *   Wait a few seconds. Your site is now live on a temporary link (e.g., `fluffy-unicorn.netlify.app`).

---

## Step 2: Connect Your Domain (www.researchpathway.co.nz)

1.  **In Netlify**:
    *   Click on **"Domain Settings"** (or "Set up a custom domain").
    *   Click **"Add custom domain"**.
    *   Enter: `www.researchpathway.co.nz`
    *   Click **Verify**.
    *   Click **Yes, add domain**.

2.  **Configure Your DNS (At your Domain Registrar)**:
    *   Log in to the website where you bought your domain (e.g., GoDaddy, Crazy Domains, OnlyDomains, etc.).
    *   Find the **DNS Settings** or **Zone Editor**.
    *   You need to add/edit a **CNAME Record**:
        *   **Type**: `CNAME`
        *   **Host / Name**: `www`
        *   **Value / Target**: `[your-netlify-site-name].netlify.app` (Copy this from the Netlify dashboard).
        *   *TTL*: Leave as default (e.g., 3600 or 1 hour).
    *   *(Optional but recommended)* Redirect the "naked" domain (`researchpathway.co.nz` without `www`):
        *   Look for an **A Record** for `@` (or blank host).
        *   Netlify will provide you with an IP address (usually `75.2.60.5`) to point this to. Check the instructions on the Netlify screen.

3.  **Wait for HTTPS**:
    *   Once the DNS is set, Netlify will automatically provision a free SSL certificate. This might take up to 24 hours (usually much faster).

---

## Alternative: GitHub Pages (If you prefer GitHub)

1.  **Create Repository**: Create a public repo named `research-pathway-website`.
2.  **Upload Files**: Upload your `website` folder contents to the `main` branch.
3.  **Create CNAME File**:
    *   Create a new file in the repository root named `CNAME` (all caps, no extension).
    *   Inside the file, write only one line:
        ```text
        www.researchpathway.co.nz
        ```
4.  **Configure DNS**:
    *   Login to your domain registrar.
    *   Add a **CNAME Record**:
        *   **Host**: `www`
        *   **Value**: `[your-github-username].github.io`
    *   Add **A Records** for the naked domain (`@`) pointing to GitHub's IPs:
        *   `185.199.108.153`
        *   `185.199.109.153`
        *   `185.199.110.153`
        *   `185.199.111.153`

---

## Which one should I choose?

*   **Choose Netlify** if you want the easiest setup. The "Drag & Drop" feature combined with their easy domain wizard is very user-friendly.
*   **Choose GitHub Pages** if you want to keep your academic profile consistent on GitHub and are comfortable managing a repository.

Both are **100% free** for this type of website.
