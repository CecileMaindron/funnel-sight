# Funnelsight

Marketing site for Funnelsight, a fictional growth analytics platform for marketing and revenue teams doing product-led growth (PLG). Built as part of a professional certification project on integrating AI into work processes (RS7424, AI-driven transformation of work processes). Funnelsight is not a real product.

**Live site:** [funnel-sight.pages.dev](https://funnel-sight.pages.dev)

## About this project

I'm a B2B growth marketer, not a software engineer. This repo is the practical half of a certification project on using AI to transform a real marketing workflow: SEO content production. The site itself, the content generation prompt, the page templates and the automation flow (n8n + Claude API) are all things I designed and iterated on, working with Claude as a collaborator on the parts that needed engineering I don't have professional depth in (GitHub API calls, workflow orchestration). What I own directly: the process design, the editorial and brand constraints the AI has to respect, the quality checks, and the judgment calls on what to automate versus keep as a manual, human-reviewed step.

## Site structure

```
/                           homepage
/trial.html                 trial signup page (disabled)
/resources.html             guides and articles hub
/playbooks/                 use-case SEO pages
/features/                  product feature SEO pages
/glossary/                  educational / GEO SEO pages
/case-studies/              illustrative case study SEO pages
/404.html                   error page
/styles.css                 single site-wide stylesheet
/sitemap.xml                sitemap submitted to Google Search Console
/content-memory.md          internal reference memory (see below)
/token-usage-log.md         API token consumption log, one line per published page
```

## Stack

Static site, plain HTML/CSS, no framework or build step, deployed on Cloudflare Pages. JavaScript is limited to a submit-prevention safeguard on the (disabled) trial form, a Google Analytics 4 tag (manual gtag.js install, not Google Tag Manager, since a single tag doesn't need the extra layer), and a lightweight consent banner implementing Google Consent Mode v2 (analytics storage denied by default, granted only after an explicit visitor choice, stored in `localStorage`). Both live in `page-shell.html` so every generated page inherits them automatically; the four core pages (`index.html`, `trial.html`, `resources.html`, `404.html`) carry the same block since they don't go through the shell.

## SEO content production

Pages under `/playbooks/`, `/features/`, `/glossary/` and `/case-studies/` are produced through a flow combining n8n and the Claude API: keyword selection, a single API call per keyword that handles both the publish/skip decision and the content generation, human validation before publishing, and automatic updates to the site's internal memory, sitemap and resource index in the same pull request.

The prompt design is the part I spent the most time on: explicit brand and editorial constraints (no invented statistics, no named competitors, no AI-sounding phrasing), a structured decision process to avoid duplicate or cannibalizing content, and a self-check step that verifies internal links and FAQ content actually match what's in the generated page before it ships. The flow also includes two reliability guardrails added after real failures during testing: it stops and flags for manual review rather than auto-retrying if a response gets cut off, and it logs token consumption per page so cost drift is visible before it becomes a problem.

`content-memory.md`, at the repo root, acts as the reference memory used to avoid duplicate content and keep internal linking consistent from page to page. The full process, the page templates, and the test/iteration log used to get there live in a separate Claude project, not in this repo.
