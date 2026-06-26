# Founder Mode — Coming Soon

A single-file, dependency-free coming-soon landing page for **Founder Mode**, an
AI-powered personal chief of staff for busy founders and CEOs.

Everything (HTML, CSS, JS) lives in [`index.html`](index.html). No build step, no
frameworks.

## Local preview

Just open the file in a browser:

```bash
open index.html
```

Or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Configure the email form (Formspree)

The email capture form posts to [Formspree](https://formspree.io).

1. Create a free account and a new form at <https://formspree.io>.
2. Copy your form endpoint (looks like `https://formspree.io/f/abcdwxyz`).
3. In `index.html`, find the `<form>` tag (marked with a `FORMSPREE SETUP`
   comment) and replace the placeholder `YOUR_FORM_ID` in the `action` attribute:

   ```html
   action="https://formspree.io/f/abcdwxyz"
   ```

That's it. Submissions appear in your Formspree dashboard. The page submits via
`fetch` for inline success/error feedback and falls back to a standard POST if
JavaScript is disabled.

## Deploy to Cloudflare Pages

This site is static, so deployment is just connecting the repo.

### Option A — Git integration (recommended)

1. Push this repo to GitHub (see below) as `founder-mode-web`.
2. In the [Cloudflare dashboard](https://dash.cloudflare.com), go to
   **Workers & Pages → Create → Pages → Connect to Git**.
3. Select the `founder-mode-web` repository.
4. Configure the build settings:
   - **Framework preset:** `None`
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/` (the repo root)
5. Click **Save and Deploy**. Cloudflare builds a preview URL like
   `founder-mode-web.pages.dev`.

### Connect the custom domain

1. In your Pages project, open **Custom domains → Set up a custom domain**.
2. Enter `founder-mode.com` (and optionally `www.founder-mode.com`).
3. If the domain's DNS is already on Cloudflare, the records are added
   automatically. Otherwise, follow the prompts to point your DNS at Cloudflare.
4. SSL is provisioned automatically — the site goes live at
   <https://founder-mode.com>.

Every push to the default branch redeploys automatically.

### Option B — Direct upload (Wrangler)

```bash
npm install -g wrangler
wrangler pages deploy . --project-name founder-mode-web
```

## Push to GitHub

```bash
git init
git add .
git commit -m "Founder Mode coming-soon landing page"
git branch -M main
git remote add origin git@github.com:<your-username>/founder-mode-web.git
git push -u origin main
```

## License

© 2026 Founder Mode. All rights reserved.
