# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML website for GrassRoots Crypto — a sole-trader crypto and AI education/consulting business. No frameworks, no build step. Vanilla HTML5 + CSS + JavaScript served via GitHub Pages at grassrootscrypto.io.

## Commands

```bash
# Lint & format (Trunk — wraps prettier, stylelint, eslint, actionlint, markdownlint, trufflehog)
trunk check --all
trunk fmt --all
```

There is no build step, test suite, or package manager. Pre-commit hooks run `trunk fmt`; pre-push runs `trunk check`.

## Architecture

**5 static HTML pages** with manually duplicated nav and footer:

- `index.html` — homepage (hero, services grid, about, contact form)
- `about.html`, `terms.html`, `disclaimer.html`, `privacy.html` — subpages

Any change to nav or footer must be applied to all 5 files.

**CSS** (`css/style.css`, `css/pages.css`):

- CSS variables for theming; dark mode via `[data-theme="dark"]` selectors
- Logo swap: `.logo-day` / `.logo-night` toggled by data-theme
- Colour palette from logo: navy `#163252`, blue `#0092ca`, green `#3daa78`, gold `#d4a643`
- Responsive breakpoints at 768px and 480px

**JS** (`js/main.js`):

- Single IIFE, no globals. Handles: dark mode toggle (localStorage `theme` key + `prefers-color-scheme`), sticky header shadow, mobile nav hamburger, fade-in via IntersectionObserver, Web3Forms contact form submission.

**Contact form** posts to Web3Forms API (`https://api.web3forms.com/submit`).

## CI/CD

- **`ci.yml`** — runs `trunk check --all` on pushes to main and PRs
- **`deploy.yml`** — deploys root directory to GitHub Pages on main push

## Formatting

Prettier: double quotes, semicolons, 2-space indent, 100 char print width, `htmlWhitespaceSensitivity: "ignore"`.

## Custom Skills

Four domain skills in `.claude/skills/` invocable via `/skill-name`:

- `/seo` — SEO audit (meta tags, Schema.org, GA4, sitemap)
- `/legal-review` — Australian legal compliance (evidence-based, must cite sources)
- `/content-review` — Voice/tone/grammar audit
- `/site-check` — Pre-deploy validation (trunk, nav/footer consistency, metadata)

## Key Rules

- **Voice:** First-person "I/my" throughout. Legal pages may use "GrassRoots Crypto" for formal statements.
- **Tone:** Professional, approachable, direct. Not corporate or AI-sounding. No waffle.
- **Legal changes require evidence** — cite a specific URL, government document, or legislation. No AI-generated "best practice".
- **Identity:** "Chris" publicly (no surname). "Chris GRC" is the handle. Don't publish unnecessary personal details.
- **Don't re-recommend rejected suggestions:** SA jurisdiction on terms, explicit refund policy, CBS regulator reference, "Adelaide, South Australia" in footer.
