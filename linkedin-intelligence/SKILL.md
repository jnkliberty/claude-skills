---
name: linkedin-intelligence
description: Data-backed LinkedIn optimization layer for producing high-performing LinkedIn content. Based on 62,130 viral posts analyzed (David Arnoux / viralbrain.ai, January 2026, BREW360 algorithm).
model: sonnet
allowed-tools:
  - WebSearch
  - WebFetch
  - mcp__exa__*
  - mcp__claude_ai_Exa_Search__*
---

# LinkedIn Intelligence

## Purpose

Optimize LinkedIn posts for reach and engagement using data from 62,130 viral posts. This skill adds LinkedIn-specific optimization on top of general copywriting quality.

## References

Read `references/algorithm-cheatsheet.md` for full data tables: BREW360 breakdown, timing, engagement rates by follower tier, format performance, character length data, paragraph count data, reading level data, hashtag data, reply frequency, word count brackets, top performer characteristics, weighted engagement rate benchmarks.

Read `references/hook-patterns.md` for hook taxonomy with win rates (curiosity gap, emotional, contrarian, story opener, bold claim), anti-patterns, two-line formula templates, ending pattern comparison including comment-for-access CTA, and transformation arc structure.

---

## Non-negotiable rules (DO)

### 1. Two-line hook formula

Every LinkedIn post opens with a two-line hook. This is the scroll-stopper.

```
Line 1: Punch. Bold claim, surprising number, or blunt honesty.

Line 2: Gap. The thing the reader needs to fill. Creates curiosity.
```

**The blank line between Line 1 and Line 2 is critical.** It creates visual breathing room and builds anticipation. Never skip it.

### 2. Curiosity gap hooks by default

Curiosity gap hooks average 6,280 engagement actions with a 66% win rate. Use them as the default hook type. Example: "Filed my LLC. Total cost: $425." is a curiosity gap. Lean into this pattern.

### 3. Post length: 200–350 words (1,250–2,200 characters)

Research says 1,250–3,000 characters (31% better engagement). Posts with 350+ words get 2.5x higher median engagement than short posts. Target range: **200–350 words / 1,250–2,200 characters.**

### 4. 14+ short paragraphs with line breaks

71% improvement over wall-of-text posts. Short paragraphs with spacing. If a paragraph has more than two sentences, break it. **But vary the rhythm** — mix one-liners with 2-3 sentence blocks. The writing should breathe, not stutter.

### 5. Grade 5–7 reading level

Posts with complex words (average 5+ letters) see 39% less engagement. Use short words. This aligns with copywriting ("80–90% one- and two-syllable words").

### 6. 0–2 hashtags maximum

3+ hashtags perform 70% worse. LinkedIn's BREW360 algorithm reads text directly — hashtags are redundant. Use zero if the post is strong. Use 1–2 only if they serve a specific community signal (like #BuildInPublic).

### 7. Personal story with transformation arc

100% of viral patterns include personal stories embedded in business/technical content. But the best viral posts go further — they show a **transformation arc**: a character faces a problem, goes through a specific change or realization, and arrives somewhere new.

Make sure each story has a clear transformation. Not just "here's what happened" but "here's who I was before, what shifted, and where I landed."

### 8. IMAGE format recommendation

IMAGE posts get 2.1x more engagement than text-only (545 avg vs 263). 8 of the top 10 viral posts use images. Top 10% performers all use IMAGE format.

When generating LinkedIn posts, include an image placeholder when one fits:

```
[IMAGE — detailed description of what nano-banana or remotion should create]
```

Not every post needs an image. But default to recommending one. Text-only is fine when the words carry everything — but IMAGE should be the first consideration.

### 9. Emoji override for LinkedIn

**Override the copywriting skill's emoji ban for LinkedIn posts.** Emojis boost LinkedIn performance by 220%. Use them to:

- Break up text visually
- Direct eyes to CTAs
- Add visual rhythm between paragraphs

Not mandatory on every post. Use when they serve the content — bullet separators, section markers, emphasis on key lines. Don't spray them randomly.

### 10. Profile-content alignment (BREW360)

BREW360 matches content to readers based on profile-content alignment. Target lanes:

- GTM automation and AI systems
- Solo consulting and freelancing
- Building in public
- Software engineering and AI tools
- Personal reflection on the entrepreneurial journey

Post in these lanes. The algorithm amplifies niche-aligned content.

### 11. End with a provocative statement, specific ask, direct challenge, or comment-for-access CTA

Never end with a generic question. "Thoughts?" and "What do you think?" are dead — they read as engagement bait. Instead:

- **Provocative statement:** A bold claim that invites contradiction or agreement
- **Specific ask:** A concrete request ("Drop a DM if you want the template")
- **Direct challenge:** Challenge the reader to act ("Look at your homepage demo. Does it show what you actually built?")
- **Comment-for-access CTA:** Describe a high-value resource, ask users to comment a specific keyword, offer to send it. Structure: "1. Connect with me 2. Comment [keyword] 3. Repost for priority access." 4 of the top 10 viral posts use this pattern. One got 5,286 comments. Works best when paired with a genuine resource offer.

