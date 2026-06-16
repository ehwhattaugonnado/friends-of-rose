# The Hellbreakers Chronicle — public wiki

This is the **public**, player-facing wiki and running log for the Hellbreakers tabletop
campaign. It is built with [MkDocs](https://www.mkdocs.org/) and
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and served from free
GitHub Pages.

## Generated — do not hand-edit

> [!IMPORTANT]
> The content under `docs/` is **generated** from a separate **private** source repo by a
> build script (`scripts/build_wiki.py` over in the private repo). **Do not hand-edit
> generated pages** — your changes will be overwritten on the next build. This repo holds
> only the site scaffold (config, theme chrome, nav-ordering `.pages` files, CI) plus
> generated player-safe content.

Publishing is opt-in: only files named in the build manifest are emitted, so nothing leaks
by accident. Sensitive material (GM notes, copyrighted manuscripts, GM-only campaign state)
never leaves the private repo.

## Obscured posture

This site is intended to be **public but obscured** — technically reachable, but not
indexed or advertised:

- Every page injects `<meta name="robots" content="noindex, nofollow">`
  (via `overrides/main.html`).
- `docs/robots.txt` serves `Disallow: /`.
- `mkdocs.yml` deliberately sets **no** `site_url`, so MkDocs Material emits **no**
  `sitemap.xml`.

Please don't add `site_url` or a sitemap.

## Preview locally

```bash
python -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000/>.

To produce the exact build the CI runs:

```bash
mkdocs build --strict
```

## How it deploys

On every push to `main`, the GitHub Actions workflow at `.github/workflows/deploy.yml`
installs `requirements.txt`, runs `mkdocs build --strict`, and deploys the resulting `site/`
to GitHub Pages.

## Navigation

The nav tree is driven by the [awesome-pages](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin)
plugin via `.pages` files (no hand-maintained `nav:` block in `mkdocs.yml`), so the
navigation adapts automatically to whatever pages the build script generates.
