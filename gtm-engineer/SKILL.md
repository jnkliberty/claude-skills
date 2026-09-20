---
name: gtm-engineer
description: Use when a client outcome requires several marketing skills composed into one recurring system. Return the routed growth system or channel build and an agent job spec for approval. Never run the campaign; use a leaf skill for a one-off post, email, or audit.
---

# Marketing Engineer: outcome to agent job spec

Marketing, GTM, and SEO leaf skills each do one task. None of them composes a client outcome into a system that keeps running. This skill is that composer.

Input: an outcome someone wants. Output: a written agent job spec, plus the routing table of which leaf skills execute each step. Then it stops and waits for you.

## What this skill expects

The routing table names leaf skills by role, not by exact package. The ones on this shelf (`cold-email`, `lead-magnets`, `signal-interpreter`, `linkedin-intelligence`, `stop-slop`) install straight from this repo. The rest (`seo-*`, `customer-research`, `territory-signal-digest`, and others named below) are placeholders for whatever tool or skill does that job in your own setup. Swap them freely; the routing and the job-spec format are the part that travels.

## When to use it

- An outcome is stated in business terms, not task terms. "More qualified demos from a specific segment." "Get cited by ChatGPT for our category."
- The answer needs three or more skills in sequence, and something has to run again next week.
- Someone asks what to build first for a client.
- A leaf skill produced a one-off and you're asked how to make it recurring.

## What it is not

| Not this | Use instead |
| --- | --- |
| A campaign runner. It never sends, publishes, or spends. | The leaf skill, after approval |
| The SEO audit | `seo-audit`, `seo-technical`, `seo-plan` |
| A goal contract | `goalify` locks a `/goal` for one autonomous run. This produces a job spec for a repeating agent |
| A workflow build | `workflow-architect` scaffolds the harness. This decides what the harness should do |
| A single deliverable | `cold-email`, `copywriting`, `seo-page`, whichever leaf matches |

## Step 1: Locate the client's Growth OS

The repo prompt beats the weak prompt. Weak: "write me ten LinkedIn posts." Repo: "read the customer truth file, read the voice file, read the last five posts that drove qualified replies, then draft five posts about the pains buyers raised this week." Same model, different context.

So before drafting anything, find the six standing files. They live in the client project root. Read the map file first:

```
<client project root>/GROWTH-OS.md
```

Format is one line per folder, folder name then path:

```markdown
# Growth OS: <client>

| Folder | Path | Last updated |
| --- | --- | --- |
| positioning | docs/positioning.md | 2026-09-02 |
| customer-truth | growth-os/customer-truth/ | 2026-09-01 |
| content-engine | growth-os/content-engine/ | 2026-08-28 |
| outbound-engine | growth-os/outbound-engine/ | 2026-08-30 |
| creative-testing | growth-os/creative-testing/ | 2026-08-22 |
| agents | growth-os/agents/ | 2026-09-02 |
```

What each folder holds:

- **positioning**: the standing claim, the sharp angle, the segment. One file.
- **customer-truth**: sales call notes, support tickets, churn notes, interviews, product feedback. Whatever raw feed captures those (call recordings, a support inbox export, a CRM notes field) is the source here.
- **content-engine**: voice guide, winning hooks, scripts, notes on what performed.
- **outbound-engine**: ICP, account research, trigger events, approved angles, banned language.
- **creative-testing**: ad angles, landing page tests, hooks, offers, results.
- **agents**: one job spec per AI worker, plus the correction log for each.

If `GROWTH-OS.md` does not exist, create it before anything else and mark missing folders as `MISSING`. A missing folder is a finding, not a blocker. Report which ones are missing when you present the spec.

## Step 2: Classify the outcome

Route to exactly one of six systems, or one channel build. One working system beats five half-built ones.

| # | System | The outcome sounds like |
| --- | --- | --- |
| 1 | Customer truth | "We all walk into the growth meeting with a different version of reality" |
| 2 | Founder content engine | "The founder sounds sharper than our marketing does" |
| 3 | Outbound signal engine | "Our outbound has no reason-to-care this week" |
| 4 | Creative testing engine | "We ship one ad angle and hope" |
| 5 | AI search visibility | "Nobody cites us in ChatGPT or AI Overviews" |
| 6 | Growth cockpit | "What changed last week and what do we do about it" |

Channel builds, when the outcome names a channel: Google Ads, Meta, LinkedIn, traditional SEO, link building, cold email.

The full routing table, system by system and channel by channel, with the exact leaf skills in order, is in `references/routing-table.md`. Read it before drafting the spec.

## Step 3: Emit the job spec

Write every agent spec the way you would write a job description. Seven fields, all seven filled, no placeholders:

