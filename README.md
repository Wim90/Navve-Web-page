# Navve Web Page

Public-facing GitHub Pages site for the [Navve](https://apps.apple.com) iOS app.

**Live site:** `https://<your-github-username>.github.io/Navve-Web-page/`
(or your custom domain once CNAME is configured)

---

## Structure

```
.
├── index.html                    # Single-page site (hero + privacy + terms)
├── CNAME                         # Custom domain (fill in to activate)
├── docs/
│   ├── PRIVACY_POLICY.md         # Privacy policy (fetched + rendered at runtime)
│   └── TERMS_AND_CONDITIONS.md   # Terms & conditions (fetched + rendered at runtime)
└── .github/
    └── workflows/
        └── deploy.yml            # GitHub Actions → GitHub Pages deployment
```

---

## How it works

`index.html` uses [marked.js](https://marked.js.org) (loaded via CDN) to fetch the two Markdown files at page load and render them into the `#privacy` and `#terms` sections. No build step is required — the site is entirely static.

---

## Deployment

### Automatic (GitHub Actions)

Every push to `main` triggers `.github/workflows/deploy.yml`, which:
1. Checks out the repo
2. Uploads the entire root as a Pages artifact
3. Deploys it to GitHub Pages

**One-time setup in GitHub:**
1. Go to **Settings → Pages**
2. Under **Source**, select **GitHub Actions**
3. Push to `main` — the action handles the rest

### Manual fallback

In **Settings → Pages** you can also set Source to **Deploy from a branch → main → / (root)** if you prefer not to use Actions.

---

## Custom Domain

1. Add your domain to the `CNAME` file (one line, no `https://`):
   ```
   navve.app
   ```
2. Add the appropriate DNS records with your registrar:
   - **Apex domain** (`navve.app`): four `A` records pointing to GitHub's IPs
   - **Subdomain** (`www.navve.app`): one `CNAME` record → `<username>.github.io`
3. Enable **Enforce HTTPS** in Settings → Pages once DNS propagates

GitHub's current IP addresses: [docs.github.com/pages/configuring-a-custom-domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

---

## Updating content

Edit the Markdown files in `docs/` and push — the live site reflects changes immediately (no rebuild needed, the browser fetches them fresh).

| File | Purpose |
|------|---------|
| `docs/PRIVACY_POLICY.md` | Privacy policy shown at `#privacy` |
| `docs/TERMS_AND_CONDITIONS.md` | Terms shown at `#terms` |

---

## App Store link

In `index.html`, find the `.store-badge` anchor and replace `href="#"` with the real App Store URL:

```html
<a class="store-badge" href="https://apps.apple.com/app/navve/idXXXXXXXXXX">
```

---

## Contact

Support: [admin@wimsightlabs.com](mailto:admin@wimsightlabs.com)
