# neoagi-docs

Documentation content for [docs.neoagi.com](https://docs.neoagi.com). Plain
Markdown/MDX, open to public PRs.

This repo is **content only** — no site build, no theme, no deploy pipeline.
The Astro/Starlight chrome and GitHub Actions deploy workflow live in
[NeoAgi/sites-docs.neoagi.com](https://github.com/NeoAgi/sites-docs.neoagi.com),
which pulls content from here at build time. See that repo's README for why
they're split (short version: once you accept public PRs, you don't want
contributors anywhere near a repo with deploy credentials).

## Structure

One top-level folder per site section — these map directly to the sidebar
groups in `sites-docs.neoagi.com/astro.config.mjs`:

```
documentation/       # end-user product docs (InContext, Kept, ...)
developer-guides/     # integration guides, API usage, SDK docs
changelog/            # release notes
```

Subfolders become nested/collapsible sidebar groups automatically. A folder
with an `index.md` gets its own landing page — give it
`sidebar: { label: Overview }` frontmatter so it doesn't show the same name
twice in the tree (once as the group header, once as its own link).

Every page needs Starlight-compatible frontmatter:

```md
---
title: Page Title
description: One line, used for <meta description> and search results.
---
```

## Branches

- **`main`** — where PRs land. Open one against this branch.
- **`release`** — what's actually live on docs.neoagi.com.
  `sites-docs.neoagi.com`'s deploy pulls from this branch specifically, not
  `main`, so merging a PR into `main` doesn't publish anything by itself —
  publishing is a separate, deliberate merge/fast-forward from `main` into
  `release`.

Both branches are meant to require review via CODEOWNERS before merging -
see `CODEOWNERS`. (Branch protection rules themselves are configured in the
repo's GitHub settings, not version-controlled here.)
