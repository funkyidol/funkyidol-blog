---
title: "Setting up Congo for a developer portfolio"
date: 2025-12-15
summary: "Practical defaults I use to turn the Congo Hugo theme into a clean portfolio + dev blog."
draft: false
tags: ["hugo", "theme", "dx"]
---

## Why Congo

Congo ships lean markup, dark-mode aware styles, and sensible typography. It also keeps customization simple through params files instead of bespoke layouts.

## Baseline configuration

- Enable search and code copy for developer-focused posts.
- Set `mainSections = ["blog"]` so the homepage recent posts pull from the blog section.
- Use `showTaxonomies = true` to surface tags for discovery.
- Add permalinks for `/blog/:slug/` and `/portfolio/:slug/` to keep URLs clean.

## Navigation

The header highlights **Portfolio**, **Blog**, and **About**, with search and a quick mail link for contact. Footer mirrors the main links for consistency.

## Content model

- `content/portfolio` for case studies with summaries that feed list pages.
- `content/blog` for articles; the homepage uses the built-in `recent-articles` partial.
- `content/_index.md` uses the `profile` and `button` shortcodes to set the hero and calls to action.

## Next steps

Add your own author image at `assets/img/profile.jpg`, wire analytics, and drop in production-ready CI for `hugo --gc --minify` so every publish stays fast and reliable.
