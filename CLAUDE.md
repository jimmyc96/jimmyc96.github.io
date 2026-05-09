# CLAUDE.md

This file gives Claude Code the full context to reconstruct a personal academic homepage in the same visual style as the reference site `https://jimmyc96.github.io/` (source: `https://github.com/jimmyc96/jimmyc96.github.io`).

---

## 1. Project Goal

Build a **personal academic homepage** that:

1. Visually matches the reference site (the GitHub Pages "minimal" theme — sidebar on the left with name + photo + links, content on the right).
2. Deploys cleanly on **GitHub Pages with zero custom build setup** (just push to `main` / `master` and enable Pages).
3. Keeps the **main page content in Markdown** (`index.md`) so the user can edit text easily without touching HTML/CSS.
4. Supports **inline images** in the Markdown — specifically small university / affiliation logos that sit next to the corresponding text.

Non-goals: no React, no Next.js, no Hugo, no Node build step, no JavaScript framework. Stay simple.

---

## 2. Technology Choice (do not deviate)

Use **Jekyll with the `jekyll-theme-minimal` remote theme**. This is the same theme the reference site uses and it is one of the GitHub Pages supported themes, so GitHub Pages will build it automatically with no Actions workflow required.

Why this stack:
- GitHub Pages builds Jekyll natively — no CI needed.
- The `minimal` theme is a single-column-with-sidebar layout that already matches the reference look.
- Content lives in plain `.md` files; the theme handles all styling.
- Images are referenced with standard Markdown `![alt](path)` syntax.

Do NOT introduce: Bundler-only gems that aren't on the [GitHub Pages supported list](https://pages.github.com/versions/), npm, webpack, custom Gemfiles beyond what's needed for local preview.

---

## 3. Required Repository Structure

Create these files in the project root:

```
.
├── _config.yml          # Jekyll config — theme + site metadata
├── index.md             # MAIN PAGE — user edits this
├── another-page.md      # Optional secondary page (e.g. publications) — keep stub
├── assets/
│   └── img/
│       ├── profile.jpg  # placeholder profile photo (use a 1:1 square placeholder)
│       └── logos/
│           ├── university-a.png  # placeholder university logo 1
│           ├── university-b.png  # placeholder university logo 2
│           └── university-c.png  # placeholder university logo 3
├── README.md            # how to edit + how to deploy
└── .gitignore           # standard Jekyll ignores
```

Image placeholders: do not download real university logos (licensing). Generate simple square placeholder PNGs (e.g. solid color with the university initials in text) or commit transparent 1×1 PNGs and tell the user in README.md to replace them. Keep each placeholder small (≤ 50 KB).

---

## 4. File Contents

### 4.1 `_config.yml`

Mirror the reference site's minimal config. Keep it short — the user should be able to read every line.

```yaml
title: Your Name
logo: /assets/img/profile.jpg
description: Welcome to my homepage.
show_downloads: false
google_analytics:
theme: jekyll-theme-minimal
```

Notes:
- `title` appears as the big heading in the sidebar.
- `logo` is the photo shown under the name in the sidebar — keep it square, around 400×400 px.
- `theme: jekyll-theme-minimal` is the **supported** form for github.com/pages-themes/minimal on GitHub Pages. Do not use `remote_theme` for this — it is unnecessary because `jekyll-theme-minimal` is on the supported themes list.

### 4.2 `index.md`

This is the main page the user will edit. Use the structure below — it mirrors the reference site (greeting → about → education → experience), and it demonstrates how to insert university logos inline.

Use a small inline `<img>` tag (not pure Markdown) for the university logos so the height can be constrained — Markdown's `![](...)` doesn't allow sizing. This is the only HTML-in-Markdown the user needs to know about, and it's documented in README.md.

Template:

```markdown
---
layout: default
title: About Me
---

# Your Name

![Profile photo](/assets/img/profile.jpg)

Welcome to my homepage.

[View My GitHub Profile](https://github.com/your-username)

## About Me

I am Your Name. Write a short bio here — current role, advisors, research interests. You can include links like [your advisor](https://example.com/) inline.

You can reach me at your.email AT example.com.

## Education

<img src="/assets/img/logos/university-a.png" alt="University A logo" height="40" align="left" hspace="10"/>

**University A** (YYYY.M – YYYY.M)

- Degree, Major
- Honors / program details

<br clear="left"/>

<img src="/assets/img/logos/university-b.png" alt="University B logo" height="40" align="left" hspace="10"/>

**University B** (YYYY.M – YYYY.M)

- Degree, Major
- Honors / program details

<br clear="left"/>

## Experience

<img src="/assets/img/logos/university-c.png" alt="Affiliation logo" height="40" align="left" hspace="10"/>

**Postdoctoral Research Fellow** (YYYY.M – Now)

- Affiliation
- Working with Prof. Someone

<br clear="left"/>

---

© YYYY Your Name · All rights reserved
```

