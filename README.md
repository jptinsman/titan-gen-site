# titan-gen.com

Static site hosting app info and privacy policies for titan-gen apps.
No build step — plain HTML/CSS. Deployed free via GitHub Pages.

## Structure
```
/index.html                     landing page (app list)
/styles.css                     shared styles
/lottery-calculator/index.html  → titan-gen.com/lottery-calculator/
/rollvert/index.html            → titan-gen.com/rollvert/
/CNAME                          custom domain for GitHub Pages
```

## Before you publish — fill these in
- **Contact email:** every page uses `support@titan-gen.com`. Set up that
  address (most registrars offer free email forwarding) or change it.
- **Effective dates:** currently `August 12, 2026`. Update per app.
- **Confirm the SDK list** matches what's actually integrated (e.g. whether
  RollVert ships Unity Analytics, whether Lottery Calculator uses Crashlytics).
- Keep the Play Console **Data safety** form and **target audience** consistent
  with these policies.

## Deploy on GitHub Pages
1. Create a **public** repo (e.g. `titan-gen-site`) and push these files to the
   default branch.
2. Repo → **Settings → Pages**. Source: *Deploy from a branch*, branch `main`,
   folder `/ (root)`. Save.
3. Under **Custom domain**, enter `titan-gen.com` and Save. (The `CNAME` file
   already sets this; either method works.)
4. Add the DNS records below at your registrar.
5. Back on the Pages screen, tick **Enforce HTTPS** once the cert is issued
   (can take a few minutes to an hour after DNS resolves).

## DNS records
Apex domains can't use a CNAME, so point the apex with A/AAAA records and use a
CNAME only on `www`. Replace `USERNAME` with your GitHub username.

**Apex (`titan-gen.com`) — A records:**
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
**Apex — AAAA records (IPv6, recommended):**
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```
**www — CNAME:**
```
www.titan-gen.com  →  USERNAME.github.io
```

Your privacy-policy URLs for Play Console will be:
- `https://titan-gen.com/lottery-calculator/`
- `https://titan-gen.com/rollvert/`

## Alternative: Cloudflare Pages
If you move your nameservers to Cloudflare (free), Cloudflare flattens CNAMEs at
the apex, so you skip the four A records. Connect the GitHub repo in the
Cloudflare Pages dashboard, add `titan-gen.com` as a custom domain, and it wires
up DNS + HTTPS automatically. Same files, no changes needed.
