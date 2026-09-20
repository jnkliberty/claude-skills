# Routing table: outcome to leaf skills

Companion to `../SKILL.md`. Leaf skills are named by role. Where a skill on this shelf covers the step, it's named directly; everything else is a placeholder for whatever tool or skill does that job in your setup.

Voice skills are client-repo scoped and do not appear in a global skills directory. Find them at `<client repo>/.claude/skills/<name>-voice/`, if the client has one.

---

## System 1: Customer truth

Outcome shape: sales, support, product, and marketing each hold a different version of the market. One standing file resolves it.

| Step | Leaf skill | What it does here |
| --- | --- | --- |
| Pull the raw feed | call-sync tooling (whatever pulls calls into a raw feed) | Calls resolved to contacts, commitments extracted |
| Interview and synthesize | `customer-research` | Conducts and synthesizes customer research, ICP research, call analysis |
| Score a single event | `signal-interpreter` | Turns one raw GTM signal into relevance, strength, confidence, why-now |
| Watch named champions | `champion-move-detection` | Live lookup per watchlist person; a champion who moved is a warm account |
| Watch category language | `term-radar` | Rising terms in the category, the words buyers are starting to use |
| Sweep the whole territory | `territory-signal-digest` | Weekly ranked brief across every account: promotions, job changes, funding, hiring, intent |
| Check the standing claim | `product-marketing-context` | The positioning document the memo is written against |
| Rivals and market | `market-research`, `competitor-monitoring`, `competitor-profiling` | Sourced competitive intel, rival movement, per-URL competitor profiles |
| Render the memo | `html-output` | Self-contained single-file HTML report |

Write-back: `growth-os/customer-truth/what-the-market-is-telling-us.md`.
Metric: a named pain that turned into a test. Not memo count.

---

## System 2: Founder content engine

Outcome shape: the founder sounds sharper on a call than the company does in public.

| Step | Leaf skill | What it does here |
| --- | --- | --- |
| Build the voice profile | `brand-voice` | Source-derived style profile from real posts, essays, docs |
| Apply the client's voice | `<name>-voice` in the client repo | The client's own voice skill, if one exists |
| Plan the topics | `content-strategy` | Topic clusters, editorial calendar, what to cover |
| LinkedIn specifics | `linkedin-intelligence` | Data-backed LinkedIn post analysis, 62k viral posts studied |
| Multi-platform assets | `content-engine` | Platform-native systems for X, LinkedIn, TikTok, YouTube, newsletters |
| Per-platform posts | `social-content` | Scheduling and platform-specific tuning |
| Page and landing copy | `copywriting` | Homepage, landing, pricing, feature, about |
| Refresh existing copy | `copy-editing` | Systematic review passes on published copy |
| Behavioral angle | `marketing-psychology` | Psychological principles applied to the angle |
| Expert-panel scoring | `content-ops` | Iterative scoring of copy, sequences, pages, strategy docs |
| Strip AI tells | `stop-slop` | Mandatory final pass on every human-facing draft |

Write-back: `growth-os/content-engine/`, one line per hook that held attention.
Metric: qualified replies or demo requests attributable to the asset. Not impressions.

One insight becomes five assets: a founder post, a short video script, a landing page line, a cold email angle, a calculator or lead magnet (`lead-magnets`).

---

## System 3: Outbound signal engine

Outcome shape: outbound has no reason-to-care this week. Timing is the product.

