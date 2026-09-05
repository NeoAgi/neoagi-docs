# neoagi-docs

Documentation content for [docs.neoagi.com](https://docs.neoagi.com). Plain
Markdown/MDX, open to public PRs.

This repo is **content only** — no site build, no theme, no deploy pipeline.

## Structure

Content lives under `src/content/docs/`, and will be pulled in to the hsoted Astro/Starlight 
frame provided by an internal repository.  Top level sidebar groups must be configured outside 
of this repository.

```
src/content/docs/
├── applications/         # end-user product docs (InContext, Kept, ...)
├── developer-guides/     # integration guides, API usage, SDK docs
└── changelog/            # release notes
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


