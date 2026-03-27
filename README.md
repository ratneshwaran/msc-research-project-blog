# GitHub Pages starter for your MSc research blog post

This folder contains a ready-to-use **GitHub Pages + Jekyll** starter for your MSc research project write-up.

## Folder structure

```text
.
├── README.md
└── docs
    ├── _config.yml
    ├── _posts
    │   └── 2026-03-27-zero-shot-cell-annotation-cancer-single-cell.md
    ├── about.md
    ├── assets
    │   └── images
    └── index.md
```

## Fastest way to publish

1. Create a new GitHub repository.
2. Upload the contents of this folder to that repository.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, choose:
   - **Source:** Deploy from a branch
   - **Branch:** `main`
   - **Folder:** `/docs`
5. Save.
6. Wait for GitHub Pages to publish your site.

## What to edit first

- `docs/_config.yml`
  - Change the title
  - Replace `YOUR_GITHUB_USERNAME`
- `docs/about.md`
  - Add your bio
- `docs/_posts/2026-03-27-zero-shot-cell-annotation-cancer-single-cell.md`
  - Add repo links
  - Tighten the wording to match your personal style
  - Add or remove figures

## Optional: rename the post URL

Rename this file:

```text
docs/_posts/2026-03-27-zero-shot-cell-annotation-cancer-single-cell.md
```

Example:

```text
docs/_posts/2026-03-27-zero-shot-cancer-single-cell-foundation-models.md
```

## Optional: preview locally with Jekyll

If you want local previewing, install Ruby and Bundler, then add a `Gemfile` for GitHub Pages dependencies.

A simple starter `Gemfile` is:

```ruby
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins
```

Then run:

```bash
bundle install
bundle exec jekyll serve --source docs
```

## Notes

- The post already includes selected figures from your dissertation assets.
- The content is written in Markdown and uses standard Jekyll front matter.
- The site uses the supported `minima` theme for a clean research-blog look.
