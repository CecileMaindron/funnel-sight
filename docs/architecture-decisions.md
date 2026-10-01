# Architecture decisions

Engineers call these architecture decision records. I'm using a simplified version so anyone curious about the reasoning, developer or marketer, can follow it.

Each entry covers one choice: what I decided, what I considered instead, and what would make me revisit it.

## Why one workflow, not several sub-workflows

**Decision:** Everything runs in a single n8n workflow. No sub-workflows.

**Context:** The canvas is wide enough that you need to scroll to see it end to end. It also has two blocks of repeated logic: six branches that pull a file from GitHub and decode it, and five branches that encode a file and push it back. On paper, both are textbook reasons to split into sub-workflows.

**Why I kept it as one:** Each of those six fetch branches targets a different file with a different role in the prompt (product facts, page template, sitemap, and so on). Splitting them into a shared sub-workflow would save a few lines of duplicated node config, not real complexity. n8n's own guidance on this backs that read: it treats "can't see the whole canvas without scrolling" as one early signal, but flags sub-workflows as the answer once you also see actual duplication *across* workflows, debugging that outlasts building, or several people needing to edit different parts at once. None of that applies here. I'm the only one building this, and each branch is still simple enough to trace end to end in a few seconds.

**What would change my mind:** If I reused the same fetch or commit logic in a second workflow, or if changing how one file gets pulled from GitHub meant editing it in five or six places by hand, that's the point where extracting a sub-workflow would start paying for itself.

## Why one API call handles both the decision and the writing

**Decision:** A single Claude call takes the keyword in and returns either a skip/duplicate verdict with reasoning, or a full page.

**Context:** I could have split this into two calls: a cheap triage step that only decides create, skip or duplicate, then a second call that writes the page only once the first one says yes.

**Why I kept it as one:** The duplicate check needed to get stronger than a keyword-and-intent comparison (see below). Judging whether a new page would actually overlap with an existing one works better when the model reasons about what the page would say, not just what it's nominally about. Keeping the decision and the writing in the same call means that reasoning stays available in the same context, instead of getting recreated in a second, disconnected prompt. Confirmed in practice: a skip or duplicate verdict returns a short reasoning block, not a full page — output tokens for those calls run in the low hundreds, against several thousand for a published page.

**Trade-off:** A two-step version would very likely be cheaper on keywords that get rejected early, since it wouldn't spend tokens writing a page that never ships.

**What would change my mind:** If skip and duplicate outcomes started dominating the keyword list and token cost became the binding constraint, a cheap triage call before a full generation call would be the natural fix.

## Why a static site, no framework

**Decision:** Plain HTML and CSS, no build step, deployed straight to Cloudflare Pages.

**Context:** A static site generator, or a JS framework, would have given me templating and component reuse.

**Why I kept it simple:** The automation writes HTML directly into the repo through a GitHub PR. Adding a build step means one more thing that can break between "Claude wrote a page" and "the page is live," in a chain that already has several moving parts. Every generated page inherits its shared header, footer and scripts from one file, `page-shell.html`, which covers the component-reuse problem without needing a framework to enforce it.

**Trade-off:** The four core pages that don't go through the shell (`index.html`, `trial.html`, `resources.html`, `404.html`) carry their own copy of that shared block. If it changes, I update it in five places by hand.

**What would change my mind:** If the site grew into hundreds of pages with more shared components than a single shell file could reasonably hold, a static site generator would start paying for its own complexity.

## Why the pipeline stops instead of retrying on a truncated response

**Decision:** If a Claude response gets cut off before completion, the flow halts and flags the keyword for manual review. It doesn't retry automatically.

**Context:** This came out of a real failure during testing, not a decision made on paper in advance.

**Why I chose stop over retry:** A cut-off response usually means the content for that keyword ran past the token budget, not that the call randomly failed. Retrying blind spends another full generation call without addressing why it happened, and risks the same cutoff again. Flagging it puts a person in the loop to decide the actual fix: raise the token limit, narrow the angle of the page, or accept a shorter one.

**Trade-off:** Nothing here self-heals. Every truncation needs a manual look before that keyword can move forward.

**What would change my mind:** If truncation turned out to have one dependable fix, like always doubling the token budget once, an automatic retry could replace the manual flag for that specific failure mode.

