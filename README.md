# Titan-Gen.com

Static site hosting app info and privacy policies for Titan-Gen apps.
No build step — plain HTML/CSS. Deployed free via GitHub Pages.

## Structure
```
/index.html                     landing page (app list)
/styles.css                     shared styles
/lottery-calculator/index.html  → Titan-Gen.com/lottery-calculator/
/rollvert/index.html            → Titan-Gen.com/rollvert/
/CNAME                          custom domain for GitHub Pages
```

## Before you publish — fill these in
- **Contact email:** every page uses `support@Titan-Gen.com`. Set up that
  address (most registrars offer free email forwarding) or change it.
- **Effective dates:** currently `August 12, 2026`. Update per app.
- **Confirm the SDK list** matches what's actually integrated (e.g. whether
  RollVert ships Unity Analytics, whether Lottery Calculator uses Crashlytics).
- Keep the Play Console **Data safety** form and **target audience** consistent
  with these policies.

## Deploy on GitHub Pages
1. Create a **public** repo (e.g. `Titan-Gen-site`) and push these files to the
   default branch.
2. Repo → **Settings → Pages**. Source: *Deploy from a branch*, branch `main`,
   folder `/ (root)`. Save.
3. Under **Custom domain**, enter `Titan-Gen.com` and Save. (The `CNAME` file
   already sets this; either method works.)
4. Add the DNS records below at your registrar.
5. Back on the Pages screen, tick **Enforce HTTPS** once the cert is issued
   (can take a few minutes to an hour after DNS resolves).

## DNS records
Apex domains can't use a CNAME, so point the apex with A/AAAA records and use a
CNAME only on `www`. Replace `USERNAME` with your GitHub username.

**Apex (`Titan-Gen.com`) — A records:**
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
www.Titan-Gen.com  →  USERNAME.github.io
```

Your privacy-policy URLs for Play Console will be:
- `https://Titan-Gen.com/lottery-calculator/`
- `https://Titan-Gen.com/rollvert/`

## Where to enter these on Squarespace
The domain is managed in the **Squarespace Domains dashboard** (this is where
former Google Domains landed). The same records above go in Squarespace — you do
not need to move the domain or change nameservers.

1. account.squarespace.com/domains → click **Titan-Gen.com** → **DNS** →
   **DNS Settings** → scroll to **Custom Records**.
2. **Delete Squarespace's default/parking records** that conflict — Squarespace
   pre-populates placeholder records, and GitHub requires you remove any default
   apex record before adding yours. Leave MX/email records alone if you use them.
3. Add the four apex **A** records: Type `A`, Name/Host `@`, Data = each GitHub
   IP (one record per IP). Optionally add the four **AAAA** records the same way.
4. Add the **CNAME**: Type `CNAME`, Host `www`, Data `USERNAME.github.io`.
5. (Recommended) Verify the domain to block takeovers: in GitHub → Settings →
   Pages → **Verify domains**, copy the `TXT` challenge, and add it in
   Squarespace as Type `TXT`, Host `_github-pages-challenge-titangen`
   (Squarespace's host field excludes the domain), Data = the value GitHub gives.
6. In GitHub → Settings → Pages, set **Custom domain** to `Titan-Gen.com`
   (matches the CNAME file here). GitHub auto-creates the www→apex redirect.
7. Wait for propagation (Squarespace can take up to ~24–72h, usually much less),
   then tick **Enforce HTTPS**.

Shortcut: Squarespace also supports **ALIAS** records. If you'd rather not manage
four A records, one ALIAS at Host `@` → `USERNAME.github.io` works and
auto-tracks GitHub's IPs — but the four A records are the battle-tested path if
you hit any snag.

## Alternative: Cloudflare Pages
If you point the domain's nameservers at Cloudflare (free), Cloudflare flattens
CNAMEs at the apex so you skip the A records entirely. Connect the GitHub repo in
the Cloudflare Pages dashboard, add `Titan-Gen.com`, and it wires up DNS + HTTPS.
Only worth it if you want Cloudflare's CDN/analytics — the Squarespace path above
needs nothing extra.
