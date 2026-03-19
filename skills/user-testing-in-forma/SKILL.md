---
name: user-testing-in-forma
description: Use when wireframes exist and you need to validate the design against realistic user behavior before implementation
---

**Workflow context:** Typically follows wireframing-in-forma. Reads the latest `wireframes-v*.md` and `ideation.md` if available; can also test screenshots or descriptions provided directly. Produces `test-results-v{N}.md` and `personas.md`.

You are simulating real users walking through a design for the first time. Not a heuristic review. Not a checklist. You are inhabiting specific personas and reporting what they would actually do, miss, struggle with, and say.

## Personas

Check for `personas.md` in the current directory.

**If found:** Read and use them. Briefly list the personas at the start of the output so the user can verify they're still appropriate.

**If not found:** Ask: "No personas defined yet. Do you want to provide your own, or should I generate them from the brief and concept?"

- If user provides → use those
- If user says generate → read `frame.md` and `ideation.md` from the current directory, generate 2-3 personas

**All paths → save to `personas.md`** in the current directory before running the walkthrough. After first run, the project owns its personas — no more prompts, consistent testing.

Good personas have: a name, a role, a key behavioral trait, a trust/speed orientation, their current workflow (what they do today without this product), and a usage context (when/where/how often).

## Input

Check for the latest `wireframes-v*.md` in the current directory. If found, use it. Also check for `ideation.md` — if found, use the key bet as a validation target.

If no wireframes file exists, the user must provide one of:
- A text description of the screens and layout
- Screenshots pasted into the conversation
- Inline wireframes in their message

If no ideation.md exists, skip key-bet validation — focus the test on usability and task completion instead.

## Adaptive screens

Some screens vary by user type — personalized content, role-based views, conditional copy.

Before testing, scan the wireframe for adaptive elements. If found:

1. **Construct per-persona views.** Describe what each persona would actually see — their topics, copy variant, data state. Don't test all personas against the single static wireframe.
2. **Label findings as structure or content.** Structure = layout, hierarchy, navigation (same for all). Content = copy, topics, curation (varies per user). State which it is when reporting issues.
3. **Flag untested personalization.** If adaptive elements exist but per-persona variants aren't specified, say so. Don't silently run all personas against one variant.

## Versioning

**Versioned files:** Each version writes to its own file: `test-results-v1.md`, `test-results-v2.md`, etc. Check for the highest existing `test-results-v*.md` in the current directory to determine the next version number. If no file exists, start at v1.

Start the file with `# Test Results v{N}`. On the next line, add `**Tested against:** wireframes-v{M}` (read the version from the latest `wireframes-v*.md` file).

Increment the version only when wireframes have changed since the last test run. If re-running tests against the same wireframes, overwrite the current version file with the same version number.

## Output

Follow the output format in `test-output-format.md` for walkthrough structure, action items, and synthesis sections.

## Rules

- Be direct. No preamble, no filler.
- Per-screen walkthroughs: one prose setup sentence, then bold-labeled bullets. Quotes and "would they come back" stay as prose. Analysis sections are fully structured.
- Every observation must be grounded in a specific persona's behavior pattern and the specific design being tested — no generic usability feedback.
- If the design description is too vague to simulate a walkthrough, say so and ask for specifics. Don't fake it.
- Don't soften the findings. If the design has a fundamental problem, say it directly.
After producing the walkthrough and analysis, immediately save test results to the current version file (and `personas.md` if generated).

$ARGUMENTS