## Why duplicate detection compares function, not just topic

**Decision:** Before generating a page, Claude checks whether it would functionally overlap with an existing one, not just whether the keyword or search intent looks similar.

**Context:** The first version only compared keywords and search intent. It let a page through that restated an existing feature page under a different angle.

**Why I changed it:** Two pages can target different keywords and still tell a user to do the exact same thing. A keyword-level check can't catch that. Comparing what the page would actually let a user do closed that gap.

**Trade-off:** This kind of check is fuzzier than a keyword match. It depends on the model's judgment of functional similarity, which is harder to unit-test or explain in one line than "these two keywords are 90% the same string."

**What would change my mind:** Not something I'd revert. If a new kind of overlap slipped through later (say, across a playbook and a case study written for different audiences but covering the same workflow), that would be the next refinement to make.

**Update:** That gap showed up sooner than expected, just not in the form I'd guessed. A test keyword came back `create` even though the page it generated overlapped in substance with one of the hand-authored `/solutions/` pages — a part of the site the overlap check didn't cover yet, since it only compared against feature and use-case pages. Extended the check to include `/solutions/` pages too, with an explicit instruction to flag a conflict in positioning, not just a duplicated capability. Same lesson as the original decision: the failure mode that gets caught is the one you thought to check for.

## Why a custom domain over the free pages.dev subdomain

**Decision:** Bought `funnelsight.dev` and pointed the site there, with the old `pages.dev` subdomain redirecting to it. Renamed the GitHub repo to match.

**Context:** Cloudflare Pages gives every project a free `*.pages.dev` subdomain, which is enough to have a live site. The sitemap had been stuck at "couldn't fetch" in Search Console for weeks despite two separate fixes for two separate suspected causes (a content bug that had emptied the file, then a cache-control header change) — neither one confirmed to work.

**Why I made the change:** The cost was negligible (a few dollars a year, prepaid for several years) against the expected upside, and a domain of its own seemed more likely to be treated as a first-party site by Google than a subdomain shared with every other project hosted on the same platform. It also made the GitHub repo easier to find on its own: searching the product name plus "github" now surfaces it, which it didn't before under the old name.

**Result:** The sitemap was fetched successfully right after the move, with no further changes needed. Five pages submitted for indexing, three already showing up in search within hours.

**Trade-off:** I can't cleanly separate how much of the fix was the new domain itself versus simply starting over with a domain that has no prior crawl history. The header change from a few days earlier is confirmed not to have worked on the old domain, so at least one hypothesis is ruled out, but the exact mechanism behind the old domain's block is still unconfirmed.

**What would change my mind:** Nothing to revisit here. If a future project hits the same "sitemap won't fetch" symptom on a `pages.dev` subdomain, this is now a data point worth checking early rather than last.

## Why prompt caching uses a 5-minute window, not the 1-hour one

**Decision:** Enabled prompt caching (`cache_control: ephemeral`) on the static block of the generation prompt — instructions, page template, product facts, site memory, sitemap — with the default 5-minute TTL rather than the 1-hour option.

**Context:** Every call resends that same static block, roughly 20-25k tokens, alongside the few hundred tokens that actually vary per keyword. Caching it is close to a free win on cost. The only real decision is which cache lifetime to pay for: 5 minutes is cheaper to write, 1 hour costs more upfront but tolerates a longer gap between calls that reuse it.

**Why I chose the shorter window:** I checked the actual shape of the workflow instead of assuming. There's no queue that holds a keyword until a human finishes reviewing the previous one before starting the next — every keyword in a run reaches the generation call back-to-back, one after another, gated only by API latency (60-100 seconds observed per call), never by how long a Slack review takes. That gap sits comfortably inside a 5-minute window even if the monthly keyword count grows somewhat from today's volume, so paying more upfront for a 1-hour window wasn't buying anything yet.

**Trade-off:** If the batch grows large enough that the time between the first and last call exceeds 5 minutes, the later calls in that batch would miss the cache and pay the full write cost again, the exact cost the caching was meant to avoid.

**What would change my mind:** If the keyword volume per run grows past what a 5-minute window reliably covers, switch to the 1-hour cache option — a one-line change, not a redesign.
