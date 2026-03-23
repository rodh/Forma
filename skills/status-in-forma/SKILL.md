---
name: status-in-forma
description: Use when starting a design session, checking what stage a design is at, or setting up a new design directory
---

**Workflow context:** Optional status check. Scans the current directory for design artifacts and suggests the next step.

## Design selection

If `$ARGUMENTS` is not empty, skip to **"Set active design"** below using `$ARGUMENTS` as the design name.

If `$ARGUMENTS` is empty, follow these steps to report status:

### 1. Scan current directory for artifacts

Search CWD and immediate subdirectories using file-search (not shell commands).

**Files:** `brief.md`, `concept.md`, `wireframes.md`, `test-results.md`, `personas.md`, `approaches.md`
**Directories:** `research/`, `sessions/`, `archive/`

Also scan for subdirectories containing any of the above.

**Stage detection** — check in reverse order, first match wins:
- Has `test-results.md` → **Has test results**
- Has `wireframes.md` → **Has wireframes**
- Has `concept.md` → **Has concept**
- Has `brief.md` → **Has brief**
- None of the above → **New**

Note the presence of `personas.md` — if it exists, mention it alongside the stage.

### 2. Report status

**If artifacts exist in CWD:**

Print an **"Existing artifacts"** markdown table (`File` | `Contents`). One row per artifact, 1-2 sentence summary each. Include `approaches.md` and `research/` (with count and summaries) only when they exist.

If both `test-results.md` and `wireframes.md` exist, read the version from the `wireframes.md` header (`# Wireframes v{N}`). Read the `**Tested against:** wireframes v{X}` line in `test-results.md`. If the wireframes version is newer than what was tested, note this — e.g., "Test results are from wireframes v2 (current wireframes are v3) — consider re-testing." Also note how many items appear under "Remaining issues" and "New findings."

Check `archive/` for prior versions to determine iteration history — e.g., "3 wireframe versions, 2 test rounds."

After the table, print a line listing what's **missing** — name each missing artifact file explicitly.

### Project inventory

Scan CWD for files and directories not already reported in the artifacts table. Exclude hidden files/directories (`.git`, `.DS_Store`, etc.) and known Forma artifacts/directories already reported above.

Group remaining files by type: **Prototypes** (web source files — filename only), **Images/Screenshots** (count and filenames), **Docs** (non-Forma `.md`/`.txt`/`.pdf` — one-line summary each), **Other** (filename and extension). Omit empty categories. Omit the entire section if no non-Forma files exist. Cap any category at 10 files — show first 5 and count the rest.

If `sessions/` exists, present a session history table (`Date` | `Type` | `Summary`). Type from the note's `**Type:**` field; summary = first sentence + compressed open threads. Most recent first; cap at 3 with "Plus {N} earlier" note.

Collect all **unresolved open threads** across sessions into a bulleted list (unresolved = not addressed by a later session's resolution or artifact change, best-effort match).

Then print a line summarizing the **current state** — what stage the design is at and any notable context.

Then print a `> **Next up:**` blockquote recommending the logical next step based on the detected stage:
- **New** → "Start with framing-in-forma to create a brief."
- **Has brief** → "Move to ideating-in-forma to explore approaches."
- **Has concept** → "Move to wireframing-in-forma to make it concrete."
- **Has wireframes** → "Move to user-testing-in-forma to validate the design."
- **Has test results** → Read the test results and recommend based on what they say: another wireframe iteration if unresolved issues remain, or prototyping if the design tested well.

Supplementary context (add when applicable): mention `research/` if it exists without `brief.md`, note prototype files alongside design artifacts, append top 2-3 unresolved open threads.

Present "Where do you want to pick up?" with options based on what exists.

**If subdirectories with artifacts exist:** Numbered list by recency with stage. Show up to 4 most recent plus option for full list or new design name.

**If no artifacts found anywhere:** Tell user to run framing-in-forma or status-in-forma with a name. Stop.

---

## Set active design

Create a subdirectory named `$ARGUMENTS` in CWD if it doesn't already exist. Ask the user to confirm first: "No design named `<name>` found. Create it?" with Yes/No options. Only create if confirmed.

If the subdirectory already exists, report its status using the artifact table format above.

Tell the user the design directory is ready and suggest the framing-in-forma skill to get started (if empty) or present "Where do you want to pick up?" options (if artifacts exist).

## Rules

- Be direct. No preamble, no filler.
- Labeled bullets for facts/constraints; prose for opinions/narratives.
