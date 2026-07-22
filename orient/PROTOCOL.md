# orient — canonical protocol (tool-agnostic)

Single source of truth for the `orient` skill across every harness (Claude Code, Codex, and any other). Tool-specific behavior — how it's triggered, and which menu legs each tool actually renders — lives in each tool's adapter; this file names every leg once (§3) so adapters can't drift, and each adapter says which it renders. Change the parse / mirror / confirm logic **here**, and let the adapters inherit it.

## What orient is

A session-opening alignment step. The user dictates a high-entropy braindump — multiple topics, filler, run-ons, no clear ask. orient mirrors back the **goals and objectives of the session** and **stops**. No work happens until the user confirms. The failure mode it prevents: latching onto sentence three and sprinting on the wrong thing. orient aligns; it does not execute.

## When NOT to orient

- A single scoped task ("fix the RLS flag on cold_outbound_accounts") — just do it.
- A pasted log, stack trace, spec, diff, or code block — read it, don't orient it.
- A normal short question — answer it.

## 1 — Parse (don't paraphrase into corporate)

Pull from the dump:

- **Goals** — the 1–3 outcomes the user wants _this session_. Outcomes, not tasks.
- **Objectives** — the concrete steps under each goal.
- **Tasks** — under any objective that bundles more than one action, the atomic, verb-first steps to do it. **Decompose only where it adds signal:** an objective that's already a single action ("set the RLS flag, confirm it sticks") stays a one-liner — no task list. Cap ~5 tasks per objective. Tasks here are a _read of the work_, not a contract: no dates, owners, estimates, or acceptance criteria — those belong to `goalify`. Crossing that line duplicates goalify.
- **Not today** — things mentioned but out of scope ("eventually", "at some point", "not now", or trailed off).
- **Open questions** — genuine ambiguities to resolve before sprinting.

Keep the user's actual phrasing for anything vague. "make the dashboard not suck" keeps "not suck" visible as an open question — do **not** smooth it into "improve dashboard UX". Cap goals at 3; group the overflow or make it an open question ("you touched 6 things — which are actually today?").

**Spotting open questions — five probe lenses** (from ce-brainstorm, grafted 2026-06-11). Lenses for _recognizing_ genuine ambiguity already in the dump — never for manufacturing questions when the dump is clear (the hard rule below stands):

