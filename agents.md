++ 
# Agents Guide

## Project at a glance
- Hugo site using the **Congo** theme.
- Primary sections: `content/blog` (posts) and `content/projects` (selected work); `mainSections` set to `blog`.
- Key pages: `content/_index.md` (home), `content/projects/_index.md` (projects list), `content/about.md` (about), `content/contact.md` (contact), and `content/speaking.md` (speaking).
- Custom permalinks: `/blog/:slug/`, `/projects/:slug/`, `/contact/:slug/`.
- Legacy path: `/portfolio/` is supported via an alias on the projects section.

## Common commands
- Local preview: `hugo server -D` (live reload, serves drafts).
- Production build: `hugo --gc --minify` (also used in `build.sh` for Cloudflare Workers).

## Content conventions
- Homepage: `content/_index.md` uses `profile` and `button` shortcodes.
- Blog posts: place Markdown in `content/blog/`; use frontmatter `title`, `date`, `summary`, `tags`.
- Projects entries: place Markdown in `content/projects/`; include `summary`, `role`, `tags`, `impact`, and `weight` (plus optional links).
- Avoid `content/posts/` unless you switch `mainSections`.
- Disable page TOC with `showTableOfContents: false` in frontmatter (defaults to true via params).

## Writing style
- Avoid contractions and other short forms. Use full forms instead (examples: `I am`, `I have`, `you are`, `cannot`, `will not`).
- Do not use `-` for sentence structure (avoid `space-hyphen-space` as a dash). Rewrite the sentence or use punctuation such as `:`, `;`, parentheses, or `—`.
- Minimize hyphens in prose. Keep `-` only where required (Markdown/frontmatter structure, URLs, file paths, code identifiers, tags, and proper names).
- Use only straight quotes: `'` and `"`. Do not use curly (smart) quotes.

## Assets
- Headshot served from `static/headshot.jpg`; `params.author.image` expects `img/profile.jpg` if you add an assets pipeline image.

## Deployment
- Target: Cloudflare Workers (see `build.sh` and `wrangler.toml`).
