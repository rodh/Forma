---
name: checkpoint
description: Check design status in the current directory, or create a named subdirectory for a new design.
---

**Workflow context:** Optional status check. Scans the current directory for design artifacts and suggests the next step.

## Design selection

If `$ARGUMENTS` is not empty, skip to **"Set active design"** below using `$ARGUMENTS` as the design name.

If `$ARGUMENTS` is empty, follow these steps to report status:

### 1. Scan current directory for artifacts

Search for design artifacts in the current directory and immediate subdirectories using your platform's file-search capabilities (not shell commands).

Check for these files in CWD:
- `brief.md`, `concept.md`, `wireframes.md`, `test-results.md`, `personas.md`

Also scan for subdirectories that contain design artifacts (any of the above files).

**Stage detection** — check in reverse order, first match wins:
- Has `test-results.md` → **Has test results**
- Has `wireframes.md` → **Has wireframes**
- Has `concept.md` → **Has concept**
- Has `brief.md` → **Has brief**
- None of the above → **New**

Note the presence of `personas.md` — if it exists, mention it alongside the stage.

### 2. Report status

**If artifacts exist in CWD:**

Print an **"Existing artifacts"** heading, then a markdown table with `File` and `Contents` columns. One row per existing artifact. The `Contents` cell is a 1-2 sentence summary of what's in that file.

```
### Existing artifacts

| File | Contents |
|------|----------|
| brief.md | Brief for checkout redesign — reduce drop-off at payment step, mobile-first constraint. |
| concept.md | Split-panel concept with inline validation. Rejected accordion approach. |
| wireframes.md | 4 screens: cart summary, shipping, payment, confirmation. Payment screen has two variants. |
```

If both `test-results.md` and `wireframes.md` exist, read the version from each file's heading (`# Wireframes v{N}`, `# Test Results v{M}`). Check the `**Tested against:** wireframes v{X}` line in test-results.md. If the wireframes version is newer than what was tested, note this — e.g., "Test results are from wireframes v2 (current wireframes are v3) — consider re-testing." Also note how many items appear under "Remaining issues" and "New findings."

If `design-log.md` exists, read it and include a brief summary of the iteration history in the status report.

After the table, print a line listing what's **missing** — name each missing artifact file explicitly.

If session notes exist in `sessions/`, read the most recent one. Include any open threads or stage checkpoint from the recap.

Then print a line summarizing the **current state** — what stage the design is at and any notable context.

Then print a `> **Next up:**` blockquote recommending the logical next step based on the detected stage:
- **New** → "Start with design-briefing to create a brief."
- **Has brief** → "Move to concept-forming to explore approaches."
- **Has concept** → "Move to wireframing to make it concrete."
- **Has wireframes** → "Move to user-testing to validate the design."
- **Has test results** → Read the test results and recommend based on what they say: another wireframe iteration if unresolved issues remain, or prototyping if the design tested well.

Present the user with a "Where do you want to pick up?" question with options based on what exists.

**If subdirectories with artifacts exist:**

Print a numbered list showing each subdirectory with its stage, sorted by recency (most recent first).

Present the user with options to choose from, showing up to 4 of the most recent designs. Include an option for typing a number from the full list or a new design name.

**If no artifacts found anywhere:**

Tell the user: "No design artifacts found. Run the design-briefing skill to start a new design here, or run checkpoint with a name to create a subdirectory." Then stop.

---

## Set active design

Create a subdirectory named `$ARGUMENTS` in CWD if it doesn't already exist. Ask the user to confirm first: "No design named `<name>` found. Create it?" with Yes/No options. Only create if confirmed.

If the subdirectory already exists, report its status using the artifact table format above.

Tell the user the design directory is ready and suggest the design-briefing skill to get started (if empty) or present "Where do you want to pick up?" options (if artifacts exist).

## File naming convention

When saving outputs, use these names:
- design-briefing → `brief.md`
- concept-forming → `concept.md`
- wireframing → `wireframes.md`
- user-testing → `test-results.md` and `personas.md`
- recap → `sessions/YYYY-MM-DD-HHMM.md`
- Iteration history → `design-log.md`

## Rules

- Be direct. No preamble, no filler.
- Labeled bullets for facts/constraints; prose for opinions/narratives.
