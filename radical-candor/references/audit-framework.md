# 7-Layer Audit Framework

Reference document for the Radical Simplicity & Candor Audit. Read this file during every audit to ensure all layers are covered with full depth.

---

## Layer 1: Core Purpose Extraction

Reduce the audit target to its essence.

**Sub-questions:**

- State what this does in one sentence. If the sentence requires "and," it's doing too much.
- Who is the specific user? Not a persona. A real person with a real problem.
- What is the single primary outcome this delivers?
- What is the "aha moment" - the first time the user gets value?
- How many steps from start to aha moment?
- What would you cut if forced to ship in one week?

**Red flags:**

- Multiple "core" purposes competing for attention
- Can't explain it without jargon
- The aha moment requires setup, configuration, or onboarding
- Value is promised but deferred ("once you set up X, then you can...")

---

## Layer 2: Overengineering Detection

Identify everything that doesn't directly strengthen the core outcome.

**Sub-questions:**

- List every feature, module, service, or component. For each: does removing it break the core outcome?
- Which parts exist for hypothetical scale that hasn't been earned?
- Which abstractions exist because "we might need flexibility later"?
- Which tools, libraries, or services compensate for unclear goals?
- Where does the architecture serve the builder's resume more than the user's outcome?
- Which configuration options could be hardcoded decisions?
- Which API endpoints have zero or near-zero usage?
- Which database tables/columns are written but never read?

**Red flags:**

- Microservices for a team of 1-3
- Abstract factory patterns for one implementation
- Plugin/extension systems with zero third-party plugins
- "Flexible" configuration that nobody changes from defaults
- Multiple caching layers before measuring what's slow
- Event-driven architecture for synchronous workflows

---

## Layer 3: Cognitive Load Audit

Count the mental cost of using and understanding this thing.

**Sub-questions:**

- How many decisions must a user make before getting value?
- How many concepts must someone understand to use this?
- How many steps to first success?
- Where do users hesitate, pause, or need documentation?
- How many navigation levels deep is the primary action?
- How many settings/options exist? How many are actually changed from defaults?
- Can a new team member understand this in one sitting?

**For code audits specifically:**

- How many files must you read to understand a single flow end-to-end?
- How many layers of indirection between an action and its effect?
- How many different patterns are used for the same type of operation?
- How many environment variables are required to run locally?

**Red flags:**

- More than 3 decisions before first value
- Documentation required for basic usage
- Onboarding takes more than 10 minutes
- More than 5 environment variables for local dev
- More than 3 levels of directory nesting for primary code
- Multiple competing patterns for the same operation

---

## Layer 4: Psychological & Incentive Audit

Expose the human motivations behind complexity.

**Sub-questions:**

- What fear is driving this complexity? (Fear of scale? Fear of looking unsophisticated? Fear of edge cases?)
- Where does building sophistication reward the builder's ego more than the user's outcome?
- Which future scenarios are being overweighted vs. present user needs?
- Is this built for users or for people evaluating the architecture?
- What would a pragmatic competitor build instead?
- Where is "best practice" being followed without questioning whether it applies here?
- Which decisions were made to avoid a conversation rather than to serve the user?

**Red flags:**

- "We need this for when we scale" (before product-market fit)
- "This is how [Big Tech Company] does it"
- Complex CI/CD for a project with one developer
- Kubernetes for an app that could run on a single server
- GraphQL for an API with 3 consumers
- Feature flags for features that will never be toggled back

---

## Layer 5: Architectural Earned Complexity

Every piece of complexity must justify its existence with evidence, not theory.

**Sub-questions:**

- For each service/module: why can't this be part of the main application?
- Could the entire system be one service? What specifically prevents that?
- List every external dependency. For each: what happens if you replace it with 50 lines of code?
- Where is state stored? Can the number of state locations be reduced?
- Is data flow explicit and traceable, or hidden behind events/queues/middleware?
- How many different data formats/serialization methods are used?
- How many different communication protocols are in play?

**Earned complexity test:** For each piece of complexity, answer:

1. What specific, measured problem did this solve?
2. What was tried before this that was simpler?
3. What would break if this were removed tomorrow?

If the answer to #1 is theoretical, #2 is "nothing," or #3 is "nothing," the complexity is unearned.

**Red flags:**

- Services that could be functions
- Queues that could be direct calls
- Separate databases that could be tables
- API gateways for internal communication
- ORMs for simple queries
- State management libraries for 3 pieces of state

---

## Layer 6: Strategic Focus

Audit whether the strategy is a sharp wedge or a dull platform.

**Sub-questions:**

- Is this a wedge (one thing done exceptionally) or a platform (many things done adequately)?
- Can the value proposition be stated and repeated in 10 seconds?
- Does messaging focus on the outcome or the mechanism?
- How many different user segments are being targeted simultaneously?
- What is being said "no" to? If the answer is "nothing," focus is absent.
- Is the competitive advantage clear without mentioning features?
- Could a stranger explain what this does after seeing it for 30 seconds?

**Red flags:**

- Messaging lists features instead of outcomes
- "We're like X but also Y and also Z"
- Targeting more than 2 user segments at launch
- Value proposition requires a paragraph instead of a sentence
- Competitive positioning based on feature count
- Can't answer "why this instead of [obvious alternative]?" in one sentence

---

## Layer 7: Subtraction Exercise

The most valuable audit layer. Force removal.

**Process:**

1. List everything (features, files, services, pages, endpoints, options, settings).
2. Rank by contribution to core outcome (1 = essential, 5 = nice-to-have).
3. Cut everything ranked 3-5. That's the 30-50% cut.
4. For everything ranked 2: can it be merged with a rank-1 item?
5. For everything ranked 1: can it be simplified further?

**Sub-questions:**

- If forced to cut 30-50% of features/scope/code, what goes first?
- Which pieces can be merged into fewer, more coherent units?
- What can be hardcoded now and made configurable only when a user requests it?
- What can be deferred to v2 without harming v1?
- Which "nice to have" items are disguised as "must have"?
- What is being kept for sunk cost reasons rather than future value?

**Red flags:**

- Nothing is cut (means the exercise wasn't done honestly)
- Only "safe" things are cut (cosmetic removals, not structural)
- "We can't cut that because we already built it" (sunk cost)
- "Users might need that someday" (speculative retention)

---

## Batching Protocol

Structure all recommendations as batched decisions. Each decision must be atomic, specific, and answerable in seconds (YES / NO / DEFER).

### Decision Format

```
[Decision ID]
Recommendation: YES / NO
Proposal: [Specific action to take]
Why: [One sentence explaining the reasoning]
Impact: [What changes as a result]
Risk: [What could go wrong]
Rollback: [How to undo if the decision is wrong]
```

### Decision ID Convention

Use phase and sequence numbers: `PHASE-1.1`, `PHASE-1.2`, `PHASE-2.1`, etc.

### Rules

- 3-7 decisions per phase. Fewer than 3 means the phase is too narrow. More than 7 means it should be split.
- Every decision must be atomic. One action per decision. No "do A and also B."
- Decisions must be answerable in seconds. If it requires deliberation, break it into smaller decisions.
- Order highest leverage to lowest within each phase.
- `YES` means "do this." `NO` means "don't do this" (preserve current state). Include both when the recommendation is to NOT do something commonly suggested.
- Include `Rollback` for every decision. If there's no rollback path, flag that explicitly as `Rollback: Irreversible - proceed with caution`.
