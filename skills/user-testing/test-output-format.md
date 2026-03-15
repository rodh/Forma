# Test Output Format

## Per-Persona Walkthroughs

This content appears under `## Detailed walkthroughs` at the end of the output — after action items, consensus issues, and highest-leverage fix. Generate it first, then synthesize the sections above from it.

Walk through each screen the persona encounters. For each screen:

- One short prose sentence setting the scene — what they notice, their posture toward the screen.
- Then bold-labeled bullets for each observation: `- **Bold label.** Explanation sentence(s).`
- If a screen has no prose setup worth writing (the persona's reaction is purely tactical), go straight to bullets.

Cover first impressions, task attempts, and friction points within the per-screen walkthrough. Every observation must be specific to this persona's behavior pattern — not generic usability notes.

**What they'd say:** A blockquote with bold label — something this person would actually say out loud, not UX jargon. Format: `> **What she'd say:** "quote"`

**Would they come back?** A bold-labeled prose paragraph. After first use, do they adopt this or revert to their old workflow? Why? This is the most important question — a design can be usable but still not adopted.

## Output Order

After the personas list, produce the following sections in this order:

### Action items

Every "fix now" consensus issue, most impactful first. Format: `- **AI-{n}.** Brief description — why it matters`

Number action items sequentially (AI-1, AI-2, AI-3...). These IDs are stable references used across test iterations. Keep it scannable — one line per item, no paragraphs.

### On subsequent tests

When `test-results.md` already exists: read prior results and compare previous action items against current wireframes. Instead of a single action items section, produce three sections (omit any that would be empty):

- **Resolved from previous test:** Items the current wireframes have addressed. Preserve original AI-{n} IDs.
- **Remaining issues:** Items still present. Preserve original AI-{n} IDs. Re-state why each still matters.
- **New findings:** Issues not in prior action items. Continue numbering from max prior ID + 1.

### Consensus issues

What problems did multiple personas hit? Numbered list, each with evidence. Below each issue, an indented sub-bullet with the verdict — ***Fix now*** or ***Defer*** — leading the line, followed by a short rationale. "Fix now" means worth addressing before moving to the next stage. "Defer" means real but acceptable — state what absorbs the risk.

### Highest-leverage fix

One recommendation, bolded, with 2–4 bullets on what it accomplishes. End with a readiness assessment: where the design stands and a clear next step (iterate wireframes, move to prototype, run another targeted test, etc.).

If the concept from the concept-forming skill included a key bet, report whether the walkthroughs validated or contradicted it.

### Detailed walkthroughs

Output all per-persona walkthroughs under a `## Detailed walkthroughs` heading — repositioned to the end so actionable findings come first.
