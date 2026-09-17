# Funnelsight — Content Memory

This file lists every page published on funnel-sight.pages.dev. It is read by n8n on every run of the flow and injected into the prompt sent to Claude, to avoid duplicates, detect cannibalization risks, and propose relevant internal links.

Format: `slug | title (H1) | page_type | target_audience | keywords | search_intent | hierarchical_position | internal_linking | status`

Possible values for `hierarchical_position`:
- `pillar` — core page, captures the generic/brand intent
- `hub` — distribution page toward specialized content (lists, organizes, doesn't target a specific keyword)
- `cluster` — satellite page targeting a precise search intent, links up to the hub/pillar
- `utility` — functional page (conversion, form...), outside SEO targeting

/ | Funnelsight — growth analytics for marketing and revenue teams | core | both | PLG growth analytics platform | commercial / navigational | pillar | → /trial.html ; ← global nav (all pages) | published
/trial | Start your free trial: Funnelsight | core | both | (none — conversion page, out of SEO scope) | transactional | utility | ← global nav + CTA from every content page | published
/resources | Resources: Funnelsight | core | both | PLG resources / growth guides | informational / navigational | hub | → 9 cluster pages (resource cards) ; ← global nav | published
/playbooks/tracking-activation-metrics-plg-teams | Tracking activation metrics for PLG teams: Funnelsight | usecase | marketing_growth | activation metrics PLG, tracking activation | informational | cluster | → / (#product), /trial.html ; ← /resources.html, /glossary/what-counts-as-activation-in-plg, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking (one-directional link, missing return link opportunity), /case-studies/plg-team-unifies-activation-retention-data (link added 2026-09-14 during this page's backfill, one-directional, missing return link opportunity) | published
/playbooks/marketing-sales-funnel-numbers-dont-match | Marketing and sales funnel numbers don't match: Funnelsight | usecase | both | marketing sales funnel alignment | informational / problem-aware | cluster | → / (#product), /trial.html ; ← /resources.html | published
/glossary/what-counts-as-activation-in-plg | What counts as activation in product-led growth: Funnelsight | educational | marketing_growth | what is activation PLG, PLG activation definition | informational / definitional | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html | published
/playbooks/spreadsheet-vs-analytics-tool-plg-tracking | Spreadsheets vs analytics tools for PLG teams: Funnelsight | usecase | both | spreadsheet vs analytics tool PLG tracking | comparative / consideration | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html, /playbooks/tracking-plg-funnel-without-data-team (link added 2026-09-15 during this page's creation, one-directional, missing return link opportunity) | published
/features/activation-retention-dashboard-plg-teams | Activation and retention dashboard for PLG teams: Funnelsight | feature | marketing_growth | activation retention dashboard PLG | commercial | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking, /trial.html ; ← /resources.html, /glossary/how-to-calculate-churn-rate-b2b-saas (one-directional link, missing return link opportunity), /glossary/how-to-calculate-net-revenue-retention-b2b-saas (one-directional link, missing return link opportunity) | published
/case-studies/plg-team-unifies-activation-retention-data | PLG team unifies activation and retention data: Funnelsight | case_study | marketing_growth | example of a PLG team unifying activation and retention data | informational / commercial | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html | published
/glossary/how-to-calculate-churn-rate-b2b-saas | How to calculate churn rate for B2B SaaS: Funnelsight | educational | both | how to calculate churn rate b2b saas, comment calculer son taux de churn b2b saas | informational | cluster | → /features/activation-retention-dashboard-plg-teams, /trial.html ; ← /resources.html, /glossary/how-to-calculate-net-revenue-retention-b2b-saas (one-directional link, missing return link opportunity) | published
/glossary/how-to-calculate-net-revenue-retention-b2b-saas | How to calculate net revenue retention (NRR): Funnelsight | educational | both | how to calculate net revenue retention, NRR calculation b2b saas | informational | cluster | → /glossary/how-to-calculate-churn-rate-b2b-saas, /features/activation-retention-dashboard-plg-teams, /trial.html ; ← /resources.html | published
/playbooks/tracking-plg-funnel-without-data-team | Track your PLG funnel without a data team: Funnelsight | usecase | marketing_growth | how to start tracking your PLG funnel without a data team | informational | cluster | → /playbooks/spreadsheet-vs-analytics-tool-plg-tracking, /trial.html ; ← /resources.html | published
/playbooks/self-serve-revenue-vs-sales-assisted-crm | Why self-serve revenue gets lost in your CRM: Funnelsight | usecase | both | self-serve revenue vs sales-assisted revenue, self-serve revenue tracking CRM | informational / problem-aware | cluster | → /glossary/how-to-calculate-net-revenue-retention-b2b-saas (one-directional link, missing return link opportunity), /trial.html ; ← /resources.html | published

(10 SEO pages published to date. Sorted by category since 2026-09-11:
/playbooks/ for usecase, /glossary/ for educational, /case-studies/ for
case_study, /features/ for feature.)
