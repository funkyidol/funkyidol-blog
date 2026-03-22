# Post Discrepency Log

## Batch 1: Newest 3 posts

### 2026 New Year Keyboard Upgrade
- Source: https://dev.to/funkyidol/2026-new-year-keyboard-upgrade-ng3
- Hugo: content/blog/2026-new-year-keyboard-upgrade.md
- Issues:
  - Date mismatch: dev publish date 2026-01-27, Hugo frontmatter date 2026-01-07.
  - Tags mismatch: dev tags keyboards, miryoku, engonomic; Hugo tags keyboards, ergonomics, miryoku, workman-layout, mechanical-keyboards, ergonomic-keyboard.
  - Canonical URL missing in Hugo frontmatter. Dev canonical URL is https://funkyidol.in/blog/2026-new-year-keyboard-upgrade/.
  - Summary mismatch: dev description does not match Hugo summary and description fields.
  - Summary typo: Ptron36 should be Pteron36.
  - Image alt text mismatch: dev uses "Photo of dismantled keys", "Closeup of sculpted keycaps", "Completed keyboard"; Hugo uses "Alt Text" and "AltText".
  - Image source mismatch: dev uses dev.to hosted images; Hugo uses local images at /blog/2026-keyboard-upgrade/image1.jpeg, image2.jpeg, image3.jpeg. Files exist in static.

### Beyond the Visuals: Why Audio UX is Critical in Android XR
- Source: https://dev.to/funkyidol/beyond-the-visuals-why-audio-ux-is-critical-in-android-xr-2pj2
- Hugo: content/blog/beyond-the-visuals-why-audio-ux-is-critical-in-android-xr-2pj2.md
- Issues:
  - Content is not a verbatim match. Copy edits remove contractions and reduce hyphenation. Examples: "It's" to "It is", "daily-driver" to "daily driver", "Don't" to "Do not", "Non-Verbal" to "Nonverbal", "head-worn" to "head worn", "what's" to "what is".
  - No images on dev or Hugo.

### Moving Away from Gitflow and Feature Branches
- Source: https://dev.to/funkyidol/moving-away-from-gitflow-and-feature-branches-3cg0
- Hugo: content/blog/moving-away-from-gitflow-and-feature-branches-3cg0.md
- Status: No discrepancies found for content, tags, canonical URL, or images.

## Batch 2: Next 3 posts

### Android Logging Performance Improvements in Production
- Source: https://dev.to/funkyidol/timber-logging-performance-improvements-in-production-56k7
- Hugo: content/blog/timber-logging-performance-improvements-in-production-56k7.md
- Status: No discrepancies found for content, tags, canonical URL, or images.

### Exploring CameraX API Beta (Part -2): Image Analysis
- Source: https://dev.to/funkyidol/exploring-camerax-api-beta-part-2-image-analysis-1hha
- Hugo: content/blog/exploring-camerax-api-beta-part-2-image-analysis-1hha.md
- Issues:
  - Body content mismatch for dev embed references. Dev uses `{% post https://dev.to/funkyidol/exploring-camerax-beta-release-part-1-19hh %}`; Hugo uses a local link.
  - Dev uses a GitHub embed `{% github https://github.com/funkyidol/CameraXSample no-readme %}`; Hugo uses a plain link.
  - Cover image present on dev (`cover_image`) is not represented in Hugo frontmatter.

### Exploring CameraX Beta (Part - 1): Basic Setup
- Source: https://dev.to/funkyidol/exploring-camerax-beta-release-part-1-19hh
- Hugo: content/blog/exploring-camerax-beta-release-part-1-19hh.md
- Issues:
  - Content match not fully verified. Dev API response did not include `body_markdown`, only `body_html`.
  - Cover image present on dev (`cover_image`) is not represented in Hugo frontmatter.

## Batch 3: Next 3 posts

### Regolith Linux - My descent into Mouse-less navigation
- Source: https://dev.to/funkyidol/regolith-linux-my-descent-into-mouse-less-navigation-17dc
- Hugo: content/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc.md
- Issues:
  - Content match not fully verified. Dev API response did not include `body_markdown`, only `body_html`.
  - Image source mismatch: dev uses dev.to CDN links; Hugo uses a mix of external regolith URLs and local images under `/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/`. Local files exist in static.

### Effective logging in Production with Firebase Crashlytics
- Source: https://dev.to/funkyidol/effective-logging-in-production-with-firebase-crashlytics-m27
- Hugo: content/blog/effective-logging-in-production-with-firebase-crashlytics-m27.md
- Status: No discrepancies found for content, tags, canonical URL, or images.

### Dual booting Ubuntu Budgie on Windows laptop
- Source: https://dev.to/funkyidol/dual-boosting-ubuntu-budgie-on-windows-laptop-4a55
- Hugo: content/blog/dual-boosting-ubuntu-budgie-on-windows-laptop-4a55.md
- Issues:
  - Cover image present on dev (`cover_image`) is not represented in Hugo frontmatter.

## Batch 4: Next 3 posts

### Why becoming & staying productive in India is difficult
- Source: https://dev.to/funkyidol/why-becoming-staying-productive-in-india-is-difficult-3b27
- Hugo: content/blog/why-becoming-staying-productive-in-india-is-difficult-3b27.md
- Issues:
  - Cover image present on dev (`cover_image`) is not represented in Hugo frontmatter.

### Novices guide to Dependency Injection & Dagger2 - Part 2 - Benefits
- Source: https://dev.to/funkyidol/novices-guide-to-dependency-injection-dagger2-part-2-benefits-3gop
- Hugo: content/blog/novices-guide-to-dependency-injection-dagger2-part-2-benefits-3gop.md
- Issues:
  - Body content mismatch for dev embed reference. Dev uses `{% link https://dev.to/funkyidol/novices-guide-to-dependency-injection--dagger2---part-1-ga5 %}`; Hugo uses a local link.
  - Dev renders a link card with image for the Part 1 reference. Hugo uses a plain link, so the card image is missing.

### Novices guide to Dependency Injection & Dagger2 - Part 1 - Introduction
- Source: https://dev.to/funkyidol/novices-guide-to-dependency-injection--dagger2---part-1-ga5
- Hugo: content/blog/novices-guide-to-dependency-injection--dagger2---part-1-ga5.md
- Status: No discrepancies found for content, tags, canonical URL, or images.
