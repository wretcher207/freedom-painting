# freedom-painting

Static multi-page site, no build step. Client: Freedom Painting, freedompainting.us.

## Pages

- `index.html` (home), `exterior-painting/`, `interior-painting/`, `house-painter-houlton-me/`.
- CSS is shared: `css/site.css`. Every page links it; nothing is inline anymore. Edit the stylesheet once, not per page.
- Rules for the subpage before/after figures are scoped to `.prose .ba-pair`. The homepage gallery also uses `.ba-pair`; an unscoped rule breaks it (happened 2026-07, fixed 2026-10).
- `url()` paths in `css/site.css` must be root-relative (`/images/...`), since the sheet lives at `/css/`.
- Subpage asset paths are root-relative (`/images/...`) so they resolve from a nested directory.
- No doorway pages: a location or service page only ships when there is real evidence (a named local job, a testimonial, gallery work). Do not mass-produce "painter in [town]" templates.

## Deploy

- Host: GitHub Pages, builds from `wretcher207/freedom-painting` branch `main`, path `/` (verified 2026-10-17: `Server: GitHub.com` header, `gh api repos/wretcher207/freedom-painting/pages`). Not Netlify; older notes that said Netlify were wrong.
- Production: https://freedompainting.us
- Ship: commit + `git push origin main`. That is the whole pipeline.
- Verify live: curl the production URL for HTTP 200 and confirm the change actually serves before calling it done.
- Gotchas: forms go to Formspree (f/xdawlbal), there is no backend. Don't recompress the JPEGs with sips/cjpeg, they get BIGGER; use `jpegtran -optimize` (ERRORS.md). The CNAME file is live: it is what points freedompainting.us at GitHub Pages. Don't delete it. `404.html` at the root is GitHub Pages' custom not-found page.
- Copy rule (MEMORY.md): site copy is owner-approved. Never change copy without an explicit ask.

## Speed (2026-10)

- Fonts are self-hosted in `/fonts` (Bebas Neue, Lora, latin subset, `@font-face` at top of `css/site.css`). No Google Fonts request.
- Images are `<picture>` with a `.webp` sibling (and `-480.webp` for homepage gallery tiles); the `.jpg` stays as the fallback and the lightbox source. A new photo needs a `.webp` sibling and `width`/`height` on the `<img>`. `picture { display: contents }` in the stylesheet keeps the existing layout rules working.
- The hero is an `<img>` in `.hero-bg` (not a CSS background) so it can be preloaded and served as WebP.
