# Funnelsight — Content Memory

This file lists every page published on funnel-sight.pages.dev. It is read by n8n on every run of the flow and injected into the prompt sent to Claude, to avoid duplicates, detect cannibalization risks, and propose relevant internal links.

Format: `slug | title (H1) | page_type | target_audience | keywords | search_intent | hierarchical_position | internal_linking | status`

Possible values for `hierarchical_position`:
- `pillar` — core page, captures the generic/brand intent
- `hub` — distribution page toward specialized content (lists, organizes, doesn't target a specific keyword)
- `cluster` — satellite page targeting a precise search intent, links up to the hub/pillar
- `utility` — functional page (conversion, form...), outside SEO targeting
- `off-flow` — hand-authored page outside the n8n generation flow, not part of the certified page-family structure defined in funnelsight-page-template.md. Listed here only so this file's duplicate/cannibalization detection still covers it. Not counted in the "SEO pages published to date" count below, which tracks certified flow output only.

/ | Funnelsight — growth analytics for marketing and revenue teams | core | both | PLG growth analytics platform | commercial / navigational | pillar | → /trial.html ; ← global nav (all pages) | published
/trial | Start your free trial: Funnelsight | core | both | (none — conversion page, out of SEO scope) | transactional | utility | ← global nav + CTA from every content page | published
/resources | Activation and retention guides for PLG teams: Funnelsight | core | both | PLG resources / growth guides | informational / navigational | hub | → 14 cluster pages (resource cards) ; ← global nav | published
/playbooks/tracking-activation-metrics-plg-teams | Tracking activation metrics for PLG teams: Funnelsight | usecase | marketing_growth | activation metrics PLG, tracking activation | informational | cluster | → / (#product), /trial.html, /glossary/what-counts-as-activation-in-plg (link added 2026-09-22 during quarterly internal linking audit, now bidirectional), /features/activation-retention-dashboard-plg-teams (link added 2026-09-22 during quarterly internal linking audit, now bidirectional), /case-studies/plg-team-unifies-activation-retention-data (link added 2026-09-22 during quarterly internal linking audit, now bidirectional) ; ← /resources.html, /glossary/what-counts-as-activation-in-plg, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking (one-directional link, missing return link opportunity), /case-studies/plg-team-unifies-activation-retention-data, /glossary/what-is-a-product-qualified-lead-pql (one-directional link, missing return link opportunity) | published
/playbooks/marketing-sales-funnel-numbers-dont-match | Marketing and sales funnel numbers don't match: Funnelsight | usecase | both | marketing sales funnel alignment | informational / problem-aware | cluster | → / (#product), /trial.html, /glossary/what-is-a-product-qualified-lead-pql (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity) ; ← /resources.html, /playbooks/self-serve-revenue-vs-sales-assisted-crm (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity) | published
/glossary/what-counts-as-activation-in-plg | What counts as activation in product-led growth: Funnelsight | educational | marketing_growth | what is activation PLG, PLG activation definition | informational / definitional | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html, /playbooks/tracking-activation-metrics-plg-teams (now bidirectional as of 2026-09-22), /glossary/what-is-a-product-qualified-lead-pql (one-directional link, missing return link opportunity), /playbooks/tracking-plg-funnel-without-data-team (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity), /playbooks/tracking-feature-adoption-plg-teams (link added 2026-09-23, one-directional, missing return link opportunity), /playbooks/tracking-expansion-revenue-signals-plg (link added 2026-09-23, one-directional, missing return link opportunity) | published
/playbooks/spreadsheet-vs-analytics-tool-plg-tracking | Spreadsheets vs analytics tools for PLG teams: Funnelsight | usecase | both | spreadsheet vs analytics tool PLG tracking | comparative / consideration | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /features/activation-retention-dashboard-plg-teams, /playbooks/tracking-plg-funnel-without-data-team (link added 2026-09-22 during quarterly internal linking audit, now bidirectional), /trial.html ; ← /resources.html, /playbooks/tracking-plg-funnel-without-data-team (now bidirectional as of 2026-09-22) | published
/features/activation-retention-dashboard-plg-teams | Activation and retention dashboard for PLG teams: Funnelsight | feature | marketing_growth | activation retention dashboard PLG | commercial | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking, /trial.html ; ← /resources.html, /playbooks/tracking-activation-metrics-plg-teams (now bidirectional as of 2026-09-22), /playbooks/spreadsheet-vs-analytics-tool-plg-tracking (now bidirectional as of 2026-09-22), /glossary/how-to-calculate-churn-rate-b2b-saas (one-directional link, missing return link opportunity), /glossary/how-to-calculate-net-revenue-retention-b2b-saas (one-directional link, missing return link opportunity), /glossary/what-is-a-product-qualified-lead-pql (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity), /playbooks/tracking-plg-funnel-without-data-team (link added 2026-09-22, second pass — redundancy trim), /playbooks/self-serve-revenue-vs-sales-assisted-crm (link added 2026-09-22, second pass — redundancy trim), /case-studies/plg-team-turns-pql-into-sales-conversation (new page, one-directional, return link opportunity) | published
/case-studies/plg-team-unifies-activation-retention-data | PLG team unifies activation and retention data: Funnelsight | case_study | marketing_growth | example of a PLG team unifying activation and retention data | informational / commercial | cluster | → /playbooks/tracking-activation-metrics-plg-teams, /trial.html ; ← /resources.html, /playbooks/tracking-activation-metrics-plg-teams (now bidirectional as of 2026-09-22) | published
/glossary/how-to-calculate-churn-rate-b2b-saas | How to calculate churn rate for B2B SaaS: Funnelsight | educational | both | how to calculate churn rate b2b saas, comment calculer son taux de churn b2b saas | informational | cluster | → /features/activation-retention-dashboard-plg-teams, /glossary/how-to-calculate-net-revenue-retention-b2b-saas (link added 2026-09-22 during quarterly internal linking audit, now bidirectional), /trial.html ; ← /resources.html, /glossary/how-to-calculate-net-revenue-retention-b2b-saas (now bidirectional as of 2026-09-22) | published
/glossary/how-to-calculate-net-revenue-retention-b2b-saas | How to calculate net revenue retention (NRR): Funnelsight | educational | both | how to calculate net revenue retention, NRR calculation b2b saas | informational | cluster | → /glossary/how-to-calculate-churn-rate-b2b-saas, /features/activation-retention-dashboard-plg-teams, /playbooks/self-serve-revenue-vs-sales-assisted-crm (link added 2026-09-22 during quarterly internal linking audit, now bidirectional), /trial.html ; ← /resources.html, /glossary/how-to-calculate-churn-rate-b2b-saas (now bidirectional as of 2026-09-22), /playbooks/self-serve-revenue-vs-sales-assisted-crm (now bidirectional as of 2026-09-22) | published
/playbooks/tracking-plg-funnel-without-data-team | Track your PLG funnel without a data team: Funnelsight | usecase | marketing_growth | how to start tracking your PLG funnel without a data team | informational | cluster | → /playbooks/spreadsheet-vs-analytics-tool-plg-tracking, /glossary/what-counts-as-activation-in-plg (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity), /features/activation-retention-dashboard-plg-teams (link added 2026-09-22, second pass — redundancy trim), /trial.html ; ← /resources.html, /playbooks/spreadsheet-vs-analytics-tool-plg-tracking (now bidirectional as of 2026-09-22) | published
/playbooks/self-serve-revenue-vs-sales-assisted-crm | Why self-serve revenue gets lost in your CRM: Funnelsight | usecase | both | self-serve revenue CRM, PLG sales assisted tracking | informational / problem-aware | cluster | → /glossary/how-to-calculate-net-revenue-retention-b2b-saas, /playbooks/marketing-sales-funnel-numbers-dont-match (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity), /features/activation-retention-dashboard-plg-teams (link added 2026-09-22, second pass — redundancy trim), /trial.html ; ← /resources.html, /glossary/how-to-calculate-net-revenue-retention-b2b-saas (now bidirectional as of 2026-09-22) | published
/glossary/what-is-a-product-qualified-lead-pql | What is a product qualified lead (PQL): Funnelsight | educational | marketing_growth | what is a product qualified lead, PQL definition | informational | cluster | → /glossary/what-counts-as-activation-in-plg, /playbooks/tracking-activation-metrics-plg-teams, /features/activation-retention-dashboard-plg-teams (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity), /trial.html ; ← /resources.html, /playbooks/marketing-sales-funnel-numbers-dont-match (link added 2026-09-22 during quarterly internal linking audit, one-directional, missing return link opportunity), /playbooks/tracking-expansion-revenue-signals-plg (link added 2026-09-23, one-directional, missing return link opportunity), /case-studies/plg-team-turns-pql-into-sales-conversation (new page, one-directional, return link opportunity) | published
/playbooks/tracking-feature-adoption-plg-teams | Tracking feature adoption for PLG teams: Funnelsight | usecase | marketing_growth | how to track feature adoption for plg teams | informational | cluster | → /glossary/what-counts-as-activation-in-plg, /trial.html ; ← /resources.html | published
/playbooks/tracking-expansion-revenue-signals-plg | Tracking expansion revenue signals in PLG: Funnelsight | usecase | marketing_growth | how to track expansion revenue signals in plg | informational | cluster | → /glossary/what-counts-as-activation-in-plg, /trial.html ; ← /resources.html | published
/case-studies/plg-team-turns-pql-into-sales-conversation | PLG team turns a PQL into a sales conversation: Funnelsight | case_study | both | how a plg team turned a product qualified lead into a sales conversation | informational | cluster | → /features/activation-retention-dashboard-plg-teams, /glossary/what-is-a-product-qualified-lead-pql, /trial.html ; ← /resources.html | published
/solutions/marketing | What self-serve growth means for marketing: Funnelsight | solution | marketing_growth | self-serve growth marketing, PLG marketing accountability | informational / commercial | off-flow | → /solutions/sales ; ← /solutions/sales, global nav Solutions dropdown (all pages) | published
/solutions/sales | Redefining the hot lead in a self-serve motion: Funnelsight | solution | sales | self-serve hot lead, PQL sales, product qualified lead sales | informational / commercial | off-flow | → /solutions/marketing ; ← /solutions/marketing, global nav Solutions dropdown (all pages) | published

(15 SEO pages published to date. Sorted by category since 2026-09-11:
/playbooks/ for usecase, /glossary/ for educational, /case-studies/ for
case_study, /features/ for feature.

Note du 17/09/2026 : l'entrée self-serve-revenue-vs-sales-assisted-crm a été
reconstituée à partir de la page HTML publiée, le log de génération
d'origine n'a pas été retrouvé dans cette conversation. keywords et
search_intent sont une estimation raisonnable, à corriger si le vrai log est
retrouvé.

Correction du 18/09/2026 : l'entrée
how-to-calculate-net-revenue-retention-b2b-saas était dupliquée en deux
lignes quasi identiques (une sans le lien entrant du 17/09, une avec).
Fusionnée en une seule ligne, conservant la version la plus à jour avec le
lien entrant.

Note du 22/09/2026 : la page what-is-a-product-qualified-lead-pql a
initialement été rédigée avec une attribution nominative à un auteur PLG
reconnu (cf. règle sur les sources externes dans
funnelsight-page-template.md). Correction demandée en révision : retrait de
l'attribution, reformulation en framing générique ("a common way to frame
this in PLG circles is..."). Version livrée déjà corrigée.

Audit maillage/répétition du 22/09/2026 (suivant prompt-audit-maillage-interne.md,
content-memory.md en entrée) : 10 liens ajoutés (7 retours de lien manquants,
3 connexions manquantes ; détail des paires et ancres dans le journal de
curation / l'échange avec Cécile du 22/09). Un cas de redondance corrigé :
la formule "you define the activation event once, and it applies
consistently across every report" était répétée sur 5 pages ; recentrée sur
/features/activation-retention-dashboard-plg-teams (page de référence pour ce
mécanisme produit), raccourcie et remplacée par un lien sur
tracking-activation-metrics-plg-teams, tracking-plg-funnel-without-data-team
et what-is-a-product-qualified-lead-pql ; reformulée sans répéter le
mécanisme sur plg-team-unifies-activation-retention-data.

Deux corrections de fond identifiées lors du premier passage d'audit manuel
(11/09 → 22/09) et appliquées à cette occasion :
1. self-serve-revenue-vs-sales-assisted-crm.html contenait deux statistiques
   non sourcées ("60-80% de revenu self-serve pour un produit PLG",
   "en dessous de 20%", "2 à 3 fois la dépense initiale"), en violation de la
   règle funnelsight-page-template.md sur les chiffres inventés. Reformulées
   en tendance qualitative, sans chiffre précis non sourcé. Le seul chiffre
   conservé (64% de revenu self-serve chez Momentive à 500M$+ d'ARR) reste
   sourcé via SaaStr et n'a pas été modifié.
2. plg-team-unifies-activation-retention-data.html (case study) ne respectait
   pas le template : la section "Result" était entièrement qualitative, sans
   le chiffre illustratif obligatoire. Ajout d'un chiffre illustratif
   ("roughly half an hour" de temps de réconciliation en moins par session),
   explicitement qualifié d'illustratif et non mesuré, conformément au
   template.

Correction du 22/09/2026 (deuxième passage — vérification post-implémentation) :
en relisant les fichiers HTML réellement publiés après le premier passage, deux
écarts ont été trouvés entre ce que cette note affirmait et l'état réel du site.
Corrigés dans ce même passage :
1. tracking-plg-funnel-without-data-team.html portait encore la formule
   redondante "you define that event once ... and it applies across every
   report from there" quasi intégralement, sans lien vers la page Feature,
   malgré la note ci-dessus affirmant le contraire. Raccourcie et liée à
   /features/activation-retention-dashboard-plg-teams.
2. self-serve-revenue-vs-sales-assisted-crm.html portait la même formule
   redondante, un cas identifié par le premier passage d'audit manuel mais
   absent de la liste de l'audit formel (`prompt-audit-maillage-interne.md`)
   et donc non traité lors de la première implémentation. Raccourcie et liée
   à /features/activation-retention-dashboard-plg-teams également.
3. tracking-activation-metrics-plg-teams.html portait une attribution
   nominative ("Wes Bush's ProductLed Playbook") dans son encadré "Common
   mistake" — même risque que celui déjà corrigé sur la page PQL le
   22/09/2026 (cf. note ci-dessus), non repéré lors des audits précédents
   car hors périmètre maillage/répétition. Attribution retirée, reformulée
   en framing générique, alignée sur le style de l'encadré équivalent sur
   marketing-sales-funnel-numbers-dont-match.html (sans attribution externe).

Note du 23/09/2026 : la page tracking-expansion-revenue-signals-plg reprend
brièvement l'argument "pas besoin de temps réel" déjà présent sur plusieurs
pages du site (spreadsheet-vs-analytics-tool-plg-tracking,
tracking-plg-funnel-without-data-team notamment). Contrairement au cas
"activation event" corrigé le 22/09, ce n'est pas ici une formule répétée
mot pour mot mais l'application du même principe éditorial ("start simple",
cf. funnelsight-page-template.md) à un nouveau contexte (fréquence de
vérification d'un signal d'expansion vs. fréquence de rafraîchissement des
données d'activation). À surveiller lors du prochain audit de maillage : si
un troisième cas apparaît avec la même formulation, envisager de centraliser
le principe sur une page de référence plutôt que de le reformuler à chaque
fois.

Note du 23/09/2026 : nouvelle page case_study
plg-team-turns-pql-into-sales-conversation ajoutée. Elle lie vers
/features/activation-retention-dashboard-plg-teams et
/glossary/what-is-a-product-qualified-lead-pql sans lien retour depuis ces
deux pages pour l'instant (opportunité de lien retour signalée dans leurs
champs internal_linking ci-dessus, à traiter lors du prochain audit de
maillage).

Note du 24/09/2026 : ajout de deux pages /solutions/marketing et
/solutions/sales, rédigées manuellement en dehors du flow n8n (hors
périmètre de la certification RS7424, à but de portfolio/SEO uniquement).
Nouveau page_type "solution" et nouvelle valeur hierarchical_position
"off-flow" introduits pour ces deux entrées uniquement (définition ajoutée
ci-dessus). Elles ne comptent pas dans les "SEO pages published to date"
citées plus bas, qui restent la production certifiée du flow n8n. Elles
sont listées ici uniquement pour que ce fichier continue de couvrir la
détection de doublons/cannibalisation sur l'ensemble du site, y compris le
contenu hors flow. Le nav global de chaque page a aussi été mis à jour :
l'ancre "Who it's for" (#audience) est remplacée par un menu déroulant
"Solutions" pointant vers ces deux pages.)
