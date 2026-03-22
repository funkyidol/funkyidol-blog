# Blog page bundle migration plan

## Purpose
Define a safe bulk migration of blog posts to Congo page bundles, with a post tracker and strict validation gates. This plan is prepared for future execution.

## Scope
- Only `content/blog/` posts are in scope.
- Candidate set: markdown files under `content/blog/*.md`.
- Exclusions: `_index.md`, existing `index.md` bundles.
- Current candidates found: 14 posts.

## Post tracker
| ID | Phase | Source post | Target bundle path | Baseline permalink | FM image action | Status |
| --- | --- | --- | --- | --- | --- | --- |
| P01 | 1 | `content/blog/2026-new-year-keyboard-upgrade.md` | `content/blog/2026-new-year-keyboard-upgrade/index.md` | `/blog/2026-new-year-keyboard-upgrade/` | none | Planned |
| P02 | 1 | `content/blog/beyond-the-visuals-why-audio-ux-is-critical-in-android-xr-2pj2.md` | `content/blog/beyond-the-visuals-why-audio-ux-is-critical-in-android-xr-2pj2/index.md` | `/blog/beyond-the-visuals-why-audio-ux-is-critical-in-android-xr/` | none | Planned |
| P03 | 1 | `content/blog/dual-boosting-ubuntu-budgie-on-windows-laptop-4a55.md` | `content/blog/dual-boosting-ubuntu-budgie-on-windows-laptop-4a55/index.md` | `/blog/dual-booting-ubuntu-budgie-on-windows-laptop/` | none | Planned |
| P04 | 1 | `content/blog/effective-logging-in-production-with-firebase-crashlytics-m27.md` | `content/blog/effective-logging-in-production-with-firebase-crashlytics-m27/index.md` | `/blog/effective-logging-in-production-with-firebase-crashlytics/` | none | Planned |
| P05 | 1 | `content/blog/exploring-camerax-api-beta-part-2-image-analysis-1hha.md` | `content/blog/exploring-camerax-api-beta-part-2-image-analysis-1hha/index.md` | `/blog/exploring-camerax-api-beta-part-2-image-analysis/` | none | Planned |
| P06 | 2 | `content/blog/exploring-camerax-beta-release-part-1-19hh.md` | `content/blog/exploring-camerax-beta-release-part-1-19hh/index.md` | `/blog/exploring-camerax-beta-part-1-basic-setup/` | none | Planned |
| P07 | 2 | `content/blog/moving-away-from-gitflow-and-feature-branches-3cg0.md` | `content/blog/moving-away-from-gitflow-and-feature-branches-3cg0/index.md` | `/blog/moving-away-from-gitflow-and-feature-branches/` | none | Planned |
| P08 | 2 | `content/blog/novices-guide-to-dependency-injection--dagger2---part-1-ga5.md` | `content/blog/novices-guide-to-dependency-injection--dagger2---part-1-ga5/index.md` | `/blog/novices-guide-to-dependency-injection-dagger2-part-1-introduction/` | none | Planned |
| P09 | 2 | `content/blog/novices-guide-to-dependency-injection-dagger2-part-2-benefits-3gop.md` | `content/blog/novices-guide-to-dependency-injection-dagger2-part-2-benefits-3gop/index.md` | `/blog/novices-guide-to-dependency-injection-dagger2-part-2-benefits/` | none | Planned |
| P10 | 2 | `content/blog/why-becoming-staying-productive-in-india-is-difficult-3b27.md` | `content/blog/why-becoming-staying-productive-in-india-is-difficult-3b27/index.md` | `/blog/why-becoming-staying-productive-in-india-is-difficult/` | none | Planned |
| P11 | 3 | `content/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc.md` | `content/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/index.md` | `/blog/regolith-linux-my-descent-into-mouse-less-navigation/` | none | Planned |
| P12 | 3 | `content/blog/timber-logging-performance-improvements-in-production-56k7.md` | `content/blog/timber-logging-performance-improvements-in-production-56k7/index.md` | `/blog/android-logging-performance-improvements-in-production/` | none | Planned |
| P13 | 3 | `content/blog/Kimi 2.5 vs 5.2 Codex.md` | `content/blog/Kimi 2.5 vs 5.2 Codex/index.md` | `/blog/testing-kimi-k2.5-for-real-world-coding-work/` | rewrite `feature` to local filename, move image | Planned |
| P14 | 3 | `content/blog/deploying-multiple-picoclaw-instances-on-a-single-machine-with-docker.md` | `content/blog/deploying-multiple-picoclaw-instances-on-a-single-machine-with-docker/index.md` | `/blog/deploying-multiple-picoclaw-instances-on-a-single-machine-with-docker/` | rewrite `feature` to local filename, move image | Planned |

