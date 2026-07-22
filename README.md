# funkyidol-blog

Hugo site using the Congo theme. Built and deployed to Cloudflare Workers.

## Quick commands

Preview locally:

```sh
hugo server --navigateToChanged
```

Build for production:

```sh
hugo --gc --minify
```

## Create a new blog post

Run the helper script from the repository root:

```sh
scripts/new-post <slug>
```

Example:

```sh
scripts/new-post learning-hugo-content-structure
```

This creates a leaf bundle at `content/blog/YYYY/MM/<slug>/index.md` using today's date and the `archetypes/blog/index.md` template. To backfill an older post, pass the date explicitly:

```sh
scripts/new-post learning-hugo-content-structure 2026-06-30
```

The generated frontmatter includes a `feature` field. If the post does not use a feature image, remove that field from the frontmatter.

### Feature images

Congo reads feature images as page resources. Place the image file inside the same bundle folder as `index.md`, then reference it by filename only in frontmatter:

```yaml
feature: "my-image.png"
featureAlt: "Descriptive alt text"
```

## Content structure

- `content/blog/YYYY/MM/<slug>/index.md` — blog posts as dated leaf bundles
- `content/projects/` — project pages
- `content/about.md` — about page
- `content/contact.md` — contact page
- `content/speaking.md` — speaking page
- `content/tools.md` — tools page

Blog public URLs are controlled by the Hugo permalink rule `/blog/:slug/`, so the dated folder structure is for repository organization and should not be used to build public links.

## Deployment

See `build.sh` and `wrangler.toml` for Cloudflare Workers deployment configuration.
