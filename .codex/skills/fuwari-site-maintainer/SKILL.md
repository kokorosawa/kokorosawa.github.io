---
name: fuwari-site-maintainer
description: Maintain and customize a Fuwari Astro blog project. Use when changing Fuwari site config, profile/avatar/nav settings, post organization, frontmatter conventions, cover images, local pnpm check/build/preview flows, Pagefind search behavior, GitHub Pages/static output, or when migrating content into src/content/posts.
---

# Fuwari Site Maintainer

## Workflow

1. Inspect the current project before editing. Prefer local conventions over generic Fuwari assumptions.
2. Use `src/config.ts` for site/profile/nav/social settings, `astro.config.mjs` for Astro/site/base integrations, and `src/content/posts/` for content.
3. Read `references/simple-guides-for-fuwari.md` when the task concerns original Fuwari post frontmatter, cover-image paths, or where posts/assets should live.
4. Keep changes scoped to the user request. Do not refactor theme internals unless the request or a verified build failure requires it.
5. Validate with:

```bash
ASTRO_TELEMETRY_DISABLED=1 pnpm check
ASTRO_TELEMETRY_DISABLED=1 pnpm build
```

Run `pnpm preview` after `pnpm build` when verifying search or static output behavior.

## Project Conventions

- Package manager: `pnpm`.
- Posts live under `src/content/posts/`.
- A simple post can be `src/content/posts/name.md`.
- A post with colocated assets should use a directory:

```text
src/content/posts/post-name/
├── cover.png
└── index.md
```

- Use project-local assets for durable personal content. External images are acceptable only when the post intentionally references a remote source.
- Search in Fuwari development mode can show fake/demo results. Use `pnpm build` followed by `pnpm preview` to verify real Pagefind search output.

## Frontmatter Contract

Use Fuwari-compatible frontmatter unless the existing content schema has been changed:

```yaml
---
title: My First Blog Post
published: 2024-01-11
description: A short summary shown on cards and feeds.
image: ./cover.jpg
tags: [Foo, Bar]
category: Front-end
draft: false
---
```

Field notes:

- `title`: post title shown on cards and detail pages.
- `published`: date or ISO timestamp.
- `description`: short summary for index/search surfaces.
- `image`: URL, `/public` path, or Markdown-relative path.
- `tags`: array of tags.
- `category`: one category string.
- `draft`: `true` hides the post from normal published views.

## Migration Notes

- Preserve meaningful source dates when migrating posts; if source commit time is requested, use the source repository's commit timestamp for each file.
- Normalize unsupported code fence language names before build, for example use `cpp` instead of `C++`.
- Keep original prose unless the user asks for rewriting.
- When importing posts from another repo, add category/tags consistently and verify the generated routes during `pnpm build`.

## Verification

- `pnpm check` catches Astro/content schema and type issues.
- `pnpm build` catches Markdown, syntax highlighting, static route, image, sitemap, and Pagefind issues.
- Use `pnpm preview --host 127.0.0.1 --port <port>` for built-site browser QA.
- If a local port is already in use, choose another port instead of stopping unrelated processes.
