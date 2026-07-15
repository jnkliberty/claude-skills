# Orient — worked examples

Few-shots in Julian's real dictation voice. The inputs are deliberately messy (filler, run-ons, lowercase) because that's what VoiceInk drops in. The mirrors are tight because that's the whole point.

---

## Example 1 — multi-topic dump → `go`

**Julian (voice):**

> ok so today i wanna get back into the client marketing metrics dashboard, the attribution thing — i think i left it with the funnel chart half wired. and also i keep meaning to close out that RLS flag, it's been sitting open forever. oh and at some point i should probably look at the investor invoice table but that's not really today honestly

**orient:**

```
Goals — this session
  1. Client marketing-metrics dashboard — finish the attribution view
  2. RLS flag — close it out

Objectives & tasks
  #1 finish the attribution view
     - wire the funnel chart to the live data
     - verify the attribution query returns correct numbers
  #2 set the RLS flag on accounts; confirm it sticks
     (atomic — no breakdown needed)

Not today (heard it, parked it)
  - investor invoice table ("not really today")

Open questions (answer before I sprint)
  - #1: "half wired" — is the funnel chart rendering at all, or stubbed?

  go            → lock this frame, I work normally from here
  fix <thing>   → correct the frame first
  deepen        → re-scan the dump for anything this frame dropped
  tasks <#>     → break goal # all the way down into its task tree
  goalify <#>   → hand goal # to goalify (structure → autonomous goal-loop)
  /goal <#>     → push goal # straight into /goal now (raw, no structuring)
```

**Julian:** `go`

**orient:** `Frame locked.` → then works #1 then #2, re-checking each against its objectives before calling it done.

---

## Example 2 — one shippable goal → escalate with `goalify`

**Julian (voice):**

> alright so basically i want to build that little free deliverability scorer thing for gtm.run, like a tool page where someone drops their domain and it checks spf dkim dmarc and gives a score. next.js, supabase if it needs storage. i kinda know what i want here

**orient:**

```
Goals — this session
  1. Free deliverability scorer at gtm.run/tools — ship a working tool page

Objectives & tasks
  #1 ship the tool page
     - domain input field
     - check SPF / DKIM / DMARC
     - compute + render a score
     stack: Next.js (+ Supabase if storage needed)

Not today
  - (nothing parked)

Open questions
  - No open questions — this reads as a clear build. Confirm and go,
    or hand it to goalify to harden into a /goal run.

  go            → lock this frame, I work normally from here
  fix <thing>   → correct the frame first
  deepen        → re-scan the dump for anything this frame dropped
  tasks 1       → break goal 1 all the way down into its task tree
  goalify 1     → hand goal 1 to goalify (structure → autonomous goal-loop)
  /goal 1       → push goal 1 straight into /goal now (raw, no structuring)
```

**Julian:** `goalify 1`

**orient:** Invokes the `goalify` skill on goal 1. Goalify classifies it (`build`), renders the mega-prompt, asks for measurable criteria, locks, and runs the goal-loop. orient's job is done at the handoff.

---

## Example 3 — it's actually ideation → flag it, don't fake objectives

**Julian (voice):**

> hmm so i've been kicking around this idea, not sure what the shape is yet, but like what if gtm.run had some kind of community thing, a slack or a circle or whatever, for fractional gtm people. i don't know if it's a lead magnet or a product or what

**orient:**

```
Goals — this session
  1. (unclear) — explore whether a gtm.run community is worth building

Objectives
  - none yet — there's no shape to break into steps

Open questions (these ARE the work right now)
  - is this a lead magnet, a paid product, or a brand play?
  - who's it for, exactly — your ICP or a broader audience?
  - what would make you call it a success vs. a distraction?

This reads as ideation, not a build — there's nothing to sprint on yet.
Want to talk it through (I ask, you answer, no code), or is there a
concrete first goal hiding in here I should mirror instead?
```

(No `go`/`goalify` menu here — you can't lock a frame that has no shape. Route to a conversation, or to `goalify`'s ideation interview if he wants structure.)

---

## Anti-example — pasted log → DO NOT orient

**Julian (paste):**

> ```
> Error: relation "accounts" does not exist
>     at Parser.parseErrorMessage (/node_modules/pg/lib/...)
>     at Socket.<anonymous> ...
> ```
>
> why is this happening

**orient:** _(does not fire)_ — This is a pasted error + a single scoped question. Skip the skill. Read the trace, diagnose, answer. Orienting a stack trace wastes a turn.
