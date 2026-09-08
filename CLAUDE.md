# CLAUDE.md — Agent instructions for 'site-unsolicitedadvice' website

Static site served by GitHub Pages at https://unsolicitedadvice.ai (custom
apex domain, HTTPS enforced). Built by Jekyll natively — GH Pages runs the
build, no CI or Gemfile needed. Simple content edits (typo, new link, add a
paragraph) can land directly on main. If you're touching structure, layouts,
or non-trivial CSS/JS, use a branch and write a quick test plan first.

## Design language

`fast` — Times New Roman, `#F0F0F0` page background, `#444` text,
W3Schools-derived topnav with `#4C8FCD` blue active state. All styling
lives in `fast.css`. Do not add a second stylesheet without a reason.

## Content model: guide collection

The site is a collection of evergreen how-to guides (e.g. "how to get
endorsed for arXiv", "how to apply to MATS"). Each guide is a standalone
page at `unsolicitedadvice.ai/<slug>/` so an individual guide can be
sent as a single link.

### To add a new guide

Drop a file at `_guides/<slug>.md` with front matter:

```
---
title: How to apply to MATS
category: applying
summary: Timeline, what mentors look for, and common mistakes.
---

### First section

Body markdown. Use `### ` for internal section headings (not `## `) so
the h1/h2 hierarchy stays clean — the site brand is the page's h1 and
the guide title is the page's h2.
```

It appears on the homepage automatically, grouped by `category`, sorted
by `title` within category. No other edits needed.

## File layout

- `_config.yml` — Jekyll config: custom `guides` collection with permalink `/:name/`, default layout `guide`
- `_layouts/default.html` — shared shell: head, brand h1, tagline, topnav
- `_layouts/guide.html` — extends default; wraps guide body in `<article>` with the title as h2
- `_guides/*.md` — individual guides (each becomes `/<slug>/`)
- `index.md` — homepage; categorized index generated from `_guides/` front matter
- `fast.css` — all styling
- `CNAME` — custom domain binding for GH Pages (`unsolicitedadvice.ai`)

## Known gaps (not-yet-scoped)

- Topnav has an About link (`/about/`) but no `about.md` yet — currently 404s
- No `robots.txt`, no sitemap, no favicon
- No local `jekyll serve` setup (no Gemfile); to preview before merging,
  either merge and view live, or `brew install ruby && bundle init && bundle add jekyll github-pages`
