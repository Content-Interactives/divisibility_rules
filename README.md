# Divisibility Rules

This repository holds a **production build** of a **Create React App** (CRA) single-page app: bundled JavaScript mounts on `#root`, with all asset URLs rooted at **`/divisibility_rules/`** for GitHub Pages.

**Live site:** [https://content-interactives.github.io/divisibility_rules](https://content-interactives.github.io/divisibility_rules)

CK-12 links, Flexbooks, and standards: [Standards.md](Standards.md).

---

## What is in this repo

| Path | Purpose |
|------|---------|
| `index.html` | CRA shell: loads hashed `main.*.js` and `main.*.css` under `/divisibility_rules/static/...` |
| `asset-manifest.json` | Maps logical entry names to hashed filenames |
| `static/js/main.*.js` | Application bundle (minified React app) |
| `static/js/488.*.chunk.js` | Async chunk (**web-vitals** reporting only) |
| `static/css/main.*.css` | Main stylesheet |
| `*.map` | Source maps for the bundles |
| `manifest.json`, `favicon.ico`, `robots.txt` | CRA / PWA metadata |

There is **no** `package.json`, `src/`, or other **source** tree in this checkout—only deployable output. Rebuilding or editing behavior requires the original CRA project (or recovering sources from the source maps, which is fragile).

---

## Stack (inferred)

- **React** (CRA webpack bundle; `react` / `react-dom` embedded in `main.*.js`)
- **Tailwind-style utility classes** appear in the shipped CSS class names (exact Tailwind version not pinned in-repo)
- **web-vitals** (lazy-loaded chunk `488`)

---

## Hosting and URL paths

`index.html` references scripts and links with **absolute** paths such as:

`/divisibility_rules/static/js/main.27afc985.js`

So the site expects to be served with **path prefix** `/divisibility_rules` (as on `*.github.io/divisibility_rules/`). Serving the folder at domain root without that prefix will **404** those assets.

Local checks:

- Use a static server and either mirror that path structure or temporarily rewrite paths if testing from another base.

The `package-lock.json` at the root only records **`serve`** as a dependency (likely for local preview); run **`npm ci`** only if you intend to use that tooling—there is no accompanying `package.json` in the listing, so lockfile may be partially orphaned.

---

## Embedding

- Full-height shell: `<body class="h-screen">`, `<div id="root" class="h-full">`.
- Iframe `src` should point at the **deployed** Pages URL so `/divisibility_rules/...` resolves correctly.

---

## Maintenance

- **Content / logic changes:** edit the **source** app elsewhere, run `npm run build`, then replace `static/`, `index.html`, `asset-manifest.json`, and related root files with the new CRA `build/` output (keeping `homepage` / `PUBLIC_URL` aligned with `/divisibility_rules`).
- After any manual deploy to Jekyll-style hosts, ensure **`_next`-style paths are not stripped**; CRA uses `static/` (no leading underscore). If GitHub Pages runs Jekyll on the branch, a **`.nojekyll`** file in the published root may still be required depending on hosting setup.
- **Fingerprinted filenames** change on every build; always ship updated `index.html` + `asset-manifest.json` together with new `static/` files.
