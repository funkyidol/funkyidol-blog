++ 
# Agents Guide

## Project at a glance
- Hugo site using the **Congo** theme.
- Primary sections: `content/blog` (posts) and `content/projects` (selected work); `mainSections` set to `blog`.
- Key pages: `content/_index.md` (home), `content/projects/_index.md` (projects list), `content/about.md` (about), `content/contact.md` (contact) and `content/speaking.md` (speaking).
- Custom permalinks: `/blog/:slug/`, `/projects/:slug/`, `/contact/:slug/`.
- Legacy path: `/portfolio/` is supported via an alias on the projects section.

## Common commands
- Local preview: `hugo server --navigateToChanged` (live reload, serves drafts).
- Compile Test: `hugo --gc --minify` (also used in `build.sh` for Cloudflare Workers).

## Content conventions
- Homepage: `content/_index.md` uses `profile` and `button` shortcodes.
- Blog posts: use page bundles at `content/blog/<slug>/index.md`; keep attached images in the same folder.
- Blog post frontmatter baseline: `title`, `date`, `summary`, `description`, `tags`, `feature`, `featureAlt`.
- For attached images, use local filenames in frontmatter and body image links.
- New blog posts: run `hugo new content/blog/<slug>/index.md` to use `archetypes/blog.md`.
- Projects entries: place Markdown in `content/projects/`; include `summary`, `role`, `tags`, `impact` and `weight` (plus optional links).
- Avoid `content/posts/` unless you switch `mainSections`.
- Disable page TOC with `showTableOfContents: false` in frontmatter (defaults to true via params).

## Blog writing and editing
- Use the repo local `blog-writing-editing` skill for any work on `content/blog` or any request to write, edit, update, review, tag, excerpt or maintain a blog post.
- Treat `docs/BLOG_WRITING_GUIDE_FOR_CODEX.md` as the source of truth for blog voice, structure, editing, evidence, bullets, maintenance and prose mechanics.

## Assets
- Headshot served from `static/headshot.jpg`; `params.author.image` expects `img/profile.jpg` if you add an assets pipeline image.

## Deployment
- Target: Cloudflare Workers (see `build.sh` and `wrangler.toml`).

## Test
Always run "compile test" after each edit.