## Batch phases (5, 5, 4)
### Phase 1
`P01` to `P05`

### Phase 2
`P06` to `P10`

### Phase 3
`P11` to `P14`

## Migration rules
1. Keep body content byte for byte unchanged.
2. Preserve all front matter fields and format (YAML or TOML or JSON), except image path rewrites for `feature`, `cover`, `thumb`.
3. Rewrite only site relative front matter image paths (`/blog/...`) to local filename (`"file.ext"`) after move.
4. Keep `featureAlt` unchanged.
5. Use `git mv` where practical for markdown and assets.
6. Do not overwrite conflicts. Mark as skipped with reason.
7. Skip posts with missing referenced image files and report them.
8. Do not rewrite body `/blog/...` links.

## Permalink safety protocol
1. Capture baseline permalink map using `hugo list all` before migration.
2. After each phase, compare permalinks for migrated posts.
3. If a permalink changes, add minimal preserving field:
   - keep existing `slug` or `url` if present,
   - otherwise add only the minimum required field (`slug` preferred) to restore exact URL.

## Validation flow
### Gate A: Preflight
- Confirm candidate list and phase split.
- Validate parser support per file front matter format.
- Validate referenced front matter image existence.
- Detect destination path and filename conflicts.

### Gate B: Per post structural validation
- `content/blog/<basename>/index.md` exists.
- original `content/blog/<basename>.md` no longer exists.
- rewritten `feature` or `cover` or `thumb` no longer uses `/blog/...`.
- referenced front matter image exists in same bundle folder.

### Gate C: Per post integrity validation
- front matter keys preserved except approved image adjustments and permalink preservation keys.
- body hash unchanged.
- moved assets counted exactly once unless explicit compatibility duplicate is required.

### Gate D: Per phase site validation
- run compile test: `hugo --gc --minify`
- collect and resolve content errors before next phase.

### Gate E: Final validation
- full tracker status resolved (`Done` or `Skipped`).
- compile test passes.
- final migration report assembled.

## Deliverables at execution time
1. migrated content in page bundle structure.
2. concise summary:
   - posts migrated
   - posts skipped
   - images moved
   - permalink preservation fields added
3. skipped list with reasons.
4. two to three before and after examples.

## Expected preflight notes from current repo state
- front matter `/blog/...` feature rewrites currently expected for 2 posts (`P13`, `P14`).
- no missing front matter image files detected during planning.
- permalink preservation checks remain mandatory during execution.

## Complete original migration instruction

Migrate all Hugo blog posts in this repo to Congo's recommended page bundle structure for article images.

### Goal
- Convert existing posts that use standalone Markdown files plus image paths in front matter
- Move each post into its own leaf bundle folder with `index.md`
- Move the referenced feature image into that same folder
- Rewrite front matter so Congo uses page resources instead of site relative paths
- Preserve slug, URL behavior, dates, tags, and all content

### Target structure
- From patterns like:
  - `content/blog/my-post.md`
  - image referenced as `/blog/my-post/my-image.png`
- To:
  - `content/blog/my-post/index.md`
  - `content/blog/my-post/my-image.png`

### Why
- Congo expects `feature`, `cover`, and `thumb` images to be page resources in the article bundle
- `feature` should point to the local filename, not a site relative `/blog/...` path

### Rules
1. Only process posts under `content/blog/`
2. Only migrate posts that are regular Markdown files, not already bundled as `index.md` or `_index.md`
3. Preserve the post body exactly
4. Preserve all front matter fields except the image path adjustments described below
5. Preserve git history as much as possible by using `git mv` where practical
6. Do not change permalinks unintentionally
7. Skip posts where the referenced image file cannot be found; report them separately
8. Produce a migration report at the end

### Detailed migration behavior

For each post file under `content/blog/**/*.md`:
- Ignore `_index.md`
- Ignore files already named `index.md`
- Determine the post basename from the filename
  - Example: `content/blog/testing-kimi-k2-5.md` → basename `testing-kimi-k2-5`
