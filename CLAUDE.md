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
- Brand palette: navy `#011936`, dark grey `#465362`, teal `#3fa17a`, gold `#ef9200`, light gold `#eeb913`, blue `#0092ca`
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

## TODO: Services & Positioning Refresh

Small, incremental updates. Do one at a time, get approval before moving to the next. Upload business card for reference before starting — align website messaging with card.

- [x] **1. Hero text** — Done. H1: "Education & Consulting in Crypto and AI" (matches business card). Subtitle: added "custom solutions" as third pillar. Services intro updated to match.
- [x] **2. Service cards — sharpen copy** — Outcome language on consulting/solutions cards ("I'll analyse your workflow and show you where AI saves you time"). Consolidate or clarify the AI-Powered Development / Hosted Custom Builds overlap. Add data migration / system integration as explicit offering.
- [x] **3. About section text** — Add a sentence about consulting/solutions alongside education. Currently reads as education-only ("I educate").
- [x] **4. Contact form dropdown** — Update options to match whatever the service cards become.
- [ ] **5. Bitcoin Payment page** — New `pay.html` with custom amount input, submits to BTCPay POS (`https://btcpay.grchomelab.xyz/apps/2g92S5VisCayAiJ7vP3bC6D6jzji/pos`). Add "Pay" link to nav (all 6 HTML files). Purpose: accept Bitcoin payments + get listed on Bitcoin business directories.
- [ ] **6. Meta / Schema.org** — Update `description` meta tags and `serviceType` array to reflect the broader offering including Bitcoin payments. Do this last, after all content changes land.

### Brief

Next time this site is worked on, review and update the services section and overall messaging. Here is the brief:

### Current reality (2026)

- AI-augmented technology consultant — uses AI tools to deliver work faster and more thoroughly than traditional approaches
- Core value: understands business AND technology, directs AI to execute at speed
- Three pillars:
  1. **Education** — Crypto and AI education (individuals, businesses, universities)
  2. **Consulting** — Business process analysis, AI integration strategy, workflow optimisation, data migration planning
  3. **Solutions** — Custom applications, data migrations, system integrations, hosted tools — built fast with AI-accelerated delivery

### Go-to-market strategy

- **Education is the entry point** — gets brand awareness, gets in front of clients, builds credibility. Education IS the upsell of AI capability because the education itself is delivered using AI tools and a custom-built platform.
- **The ai-dashboard IS the portfolio piece** — a full production app (SvelteKit, ECharts, slide presenter, live data) built entirely with AI. Screenshot polished slides and sessions for the website once ready. This proves both education quality AND build capability.
- **Three planned free engagements for case studies:**
  1. Local community centre — education session
  2. NGO/non-profit — education or consulting
  3. Small business — website build or business optimisation (custom solution)
- These produce testimonials and real proof of delivery across all three pillars
- **Crypto + AI intersection consulting** — a niche where Chris has deep expertise that most AI consultants lack

### What needs updating on the site

**Hero:**

- Do not drop education — expand: "Crypto and AI Education, Consulting and Custom Solutions" or similar
- Subtitle should mention all three pillars, not just education

**Services grid (6 cards):**

- Keep all cards but sharpen consulting and solutions with outcome language
- "I will analyse your workflow and show you where AI saves you time" not "workflow audit and AI opportunity mapping"
- Each solution card should tie back: "Built with the same approach I use for client work"
- Add data migration / system integration as explicit offering
- "AI-Powered Development" and "Hosted Custom Builds" overlap — consolidate or clarify
- Contact form dropdown must match whatever the services become

**About page:**

- Keep THORChain history, YouTube videos, AI tools list — this is proof of being real, not a fly-by-night AI consultant
- 5+ years of content creation and infrastructure work IS the differentiator
- "AI Tools I Use" — reframe from "here is my toolkit" to "I use these daily and know which to reach for depending on what you need"
- Add a paragraph about what is being built NOW (the dashboard, the infrastructure, the consulting toolkit)
- Once case studies land, add a "Recent Work" section with testimonials
- Do not remove achievements — they prove depth. Expand with consulting/solutions work as it happens.

**Schema.org / meta:**

- serviceType array needs to match new services
- Meta descriptions should reflect consulting/solutions, not just education
- Update after content changes land

### Key positioning notes

- **Do not oversell** — sole trader, not an agency. Honest and direct.
- **The differentiator from AI consultants who know nothing** is depth: 21+ years IT, actual tool expertise across multiple platforms (Claude, Grok, Perplexity, ChatGPT, Gemini), built real infrastructure, can explain WHY to use which tool for which job. The tools list on the about page proves this — do not remove it.
- **Education as upsell** — "I just showed you how AI works using a tool I built with AI. If I can build this, imagine what I can build for your business."
- **Do not compare to or badmouth competitors** — let the work speak

### Constraints

- Keep first-person voice, direct tone, no corporate waffle
- Keep existing site structure (static HTML, same nav)
- Crypto education stays — core offering
- Do not weaken education positioning — expand alongside it
- Propose changes first, do not edit without approval
- Update all 5 HTML files if nav/footer text changes
- Run /site-check after any changes
