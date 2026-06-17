# Handoff — Freedom Painting

For the next chat: pick this up cold.

## Status (verified 2026-06-16)

- Live site `https://freedompainting.us/` returns HTTP 200.
- Latest commit on `main`: [`696ade9`](https://github.com/wretcher207/freedom-painting/commit/696ade9). Pushed. Working tree clean.
- Netlify auto-deploys from `main` (no manual deploy step).
- Lighthouse mobile (verified locally, last run before deploy): **Accessibility 100, Best Practices 100, SEO 100, Agentic Browsing 100 — 50 passed, 0 failed**.

## What's in the repo

- [index.html](index.html) — the whole site. Single-page static.
- [images/](images/) — 87 JPEGs (80 pre-existing + 7 new). All optimized.
- [favicon-16x16.png](favicon-16x16.png) / [favicon-32x32.png](favicon-32x32.png) / [apple-touch-icon.png](apple-touch-icon.png) — generated from `Logo.jpg` via `sips`.
- [SEO-STATUS.md](SEO-STATUS.md) — current SEO state + open TODOs (GBP, service-list confirmation).
- [MEMORY.md](MEMORY.md) — decision log; read the 2026-06-16 entry for the four-phase session that just shipped.
- [ERRORS.md](ERRORS.md) — gotchas (image encoder behavior, Chrome MCP quirks). Read before suggesting image-compression strategies.
- [.gitignore](.gitignore) — ignores `.review/` (local screenshots) and `.DS_Store`.
- [CNAME](CNAME), [robots.txt](robots.txt), [sitemap.xml](sitemap.xml), [google87357928efe5f7fa.html](google87357928efe5f7fa.html) — GitHub Pages/Netlify + Search Console plumbing.

## What shipped this session

Five commits. Newest first:
1. [`696ade9`](https://github.com/wretcher207/freedom-painting/commit/696ade9) — revert Phase 2 copy changes; strip new BA captions.
2. [`fe71f09`](https://github.com/wretcher207/freedom-painting/commit/fe71f09) — Phase 4: 3 new before/after pairs + 1 wide project tile; lightbox empty-src bug fix.
3. [`7b98ea1`](https://github.com/wretcher207/freedom-painting/commit/7b98ea1) — Phase 3: SEO + perf + a11y → Lighthouse 100×4.
4. [`959644b`](https://github.com/wretcher207/freedom-painting/commit/959644b) — Phase 2 design: emoji icons → real project photos in service cards. *(Copy edits in this commit were reverted in `696ade9`.)*
5. [`ea03d76`](https://github.com/wretcher207/freedom-painting/commit/ea03d76) — Phase 1 simplify: deleted orphaned `minerva_production.py`, deduped testimonials, dropped dead labels, modernized JS.

## Open items / next-step options

Order by impact:

1. **Google Business Profile** — single biggest open SEO win. Needs Rodney's business address. Steps in [SEO-STATUS.md](SEO-STATUS.md).
2. **Confirm service list with Rodney** — site advertises 3 services; the (deleted) chatbot system prompt listed 6 including Cabinet Refinishing, Deck & Fence Staining, Wall Repair. Gallery already shows cabinet and deck work. Either expand or confirm out of scope.
3. **(Optional) "Meet Rodney" section** — testimonials name him 6+ times, site never shows him. Would need a portrait photo. Flagged in Phase 2 critique, not actioned.

## How to run / verify locally

```bash
cd /Users/ghostintheshell/workspace/freedom-painting
python3 -m http.server 8765
# open http://localhost:8765
```

Lighthouse via Chrome DevTools MCP, mobile device emulation. Report goes to `.review/report.html`.

## Key facts

- **Hosting**: Netlify, deploys from this GitHub repo (`wretcher207/freedom-painting`).
- **Form backend**: Formspree (`https://formspree.io/f/xdawlbal`) — no own backend. The deleted `minerva_production.py` was never wired in.
- **Domain**: `freedompainting.us` (see [CNAME](CNAME)).
- **Search Console**: verified via URL prefix, sitemap submitted.
- **Owner contact**: Rodney McEwen, (207) 502-9970, freedompainting207@outlook.com.

## Gotchas to read BEFORE acting

- [ERRORS.md — image re-encoding](ERRORS.md) — don't bulk-recompress these JPEGs with `sips` or `cjpeg`; they'll get *bigger*. Use `jpegtran -optimize` for lossless gains.
- **Copy is off-limits**. The hero pill chip, the section eyebrows, the contact-badge chips — those are owner-approved voice. impeccable's "AI grammar" calls don't apply. Structural / cosmetic / perf changes are pre-authorized; copy changes need an explicit ask.
- **Working dir drift**: `cd images && ...` will leave subsequent Bash calls inside `images/`. Use absolute paths or `cd` back.