| Step | Leaf skill | What it does here |
| --- | --- | --- |
| Define the ICP | `outbound-engine` | End-to-end ICP definition, expert panel scoring, sequence copy |
| Build the list | `prospecting` | Find and qualify prospects across B2B SaaS and local |
| Resolve names to domains | `company-domain-resolver` | CSV or CRM export to clean domains before enrichment |
| Enrich, waterfall | `lead-intelligence` | Agent-powered signal scoring, mutual ranking, warm paths. Data stack: Apollo, LeadMagic, Apify, PredictLeads, BuiltWith, Findymail |
| Pull engagers | `linkedin-intelligence` | People who engaged with category content |
| Score the trigger | `signal-interpreter` | Why-now for this account, this week |
| Watch named champions | `champion-move-detection` | Champion moved to a new company = new account with a warm path |
| Refresh the database | `track-contact-job-changes` | Quarterly sweep for contacts who moved |
| Draft the touch | `cold-email` | Subject lines, opens, body, CTA, follow-up sequences |
| Draft the full sequence | `multichannel-campaign-builder` | Every touch across LinkedIn and email, three angles to choose from |
| Lifecycle and drip | `email-sequence` | Automated flows for anyone who converts |
| Sales collateral | `sales-enablement`, `sales-playbook` | Decks, one-pagers, objection handling, pre-call briefs |
| Warehouse pattern | `gtm-data-architecture` | Warehouse-native and zero-copy GTM data design |
| Final prose gate | `stop-slop` | Before the draft goes out for approval |

Write-back: `growth-os/outbound-engine/`, with banned language and approved angles updated after every review.
Metric: positive replies from qualified accounts. Messages sent is activity.
**Gate: draft only. A human sends.**

---

## System 4: Creative testing engine

Outcome shape: one angle ships and everyone hopes.

| Step | Leaf skill | What it does here |
| --- | --- | --- |
| Generate variations | `ad-creative` | Headlines, descriptions, primary text, full ad variations, any platform |
| Platform mechanics | `ads` / `paid-ads` | Google, Meta, LinkedIn, X campaign structure |
| Meta operating decisions | `meta-ads-operating-system` | Pause, scale, graduate, budget, creative count, with thresholds |
| Design the test | `ab-test-setup` | Split test design, sample size, what counts as a result |
| Page conversion | `cro`, `page-cro`, `form-cro`, `signup-flow-cro`, `onboarding-cro`, `popup-cro`, `paywall-upgrade-cro` | Conversion work, one skill per surface |
| Measurement | `analytics-tracking` | GA4, conversion tracking, event setup so results are readable |
| Images | `nano-banana` | All image generation. Required for any visual asset |

Write-back: `growth-os/creative-testing/results.md`, one row per angle with its result.
Metric: cost per qualified conversion by angle. Not click-through alone.

---

## System 5: AI search visibility

AI search sources from pages one through three of traditional results. Traditional SEO is how you get there. The content shapes that perform: "best X for Y", "X vs Y", "X alternatives", "X review".

| Step | Leaf skill | What it does here |
| --- | --- | --- |
| Read the live account | `seo-google` | Search Console, URL inspection, PageSpeed, CrUX, GA4 organic |
| Keyword data | `seo-dataforseo` | SERP, volume, difficulty, intent, trends, backlinks |
| Third-party data | `seo-ahrefs`, `seo-seranking`, `seo-bing` | Alternate providers when the primary source misses |
| Rank by intent | `seo-cluster` | SERP-overlap clustering, hub-and-spoke architecture, internal link matrix |
| Strategy and roadmap | `seo-plan` | Industry templates, competitive analysis, implementation order |
| Read what already ranks | `seo-competitor-pages`, `competitor-alternatives` | X vs Y layouts, alternatives pages, feature matrices |
| Diagnose a mismatch | `seo-sxo` | Reads SERPs backwards for page-type mismatch and persona scoring |
| Write the brief | `seo-content-brief` | Per-section word counts, competitor scoring, page-type templates |
| Add founder POV | positioning file + client voice skill | The step no competitor can copy |
| Draft the page | `seo-page` | On-page, meta, schema, images, page speed for one URL |
| Structured data | `seo-schema` | JSON-LD, rich results |
| AI-answer readiness | `ai-seo`, `seo-geo` | Citation readiness for ChatGPT, Perplexity, AI Overviews, Gemini |
| Measure citations | `seo-profound` | Time-series brand citation rates across LLMs |
| Technical floor | `seo-technical`, `seo-audit`, `seo-sitemap`, `seo-hreflang` | Crawlability, indexability, security, Core Web Vitals |
| At scale | `programmatic-seo`, `seo-programmatic` | Template-driven keyword coverage |
| Local | `seo-local`, `seo-maps` | Google Business Profile, NAP, citations, geo-grid |
| Crawl a site | `seo-firecrawl` | Full-site crawl and map |
| Links | `seo-backlinks` | Referring domains, anchor text, toxic links, competitor gap |
| Voice pass | client voice skill, then `stop-slop` | Before publish |

