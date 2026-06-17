# Freedom Painting — decision log

Persistent decisions and session summaries. Append, don't rewrite.

---

## 2026-06-16 — Repo review / simplify / design / SEO+perf / new gallery assets

### Worked on
Full multi-phase review of the freedompainting.us static site after months of no touches. Cleanup + simplification, design critique, SEO/perf/a11y to Lighthouse 100, then integration of 7 new gallery assets.

### Completed
- **Phase 1 simplify** ([ea03d76](https://github.com/wretcher207/freedom-painting/commit/ea03d76)): deleted orphaned `minerva_production.py` Flask backend (never wired into live site — live form uses Formspree), deduped 10 testimonial cards into a JS `innerHTML += innerHTML` clone for the marquee, stripped 50 generic `.project-label` spans, removed the hero stats row that duplicated the trust banner below, dropped the deprecated `keywords` meta, moved all inline styles into a `.UTILITIES` CSS block, modernized `var` → `const/let` + arrow funcs throughout the script. Net **−409 lines**.
- **Phase 2 design pass** ([959644b](https://github.com/wretcher207/freedom-painting/commit/959644b)): replaced the emoji-circle service card icons with real Freedom Painting project photos (p06 / p25 / p36). *(Subsequent copy changes reverted — see Decisions.)*
- **Phase 3 SEO + perf + a11y** ([7b98ea1](https://github.com/wretcher207/freedom-painting/commit/7b98ea1)): favicon set (16/32/180) generated from `Logo.jpg` via `sips`, `<link rel="preload" fetchpriority="high">` on hero image, `decoding="async"` on all 64 below-fold images, lossless `jpegtran -optimize -progressive` pass on all 80 images (−728 KB), hero re-encoded at q65 (284 K → 244 K), four WCAG AA contrast fixes (`.testimonial-date`, `.testimonial-source`, `.trust-text small`, `.footer-bottom`), darkened `.btn-facebook` background to clear contrast on white text, updated `sitemap.xml` lastmod, refreshed `SEO-STATUS.md`. **Lighthouse mobile: Accessibility 100, Best Practices 100, SEO 100, Agentic Browsing 100 — 50 passed, 0 failed.**
- **Phase 4 new gallery assets** ([fe71f09](https://github.com/wretcher207/freedom-painting/commit/fe71f09)): added 3 before/after pairs at top of BA grid (Front Door / Log Home / Deck) and 1 wide project tile (blue-house crew shot) to Completed Projects. New images resized to 1200 px max + re-encoded at q78 (~58% smaller than raw camera files). Also fixed a latent bug — the lightbox `<img src="">` was issuing a stray fetch of the document URL.
- **Revert copy** ([696ade9](https://github.com/wretcher207/freedom-painting/commit/696ade9)): per David's feedback restored hero pill chip, h1 with forced `<br>`, four section eyebrows, contact-badges chip row; stripped captions on the 3 new BA pairs. Functional/cosmetic/perf changes from earlier phases retained.

### In progress
None.

### Decisions made
- **`minerva_production.py` deleted, not relocated**. Why: it was a Flask chatbot/quote-form backend that was never wired into `index.html` (which uses Formspree). Keeping it in the static-site repo was misleading. If David ever wants a chat widget, the code lives in git history and belongs in its own repo. Rejected: leaving it in place "in case." Rejected: moving it to a new repo (no live deployment exists, premature).
- **Service card style: real photos over icons**. Why: the emoji-circle "icon-card trinity" is the SaaS-feature-grid cliché; for a painter's site, real project photos read as portfolio, not template. David approved before applied. Rejected: keeping icons, breaking the 3-up grid into asymmetric cards.
- **Image strategy: lossless `jpegtran` only, except hero**. Why: tried `sips` and re-encoding via `cjpeg` at q78/q82 on existing JPEGs — both produced files *larger* than the source. The originals were already well-compressed. Only `jpegtran -optimize` (lossless) gave real savings (5.7%), and only the hero (LCP element) earned the tradeoff of cjpeg q65 with mild quality loss. Logged in `ERRORS.md`. Rejected: bulk re-encode at any quality (made files bigger).
- **Copy is off-limits during design critiques on client sites**. Why: I stripped the hero pill, section eyebrows, and contact badges in Phase 2 because impeccable flagged them as "AI grammar." David's reaction: *"not crazy about the captions or the copy, revert."* The copy was owner-approved voice, not slop. Going forward: structural/cosmetic/perf changes pre-authorized; copy needs an explicit ask. Logged as a personal feedback memory.
- **New BA pairs at top of grid, no captions**. Why: latest work first is the gallery convention here; David said simple before/afters don't need captions. Existing 11 pairs keep their captions as before.

### Next session priorities
- **Google Business Profile setup** — needs Rodney's business address. See `SEO-STATUS.md` for the full steps. This is the single biggest open SEO win.
- **Confirm service list with Rodney** — site lists 3 services (Exterior / Interior / Color Consultation). The deleted backend's system prompt listed 6 (also Cabinet Refinishing, Deck & Fence Staining, Wall Repair / Prep). The gallery already shows cabinet work and deck work, so the site is currently undersell. Either expand the services section or confirm those aren't offered.
- **(Maybe)** Add a "Meet Rodney" moment. The testimonials name him 6+ times; the site never shows his face. Would need a photo. Flagged in Phase 2 critique but not actioned.
