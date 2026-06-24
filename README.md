# neve-legal

Public legal documents for **Neve** apps, served as a static site via Cloudflare Pages at
**https://legal.nevestudio.app**.

One repo = one concern (legal site) = one subdomain. Marketing / landing pages live elsewhere
(`nevestudio.app`), Cloudflare Workers handle app APIs (`flight.` / `config.` / `places.`).

## Live URLs

- **Hub**: https://legal.nevestudio.app/
- **Carry**
  - Privacy: https://legal.nevestudio.app/carry/privacy/ ([中文](https://legal.nevestudio.app/carry/privacy/zh))
  - Terms: https://legal.nevestudio.app/carry/terms/ ([中文](https://legal.nevestudio.app/carry/terms/zh))

## Structure

```
.
├── index.html              # Neve legal hub — lists each app
└── carry/
    ├── index.html          # Carry legal hub
    ├── privacy/
    │   ├── index.html      # English Privacy Policy (default)
    │   └── zh.html         # 简体中文隐私政策
    └── terms/
        ├── index.html      # English Terms of Service
        └── zh.html         # 简体中文服务条款
```

Adding a new app: create `<app>/privacy/` and `<app>/terms/` (same per-locale layout) and add a
row to the root `index.html` hub. URLs become `legal.nevestudio.app/<app>/<doc>/[zh]`.

## Deploy (Cloudflare Pages)

- Project tracks this repo; production branch `main`; **no build command** (static); root output `/`.
- Custom domain `legal.nevestudio.app`. Pages serves clean URLs (trailing slash + `index.html`,
  and `/x.html` 308 → `/x`), so the app links to `…/zh` without the `.html` suffix.
- Push to `main` → Pages redeploys within ~1 min (then ~5 min edge cache).

## Updating a document

1. Edit the HTML; update the "Last updated" date in the page heading.
2. Keep EN + 中文 in sync. **Do not remove PIPL clause 14** in `carry/privacy/zh.html`
   (Mainland China requirement; EN page does not need it).
3. Commit + push.

## Contact

murphy.lyu@icloud.com
