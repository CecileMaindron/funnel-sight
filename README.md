# Funnelsight

![Live site](https://img.shields.io/badge/live_site-funnel--sight.pages.dev-372F72)
![Stack](https://img.shields.io/badge/stack-n8n_%2B_Claude_API-D9A441)
![Status](https://img.shields.io/badge/status-fictional_company-14161F)

Funnelsight is a fictional growth analytics platform for marketing and revenue teams. It's built around a product-led growth motion, self-serve or hybrid with product-led sales.

It isn't a real product. It's the practical half of a certification project (RS7424, AI-driven transformation of work processes) on using AI to change how a piece of marketing work actually gets done, not just generate text faster.

**Live site:** [funnel-sight.pages.dev](https://funnel-sight.pages.dev)

## The problem

SEO content production breaks down the same way in most small marketing teams. No dedicated writer. Output split across whoever has an hour free. No shared template, no consistent quality bar.

The pages that come out aren't bad. They're inconsistent. And once tone and structure vary from page to page, nobody can explain why one underperforms, because nothing about how it was made was ever standardized.

## The solution

A single, auditable pipeline: keyword in, decision and page out, human review before anything ships. n8n orchestrates it. Claude decides whether a keyword earns a new page, and writes it if so. Nothing reaches GitHub without a person approving it first.

I'm a B2B growth marketer, not a software engineer. The engineering I don't have professional depth in (GitHub API calls, workflow orchestration) is where I worked with Claude as a collaborator. The process design, the editorial and brand constraints, the quality checks, and every call on what to automate versus keep manual: that part is mine.

## Site structure

```
/                           homepage
/trial.html                 trial signup page (disabled)
/resources.html             guides and articles hub
/playbooks/                 use-case SEO pages
/features/                  product feature SEO pages
/glossary/                  educational / GEO SEO pages
/case-studies/              illustrative case study SEO pages
/solutions/                 audience-specific pages (hand-authored, outside the automated flow below)
/404.html                   error page
/styles.css                 single site-wide stylesheet
/sitemap.xml                sitemap submitted to Google Search Console
/content-memory.md          internal reference memory (see below)
/token-usage-log.md         API token consumption log, one line per published page
```

## Stack

Static site, plain HTML and CSS. No framework, no build step. Deployed on Cloudflare Pages.

JavaScript stays minimal: a submit-prevention safeguard on the (disabled) trial form, a Google Analytics 4 tag (manual `gtag.js` install, not Google Tag Manager, since a single tag doesn't need the extra layer), and a lightweight consent banner implementing Google Consent Mode v2. Analytics storage is denied by default and only granted after an explicit visitor choice, stored in `localStorage`.

Both live in `page-shell.html`, so every generated page inherits them automatically. The four core pages, `index.html`, `trial.html`, `resources.html`, `404.html`, carry the same block since they don't go through the shell.

## SEO content production

Pages under `/playbooks/`, `/features/`, `/glossary/` and `/case-studies/` go through a flow combining n8n and the Claude API. One API call per keyword handles the publish/skip decision and the content generation. A human validates before anything publishes. The site's internal memory, sitemap and resource index update automatically, in the same pull request.

The prompt is where I spent the most time. It sets explicit brand and editorial constraints: no invented statistics, no named competitors, no AI-sounding phrasing. It also runs a structured decision process to avoid duplicate or cannibalizing content, and a self-check step that verifies internal links and FAQ content actually match the generated page before it ships.

The duplicate-detection logic went through a real iteration. An early version compared keywords and search intent only, and let a page through that restated an existing feature under a different angle. It now also compares what the page would actually let a user do. That catches functional overlap a keyword-level check misses.

Two reliability guardrails were added after real failures during testing, not designed in from day one:
- the flow stops and flags for manual review if a response gets cut off, instead of auto-retrying
- it logs token consumption per page, so cost drift is visible before it becomes a problem

## Human oversight and governance

Nothing reaches the live site without a human decision at two points.

Claude's generation call can only propose `create`, `skip` or `duplicate`. It never publishes directly. A `create` proposal goes to a Slack review before anything is written to GitHub. If it's rejected, the reviewer's notes feed automatically into the next generation pass, instead of starting over from a blank prompt.

Once approved, everything ships together in a single pull request: the new page, plus any update to the internal memory, sitemap and resource index. The automation opens the PR. A person merges it.

The repo's `main` branch is protected. No direct pushes are possible, a PR is required every time, and that rule can't be bypassed even by an admin token. The human review step is a structural guarantee, not a convention that could slip under deadline pressure.

A separate log records every keyword the system processes, published or not: the decision, the reasoning, and the full generated text where relevant. Over time, that log shows which kinds of keywords get skipped or flagged as duplicates, and how often a first draft needs rework, not just the pages that made it to publication.

`content-memory.md`, at the repo root, is the reference memory used to avoid duplicate content and keep internal linking consistent from page to page. The full process, the page templates, and the test and iteration log used to get there live in a separate Claude project, not in this repo.
