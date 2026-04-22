# Repository Guidelines

## Project Structure & Module Organization
This repository is a small Jekyll site for GitHub Pages. Root Markdown files such as `index.md` and `about.md` define pages. Posts live in `_posts/` and should use `YYYY-MM-DD-title.md`. Shared HTML overrides go in `_includes/`. Site settings live in `_config.yml`. Do not edit generated output in `_site/` or vendored files in `vendor/`.

## Build, Test, and Development Commands
Use the Ruby version specified in `.ruby-version` before running Bundler or Jekyll commands. Install dependencies with `bundle install`. Run locally with `bundle exec jekyll serve`. Validate changes with `bundle exec jekyll build`; this is the main check for broken config, front matter, and Liquid templates. Update `Gemfile.lock` through Bundler, not by hand.

## Coding Style & Naming Conventions
Use Markdown with valid YAML front matter. Keep filenames lowercase with hyphens. Follow existing Jekyll keys such as `layout`, `title`, and `permalink`. In `_includes/`, prefer small, semantic HTML changes that stay compatible with the `minima` remote theme.

## Testing Guidelines
There is no dedicated test suite. Treat `bundle exec jekyll build` as the required pre-PR check. For content edits, verify links, headings, and code fences in the local site. For new posts, double-check the filename and front matter before committing.

## Security & Configuration Tips
Do not commit secrets or machine-specific settings. `_config.yml` is public and should contain only site-safe metadata. When changing gems, prefer versions supported by `github-pages` to avoid deploy issues.
