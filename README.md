# neve-web

All of **Neve**'s static web, one repo organized **by site**. Each top-level folder is an
independent site with its own Cloudflare Pages project (its own custom domain + Root directory),
so domains, deploys, and lifecycles stay cleanly separated while living in one place.

| Folder | Site | Domain | Cloudflare Pages (Root directory) | Build |
|---|---|---|---|---|
| `legal/` | Legal documents | `legal.nevestudio.app` | project root = `legal/` | none (static) |
| `site/`  | Studio landing (placeholder) | `nevestudio.app` *(not wired yet)* | project root = `site/` | TBD |

Adding a site later → new top-level folder + new Pages project pointing its Root directory there.
A folder can graduate to its own repo if it ever grows a heavy toolchain — cheap to split.

## Live URLs

- **Legal hub**: https://legal.nevestudio.app/
- **Carry**
  - Privacy: https://legal.nevestudio.app/carry/privacy/ ([中文](https://legal.nevestudio.app/carry/privacy/zh))
  - Terms: https://legal.nevestudio.app/carry/terms/ ([中文](https://legal.nevestudio.app/carry/terms/zh))

> URLs have no `legal/` prefix because the legal Pages project's **Root directory is `legal/`** —
> `legal/carry/privacy/` is served at `legal.nevestudio.app/carry/privacy/`.

## Structure

```
.
├── legal/                      # → legal.nevestudio.app  (Pages root = legal/)
│   ├── index.html              # Neve legal hub — lists each app
│   └── carry/
│       ├── index.html          # Carry legal hub
│       ├── privacy/{index.html, zh.html}   # EN (default) + 简体中文
│       └── terms/{index.html, zh.html}
└── site/                       # → nevestudio.app  (placeholder; project not wired yet)
    └── index.html
```

## Updating a legal document

1. Edit the HTML; update the "Last updated" date in the page heading.
2. Keep EN + 中文 in sync. **Do not remove PIPL clause 14** in `legal/carry/privacy/zh.html`
   (Mainland China requirement; EN page does not need it).
3. Commit + push `main` → the legal Pages project redeploys (~1 min, then ~5 min edge cache).
   (A push redeploys every Pages project on this repo; harmless for static sites. If a future
   framework site needs it, add path-based build skipping.)

## Adding a new app's legal docs

Create `legal/<app>/privacy/` and `legal/<app>/terms/` (same per-locale layout) and add a row
to `legal/index.html`. URLs become `legal.nevestudio.app/<app>/<doc>/[zh]`.

## Contact

murphy.lyu@icloud.com