- **Evidence** — a goal rests on an assumption nobody verified ("clients want X" — seen where?)
- **Specificity** — a vague phrase is doing load-bearing work (quote it, don't smooth it)
- **Counterfactual** — success is described, failure isn't ("what would make this a miss?")
- **Attachment** — a tool or solution is named where the underlying problem is unstated
- **Durability** — the ask hard-codes something that shifts (client, model, pricing) soon

When a goal escalates via `goalify <#>`, the same probes drive its clarify step (`goalify/REWRITER_PROTOCOL.md` Step 4) — orient surfaces the ambiguity, goalify resolves it.

**Parse craft — ask vs musing (Fable handover, 2026-07-06).** Dictated speech mixes three species; routing them wrong is orient's costliest failure:

- **The verb test.** Asks travel with commitment verbs near "I want / can you / let's / I need." Musings travel with "I wonder / I keep thinking / at some point / it'd be cool if." A musing routes to Not-today or an open question — never to a goal. Building a musing is the most expensive misread available.
- **Repetition outranks position.** The topic that comes back twice is the real priority, even phrased as an aside, even arriving mid-ramble. Conversely: the last topic dictated is merely the freshest thought, not the most important. Weight by return-visits and emphasis (profanity, "really", "I keep"), not by order.
- **An aside that contains a decision is a constraint, not a topic.** "Oh and we're off that tool now, by the way" doesn't get its own goal — it attaches to every goal it silently modifies.
- **Trailing deferral is explicit scope.** "We can talk about that later" / "but that's a separate thing" = Not-today, verbatim, every time. Don't promote it because it sounds interesting.

## 1.5 — Pre-render self-test (silent)

Answer these before rendering the mirror; any "no" means re-parse, not render:

1. Which single phrase in the dump carries the most unstated intent — and does it appear verbatim in the frame?
2. What did he circle back to twice — and is it goal #1, or is there a stated reason it isn't?
3. Which part of the frame am I most tempted to smooth into cleaner language? (That's the part to quote instead.)
4. Is anything in the frame my inference wearing his words? Move it to an open question or mark it.
5. If he replies `go` right now, could I start every goal without asking another question? Whatever I'd have to ask is an open question — surface it now.

## 2 — Mirror back (this is the entire turn)

No preamble. No "Great, here's what I heard." Lead straight into the frame:

```
Goals — this session
  1. <goal> — <one-line outcome>
  2. <goal> — <one-line outcome>

Objectives & tasks
  #1 <objective — concrete step>
     - <task>
     - <task>
  #2 <objective — atomic, no breakdown needed>

Not today (heard it, parked it)
  - <thing>

Open questions (answer before I sprint)
  - <q>
```

Omit any empty section. If there are no open questions, say so in one line — don't invent them. Nest tasks **only** under objectives that bundle 2+ actions; leave an atomic objective as a single line (don't pad it with a one-item list).

**Mirror quality bar — a frame passes when all of these hold (pass/fail, no adjectives):**

- [ ] Every sentence of the dump maps to a goal, objective, task, not-today, or open question — or is filler you could name if asked.
- [ ] Goals ≤ 3.
- [ ] Every load-bearing vague phrase appears verbatim, in quotes, somewhere in the frame.
- [ ] Every open question traces to actual dump text — zero invented questions.
- [ ] Any topic mentioned twice or more appears as a goal or an explicitly-reasoned open question — never silently dropped.
- [ ] Zero work tool-calls before `go`; reads only if strictly needed to render the frame.
- [ ] The confirm menu is rendered, once, at the end — and the turn stops there.

A frame that fails any line gets fixed before rendering, not annotated after.

## 3 — Offer the menu, then STOP

End every mirror with the confirm menu. The base menu, always rendered:

```
  go            → lock this frame, work normally from here
  goalify <#>   → structure goal # into a locked autonomous goal-loop
  workflow <#>  → build + run a multi-agent harness on goal #
  …or reply in plain words — corrections, "look again", "break goal N down"; the frame updates and re-renders
```

**The verbs are shortcuts, not a grammar.** Any free-text reply is valid: a correction re-renders the frame (the old `fix`), "look again" re-scans the dump for anything this frame dropped (the old `deepen`), "break goal N down" expands that goal's task tree (the old `tasks`). Only `go` locks the frame. Roughly 60% of real replies are plain words — treat free text as the default path, not a fallback.

Append these two lines **only when the mirror itself flags the condition** — the standing menu stays lean, and the line rides the in-mirror callout the paragraphs below already mandate:

```
  grill <#>     → goal # is high-stakes: interview → locked PLAN.md → Codex attacks it
  blindspot <#> → goal # is unfamiliar territory: read-only unknowns sweep first
```

When a goal is visibly high-stakes, say so in the mirror and recommend `grill <#>` for it — don't wait for Julian to remember the option exists. High-stakes for Julian's work, evidence-ranked in an internal registry: outbound sends (list/volume/sender) · client CRM or data writes · pricing or commercial commitments · client copy where the voice/persona could be wrong · send-infra/deliverability config · real-money moves · secrets · autonomous loops with external reach · client-visible deploys · bulk enrichment spend · client-facing automation output (reports/digests) · modifying human-approved copy. Classic software stakes (auth, schema, migrations) count where he actually builds — Supabase, dashboards.

When a goal visibly touches territory neither Julian nor the session knows — a new domain, an unfamiliar part of a codebase, or no prior art in the vault or memory — say so in the mirror and recommend `blindspot <#>`. Assess this only from what's already visible in the dump; do not make tool calls to decide (extends the "Kept lazy" rule).

Adapters add or drop the tool-specific legs. `workflow <#>` and `grill <#>` are Claude Code legs: the Claude adapter renders `workflow` in the base menu and `grill` when a goal is flagged high-stakes; the Codex adapter renders neither — no dynamic-workflows engine, and the grill chain is Claude-driven — and instead points to Claude Code when the shape fits. `blindspot <#>` is tool-agnostic: any harness carrying finding-unknowns renders it contextually. After the menu, **stop**. Do not begin work. Do not read files "to get a head start." The mirror + menu is the whole response.

## 4 — On the response

- **`go`** → print `Frame locked.` Hold the frame as the session's north star; before claiming any goal done, re-check it against its objectives and flag drift rather than silently expanding.
- **Free text — the default reply** → the verbs are shortcuts; plain words do the same jobs and re-render the frame:
  - A **correction** ("no, goal 2 is really about X", "drop the third one") updates only that part of the frame, re-renders, re-offers the menu (the old `fix`).
  - **"Look again" / "re-scan" / "what did you miss"** → one-shot re-parse of the original dump plus any replies since, hunting for goals, objectives, tasks, or constraints the frame dropped — apply the five probe lenses while hunting. Re-render with anything new marked `(recovered)`, re-offer the menu (the old `deepen`; same meaning as goalify's lock-time `deepen`, never a gate).
  - **"Break goal N down"** → on-demand override of the auto-hybrid: break goal N _all the way_ down into its task tree, decomposing every objective under it into atomic steps — including the ones the default mirror left as one-liners. Re-render goal N with the expanded tasks, re-offer the menu. Still a read, not a contract (no dates / owners / criteria — that's goalify's job); this deepens only the task layer of one goal you already see (the old `tasks`).
  - Anything else that reads as intent about the frame → apply it and re-render. When a reply is genuinely ambiguous, ask one sharp question instead of guessing.
- **`goalify <#>`** → invoke the `goalify` skill on goal #. goalify owns classification, the mega-prompt, the lock, and the run from there.
- **`blindspot <#>`** _(contextual — the menu line renders only when the mirror flagged goal # as unfamiliar territory, but the verb still works if typed against any goal)_ → run the finding-unknowns skill's Ritual 1 on goal #: sweep the territory (reads only — repo, docs, git history, memory), report 3–7 unknowns in plain English, each tagged `[needs Julian]` or `[I can resolve — doing it]`, fold them into the frame's Open questions, re-render, re-offer the menu. Like a re-scan, this is an escalation read, not work — the no-work-before-`go` rule stands.
- **`grill <#>`** _(contextual — the menu line renders only when the mirror flagged goal # as high-stakes, but the verb still works if typed against any goal)_ → invoke the `grill-me-codex` skill on goal #: Act 1 interviews Julian until the plan is locked into `PLAN.md`, Act 2 has Codex adversarially review it (bounded rounds), optional Act 3 hands the build to Codex with Claude as diff-reviewer. For a goal that already has a written plan, `codex-plan-review` is the direct door (Act 2 only). Use for high-stakes goals where being wrong is expensive; goalify remains the door for autonomous routine builds.

A tool adapter handles any options it added (Claude Code: `workflow <#>`).

## Loop shape

Per Anthropic's loop taxonomy: orient is one iteration of a **turn-based loop** whose stop condition is the confirm menu — the human is the evaluator. Deliberately no judge model, no turn caps, no goal-loop machinery inside orient itself; those live behind the escalation hatches (`goalify`, tool adapters). If orient ever needs a cap, that's a sign work leaked into it — the bug is the leak, not the missing cap.

## Kept lazy

The base mirror does **not** classify work-type — it's a fast reflection, not a goal-loop. Only at escalation (when the user picks `goalify <#>`, or a tool-specific option) do you reach for a classifier. Don't pre-classify; it's wasted work if the user just says `go`.

## Hard rules

- **The mirror is the whole turn.** Never start work before `go`. No file reads, edits, or tool calls beyond what's needed to render the frame.
- **One to three goals, max.** More than that, ask which matter today.
- **Decompose only where it adds signal.** Break an objective into tasks only when it bundles 2+ actions; atomic objectives stay one-liners. Never pad a frame with busywork tasks just to fill the tier.
- **Tasks are a read, not a contract.** No dates, owners, estimates, or acceptance criteria in the mirror — those are `goalify` territory. orient shows the _shape_ of the work; goalify locks it.
- **Quote, don't smooth.** Keep vague phrasing visible as an open question instead of inventing a polished version.
- **Don't fabricate open questions.** If the dump is clear, say "No open questions — confirm and go."
- **Don't orient a non-dump.** See "When NOT to orient" above.
- **Banned words** (Julian's global rules): never use _leverage / synergy / disrupt / game-changer_.
- **No vault writes.** orient aligns; it does not file notes (that's `braindump`).
