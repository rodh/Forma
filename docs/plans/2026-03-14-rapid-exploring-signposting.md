# Rapid-Exploring Signposting Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Elevate rapid-exploring as the recommended default path after concept-forming presents approaches, with an explicit choice point that surfaces all four post-approach options.

**Architecture:** Edit concept-forming's SKILL.md to replace the implicit "which resonates?" with a structured choice point. Update three docs files to reflect the new recommended flow order.

**Tech Stack:** Markdown skill definitions, documentation

**Design doc:** `docs/plans/2026-03-14-rapid-exploring-signposting-design.md`

---

### Task 1: Update concept-forming Step 1 choice point

**Files:**
- Modify: `skills/concept-forming/SKILL.md:28-33` (the "End by asking which approach resonates" paragraph)

**Step 1: Replace the "which approach resonates" ending of Step 1**

Find this text at the end of the Step 1 section (after the approaches.md format block):

```markdown
End by asking which approach resonates (multiple choice). **Stop and wait.**
```

Replace with:

```markdown
After saving approaches, present the choice point:

> How do you want to proceed?
> - **Rapid-explore** — auto-develop all approaches to wireframe depth, then compare and combine (recommended)
> - **Pick [Approach Name]** — develop one through dialogue
> - **Explore [Approach Name]** — dig deeper into one before committing
> - **Branch** — create parallel design pipelines

**Stop and wait.**

If the user says "go," "proceed," or anything non-specific without naming an approach, default to rapid-explore — tell them to invoke the rapid-exploring skill.

If the user picks an approach by name, continue to Step 2 (Tensions) as normal.

If the user says "explore [name]," follow the Exploration mode section below.

If the user says "branch," tell them to invoke the concept-branching skill.
```

**Step 2: Remove the redundant exploration mode trigger text**

The current Exploration mode section (starting "After presenting approaches and saving to `approaches.md`, the user may say 'explore [Approach Name] further' instead of choosing one.") still works — it describes what happens when the user picks that option. No change needed to this section.

**Step 3: Verify the file reads correctly**

Read `skills/concept-forming/SKILL.md` end-to-end and verify:
- Step 1 ends with the choice point, not "which approach resonates"
- Steps 2-4 still follow naturally for the "pick one" path
- Exploration mode section is unchanged
- No duplicate or contradictory instructions

**Step 4: Commit**

```bash
git add skills/concept-forming/SKILL.md
git commit -m "Add explicit choice point after concept-forming approaches with rapid-explore as default"
```

---

### Task 2: Reorder rapid-explore in philosophy.md

**Files:**
- Modify: `docs/philosophy.md:63-78` (the "Refine vs. explore vs. branch" section)

**Step 1: Move rapid-explore paragraph before explore**

Current order: Refine → Major version → Explore → Rapid-explore → Branch

New order: Refine → Major version → Rapid-explore → Explore → Branch

Move the **Rapid-explore** paragraph (currently after Explore) to sit **before** Explore.

**Step 2: Add "default after concept-forming" note to the rapid-explore paragraph**

Update the rapid-explore paragraph to read:

```markdown
**Rapid-explore** (default after concept-forming) when you want to see all approaches materialized to wireframe depth before committing. After concept-forming presents approaches, invoke rapid-exploring to auto-develop all directions — resolving tensions autonomously, generating wireframes for each, then combining the best elements. Fastest path from "multiple ideas" to "one concrete direction" at the cost of human nuance in tension resolution.
```

The only change from current text is adding "(default after concept-forming)" after the bold label.

**Step 3: Update the key signals paragraph**

Current:
```
The key signals: if you're tweaking within a stage, refine. If you want to compare approaches before committing, explore. If you want to compare approaches *visually* rather than *conceptually*, rapid-explore. If you're crossing stages or making structural revisions, major version. If you need full parallel pipelines through wireframing and testing, branch.
```

New (reorder to match paragraph order):
```
The key signals: if you're tweaking within a stage, refine. If you want to compare approaches *visually* rather than *conceptually*, rapid-explore — this is the default after concept-forming. If you want to compare approaches through dialogue before committing, explore. If you're crossing stages or making structural revisions, major version. If you need full parallel pipelines through wireframing and testing, branch.
```

**Step 4: Verify and commit**