### 12. Subtle product promotion

When promoting a product (gtm.run, a tool, a service), embed it within a value-first story rather than pitching directly. The top viral posts that promote products all lead with story or insight first and mention the product naturally afterward. The reader gets value whether they click or not.

### 13. Authority engagement

Comments from influential figures signal the algorithm to show your post to their entire network. When engaging with others' content, your comments amplify your own reach. Thoughtful comments on high-profile posts are a growth lever.

### 14. Signature phrases

Use consistent phrases to build trust and recognition over time. Recurring language patterns make content instantly recognizable in the feed.

### 15. Posting schedule

- **Best day:** Sunday (457 avg engagement)
- **Good day:** Tuesday (422 avg engagement)
- **Avoid:** Saturday (301 avg engagement — worst day)
- **Time window:** 12–2 PM UTC (Midday) or 3–5 PM UTC (Afternoon) — both equally strong. Best specific hours: 12:00, 15:00, 22:00 UTC.
- **Frequency:** 3–5x per week. Not daily. Daily posting hurts reach.

---

## AVOID list (DON'T)

### List-promise hooks

"7 ways to..." and "5 things you need to..." are dead last in hook performance (28 avg engagement, 0% win rate). Overused. Clickbaity. Never use them.

### Generic ending questions

"Thoughts?" / "What do you think?" / "Agree?" — all dead. They read as engagement manipulation under BREW360. Use provocative statements, specific asks, direct challenges, or comment-for-access CTAs instead.

### 3+ hashtags

70% worse performance. The algorithm reads your text directly. Hashtags are redundant at best, spammy at worst.

### Corporate jargon

The #1 reason for post failure in the dataset. Jargon kills emotional connection.

### Saturday posting

Worst day for any creator analyzed. 301 avg engagement vs. Sunday's 457. Save your best content.

### Short shallow updates

Long-form (1,250+ chars) drives 31% better engagement. Quick updates without depth don't perform.

### Wall of text

No paragraph breaks = scroll past. Always use 14+ short paragraphs with spacing.

### Deleting underperforming posts early

BREW360 can resurface posts days later if engagement continues. Don't delete in the first hour. Give it time.

### Direct product pitches

Never lead with the product. Lead with value, story, or insight. Product comes naturally after.

---

## Small account advantage

Accounts under 10K followers have a built-in advantage.

| Account Size  | Engagement Rate |
| ------------- | --------------- |
| <1K followers | 2.38%           |
| 1K–10K        | 1.00%           |
| 10K–50K       | 0.88%           |
| 100K+         | 0.25%           |

**369% higher engagement** for accounts under 10K vs. 50K+. Smaller accounts have tighter communities who actually engage. Optimize for engagement (comments, replies, conversations) over raw impressions. Reply to every comment with substance.

The top 1% of creators reply 286 times per week — 741% more often than average. Engagement begets engagement.

---

## High-opportunity topics

These topics are underserved on LinkedIn with high engagement potential:

| Topic                | Avg Engagement     | Note                            |
| -------------------- | ------------------ | ------------------------------- |
| Personal Development | 1,517              | Highest overall                 |
| Communication        | 1,238              | 13% viral rate                  |
| Marketing Automation | 959                | Core lane for GTM content       |
| Software Engineering | High interest      | 13% viral rate, low competition |
| Personal Reflection  | Exceptional        | Underrated but top-performing   |
| Sales / Automation   | Best comment ratio | Strong early momentum           |

Build-in-public content at the intersection of Software Engineering, Marketing Automation, and Personal Reflection is a high-opportunity zone.

---

## Pre-posting checklist

Run before publishing any LinkedIn post:

- [ ] Hook uses two-line formula with blank line between
- [ ] 1,250–2,200 characters / 200–350 words
- [ ] 14+ short paragraphs with line breaks
- [ ] Grade 5–7 reading level (short words, simple sentences)
- [ ] 0–2 hashtags
- [ ] Personal story with transformation arc (who before → what shifted → where landed)
- [ ] IMAGE considered — placeholder included if one fits
- [ ] Emojis used strategically (not banned on LinkedIn — 220% boost)
- [ ] Ending is a provocative statement, specific ask, direct challenge, or comment-for-access CTA
- [ ] Content aligns with target lanes (GTM, AI, solo consulting, build-in-public)
- [ ] Writing breathes — varied paragraph lengths, not staccato fragments
- [ ] Scheduled for Sunday or Tuesday, 12–2 PM or 3–5 PM UTC

---

## Override rule

If a voice/style skill is configured, it takes priority over algorithm rules. The data serves the writing — never the reverse.
