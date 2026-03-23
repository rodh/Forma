---
name: ideating-in-forma
description: Use when you have a working brief and need to explore solution directions — presents genuinely different approaches as text, then helps you pick or combine before committing
---

**Workflow context:** Typically follows framing-in-forma. Reads `brief.md` if available; otherwise asks the user for problem context directly. Produces `concept.md` and `approaches.md`.

## Finding upstream context

Check for `brief.md` in the current directory. If found, use it. If not, ask: "No brief found. Describe the problem you're solving, who it affects, and any known constraints — I'll work from that."

## How to run the skill

Present one section at a time. **Stop and wait for the user's reaction before moving to the next step.**

### Step 1 — Resolve open questions

Read the **Open questions** section from `brief.md`. Ask each open question one at a time using multiple choice options. **Stop and wait** after each question — do not batch them or continue until the user answers.

After open questions are resolved, ask 1-2 framing questions if the user's priorities aren't already clear — what they value most, what they'd sacrifice. **Stop and wait** after each. Skip if the brief makes priorities obvious.

**Do not propose approaches until all open questions are resolved.**

### Step 2 — Approaches

Present 2-3 approaches. For each: core interaction model (one sentence), what it prioritizes, what it sacrifices, when it wins, when it struggles. Use labeled bullets. Approaches must differ in interaction model, not just UI chrome.

Immediately save to `approaches.md`, overwriting in place.

**Stop and wait** for the user's reaction.

**Branching:**
- **One approach only** (narrowed during framing or only one viable): skip to Step 3 (Tensions).
- **User picks a specific approach**: go to Step 3 with that approach.
- **User doesn't pick:** ask them to choose — "Which approach do you want to explore?"

### Step 3 — Tensions

Present the key design tensions for the chosen direction — not generic UX trade-offs, but the ones that matter for this problem and these users. Use labeled bullets (`- **Tension name.** Explanation`).

Not every tension needs a question — some are informational. If a tension requires a design decision, ask one question at a time. **Stop and wait** after each question.

### Step 4 — Concept direction

After tensions are resolved, present the concept direction:
- "We're going with [approach] because [reason grounded in user need]."
- "The core interaction is [describe the pattern]."
- "The key bet is [state the assumption about user behavior]."
- "We'll know this works if [observable signal]."
- "The biggest risk is [what could make this wrong]."

**Stop and wait** for explicit approval before saving.

### Step 5 — Save

After the user approves, save to `concept.md`, overwriting in place. Also save after each subsequent iteration round.

## Rules

**Handling pushback:** Don't defend approaches — rethink with their constraint. If they reject all approaches, the objection reveals the real constraint — ask for it. If they already have a direction, pressure-test it instead of exploring. If the concept isn't converging after 3 rounds, the brief is probably missing something — name it.

- Be direct. No preamble, no filler. Labeled bullets for trade-offs and scenarios; prose for concept direction and key bet reasoning.
- The concept direction must be specific enough to wireframe against. "A clean, intuitive interface" is not a concept direction. "A batch-action queue where the advisor reviews exceptions only, with the system auto-resolving anything above 90% confidence" is.
- If the user's instinct is strong, don't manufacture disagreement — pressure-test briefly and help them move forward. Flag diminishing returns if they're wordsmithing a solid concept.
- **YAGNI.** Strip functionality not implied by the brief. Add a **Trimmed** note.
- **Hard gate.** Do not suggest wireframing-in-forma until the user explicitly approves the concept direction. Once approved, wireframing-in-forma is the natural next step — it produces key screens + stubs, with hydration as a later step.
- **Asking questions:** Use `AskUserQuestion` with labeled options. One question per tool call. Open-ended only when the answer space is too wide for options. If unavailable, fall back to text with lettered options.

$ARGUMENTS
