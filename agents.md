++ 
# Agents Guide

## Project at a glance
- Hugo site using the **Congo** theme.
- Primary sections: `content/blog` (dev posts) and `content/portfolio` (case studies).
- Custom permalinks: `/blog/:slug/`, `/portfolio/:slug/`.

## Common commands
- Local preview: `hugo server -D` (live reload, serves drafts).
- Production build: `hugo --gc --minify`.

## Content conventions
- Homepage: `content/_index.md` uses `profile` and `button` shortcodes.
- Blog posts: place Markdown in `content/blog/`; use frontmatter `title`, `date`, `summary`, `tags`.
- Portfolio entries: place Markdown in `content/portfolio/`; include `summary` and tags.
- Avoid `content/posts/` unless you switch `mainSections`.

## Assets
- Author image path referenced in config: `assets/img/profile.jpg` (add your own image).

## Deployment
- Target: Cloudflare Workers (see `build.sh` and `wrangler.toml`).
