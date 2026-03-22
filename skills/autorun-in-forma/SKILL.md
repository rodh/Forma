---
name: autorun-in-forma
description: Use when you want a complete first-draft design from raw context — runs the full pipeline autonomously and produces all artifacts end-to-end without interaction
---

**Workflow context:** Autonomous alternative to the interactive pipeline. Orchestrates real -in-forma skills via subagents, so each phase uses the full richness of the actual skill rather than a simplified approximation. No user interaction during the run.

## Input

The user provides raw context — the same messy input framing-in-forma accepts. If no input is provided after the skill name, ask once: "What are you designing? Paste raw context — tickets, requirements, notes, anything."

## Decision protocol

Every autonomous decision gets documented with: what was decided, alternatives considered, reasoning, and a confidence tag — **[confident]** (input strongly implied the choice) or **[review]** (genuinely competing options, user should verify).

## Subagent wrapper

Every subagent dispatched in this pipeline receives this preamble in its prompt:

> You are running `{skill-name}` autonomously as part of a design pipeline.
>
> **Auto-resolve protocol:** Do NOT use AskUserQuestion or ask the user anything. When the skill would normally ask a question or wait for user input, resolve the question yourself. For every auto-resolved question, document:
> - **Decision:** What you decided
> - **Alternatives:** What other options existed
> - **Reasoning:** Why you chose this option
> - **Confidence:** **[confident]** (input strongly implied) or **[review]** (genuinely competing options)
>
> Write all output files to: `{working-directory}`
>
> Invoke the skill `{skill-name}` using the Skill tool and follow its full process.

## Pipeline

Create a timestamped directory: `run-YYYY-MM-DD-HHMM/`. All artifacts go inside it.

### Phase 1 — Frame

Dispatch a subagent:
- **Skill:** `framing-in-forma`
- **Args:** The raw user context (passed as the skill's arguments)
- **Working directory:** The run root
- **Auto-resolve:** The targeted questions framing would normally ask the user
- **Expected output:** `brief.md`

Wait for completion before proceeding.

### Phase 2 — Ideate

Dispatch a subagent:
- **Skill:** `ideating-in-forma`
- **Args:** None (reads `brief.md` from the run directory)
- **Working directory:** The run root
- **Auto-resolve:** Open questions from brief, approach selection, design tensions, concept approval
- **Additional instruction:** Skip step B ("Generate wireframes") in the autonomous pipeline — produce only the concept direction per approach. Do NOT create the `exploration/` directory or files. Instead, write each approach's concept direction directly to `{approach-slug}/concept.md`. Also skip the "Comparison and combination" step. Stop after producing `approaches.md` and the per-approach `concept.md` files.
- **Expected output:** `approaches.md`, `{approach-slug}/concept.md` files

Wait for completion. Parse `approaches.md` to extract approach slugs for Phase 3.

### Phase 2b — Setup approach directories

For each approach extracted from `approaches.md`:

1. Create a subdirectory (kebab-case slug) if it doesn't already exist.
2. Generate `personas.md` at the run root from `brief.md` — unless `personas.md` already exists upstream (in the directory where autorun was invoked), in which case copy that instead.

### Phase 3 — Per-approach pipeline

Process all approaches concurrently — each is independent with no shared mutable state. Use parallel subagents.

For each approach:

#### 3a — Wireframe

Dispatch a subagent:
- **Skill:** `wireframing-in-forma`
- **Args:** None (reads `concept.md` from the approach subdirectory)
- **Working directory:** The approach subdirectory
- **Auto-resolve:** Iterative feedback (agent self-critiques and refines)
- **Expected output:** `wireframes.md`

#### 3b — User test

Dispatch a subagent (after 3a completes):
- **Skill:** `user-testing-in-forma`
- **Args:** None (reads `wireframes.md` and `concept.md` from the approach subdirectory; finds `personas.md` via parent-directory fallback)
- **Working directory:** The approach subdirectory
- **Auto-resolve:** Already autonomous (no user questions in this skill)
- **Expected output:** `test-results.md`

#### 3c — Iterate (cap: 1 cycle)

After testing, read `test-results.md`. If any consensus issues are tagged "Fix now":
1. Re-invoke `wireframing-in-forma` subagent to revise wireframes based on findings
2. Re-invoke `user-testing-in-forma` subagent to retest
3. Stop after one iteration regardless — note any remaining Fix Now items as unresolved

### Phase 4 — Summarize

This phase is NOT a skill invocation — autorun itself produces `run-summary.md` at the run root.

Read all artifacts from all approaches and produce these sections:

- **Approach comparison.** One-line concept per approach, how each tested, key structural differences.
- **Key bets.** Which bets validated vs. failed per approach.
- **Recommendation.** Which approach tested strongest, or suggested combination.
- **Decision trail.** Table with columns: phase, decision, alternatives, reasoning, confidence tag. Aggregate all auto-resolved decisions from all subagent outputs.
- **Items for review.** All [review]-tagged decisions as a scannable checklist.
- **Unresolved issues.** Remaining Fix Now items across approaches after iteration cap.

## Directory structure

```
run-YYYY-MM-DD-HHMM/
  brief.md
  approaches.md
  personas.md
  {approach-slug}/
    concept.md
    wireframes.md
    test-results.md
  {approach-slug}/
    ...
  run-summary.md
```

## Rules

- No user interaction during the run. Auto-resolve everything, document everything.
- Each phase invokes the real -in-forma skill via subagent — do NOT reimplement skill logic inline.
- Approach slugs are kebab-case derived from the approach name.
- Each approach subdirectory is a valid working directory for interactive skills — users can `cd` into one and run wireframing-in-forma or user-testing-in-forma to iterate further.
- If upstream context includes `personas.md` in the current directory, use those personas instead of generating new ones.

## Raw context

$ARGUMENTS
