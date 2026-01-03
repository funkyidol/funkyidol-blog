++ 
# Agents Guide

## Project at a glance
- Hugo site using the **Congo** theme.
- Primary sections: `content/blog` (dev posts) and `content/portfolio` (case studies); `mainSections` set to `blog`.
- Key pages: `content/_index.md` (home) and `content/about.md` (about).
- Custom permalinks: `/blog/:slug/`, `/portfolio/:slug/`.

## Common commands
- Local preview: `hugo server -D` (live reload, serves drafts).
- Production build: `hugo --gc --minify` (also used in `build.sh` for Cloudflare Workers).

## Content conventions
- Homepage: `content/_index.md` uses `profile` and `button` shortcodes.
- Blog posts: place Markdown in `content/blog/`; use frontmatter `title`, `date`, `summary`, `tags`.
- Portfolio entries: place Markdown in `content/portfolio/`; include `summary` and tags.
- Avoid `content/posts/` unless you switch `mainSections`.
- Disable page TOC with `showTableOfContents: false` in frontmatter (defaults to true via params).

## Assets
- Headshot served from `static/headshot.jpg`; `params.author.image` expects `img/profile.jpg` if you add an assets pipeline image.

## Deployment
- Target: Cloudflare Workers (see `build.sh` and `wrangler.toml`).
