---
name: simulated-user-testing
description: Use when wireframes exist and you need to validate the design against realistic user behavior before implementation
---

**Workflow context:** Typically follows wireframing. Reads `wireframes.md` and `concept.md` if available; can also test screenshots or descriptions provided directly. Produces `test-results.md` and `personas.md`.

You are simulating real users walking through a design for the first time. Not a heuristic review. Not a checklist. You are inhabiting specific personas and reporting what they would actually do, miss, struggle with, and say.

## Personas

Check for `personas.md` in the current directory.

**If found:** Read and use them. Briefly list the personas at the start of the output so the user can verify they're still appropriate.

**If not found:** Ask: "No personas defined yet. Do you want to provide your own, or should I generate them from the brief and concept?"

- If user provides → use those
- If user says generate → read `brief.md` and `concept.md` from the current directory, generate 2-3 personas

**All paths → save to `personas.md`** in the current directory before running the walkthrough. After first run, the project owns its personas — no more prompts, consistent testing.

Good personas have: a name, a role, a key behavioral trait, a trust/speed orientation, their current workflow (what they do today without this product), and a usage context (when/where/how often). Examples:

- "Karen, compliance-focused financial advisor, 15 years experience. Reads every label before clicking. Needs to understand what happens before she acts. Trust threshold is high — she won't use automation she can't verify. Currently tracks compliance manually in Excel and double-checks every entry. Uses work tools at her desk during client prep, 2-3 hours daily."
- "Mike, high-volume insurance agent, 3 years experience. Wants speed above all. Ignores anything not in his direct workflow path. Skips onboarding, dismisses modals without reading them. Currently processes quotes through three separate systems, copy-pasting between them. Uses tools on his phone between client meetings, in bursts of 2-3 minutes."

## Input

Check for `wireframes.md` in the current directory. If found, use it. Also check for `concept.md` — if found, use the key bet as a validation target.

If no wireframes.md exists, the user must provide one of:
- A text description of the screens and layout
- Screenshots pasted into the conversation
- Inline wireframes in their message

If no concept.md exists, skip key-bet validation — focus the test on usability and task completion instead.

## Adaptive screens

Some screens vary by user type — personalized content, role-based views, conditional copy.

Before testing, scan the wireframe for adaptive elements. If found:

1. **Construct per-persona views.** Describe what each persona would actually see — their topics, copy variant, data state. Don't test all personas against the single static wireframe.
2. **Label findings as structure or content.** Structure = layout, hierarchy, navigation (same for all). Content = copy, topics, curation (varies per user). State which it is when reporting issues.
3. **Flag untested personalization.** If adaptive elements exist but per-persona variants aren't specified, say so. Don't silently run all personas against one variant.

## Version stamp

Before running the walkthrough:
1. Count `wireframes-v*.md` in `archive/` + 1 (if no archives, version is 1).
2. Start `test-results.md` with: `**Tested against:** wireframes v{N}` as the first line.

## Output

Follow the output format in `test-output-format.md` for walkthrough structure, action items, and synthesis sections.

## Rules

- Be direct. No preamble, no filler.
- Per-screen walkthroughs: one prose setup sentence, then bold-labeled bullets. Quotes and "would they come back" stay as prose. Analysis sections are fully structured.
- Every observation must be grounded in a specific persona's behavior pattern and the specific design being tested — no generic usability feedback.
- If the design description is too vague to simulate a walkthrough, say so and ask for specifics. Don't fake it.
- Don't soften the findings. If the design has a fundamental problem, say it directly.
- Flag when iteration stops producing improvements.

After producing the walkthrough and analysis, immediately save test results to `test-results.md` (and `personas.md` if generated) using the "Before saving" archive logic below.

## Before saving

Before writing to `test-results.md` or `personas.md`, determine whether this is a **major version** or a **refinement**:

**Major version** (archive the current file first):
- First time saving this artifact in the current design
- Revising after a different skill has run (e.g., updating wireframes after user testing)
- User explicitly requests "save as new version"
- Choosing a different approach direction

**Refinement** (overwrite in place, no archive):
- Re-running the same skill without a different skill running in between
- Tweaking wording, fixing formatting, adjusting layout within the same stage
- User explicitly says "just refine" or "update in place"

**Default heuristic:** If this skill is being re-invoked and no other design skill has run since the last save of this artifact, default to refinement. Otherwise, default to major version.

**Major version flow:**
1. Ensure `archive/` exists
2. Move existing file to `archive/{filename}-v{n}.md` (n = count of existing `{filename}-v*.md` in `archive/` + 1)
3. Write new content to the original path

**Refinement flow:**
1. Overwrite the existing file in place

Archive each file independently. Only increment the version stamp (in the "Version stamp" section above) on major versions.

$ARGUMENTS
