# Founder Mode — Landing Page

The landing page for **Founder Mode** — a white-glove service that hand-builds a
personal AI chief of staff for a few founders at a time. The page is an
application/access-request flow, not a mass waitlist.

Everything (HTML, CSS, JS) lives in a single file: [`index.html`](index.html).
No build step, no frameworks, no dependencies.

## Design

- **Palette:** Obsidian & Champagne — near-black canvas with a champagne-gold
  accent (`#c9a45c`), for a private, members-only feel.
- **Type:** Fraunces serif for display headlines, Inter for UI/body.
- Animated gold hero glow, gold hairlines, generous negative space.
- Fully mobile responsive.

## Content structure

- **Hero** — wordmark, "Onboarding 10 founders this quarter" badge, serif
  headline, and the application form.
- **Application form** — name, work email, company, and "What's eating your time
  right now?" Submissions are qualified leads, not anonymous emails.
- **How it works** — 3 steps: we learn how you work → we build your agent → it
  runs your mornings.
- **Closing CTA** — scarcity ("we only take a few founders at a time") + repeat
  Request Access button.

## Local preview

```bash
open index.html
# or serve it:
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Email capture (Formspree)

The form posts to [Formspree](https://formspree.io), endpoint
`https://formspree.io/f/mbdvgvrv` (set in the `<form action>` in
[`index.html`](index.html)).

- Submissions land in the Formspree dashboard **and** are emailed to you.
- **First-use activation:** Formspree emails a one-time confirmation the first
  time the form is submitted — click that link once to activate, or early
  submissions won't come through. Submit the form yourself once to trigger it.
- The free tier covers **50 submissions/month**, ample for an application flow.
- The page submits via `fetch` for inline success/error feedback and falls back
  to a standard POST if JavaScript is disabled.

To point at a different form, replace the `action` URL in the `<form>` tag.

## Deploy to Cloudflare Pages

This site is static, so deployment is just connecting the repo.

### Option A — Git integration (recommended)

1. The repo is already on GitHub as `founder-mode-web`.
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

## License

© 2026 Founder Mode. All rights reserved.