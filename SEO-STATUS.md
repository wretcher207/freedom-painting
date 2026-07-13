# Freedom Painting — SEO Status

> Last updated: 2026-07-13

## Completed

- Google Search Console verified and sitemap submitted
- LocalBusiness (HousePainter) structured data with 58 five-star reviews, services, service area
- Open Graph meta tags fixed (absolute URL for image, added og:url, og:site_name)
- Twitter card meta tags added
- Canonical tag added
- 60+ gallery image alt tags rewritten from generic "Completed project" to descriptive text
- robots.txt created
- sitemap.xml created
- **Favicon set added** (favicon-16x16.png, favicon-32x32.png, apple-touch-icon.png) — generated from Logo.jpg
- **Hero image preload** added with `fetchpriority="high"` (faster LCP)
- **`decoding="async"`** added to all 64 below-fold images
- **Lossless `jpegtran` pass** on all 80 images (728 KB / 5.7% saved)
- **Hero image recompressed** at quality 65 (284K → 244K, 14% smaller)
- **Accessibility fixes** to pass Lighthouse 100: bumped contrast on `.testimonial-date`, `.testimonial-source`, `.trust-text small`, and `.btn-facebook` background
- **Phase 1 simplify** (June 2026): deleted orphaned `minerva_production.py`, deduped testimonials, removed dead labels, modernized JS
- **Phase 2 design pass** (June 2026): stripped AI-grammar eyebrows + repeated badge chips, swapped service-card emoji circles for real Freedom Painting project photos

## Google Business Profile — EXISTS (verified 2026-07-13)

The old note here said GBP was never set up. That was wrong. Verified in-browser on
2026-07-13: **"Freedom Painting LLC Houlton, ME"** exists, David manages it
(profile manager view loads), category Painter, phone (207) 502-9970, website linked,
areas served "Houlton and nearby areas".

The GBP problems are different from what we thought, in priority order:

- [ ] **DUPLICATE LISTING.** A second "Freedom Painting LLC" (no reviews, same phone) shows
      in Businesses results alongside the managed one. Duplicates split ranking signals.
      Report as duplicate / request merge into the managed profile. **Highest leverage item.**
- [ ] **Only 1 Google review** vs 61 on Facebook. Google reviews are a top-3 local ranking
      factor; Facebook recommendations count for nothing. Use the profile's "Ask for reviews"
      link and have Rodney text it to past customers. **Fastest-moving lever.**
- [ ] **Profile Strength incomplete.** Google is prompting: complete info, add photos, add
      social profiles. 80 gallery photos exist on the site and almost none are on the profile.
- [ ] **Hours say "Open 24 hours"** — wrong and it reads as sloppy. Set real hours.
- [ ] **Name/NAP mismatch.** GBP = "Freedom Painting **LLC**", site = "Freedom Painting",
      Facebook = "**Hodgdon** ME" while site/GBP = Houlton. Google prints
      *"Missing: LLC | Show results with: LLC"* under the site result, i.e. it can't cleanly
      tie site to profile. Make the legal name + locality identical across site, schema,
      GBP, and Facebook.

## To Do (site)

- [ ] **Confirm service list with Rodney** — Site advertises 3 services (Exterior / Interior / Color Consultation). Earlier backend SYSTEM_PROMPT listed 6 (also Cabinet Refinishing, Deck & Fence Staining, Wall Repair). Evidence they DO these: gallery shows cabinet + deck work, and testimonials explicitly mention deck staining ("staining our old deck") and wall patching. Service pages are written and ready to ship once he confirms he sells them.
- [ ] **More location pages** — only Houlton shipped. Others need a real cited job in that town first; templated "painter in [town]" pages are doorway pages and Google penalizes them.
- [ ] **aggregateRating in homepage schema is self-serving** (58 hard-coded FB reviews). Not eligible for review rich results on a LocalBusiness and carries some policy risk. Real Google reviews are the fix.

## Site Info

- **URL:** https://freedompainting.us
- **Hosting:** Netlify (deploys from GitHub repo)
- **Repo:** https://github.com/wretcher207/freedom-painting.git
- **Tech:** Single-page static HTML site
- **Search Console:** Verified (URL prefix method)

## Lighthouse (mobile, June 2026)

| Category | Score |
|---|---|
| Accessibility | 100 (target) |
| Best Practices | 100 |
| SEO | 100 |

## Pages (as of 2026-07-13)

| URL | Schema |
|---|---|
| `/` | HousePainter |
| `/exterior-painting/` | Service + BreadcrumbList |
| `/interior-painting/` | Service + BreadcrumbList |
| `/house-painter-houlton-me/` | HousePainter + BreadcrumbList + FAQPage |

All four in `sitemap.xml`. Resubmit the sitemap in Search Console so the three new URLs get crawled.
