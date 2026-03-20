---
name: status-in-forma
description: Check design status in the current directory, or create a named subdirectory for a new design.
---

**Workflow context:** Optional status check. Scans the current directory for design artifacts and suggests the next step.

## Design selection

If `$ARGUMENTS` is not empty, skip to **"Set active design"** below using `$ARGUMENTS` as the design name.

If `$ARGUMENTS` is empty, follow these steps to report status:

### 1. Scan current directory for artifacts

Search for design artifacts in the current directory and immediate subdirectories using your platform's file-search capabilities (not shell commands).

Check for these files in CWD:
- `frame.md`, `ideation.md`, `wireframes.md`, `test-results.md`, `personas.md`, `approaches.md`

Also check for these directories:
- `exploration/` — approach wireframes from ideating-in-forma
- `research/` — research output from thinking-in-forma
- `sessions/` — session notes from log-in-forma and thinking-in-forma
- `archive/` — prior versions of wireframes and test results

Also scan for subdirectories that contain design artifacts (any of the above files).

**Stage detection** — check in reverse order, first match wins:
- Has `test-results.md` → **Has test results**
- Has `wireframes.md` → **Has wireframes**
- Has `ideation.md` → **Has ideation**
- Has `frame.md` → **Has frame**
- None of the above → **New**

Note the presence of `personas.md` — if it exists, mention it alongside the stage.

### 2. Report status

**If artifacts exist in CWD:**

Print an **"Existing artifacts"** heading, then a markdown table with `File` and `Contents` columns. One row per existing artifact. The `Contents` cell is a 1-2 sentence summary of what's in that file.

```
### Existing artifacts

| File | Contents |
|------|----------|
| frame.md | Brief for checkout redesign — reduce drop-off at payment step, mobile-first constraint. |
| ideation.md | Split-panel concept with inline validation. Rejected accordion approach. |
| wireframes.md | 4 screens: cart summary, shipping, payment, confirmation. Payment screen has two variants. |
| approaches.md | 3 approaches evaluated during ideation. |
| exploration/ | 3 approach wireframes from ideation. |
| research/ | 2 files: competitive-analysis.md, payment-ux-patterns.md |
```

Include `approaches.md`, `exploration/` (with count of files), and `research/` (with count and brief summaries) rows only when they exist.

If both `test-results.md` and `wireframes.md` exist, read the version from the `wireframes.md` header (`# Wireframes v{N}`). Read the `**Tested against:** wireframes v{X}` line in `test-results.md`. If the wireframes version is newer than what was tested, note this — e.g., "Test results are from wireframes v2 (current wireframes are v3) — consider re-testing." Also note how many items appear under "Remaining issues" and "New findings."

Check `archive/` for prior versions to determine iteration history — e.g., "3 wireframe versions, 2 test rounds."

After the table, print a line listing what's **missing** — name each missing artifact file explicitly.

### Project inventory

Scan CWD for files and directories not already reported in the artifacts table. Exclude hidden files/directories (`.git`, `.DS_Store`, etc.) and known Forma artifacts/directories already reported above.

Group remaining files by type:

- **Prototypes**: `.html`, `.css`, `.js`, `.jsx`, `.tsx`, `.svelte`, `.vue` files. List filename only.
- **Images/Screenshots**: `.png`, `.jpg`, `.jpeg`, `.gif`, `.svg`, `.webp` files. List count and filenames.
- **Docs**: `.md`, `.txt`, `.pdf` files not already reported. Read for a one-line summary.
- **Other**: Anything else. List filename and extension.

Omit empty categories. Omit the entire section if no non-Forma files exist. Cap any single category at 10 files — show first 5 and a count of the rest.

If session notes exist in `sessions/`, present a session history table:

| Date | Type | Summary |
|------|------|---------|

- **Type**: Read from the `**Type:**` field in the session note (Thinking or Debrief).
- **Summary**: First sentence of session summary, plus any unresolved open threads compressed to one line.
- Sort most recent first. If more than 5 sessions, show the 3 most recent and note: "Plus {N} earlier sessions in `sessions/`."

After the table, collect all **unresolved open threads** across sessions into a single bulleted list. An open thread is unresolved if no later session's resolution or artifact change addresses it (best-effort keyword match).

Then print a line summarizing the **current state** — what stage the design is at and any notable context.

Then print a `> **Next up:**` blockquote recommending the logical next step based on the detected stage:
- **New** → "Start with framing-in-forma to create a frame."
- **Has frame** → "Move to ideating-in-forma to explore approaches."
- **Has ideation** → "Move to wireframing-in-forma to make it concrete."
- **Has wireframes** → "Move to user-testing-in-forma to validate the design."
- **Has test results** → Read the test results and recommend based on what they say: another wireframe iteration if unresolved issues remain, or prototyping if the design tested well.

Supplementary context (add to the stage-based recommendation when applicable):
- If `research/` exists but no `frame.md`, mention: "Research exists in `research/` — this context can feed into framing-in-forma."
- If prototype files exist alongside wireframes or test results, mention: "Prototypes exist alongside design artifacts — consider whether recent test results should inform prototype updates."
- If unresolved open threads exist, append the top 2-3 to the recommendation.

Present the user with a "Where do you want to pick up?" question with options based on what exists.

**If subdirectories with artifacts exist:**

Print a numbered list showing each subdirectory with its stage, sorted by recency (most recent first).

Present the user with options to choose from, showing up to 4 of the most recent designs. Include an option for typing a number from the full list or a new design name.

**If no artifacts found anywhere:**

Tell the user: "No design artifacts found. Run the framing-in-forma skill to start a new design here, or run status-in-forma with a name to create a subdirectory." Then stop.

---

## Set active design

Create a subdirectory named `$ARGUMENTS` in CWD if it doesn't already exist. Ask the user to confirm first: "No design named `<name>` found. Create it?" with Yes/No options. Only create if confirmed.

If the subdirectory already exists, report its status using the artifact table format above.

Tell the user the design directory is ready and suggest the framing-in-forma skill to get started (if empty) or present "Where do you want to pick up?" options (if artifacts exist).

## File naming convention

When saving outputs, use these names:
- framing-in-forma → `frame.md`
- ideating-in-forma → `ideation.md`, `wireframes.md`, `approaches.md`, `exploration/{approach-slug}.md`
- wireframing-in-forma → `wireframes.md` (previous versions archived to `archive/wireframes-v{N}.md`)
- user-testing-in-forma → `test-results.md` and `personas.md` (previous results archived to `archive/test-results-v{N}.md`)
- log-in-forma → `sessions/YYYY-MM-DD-HHMM.md`
- thinking-in-forma → `sessions/YYYY-MM-DD-HHMM.md` (thinking session) and optionally `research/{topic-slug}.md`

## Rules

- Be direct. No preamble, no filler.
- Labeled bullets for facts/constraints; prose for opinions/narratives.
