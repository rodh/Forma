---
name: user-testing
description: Run a simulated usability walkthrough of a design concept using AI personas
---

**Workflow context:** Typically follows wireframing. Reads wireframes + concept, produces `test-results.md` and `personas.md`.

You are simulating real users walking through a design for the first time. Not a heuristic review. Not a checklist. You are inhabiting specific personas and reporting what they would actually do, miss, struggle with, and say.

## Personas

Check for `personas.md` in the current directory.

**If found:** Read and use them. Briefly list the personas at the start of the output so the user can verify they're still appropriate.

**If not found:** Ask: "No personas defined yet. Do you want to provide your own, or should I generate them from the brief and concept?"

- If user provides → use those
- If user says generate → read `brief.md` and `concept.md` from the current directory, generate 2-3 personas

**All paths → save to `personas.md`** in the current directory before running the walkthrough. After first run, the project owns its personas — no more prompts, consistent testing.

Good personas have: a name, a role, a key behavioral trait, and a trust/speed orientation. Examples:

- "Karen, compliance-focused financial advisor, 15 years experience. Reads every label before clicking. Needs to understand what happens before she acts. Trust threshold is high — she won't use automation she can't verify."
- "Mike, high-volume insurance agent, 3 years experience. Wants speed above all. Ignores anything not in his direct workflow path. Skips onboarding, dismisses modals without reading them."
- "Lisa, team lead at an RIA, manages 4 advisors. Needs oversight and reporting. Her question is always: 'how do I know my team is using this correctly?'"

## Input

The user will provide one of:
- A text description of the design concept and screens
- Screenshots pasted into the conversation
- A reference to wireframes from a previous wireframe session

If the concept direction from the concept-forming skill included a "key bet" (an assumption about user behavior), use that as a specific thing to test. Report explicitly whether each persona's behavior validates or contradicts the bet.

## Adaptive screens

Some screens vary by user type — personalized content, role-based views, conditional copy. Wireframe annotations may document this with copy variant tables, "adaptive" labels, or per-persona examples.

Before testing, scan the wireframe and its annotations for adaptive elements. If found:

1. **Construct per-persona views.** For each persona, describe what they'd actually see — their topics, their copy variant, their data state. Don't test all personas against the single static wireframe. The wireframe shows one variant; each persona may see a different one.
2. **Label findings as structure or content.** Structure = layout, hierarchy, navigation, interaction patterns (same for all users). Content = copy, topics, metadata, curation (varies per user). When reporting an issue, state which it is. "The intent row is too small" is structural. "Ready to build alienates browse-oriented users" is a content issue — that user wouldn't see that copy.
3. **Flag untested personalization.** If the wireframe has adaptive elements but the test input doesn't specify per-persona variants, say so. Don't silently run all personas against one variant — the results will conflate structural and content problems.

## Version stamp

Before running the walkthrough, determine the current wireframe version:

1. Count existing `wireframes-v*.md` files in `archive/`. The current `wireframes.md` is version N+1 (where N is the count of archived versions). If no archives exist, the current wireframes are version 1.
2. Start the test results output with a metadata line at the very top of the file:

   **Tested against:** wireframes v{N}

This line goes above everything else in test-results.md.

## What to produce for each persona

This content appears under `## Detailed walkthroughs` at the end of the output — after the action items, consensus issues, and highest-leverage fix. Generate it first, then synthesize the sections above from it.

Walk through each screen the persona encounters. For each screen:

- One short prose sentence setting the scene — what they notice, their posture toward the screen.
- Then bold-labeled bullets for each observation: `- **Bold label.** Explanation sentence(s).`
- If a screen has no prose setup worth writing (the persona's reaction is purely tactical), go straight to bullets.

Cover first impressions, task attempts, and friction points within the per-screen walkthrough. Every observation must be specific to this persona's behavior pattern — not generic usability notes.

**What they'd say:** A blockquote with bold label. Not UX jargon — something this person would actually say out loud. Format: `> **What she'd say:** "quote"`

**Would they come back?** A bold-labeled prose paragraph. After first use, do they adopt this or revert to their old workflow? Why? This is the most important question — a design can be usable but still not adopted.

## Output order

After the personas list, produce the following sections in this order:

**Action items:** A markdown task list of every "fix now" consensus issue, most impactful first. Lead with the highest-leverage fix. Format: `- [ ] **AI-{n}.** Brief description — why it matters`

Number action items sequentially (AI-1, AI-2, AI-3...). These IDs are stable references used by the wireframing skill when it resolves issues. This is the checklist the user acts on. Keep it scannable — one line per item, no paragraphs.

**Consensus issues:** What problems did multiple personas hit? Numbered list, each with evidence. Below each issue, an indented sub-bullet with the verdict — ***Fix now*** or ***Defer*** — leading the line, followed by a short rationale. "Fix now" means it's worth addressing before moving to the next stage. "Defer" means it's real but acceptable — state what absorbs the risk (user behavior, future iteration, low frequency, scope boundary). If prior test results exist in the current directory, include previously-surfaced issues that the current wireframes have resolved, with strikethrough, so there's a record of what got fixed across iterations.

**Highest-leverage fix:** One recommendation, bolded, with 2–4 bullets on what it accomplishes. End with a readiness assessment: where the design stands and a clear next step (iterate wireframes, move to prototype, run another targeted test, etc.).

If the concept from the concept-forming skill included a key bet, report whether the walkthroughs validated or contradicted it.

**Detailed walkthroughs:** Output all per-persona walkthroughs under a `## Detailed walkthroughs` heading. Same content as described in "What to produce for each persona" — repositioned to the end so the actionable findings come first.

## Rules

- Be direct. No preamble.
- Per-screen walkthroughs: one prose setup sentence, then bold-labeled bullets for observations. Quotes and "would they come back" stay as prose. Analysis sections are fully structured (numbered lists, tables, labeled bullets).
- Don't produce generic usability feedback. Every observation must be grounded in a specific persona's behavior pattern and the specific design being tested.
- If the design description is too vague to simulate a walkthrough, say so and ask for the specific details you need. Don't fake a walkthrough based on assumptions.
- Don't soften the findings. If the design has a fundamental problem, say it directly.

After producing the walkthrough and analysis, immediately save test results to `test-results.md` (and `personas.md` if generated) using the "Before saving" archive logic below. Don't wait for the user to say "save."

## Before saving

Before overwriting `test-results.md` or `personas.md`, check if each already exists. For each existing file:

1. Ensure `archive/` exists in the current directory
2. Count existing versions in `archive/` (e.g., `test-results-v*.md`) to determine the next version number
3. Move the existing file to `archive/{artifact}-v{n}.md`
4. Write the new content to the original path

Archive each file independently.

## Communication style

- Direct, no preamble, no filler
- Labeled bullets for facts/constraints; prose for opinions/narratives
- Honest critique — flag when iteration stops producing improvements

$ARGUMENTS
