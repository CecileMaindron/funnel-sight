# Funnelsight

Marketing site for Funnelsight, a fictional growth analytics platform for marketing and revenue teams doing product-led growth (PLG). Built as part of a professional certification project on integrating AI into work processes. Funnelsight is not a real product.

**Live site:** [funnel-sight.pages.dev](https://funnel-sight.pages.dev)

## Site structure

```
/                           homepage
/trial.html                 trial signup page (disabled)
/resources.html             guides and articles hub
/playbooks/                 use-case SEO pages
/glossary/                  educational SEO pages
/404.html                   error page
/styles.css                 single site-wide stylesheet
/sitemap.xml                sitemap submitted to Google Search Console
```

## Stack

Static site, plain HTML/CSS, no framework or build step, deployed on Cloudflare Pages. No JavaScript beyond a submit-prevention safeguard on the (disabled) trial form.

## SEO content production

Pages under `/playbooks/` and `/glossary/` are produced through a flow combining n8n and the Claude API: keyword selection, content generation, human validation before publishing. The full process and the page templates used live in a separate Claude project, not in this repo.

`content-memory.md`, at the repo root, acts as the reference memory used to avoid duplicate content and keep internal linking consistent from page to page. A copy is also kept in the dedicated Claude generation project as a convenience shortcut during the manual testing phase.