Two things to get right here:
- The `<img ... align="left" hspace="10"/>` followed later by `<br clear="left"/>` is the simplest way to float a small logo to the left of a block of text in the minimal theme without writing any CSS. It works inside Markdown because Jekyll passes raw HTML through.
- The YAML front matter (`layout: default`, `title: About Me`) at the top is required for the page title to render correctly.

### 4.3 `another-page.md`

Stub a secondary page so the "more pages" pattern is in place — the user can later use it for Publications, CV, etc.

```markdown
---
layout: default
title: Another Page
---

# Another page

This is a secondary page. You can use it for publications, a CV, or anything else.

[Back to Home](/)
```

### 4.4 `README.md`

Write a short README aimed at the **owner of the site** (not other developers). Cover:

1. **What this is** — one sentence.
2. **How to edit content** — open `index.md`, change text, commit, push. GitHub Pages will rebuild within a minute.
3. **How to change the profile photo** — replace `assets/img/profile.jpg`, keep the same filename or update `_config.yml`.
4. **How to add or change a university logo** — drop a PNG into `assets/img/logos/`, reference it in `index.md` with the `<img src="..." height="40" align="left" hspace="10"/>` pattern shown in the file.
5. **How to enable GitHub Pages** — Settings → Pages → Source: Deploy from a branch → `main` / `master`, folder `/ (root)`. Site will be at `https://<username>.github.io/`.
6. **Optional: previewing locally** — `bundle install && bundle exec jekyll serve` with a minimal Gemfile (`source "https://rubygems.org"` + `gem "github-pages", group: :jekyll_plugins`). Keep this section short and clearly marked as optional.

### 4.5 `.gitignore`

Standard Jekyll ignores:

```
_site/
.sass-cache/
.jekyll-cache/
.jekyll-metadata
vendor/
.bundle/
Gemfile.lock
.DS_Store
```

---

## 5. Style Fidelity Checklist

After building the project, the result should look like the reference site:

- [ ] Left sidebar contains: site title (large), profile photo, description, "View on GitHub" / download buttons (the theme renders these from `_config.yml` automatically).
- [ ] Right column contains the rendered Markdown of `index.md`.
- [ ] Headings use the theme's default sans-serif type scale — do not override.
- [ ] Profile photo appears once at the top of `index.md` (in addition to the sidebar — this matches the reference site's pattern of `![Logo](...)` near the top of `index.md`).
- [ ] University logos appear small (~40 px tall), to the left of the corresponding institution heading, with the text wrapping next to them.
- [ ] No custom CSS files, no `_sass/` overrides, no `_layouts/` overrides. The theme's defaults are the style.

If at any point you feel tempted to add custom CSS or a layout override to match the look more closely — stop. The minimal theme is *itself* the look. Just use it.

---

## 6. Things to Avoid

- Do not fork the upstream `pages-themes/minimal` repo wholesale (the reference site did this, but it pulls in `_layouts/`, `_sass/`, `script/`, `docs/`, `Gemfile`, `.travis.yml`, and a `.gemspec` that the user does not need). A clean theme-only install is easier for the user to maintain.
- Do not add a `Gemfile.lock` to the repo.
- Do not add `node_modules`, `package.json`, or any JS tooling.
- Do not write inline CSS in `index.md` beyond the `<img align hspace>` / `<br clear>` pattern shown.
- Do not embed university logos as base64. Keep them as separate files in `assets/img/logos/`.
- Do not commit copyrighted university logos in placeholders — generate plain placeholders and instruct the user to substitute.

---

## 7. Definition of Done

1. The project builds locally with `bundle exec jekyll serve` (if Ruby is available) and renders the home page with a sidebar + content layout.
2. `index.md` contains all four sections (Greeting / About / Education / Experience) with at least three university logo placeholders inline.
3. Pushing to a `<username>.github.io` repo with Pages enabled produces a working live site without any further configuration.
4. The user can edit `index.md` and see changes reflected after the next push, without ever opening an HTML or CSS file.
5. `README.md` walks the user through the four common edits (text, photo, logo, new page) in plain language.

When all four are true, the task is complete.