- Create a folder with the same basename beside the file
  - `content/blog/testing-kimi-k2-5/`
- Move the markdown file into that folder as `index.md`

### Front matter changes
- If front matter contains:
  - `feature: /blog/some-folder/image.png`
  - rewrite to:
  - `feature: "image.png"`
- Keep `featureAlt` unchanged
- If `cover` or `thumb` exist and use similar `/blog/...` paths, also rewrite them to just the filename if the file is moved into the bundle
- Do not invent new front matter fields unless needed for permalink preservation

### Image move behavior
- If `feature` contains a site relative path like `/blog/foo/bar.png`
  - locate the corresponding file in the repo
  - move that image into the new bundle folder
  - rewrite front matter value to the image filename only
- If multiple image fields point to different files, move all referenced files into the bundle folder
- If the source image is already inside the target folder, only rewrite front matter
- Do not overwrite files silently; if name conflicts happen, report them

### Permalink safety
- We must preserve the public URL of each post
- Before changing anything, inspect the site's current content organization
- If posts currently derive URLs from filenames and the move to `index.md` would change URLs, add explicit front matter to preserve them
- Preferred approach:
  - preserve the existing slug or URL exactly
  - if a post already has `slug`, keep it
  - if it already has `url`, keep it
  - if neither exists and moving to a bundle could change output URL, add whichever minimal field is required to preserve the current URL
- Do not guess; verify by checking current Hugo conventions in this repo's structure

### Validation
After migration:
1. Verify every migrated post now exists as:
   - `content/blog/<post-name>/index.md`
2. Verify every rewritten `feature` field points only to a local filename, not `/blog/...`
3. Verify the referenced file exists inside the same folder as `index.md`
4. Verify no Markdown content was lost
5. Verify no duplicate copies of moved images remain unless necessary
6. If there is a local Hugo build command in the repo, run it and report any content errors
7. Report all skipped posts and why they were skipped

### Edge cases
- If a post has no `feature`, leave it alone except for bundling if required by the migration scope
- If a post already lives in a bundle folder but uses `/blog/...` in front matter, only rewrite the front matter and move missing referenced assets into the bundle if needed
- If a post references images in the body using absolute `/blog/...` paths, do not rewrite those unless explicitly requested
- If front matter is TOML or JSON instead of YAML, preserve the original format
- Preserve quote style where practical, but correctness matters more than formatting fidelity

### Deliverables
1. Apply the migration
2. Provide a concise summary including:
   - number of posts migrated
   - number of posts skipped
   - number of images moved
   - any permalink preservation fields added
3. List skipped files with reasons
4. Show 2 to 3 representative before and after examples

### Example transformation

Before:
- `content/blog/testing-kimi-k2-5.md`

Front matter:

```yaml
---
title: Testing Kimi K2.5 for Real-World Coding Work
date: 2026-01-29
description: Hands-on notes from evaluating Moonshot AI's Kimi K2.5 with Factory Droid, and how it compares to GPT-5.2 Codex for everyday engineering tasks.
tags:
  - ai
  - llms
feature: /blog/kimi2.5-vs-5.2codex/kimi2.5-vs5.2codex.png
featureAlt: "Engineer comparing Kimi K2.5 and GPT-5.2 Codex side by side"
---
```

After:

- `content/blog/testing-kimi-k2-5/index.md`
- `content/blog/testing-kimi-k2-5/kimi2.5-vs5.2codex.png`

Front matter:

```yaml
---
title: Testing Kimi K2.5 for Real-World Coding Work
date: 2026-01-29
description: Hands-on notes from evaluating Moonshot AI's Kimi K2.5 with Factory Droid, and how it compares to GPT-5.2 Codex for everyday engineering tasks.
tags:
  - ai
  - llms
feature: "kimi2.5-vs5.2codex.png"
featureAlt: "Engineer comparing Kimi K2.5 and GPT-5.2 Codex side by side"
---
```

### Implementation notes

- Prefer a scripted migration over manual edits
- Use a front matter parser rather than regex only editing where possible
- Use `git mv` for file moves
- Make changes in one commit with a message like:
  - `migrate blog posts to Congo page bundles`

Do not ask for confirmation. Inspect the repo, perform the migration safely, and present the report.
