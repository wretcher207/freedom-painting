# Freedom Painting — gotchas

Things that took more than two attempts. Read before suggesting the same approach.

---

## Re-encoding already-optimized JPEGs makes them bigger

**What didn't work:**
- `sips -s format jpeg -s formatOptions 60..82 image.jpg`: every quality level produced a file *larger* than the source.
- `djpeg image.jpg | cjpeg -quality 78 ...`: same — output ~10% bigger than input.

**What worked:**
- `jpegtran -copy none -optimize -progressive image.jpg > out.jpg` (lossless): ~5–6% smaller, zero quality loss. Safe to bulk-apply.
- For the LCP-critical hero image specifically, dropping to `cjpeg -quality 65` saved an additional 14% on top of lossless — but only because the hero earns the tradeoff. Don't apply to gallery thumbnails.

**Note for next time:**
- The Freedom Painting source photos came out of the camera/export pipeline already well-tuned. Don't promise "30-50% savings" before running it on a sample first.
- Bulk re-encoding pipeline that's safe for any JPEG set: `jpegtran -optimize -progressive`. Anything more aggressive is per-image.
- macOS `sips` is NOT a competitive JPEG encoder. Use `jpegtran`/`cjpeg` from `jpeg-turbo` (`brew install jpeg-turbo`, already installed here).

---

## Chrome DevTools MCP `take_screenshot` times out on freshly-loaded pages

**What didn't work:**
- Calling `take_screenshot` immediately after `navigate_page` on the gallery section (50 lazy-loaded images) — `Page.captureScreenshot timed out` repeatedly.
- Increasing JPEG quality lower (70 → 65) didn't help; it's not an encode problem.

**What worked:**
- `sleep 3` (or 4 for gallery, 2 for hero) between navigate and screenshot. Lets lazy-loaded images settle.
- Even after settle, occasional spurious timeouts; just retry once more.

**Note for next time:**
- Standard recipe: `navigate_page` → `Bash sleep 3` → `take_screenshot`. Don't promise instant after-shots in a busy gallery page.
- Full-page screenshots (`fullPage: true`) timed out reliably on the gallery. Take viewport screenshots per anchor instead.

---

## Chrome DevTools MCP window resize fails when window is maximized

**What didn't work:**
- `resize_page(390, 844)` on a maximized Chrome window → `Restore window to normal state before setting content size`.

**What worked:**
- `emulate({viewport: "390x844x3,mobile,touch"})` for mobile device emulation instead. Better anyway — gives a real mobile UA, DPR, touch flags.

**Note for next time:**
- Default to `emulate` for viewport changes, not `resize_page`. The latter only works with a normal-state window.
