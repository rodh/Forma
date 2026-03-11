# Quick Start Guide

> **Platform syntax:** Claude Code uses `/skill-name`, Codex CLI uses `$skill-name`. This guide uses plain skill names — adapt to your platform.

Pick the scenario that matches your task. Follow the skills in order. Skip what doesn't apply.

---

## New idea from scratch

**Pattern:** design-briefing → concept-forming → wireframing → user-testing

```
mkdir my-app && cd my-app

design-briefing
I want to build a personal content saving app. I keep finding useful stuff
on Reddit, YouTube, LinkedIn — but I never go back to it. I want something
that captures content fast, organizes it with AI, and helps me use it later.

concept-forming

wireframing home screen, save flow, topic briefing

user-testing
```

---

## Work tickets

### Bug fix (visual/UI)

**Pattern:** design-briefing → wireframing → optional user-testing

Skip concept-forming — the problem and solution space are narrow enough to go straight to wireframing.

```
mkdir STASH-fix-autodismiss && cd STASH-fix-autodismiss

design-briefing
Ticket STASH-42: Save confirmation toast auto-dismisses after 2 seconds.
Users can't read the full message before it disappears. Increase dismiss
timer and make the undo target clearly tappable.

wireframing save confirmation toast with extended timer and prominent undo action
```

### Bug fix (behavioral/logic)

**Pattern:** design-briefing → wireframing → user-testing

Always run user-testing — behavioral bugs affect task completion.

### Feature iteration

**Pattern:** design-briefing → optional concept-forming → wireframing → user-testing

Skip concept-forming if the direction is obvious (e.g., "add sort options to a list").

### Feature modification

**Pattern:** design-briefing → concept-forming → wireframing → user-testing

Run the full workflow — you're rethinking the approach.

---

## Resuming work

Run quickflow-status with no arguments in a directory with design artifacts. It shows:

- **Artifact table** — one row per existing file with a content summary
- **Missing artifacts** — what hasn't been created yet
- **Session context** — open threads from the most recent quickflow-recap
- **"Where do you want to pick up?"** — options to continue, advance, or re-run a stage

Or use quickflow-status with a name argument to create a named subdirectory and work from there.

---

## Skipping stages

| Stage | Safe to skip when |
|---|---|
| concept-forming | Direction is obvious. Bug fixes, minor iterations, well-defined tickets. |
| user-testing | Change is cosmetic, low-risk, doesn't affect task completion. |
| quickflow-recap | Session was straightforward, no decisions worth preserving. |

Never skip design-briefing. Even simple fixes benefit from a clear brief.

---

## Good to know

**Auto-save.** All skills save their output immediately. If an artifact already exists, the previous version is archived to `archive/` with a version number before the new version overwrites it.

**Any skill can be the entry point.** quickflow-status is optional — run design-briefing directly if you don't need the status check.

**Flat directory model.** Skills operate on the current working directory. No required project structure — just `cd` into a directory and start.
