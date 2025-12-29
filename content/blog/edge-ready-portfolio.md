---
title: "Shipping an edge-ready portfolio with Hugo + Cloudflare"
date: 2025-12-22
summary: "How I paired Hugo’s simplicity with Cloudflare Workers to keep a personal site fast, secure, and easy to ship."
draft: false
tags: ["hugo", "cloudflare", "performance"]
---

## Goals

- Ship a personal site that stays <1s LCP worldwide without heroic caching.
- Keep content updates decoupled from code releases.
- Avoid bespoke servers; lean on managed edge primitives.

## Architecture

- **Build:** `hugo --gc --minify` produces hashed assets and WebP images. Fingerprints become cache keys.
- **Edge:** Cloudflare Workers serve HTML from KV with stale-while-revalidate. Static assets are pinned in R2 with immutable caching.
- **Routing:** Pretty permalinks (`/blog/:slug/`, `/portfolio/:slug/`) plus auto-generated sitemap and RSS feed.
- **Observability:** Request logs ship to Durable Objects; Workers traces export to an OTLP collector.

## Developer experience

- `wrangler deploy` releases are atomic and reversible; feature branches get preview URLs.
- Search index is shipped as `index.json` for offline-friendly search UI.
- Appearance and search actions live in the header for quick navigation.

## What’s next

- Add image CDN rules for AVIF fallbacks.
- Push lighthouse budgets into CI so regressions block merges.
- Experiment with ISR-like partial rebuilds using Hugo build manifests.
