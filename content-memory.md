# Funnelsight — Content Memory

Ce fichier liste toutes les pages publiées sur funnel-sight.pages.dev. Il est lu par n8n à chaque exécution du flow et injecté dans le prompt envoyé à Claude, pour éviter les doublons, détecter les risques de cannibalisation, et proposer un maillage interne pertinent.

Format : `slug | title (H1) | page_type | target_audience | keywords | search_intent | hierarchical_position | internal_linking | status`

Valeurs possibles pour `hierarchical_position` :
- `pillar` — page cœur, capte l'intention générique/marque
- `hub` — page de distribution vers le contenu spécialisé (liste, organise, ne cible pas un mot-clé précis)
- `cluster` — page satellite ciblant une intention de recherche précise, remonte vers le hub/pillar
- `utility` — page fonctionnelle (conversion, formulaire...), hors ciblage SEO

/ | Funnelsight — growth analytics for marketing and revenue teams | core | both | PLG growth analytics platform | commercial / navigational | pillar | → /trial.html ; ← nav globale (toutes les pages) | published
/trial | Start your free trial: Funnelsight | core | both | (aucun — page de conversion, hors ciblage SEO) | transactional | utility | ← nav globale + CTA depuis toutes les pages de contenu | published
/resources | Resources: Funnelsight | core | both | PLG resources / growth guides | informational / navigational | hub | → 7 pages cluster (cartes ressources) ; ← nav globale | published
/playbooks/tracking-activation-metrics-plg-teams | Tracking activation metrics for PLG teams: Funnelsight | usecase | marketing_growth | activation metrics PLG, tracking activation | informational | cluster | → / (#product), /trial.html ; ← /resources.html, /glossary/what-counts-as-activation-in-plg, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking (lien non réciproque — opportunité de maillage retour), /case-studies/plg-team-unifies-activation-retention-data (lien ajouté le 14/09/2026 lors du backfill de cette dernière, non réciproque — opportunité de maillage retour) | published
/playbooks/marketing-sales-funnel-numbers-dont-match | Marketing and sales funnel numbers don't match: Funnelsight | usecase | both | marketing sales funnel alignment | informational / problem-aware | cluster | → / (#product), /trial.html ; ← /resources.html | published
/glossary/what-counts-as-activation-in-plg | What counts as activation in product-led growth: Funnelsight | educational | marketing_growth | what is activation PLG, PLG activation definition | informational / definitional | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html | published
/playbooks/spreadsheet-vs-analytics-tool-plg-tracking | Spreadsheets vs analytics tools for PLG teams: Funnelsight | usecase | both | spreadsheet vs analytics tool PLG tracking | comparative / consideration | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html | published
/features/activation-retention-dashboard-plg-teams | Activation and retention dashboard for PLG teams: Funnelsight | feature | marketing_growth | activation retention dashboard PLG | commercial | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking, /trial.html ; ← /resources.html, /glossary/how-to-calculate-churn-rate-b2b-saas (lien non réciproque — opportunité de maillage retour) | published
/case-studies/plg-team-unifies-activation-retention-data | PLG team unifies activation and retention data: Funnelsight | case_study | marketing_growth | example of a PLG team unifying activation and retention data | informational / commercial | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html | published
/glossary/how-to-calculate-churn-rate-b2b-saas | How to calculate churn rate for B2B SaaS: Funnelsight | educational | both | how to calculate churn rate b2b saas, comment calculer son taux de churn b2b saas | informational | cluster | → /features/activation-retention-dashboard-plg-teams, /trial.html ; ← /resources.html | published

(7 pages SEO publiées à ce jour. Rangées par catégorie depuis le 11/09/2026 :
/playbooks/ pour usecase, /glossary/ pour educational, /case-studies/ pour
case_study, /features/ pour feature.)
