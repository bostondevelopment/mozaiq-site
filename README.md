# mozaiq-site

Public-facing static pages for the Mozaiq iOS app: privacy policy, terms of service,
support page, and a minimal landing page. Used to satisfy App Store Connect's
required URLs (privacy policy, support).

Visit https://bostondevelopment.github.io/mozaiq-site/ 

## Files

- `index.html` — landing page
- `privacy.html` — privacy policy (App Store Connect: **Privacy Policy URL**)
- `terms.html` — terms of service (App Store Connect: **License Agreement** if used)
- `support.html` — support / contact (App Store Connect: **Support URL**)
- `style.css` — shared Mozaiq-styled CSS

Pure static HTML/CSS. No build step. Works locally by opening any `.html` in a browser.

## Before you publish

**Update the support email.** All four pages reference `support@mozaiq.app`, which
is a placeholder. Either:
- Register that email at a domain you own and point MX to your inbox, OR
- Find-and-replace `support@mozaiq.app` with whatever email you'll actually monitor
  (e.g. your personal Gmail). You can change it later — just be consistent so
  App Store Connect matches.

```bash
# Quick swap (macOS sed):
cd mozaiq-site
sed -i '' 's/support@mozaiq.app/YOUR-EMAIL@example.com/g' *.html
```

Optionally, update the governing-law jurisdiction in `terms.html` (currently
Massachusetts) if you're not based there.

## Deploy: Vercel (recommended, ~5 min)

Free, custom domain support, deploys on git push.

1. Push this folder to a GitHub repo (public or private — Vercel handles both):
   ```bash
   cd /Users/michael/Documents/Code/mozaiq-site
   git init && git add . && git commit -m "Initial site"
   gh repo create mozaiq-site --private --source=. --push
   ```
2. Go to [vercel.com/new](https://vercel.com/new) → import the repo
3. **Framework Preset:** "Other" — Vercel will detect it as static HTML
4. Click Deploy. You get a URL like `https://mozaiq-site.vercel.app`
5. Paste that URL (plus `/privacy.html`, `/support.html`) into App Store Connect

## Deploy: GitHub Pages (requires public repo on free plan)

1. Push this folder as a **public** GitHub repo
2. Repo Settings → Pages → Source: `main` branch, root folder
3. URL: `https://<your-username>.github.io/mozaiq-site/`
4. Paste those URLs into App Store Connect

## Deploy: Cloudflare Pages (also free)

Same flow as Vercel. Slightly faster cold loads. Use [pages.cloudflare.com](https://pages.cloudflare.com).

## URLs to paste into App Store Connect

After deploying, paste these in **App Store Connect → App Information**:

| Field | URL |
|---|---|
| Privacy Policy URL | `https://your-domain/privacy.html` |
| Support URL | `https://your-domain/support.html` |
| Marketing URL (optional) | `https://your-domain/` |

## Updating the site later

It's just static HTML. Edit, commit, push — Vercel / GitHub Pages auto-redeploy.
No build step. No framework to update.
