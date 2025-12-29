---
title: "Edge-rendered portfolio on Cloudflare Workers"
date: 2025-12-18
summary: "Hugo-driven portfolio deployed to Cloudflare Workers with automatic image optimization, fast cold starts, and zero-downtime releases."
draft: false
tags: ["cloudflare", "hugo", "edge"]
---

## Problem

Create a personal site that stays fast globally, avoids cold-start penalties, and supports content-driven updates without touching the deployment pipeline.

## Approach

- Built the site with Hugo for predictable static builds and low maintenance.
- Deployed to Cloudflare Workers with static asset caching, image WebP conversion, and cache-busting fingerprints.
- Wired CI to run `hugo --gc --minify`, smoke-test HTML, and push immutable assets to Workers KV.
- Added rollback-friendly release channels with atomic `wrangler` deploys.

## Stack

- Hugo (Congo theme), Tailwind-derived styling
- Cloudflare Workers + KV, Cloudflare Images
- GitHub Actions for build + deploy

## Outcome

- <100ms TTFB globally and sub-1s LCP for image-heavy pages.
- One-command content releases with automatic cache invalidation.
- Error budget tracking via durable logs and request tracing.
