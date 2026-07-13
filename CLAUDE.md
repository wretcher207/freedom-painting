# freedom-painting

Static multi-page site, no build step. Client: Freedom Painting, freedompainting.us.

## Pages

- `index.html` (home), `exterior-painting/`, `interior-painting/`, `house-painter-houlton-me/`.
- CSS is shared: `css/site.css`. Every page links it; nothing is inline anymore. Edit the stylesheet once, not per page.
- `url()` paths in `css/site.css` must be root-relative (`/images/...`), since the sheet lives at `/css/`.
- Subpage asset paths are root-relative (`/images/...`) so they resolve from a nested directory.
- No doorway pages: a location or service page only ships when there is real evidence (a named local job, a testimonial, gallery work). Do not mass-produce "painter in [town]" templates.

## Deploy

- Host: Netlify, auto-deploys from GitHub `wretcher207/freedom-painting` branch `main` (HANDOFF.md). Site is dashboard-linked; there is no netlify.toml or .netlify/state.json in this repo.
- Production: https://freedompainting.us
- Ship: commit + `git push origin main`. That is the whole pipeline.
- Verify live: curl the production URL for HTTP 200 and confirm the change actually serves before calling it done.
- Gotchas: forms go to Formspree (f/xdawlbal), there is no backend. Don't recompress the JPEGs with sips/cjpeg, they get BIGGER; use `jpegtran -optimize` (ERRORS.md). The CNAME file may be a GitHub Pages leftover; whether Netlify uses it is unconfirmed.
- Copy rule (MEMORY.md): site copy is owner-approved. Never change copy without an explicit ask.