```markdown
## Agent: <name>

**Data source**: which systems, which files, which APIs. Name them.
**Run schedule**: weekday morning, every Monday, on new-call-landed. Absolute, not "regularly".
**Filters**: what gets dropped before the agent thinks. ICP bounds, recency, exclusions.
**Expected output + what good looks like**: the artifact, its path, and one sentence describing a good one.
**Approval step**: who reviews, where the draft lands, what blocks the send.
**Metric that matters**: signal, never activity. Qualified replies, not messages sent.
**Write-back location**: which Growth OS folder gets the result, so the system gets smarter.
```

Under each field, name the leaf skills that do the work. Example, SEO opportunity to published page:

`seo-google` (Search Console) → `seo-dataforseo` (volume, difficulty, intent) → `seo-cluster` (rank by intent) → `seo-competitor-pages` (read what ranks) → founder POV from the positioning file → `seo-content-brief` → `seo-page` → client voice skill → human approval.

Example, cold email:

`linkedin-intelligence` (pull engagers) → `lead-intelligence` (waterfall enrichment) → `signal-interpreter` (score the trigger) → `cold-email` or `multichannel-campaign-builder` (draft) → `stop-slop` → draft-only gate.

## Step 4: STOP

Present the spec. Do not build it. Do not run it. Wait for approval.

On approval, hand execution to one of two places:

- Recurring system → `workflow-architect`, which scaffolds and schedules the harness.
- One-off proof run → the named leaf skills, in the spec's order, once.

**Train it like a new hire.** Start with a scope smaller than the spec allows. Watch the first three runs. Every correction goes into the client's Growth OS `agents/` folder as a line under that agent's spec. Widen scope only after a clean run. Corrections compound; unlogged corrections evaporate.

## Pre-flight: infrastructure checklist

An agent is code with a thinking loop pointed at a live data stream. Before promising a recurring system, check what the executing agent can actually reach. Answer yes or no for each, in writing:

| Capability | Have it? | Notes |
| --- | --- | --- |
| Data pipeline (source to store) | | |
| Data warehouse or analytics store | | |
| Cloud server for scheduled runs | | |
| Media storage (images, video) | | |
| Postgres for agent state | | |
| Cron or launchd for recurring tasks | | |
| Application authentication | | |
| Shareable links for review | | |
| Git origin for multiplayer access | | |
| API gateway (Apollo, Apify, PredictLeads, DataForSEO, nano-banana) | | |

Any `no` becomes a line in the spec under a `Blocked on` heading. Do not design around a capability the client does not have.

## House rules that override the source articles

- **No Clay.** A weaker data stack than a direct-vendor stack. Default data stack: Apollo, LeadMagic, Apify, PredictLeads, BuiltWith, Findymail.
- **Draft, don't send.** Every spec touching an outbound surface, client CRM, or a published page carries a human approval field. Say the gate out loud before drafting: "drafting only, you send."
- **Never drive a real browser for scraping.** Route any scraping step through a sandboxed or headless browser instead.
- **Client copy uses that client's own voice skill**, if one exists.
- **The four house-banned words never appear** in the spec or in anything it produces: leverage, synergy, disrupt, game-changer.
- **High-stakes specs go through a plan review before execution** if they touch a registry stake (outbound sends, client CRM writes, pricing, send infrastructure, real money).

## Worked example: illustrative only

A B2B SaaS client selling to marketing and RevOps teams wants more demo requests from a specific segment. No client facts below are real; this is shape, not data.

```markdown
## Agent: segment-demo-signal

Data source: CRM closed-won and closed-lost from the last 4 quarters;
  call notes from the customer-truth feed; the positioning file; LinkedIn
  engagers on the last 10 company posts.
Run schedule: every Monday 07:00, plus on any new call landing in the customer-truth feed.
Filters: accounts matching the ICP band in outbound-engine/icp.md only;
  drop anyone touched in the last 45 days; drop non-decision titles.
Expected output + what good looks like: growth-os/customer-truth/what-the-market-is-telling-us.md,
  rewritten weekly. A good memo quotes five real lines from calls this week
  and names one test that creates pipeline, with the receipt for each claim.
Approval step: the operator reads the memo. Nothing leaves the workspace until
  the named test is approved.
Metric that matters: demo requests from the target segment. Not memo length,
  not accounts scanned.
Write-back location: growth-os/customer-truth/, and corrections to growth-os/agents/segment-demo-signal.md.

Leaf skills: customer-research → signal-interpreter → territory-signal-digest
  → product-marketing-context (positioning check) → html-output (the memo)
Blocked on: no warehouse, so CRM pulls run through the API each week.
```

## Related

`references/routing-table.md` · `workflow-architect` · `goalify` · `product-marketing-lead`
