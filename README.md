# Airdope Content

Content repository for the [Airdope](https://airdope.com) blog and guides.

## Structure

```
├── manifest.json          # Index of all posts and guides
├── blog/                  # Blog posts
│   ├── *.md              # Markdown files with frontmatter
│   └── images/           # Blog post images
├── guides/               # How-to guides
│   ├── *.md              # Markdown files with frontmatter
│   └── images/           # Guide images
```

## Adding Content

### Blog Post

1. Create a new `.md` file in `blog/`
2. Add frontmatter (see below)
3. Add an entry to `manifest.json` under `blog`
4. Commit and push — changes go live within 5 minutes

### Guide

1. Create a new `.md` file in `guides/`
2. Add frontmatter with `category` and `order` fields
3. Add an entry to `manifest.json` under `guides`
4. Commit and push

## Frontmatter

### Blog

```yaml
---
title: "Post Title"
slug: "post-slug"
excerpt: "Short description for cards and SEO"
coverImage: "blog/images/cover.jpg"    # optional, relative to repo root
date: "2026-02-18"
author:
  name: "Author Name"
tags: ["tag1", "tag2"]
published: true
---
```

### Guide

Same as blog, plus:

```yaml
category: "Getting Started"
order: 1
```

## Images

Place images in the relevant `images/` directory and reference them with a relative path from the repo root in the `coverImage` frontmatter field, or use standard markdown image syntax in the body.
