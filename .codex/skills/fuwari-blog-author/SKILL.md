---
name: fuwari-blog-author
description: Write and edit Fuwari Astro blog posts in Markdown/MDX. Use when creating or revising files under src/content/posts, choosing Fuwari frontmatter, using Fuwari extended Markdown features, Expressive Code blocks, admonitions, repository cards, spoilers, embedded videos, tags/categories, or draft handling.
---

# Fuwari Blog Author

## Workflow

1. Inspect nearby posts in `src/content/posts/` before writing, especially frontmatter shape, language, heading style, and category/tag conventions.
2. Create normal posts as `.md` files under `src/content/posts/`; use a subdirectory with `index.md` when the post has colocated assets such as `cover.jpeg`.
3. Use the frontmatter contract below. Keep values stable and explicit; do not invent extra fields unless the project schema already supports them.
4. Load only the reference needed for the requested feature:
   - `references/markdown.md`: baseline Markdown examples.
   - `references/markdown-extended.md`: GitHub repo cards, admonitions, GitHub callout syntax, spoilers.
   - `references/expressive-code.md`: code block titles, terminal/editor frames, line/text markers, diffs, word wrap, collapsible sections, line numbers.
   - `references/video.md`: YouTube/Bilibili iframe embeds.
   - `references/draft.md`: `draft: true` / `draft: false` behavior.
5. After editing project posts, run `ASTRO_TELEMETRY_DISABLED=1 pnpm check`. Run `ASTRO_TELEMETRY_DISABLED=1 pnpm build` when syntax highlighting, images, embedded HTML, or search/indexing may be affected.

## Frontmatter

Use this shape unless nearby posts establish a narrower convention:

```yaml
---
title: My First Blog Post
published: 2024-01-11
description: A short summary shown on the index page.
image: ./cover.jpg
tags: [Foo, Bar]
category: Front-end
draft: false
---
```

Rules:

- `title`, `published`, `tags`, `category`, and `draft` are the core fields.
- `description` should be short enough for card summaries.
- `image` can be an absolute URL, a `/public` path, or a path relative to the Markdown file.
- Use ISO timestamps only when the project or imported source needs time precision; date-only values are fine for ordinary posts.
- Set `draft: true` for unpublished work; draft posts should not be treated as visible content.

## Content Patterns

- Prefer fenced code blocks with an explicit language such as `ts`, `js`, `bash`, `c`, or `cpp`. Use `cpp`, not `C++`.
- Use Expressive Code annotations only when they help readers: `title="file.ts"`, `{1,4-6}`, `ins={3}`, `del={2}`, `wrap`, `showLineNumbers`, or `collapse={1-5}`.
- Use admonitions for callouts:

```markdown
:::note
Short note text.
:::
```

- Use GitHub syntax callouts when importing content that already uses them:

```markdown
> [!TIP]
> The GitHub syntax is supported.
```

- Use repository cards with `::github{repo="owner/repo"}`.
- Embed videos with iframe HTML only when the platform embed code is trusted and the post needs the player inline.

## Checks

- Confirm Markdown fences are closed.
- Confirm local image paths are correct relative to the Markdown file.
- Confirm headings do not duplicate the page title unnecessarily unless the source post intentionally includes that heading.
- Confirm imported code blocks use a supported language name for Expressive Code.
