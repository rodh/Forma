---
name: ideating-in-forma
description: Use when you have a working brief and need to explore solution directions — develops all approaches to wireframe depth, then lets you compare and combine before committing
---

**Workflow context:** Typically follows framing-in-forma. Reads `brief.md` if available; otherwise asks the user for problem context directly. Produces `concept.md`, `wireframes.md`, `approaches.md`, and `exploration/` files.

## Finding upstream context

Check for `brief.md` in the current directory. If found, use it. If not, ask: "No brief found. Describe the problem you're solving, who it affects, and any known constraints — I'll work from that."

## Before proposing approaches

Resolve any open questions from the brief first (one at a time, multiple choice preferred). Then ask 1-2 framing questions if priorities aren't already clear — what they value most, what they'd sacrifice. Skip if the brief makes priorities obvious.

## How to run the skill

Present one section at a time. **Stop and wait for the user's reaction before moving to the next step.**

### Step 1 — Approaches

Present 2-3 approaches. For each: core interaction model (one sentence), what it prioritizes, what it sacrifices, when it wins, when it struggles. Use labeled bullets. Approaches must differ in interaction model, not just UI chrome.

Immediately save to `approaches.md`, overwriting in place.

**Stop and wait** for the user's reaction.

**Branching:**
- **One approach only** (narrowed during framing or only one viable): skip pipeline, go to Step 2 (Tensions).
- **User picks a specific approach**: go to Step 2 (Tensions) with that approach — quiet escape hatch, don't present it as an option.
- **Otherwise** (user says "go," reacts without picking, or any non-specific response): proceed to autonomous pipeline below.

### Autonomous pipeline

Process each approach from `approaches.md` sequentially. For each approach:

#### A. Auto-resolve tensions

Identify 2-3 key design tensions specific to this approach (not generic UX trade-offs). For each, resolve by picking the option that best aligns with the approach's priorities. Document: what was decided, alternatives considered, why this resolution fits.

#### B. Generate concept direction

Produce a compact concept summary: core interaction model (one sentence), what it prioritizes, the key bet (assumption about user behavior), biggest risk. Auto-generated — no user input needed.

#### C. Generate wireframes

Full ASCII wireframes following `wireframe-conventions.md`. These must be production-quality wireframes, not rough sketches.

#### Output per approach

Save each to `exploration/{approach-slug}.md` (create directory if needed). Three sections: **Auto-resolved tensions**, **Concept direction**, **Wireframes**.

### Comparison and combination

After all approaches are processed, present: one-line concept per approach, key structural differences across wireframes, which tensions resolved differently. Ask: "Which elements do you want to keep from each? Describe the combination, or pick one outright."

- **Picks one:** Promote that approach's concept direction and wireframes directly.
- **Describes a combination:** Generate combined wireframe + synthesized concept direction. Present for approval before promoting.

Promote final result to `concept.md` and `wireframes.md`.

### Step 2 — Tensions

Present the key design tensions for the chosen direction — not generic UX trade-offs, but the ones that matter for this problem and these users. Use labeled bullets (`- **Tension name.** Explanation`).

Not every tension needs a question — some are informational. If a tension requires a design decision, ask one question at a time. **Stop and wait** after each question.

### Step 3 — Concept direction

After tensions are resolved, present the concept direction:
- "We're going with [approach] because [reason grounded in user need]."
- "The core interaction is [describe the pattern]."
- "The key bet is [state the assumption about user behavior]."
- "We'll know this works if [observable signal]."
- "The biggest risk is [what could make this wrong]."

**Stop and wait** for explicit approval before saving.

### Step 4 — Save

After the user approves, save to `concept.md`, overwriting in place. Also save after each subsequent iteration round.

## Rules

**Handling pushback:** Don't defend approaches — rethink with their constraint. If they reject all approaches, the objection reveals the real constraint — ask for it. If they already have a direction, pressure-test it instead of exploring. If the concept isn't converging after 3 rounds, the brief is probably missing something — name it.

- Be direct. No preamble, no filler. Labeled bullets for trade-offs and scenarios; prose for concept direction and key bet reasoning.
- The concept direction must be specific enough to wireframe against. "A clean, intuitive interface" is not a concept direction. "A batch-action queue where the advisor reviews exceptions only, with the system auto-resolving anything above 90% confidence" is.
- If the user's instinct is strong, don't manufacture disagreement — pressure-test briefly and help them move forward. Flag diminishing returns if they're wordsmithing a solid concept.
- Autonomous pipeline wireframes must meet wireframing skill quality standard — full ASCII, realistic placeholders, labeled screens, state variations. Not rough sketches.
- Auto-resolution reasoning must be specific to the approach's priorities, not generic. Document every autonomous decision — the user needs to see exactly what was decided and why.
- **YAGNI.** Strip functionality not implied by the brief. Add a **Trimmed** note.
- **Hard gate.** Do not suggest wireframing-in-forma until the user explicitly approves the concept direction.
- **Asking questions:** Use `AskUserQuestion` with labeled options. One question per tool call. Open-ended only when the answer space is too wide for options. If unavailable, fall back to text with lettered options.

$ARGUMENTS
