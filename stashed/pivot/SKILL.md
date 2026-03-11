---
name: pivot
description: Pivot the current design into a variant for exploring a different direction
---

**Workflow context:** Creates a variant directory for exploring a different direction. Copies the brief, lets you re-run the concept-forming skill with a new approach.

## Pivot the current design

Works in any directory with design artifacts. Creates a sibling directory with the brief copied.

$ARGUMENTS contains the variant name as the first word or hyphenated slug (e.g., "alt-nav", "simplified", "mobile-first"), optionally followed by fork context describing the intent of this fork.

### Steps

1. Check if the current directory name contains `--`. If so, stop and tell the user: "Can't pivot a pivot. Pivot the parent instead: run the pivot skill from `{parent}`" (where parent is the part before `--`).
2. Get the current directory name. Create the sibling directory: `../{current-dir-name}--{variant-name}/`
3. Copy only `brief.md` from the current directory into the new directory.
4. If $ARGUMENTS contains text beyond the variant name, treat it as fork context. Append a `## Fork intent` section to the fork's `brief.md` that captures:
   - What direction this fork explores (in the user's words, cleaned up)
   - What it keeps from the parent
   - What it strips or changes
   - Why it diverges
5. Read the current directory's `concept.md` (if it exists) and summarize what direction the parent took — so the user knows what they're diverging from.
6. Tell the user: "Pivoted from {parent}. The brief is shared. Run the concept-forming skill to explore a new direction."

### Error handling

- If $ARGUMENTS is empty: "Usage: `pivot variant-name` — e.g., `pivot alt-nav`"
- If the pivot directory already exists: "That pivot already exists. `cd` into it to resume, or choose a different name."
- If the current directory has no `brief.md`: "No brief found in the current directory. Run the design-briefing skill first."

## Communication style

- Direct, no preamble, no filler
- Labeled bullets for facts/constraints; prose for opinions/narratives
- Honest critique — flag when iteration stops producing improvements
