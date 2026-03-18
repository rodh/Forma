---
name: recap
description: Capture session context — decisions, insights, and open threads — in a debrief before ending a design session
---

**Workflow context:** Captures session decisions and open threads to `sessions/YYYY-MM-DD-HHMM.md`. Run at the end of any session worth preserving.

You are debriefing a design session. The formal artifacts capture polished outputs, but the thinking between them — rejected directions, refinements, insights from the back-and-forth — lives only in this conversation. Your job is to extract everything that would otherwise be lost and save it as session notes.

## 1. Read existing artifacts

Read all design files in the current directory: `brief.md`, `concept.md`, `wireframes-v*.md`, `test-results-v*.md`, and any existing session notes in `sessions/`. These represent what's already been captured. Your job is to find what hasn't.

## 2. Identify what's not in the artifacts

Review the conversation for decisions, rejected directions, insights, open questions, and next steps that aren't captured in the saved files.

## 3. Generate session notes

Write the session notes using this structure:

**Session summary** — 2-3 sentences on what was explored and accomplished this session. Set the context for someone (including future-you) picking this up cold.

**Decisions made** — What was agreed on, including directions that were considered and rejected. For each decision, include the reasoning. These are the "why" behind the current state of the artifacts.

**Key insights** — Observations, reframings, or ideas that emerged from the back-and-forth that aren't captured in the formal artifacts. The stuff that would be lost if this session ended without saving.

**Artifact changes** — What was created or updated this session, with a one-line summary of what changed in each.

**Stage checkpoint:**
- **Current stage:** [which stage was active when the session ended]
- **Status:** Complete / In progress
- **If in progress, what remains:** [specific next steps to finish the stage]

Determine this from the conversation context — what commands were run, whether the user expressed satisfaction with the output or wanted more iteration.

**Open threads** — Unresolved questions, next steps mentioned but not acted on, things to pick up next session. Each thread should be specific enough to resume from without re-reading the full conversation.

## 4. Write the session notes

Create the `sessions/` directory in the current directory if it doesn't exist. Write the session notes to `sessions/YYYY-MM-DD-HHMM.md` using the current date and time. The timestamp ensures every session gets its own file.

## 5. Confirm

Print a short summary of what was captured — how many decisions, insights, and open threads — so the user can verify before wrapping up. If something looks wrong or missing, they can correct it now.

## Rules

- Be direct. No preamble, no filler.
- Use labeled bullets for decisions and insights when there are multiple discrete items. Use prose for the session summary (it's narrative context). Open threads are already a numbered list — keep that.
- Capture what's not already in the artifacts. Don't repeat what's already saved — the point is to capture the delta.
- If the session was light (just a quick check-in or minor edit), say so. Don't manufacture substance. A short session note is better than a padded one.
- If the user provides additional context via `$ARGUMENTS`, incorporate it into the session notes — it may flag something you'd otherwise miss.

$ARGUMENTS