Write-back: `growth-os/content-engine/`, plus the brief archive.
Metric: citations and qualified organic demo requests. Not raw impressions.

**Link building, the concrete build:** `seo-backlinks` finds a stale page many sites link to → write the better version (`seo-content-brief` → `seo-page`) → `lead-intelligence` finds the linking sites' contacts → `cold-email` drafts the swap request → draft-only gate.

---

## System 6: Growth cockpit

Outcome shape: an executive wants one weekly view of what changed and what to do about it.

| Step | Leaf skill | What it does here |
| --- | --- | --- |
| Aggregate the week | `territory-signal-digest`, `competitor-monitoring` | Account movement and rival movement |
| Read the numbers | `analytics-tracking` | The tracking that makes the numbers real |
| Strategic synthesis | `product-marketing-lead` | Head-of-PMM layer across positioning, messaging, ICP, competitive intel |
| Plan the next move | `marketing-plan`, `marketing-ideas` | The full plan, and the tactic library |
| Render it | `html-output` | Single-file HTML report |

Write-back: `growth-os/agents/cockpit.md` for corrections; the memo itself to a reports folder.
Metric: decisions made from the memo. A memo nobody acts on is activity.

---

## Channel builds

Use when the outcome names a channel rather than a system.

| Channel | Order | Leaf skills |
| --- | --- | --- |
| Google Ads | Bottom-funnel keywords → ad groups as keyword families → keyword, ad, and landing page all say the same thing → negative-match by LLM intent judge | `seo-dataforseo` → `ads` → `ad-creative` → `page-cro` → `analytics-tracking` |
| Meta | Scrape desired outcomes → build ads around them → one Advantage+ campaign, broad, CBO, bid to the deepest event hitting ~50/week → spend the time on more creative | `customer-research` → `ad-creative` → `meta-ads-operating-system` → `nano-banana` |
| LinkedIn | Remix what already went viral in the category → publish → thought-leadership ad with a signup CTA → engagers feed cold outbound | `linkedin-intelligence` → `social-content` → `ads` → `lead-intelligence` → `cold-email` |
| Traditional SEO | Bottom-funnel brand-adjacent terms (X vs Y, X alternative, X review, how to X) → read page one → write with the client's POV → refresh monthly | See System 5 |
| Link building | Find the stale linked-to page → write better → outreach to its linkers | `seo-backlinks` → `seo-content-brief` → `seo-page` → `lead-intelligence` → `cold-email` |
| Cold email | LinkedIn engagers → 3-5 provider waterfall → validate → warm inboxes → send | `linkedin-intelligence` → `lead-intelligence` → `outbound-engine` → `cold-email` → draft-only gate |

---

## Skills the routing deliberately does not use

- **Clay.** A weaker fit than a direct-vendor data stack. This router never routes to it.
- **`hook-development`.** Despite the name, that's a Claude Code hooks skill, not a marketing-hooks skill.
- **Browser automation via a real, driven browser.** Any scraping step runs through a sandboxed or headless browser instead.

## The signal layer

A related set of ten free GTM skills (a hire, a job change, a funding round, a champion move, a rising term, a domain resolve, a multichannel sequence, a competitor move, a warehouse pattern, a cold email) covers the signal and data layer of this router. They stay separate leaf skills; this router names them per step above: `company-domain-resolver`, `track-contact-job-changes`, `champion-move-detection`, `territory-signal-digest`, `signal-interpreter`, `term-radar`, `multichannel-campaign-builder`, `competitor-monitoring`, `gtm-data-architecture`, `cold-email`.
