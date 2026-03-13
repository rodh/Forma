---
name: concept-branching
description: Use when you want to explore an alternative design direction from the current project, either fresh from the brief or branching into an unchosen concept approach
---

**Workflow context:** Creates a variant directory for exploring a different direction. Copies the brief and personas, lets you re-run concept-forming with a new approach — or branch directly into an unchosen approach from `approaches.md`.

## Pivot the current design

Works in any directory with design artifacts. Creates a sibling directory with shared artifacts copied.

$ARGUMENTS contains the variant name as the first word or hyphenated slug (e.g., "alt-nav", "simplified", "mobile-first"), optionally followed by `--approach "Approach Name"` to branch into a specific unchosen approach, and optionally followed by additional fork context.

## Mode 1: Fresh pivot

`concept-branching variant-name [optional fork context]`

### Steps

1. Check if the current directory name contains `--`. If so, stop and tell the user: "Can't pivot a pivot. Pivot the parent instead: run the concept-branching skill from `{parent}`" (where parent is the part before `--`).
2. Get the current directory name. Create the sibling directory: `../{current-dir-name}--{variant-name}/`
3. Copy `brief.md` from the current directory into the new directory.
4. Copy `personas.md` from the current directory into the new directory (if it exists).
5. If $ARGUMENTS contains text beyond the variant name (and not `--approach`), treat it as fork context. Append a `## Fork intent` section to the fork's `brief.md` that captures:
   - What direction this fork explores (in the user's words, cleaned up)
   - What it keeps from the parent
   - What it strips or changes
   - Why it diverges
6. Read the current directory's `concept.md` (if it exists) and summarize what direction the parent took — so the user knows what they're diverging from.
7. Tell the user: "Pivoted from {parent}. The brief and personas are shared. Run concept-forming to explore a new direction."

## Mode 2: Branch into unchosen approach

`concept-branching variant-name --approach "Approach Name"`

### Steps

1. Check if the current directory name contains `--`. If so, stop: "Can't pivot a pivot. Pivot the parent instead: run the concept-branching skill from `{parent}`."
2. Get the current directory name. Create the sibling directory: `../{current-dir-name}--{variant-name}/`
3. Copy `brief.md` from the current directory into the new directory.
4. Copy `personas.md` from the current directory into the new directory (if it exists).
5. Read `approaches.md` from the current directory.
6. Find the named approach by fuzzy-matching on section headings (e.g., `## Approach B: Dashboard-first` matches "Dashboard-first" or "dashboard").
7. Save the matched approach description as `concept.md` in the variant directory. Prepend this header:

```markdown
**Status: Approach only — tensions not yet resolved. Run concept-forming to finalize.**

---

```

8. Tell the user: "Pivoted into [Approach Name]. The brief and personas are shared. Run concept-forming to work through tensions, or wireframing if you want to go straight to layout."

## Error handling

- If $ARGUMENTS is empty: "Usage: `concept-branching variant-name` — e.g., `concept-branching alt-nav` or `concept-branching alt-nav --approach "Approach B"`"
- If the pivot directory already exists: "That pivot already exists. `cd` into it to resume, or choose a different name."
- If the current directory has no `brief.md`: "No brief found in the current directory. Run the design-briefing skill first."
- If `--approach` is specified but no `approaches.md` exists in the current directory: "No approaches.md found. Run concept-forming in the parent first to generate approaches."
- If `--approach` name doesn't match any heading in `approaches.md`: "No approach matching '[name]' found. Available approaches: [list headings]."

## Communication style

- Direct, no preamble, no filler
- Labeled bullets for facts/constraints; prose for opinions/narratives
- Honest critique — flag when iteration stops producing improvements