Read `docs/philosophy.md` and verify the section order is Refine → Major version → Rapid-explore → Explore → Branch.

```bash
git add docs/philosophy.md
git commit -m "Reorder philosophy doc to reflect rapid-explore as default post-concept path"
```

---

### Task 3: Update guide.md structure

**Files:**
- Modify: `docs/guide.md:10-22` (the "How the stages connect" section)

**Step 1: Update concept-forming description to mention choice point**

Find the current concept-forming paragraph:

```markdown
**Concept forming** explores the solution space. It presents genuinely different approaches — not three flavors of the same idea, but different interaction models with different trade-offs. You converge on a concept direction: "We're going with X because Y. The key bet is Z. We'll know it works if W."
```

Replace with:

```markdown
**Concept forming** explores the solution space. It presents genuinely different approaches — not three flavors of the same idea, but different interaction models with different trade-offs. After presenting approaches, it offers a choice: rapid-explore all approaches to wireframe depth (recommended), pick one to develop through dialogue, explore one deeper, or branch into parallel pipelines.
```

**Step 2: Move rapid-exploring paragraph to sit directly after concept-forming**

The rapid-exploring paragraph currently sits between user testing and concept branching. Move it to sit immediately after the concept-forming paragraph (before wireframing), since it's now the recommended next step.

**Step 3: Verify and commit**

Read `docs/guide.md` and verify:
- Concept-forming description mentions the choice point
- Rapid-exploring paragraph follows concept-forming
- Order is: design-briefing → concept-forming → rapid-exploring → wireframing → user testing → concept branching

```bash
git add docs/guide.md
git commit -m "Update guide to show rapid-exploring as recommended step after concept-forming"
```

---

### Task 4: Update quickstart.md default flow

**Files:**
- Modify: `docs/quickstart.md:9-26` (the "New idea from scratch" section)

**Step 1: Update the pattern line**

Find:
```markdown
**Pattern:** design-briefing → concept-forming → wireframing → user-testing
```

Replace with:
```markdown
**Pattern:** design-briefing → concept-forming → rapid-exploring → wireframing → user-testing
```

**Step 2: Update the example command sequence**

Find:
```
/design-briefing
I want to build a personal content saving app. I keep finding useful stuff
on Reddit, YouTube, LinkedIn — but I never go back to it. I want something
that captures content fast, organizes it with AI, and helps me use it later.

/concept-forming

/wireframing home screen, save flow, topic briefing

/user-testing
```

Replace with:
```
/design-briefing
I want to build a personal content saving app. I keep finding useful stuff
on Reddit, YouTube, LinkedIn — but I never go back to it. I want something
that captures content fast, organizes it with AI, and helps me use it later.

/concept-forming

/rapid-exploring

/wireframing home screen, save flow, topic briefing

/user-testing
```

Note: wireframing is still shown because the user may want to iterate on the wireframes that rapid-exploring promoted — rapid-exploring produces wireframes but they may need refinement.

**Step 3: Update the feature modification pattern**

Find:
```markdown
### Feature modification

**Pattern:** design-briefing → concept-forming → wireframing → user-testing

Run the full workflow — you're rethinking the approach.
```

Replace with:
```markdown
### Feature modification

**Pattern:** design-briefing → concept-forming → rapid-exploring → wireframing → user-testing

Run the full workflow — you're rethinking the approach. Rapid-exploring auto-develops all concept directions to wireframe depth so you can compare visually before committing.
```

**Step 4: Verify and commit**

Read `docs/quickstart.md` and verify rapid-exploring appears in the default flows.

```bash
git add docs/quickstart.md
git commit -m "Update quickstart flows to include rapid-exploring in default pipeline"
```

---

### Task 5: Final verification

**Step 1: Read all four modified files and verify consistency**

- `skills/concept-forming/SKILL.md` — choice point exists after Step 1
- `docs/philosophy.md` — rapid-explore listed before explore, noted as default
- `docs/guide.md` — rapid-exploring follows concept-forming, description mentions choice point
- `docs/quickstart.md` — default flows include rapid-exploring

**Step 2: Verify no contradictions**

Check that:
- concept-forming doesn't still say "which approach resonates?" anywhere
- philosophy.md paragraph order matches key signals order
- guide.md stage order matches quickstart.md pattern lines
- No file references rapid-exploring as "optional" or "alternative" — it's now "recommended"
