# Forma Guide

Forma is a design toolkit for rapid iteration — a set of skills that give your coding agent a design practice. It optimizes for decisions, not pixels — each stage forces a commitment before the next one begins.

---

## How the stages connect

Each skill reads the previous stage's artifact, does its work through dialogue or structured processing, and writes a file to the current directory.

**Framing** opens a dialogue to distill messy input into a problem statement, constraints, known context, open questions, and an opinionated first instinct. It asks clarifying questions one at a time — probing gaps, surfacing ambiguity, testing assumptions — before synthesizing the frame.

**Ideating** explores the solution space. It presents genuinely different approaches — different interaction models with different trade-offs — then auto-develops all of them to wireframe depth. You compare the materialized approaches and pick one or combine elements from several. The result promotes to `ideation.md` and `wireframes-v1.md`.

**User testing** runs simulated usability walkthroughs with behavioral personas (generated from the frame, provided by you, or loaded from `personas.md`). Each persona encounters the design independently and surfaces friction that generic review misses. Results include consensus issues, a highest-leverage fix, and a check against the concept's key bet.

**Wireframing** translates or refines screen structure using ASCII art. After ideating-in-forma produces initial wireframes, wireframing-in-forma handles iteration — fixing issues from user-testing-in-forma, adjusting layout, adding screens. Wireframing and user testing form a loop: fix issues, retest, repeat until stable. Iteration caps at three rounds.

---

## What you can brief

Framing-in-forma accepts any messy input — tickets, Slack threads, screenshots, PRDs, user feedback, analytics, sketches, competitor UI, meeting transcripts, personal observations. Combine them freely. A typical briefing might include a Jira ticket, two Slack messages that add context the ticket missed, and a note about what you noticed trying the current flow. Thin input produces thin briefs.

---

## Scenario patterns

> **Platform syntax:** Claude Code uses `/skill-name`, Codex CLI uses `$skill-name`. This guide uses plain skill names — adapt to your platform.

Pick the scenario that matches your task. Follow the skills in order. Skip what doesn't apply.

### New idea from scratch

**Pattern:** framing-in-forma → ideating-in-forma → user-testing-in-forma → [wireframing-in-forma ↔ user-testing-in-forma]

```
mkdir my-app && cd my-app

/framing-in-forma
I want to build a personal content saving app. I keep finding useful stuff
on Reddit, YouTube, LinkedIn — but I never go back to it. I want something
that captures content fast, organizes it with AI, and helps me use it later.

/ideating-in-forma

/user-testing-in-forma

/wireframing-in-forma (fix issues from testing)

/user-testing-in-forma (retest)
```

### Bug fix (visual/UI)

**Pattern:** framing-in-forma → wireframing-in-forma → optional user-testing-in-forma

Skip ideating-in-forma — the problem and solution space are narrow enough to go straight to wireframing.

### Bug fix (behavioral/logic)

**Pattern:** framing-in-forma → wireframing-in-forma → user-testing-in-forma

Always run user-testing-in-forma — behavioral bugs affect task completion.

### Feature iteration

**Pattern:** framing-in-forma → optional ideating-in-forma → wireframing-in-forma → user-testing-in-forma

Skip ideating-in-forma if the direction is obvious (e.g., "add sort options to a list").

### Feature modification

**Pattern:** framing-in-forma → ideating-in-forma → user-testing-in-forma → [wireframing-in-forma ↔ user-testing-in-forma]

Run the full workflow — you're rethinking the approach. Ideating-in-forma auto-develops all directions to wireframe depth so you can compare visually before committing.

### Thinking partner

**Pattern:** thinking-in-forma (at any point)

When you need to understand a problem, assess level of effort, or reason through a design decision. Works with or without existing artifacts — if you have a ticket and no design work yet, it decomposes the problem and assesses what level of design response it warrants. If you're mid-process, it handles hunches, what-ifs, and decisions against your existing artifacts. Dialogue scales with ambiguity — vague inputs get more back-and-forth, clear inputs get autonomous analysis.

### Resuming work

Run checkpoint-in-forma with no arguments in a directory with design artifacts. It shows existing artifacts, missing artifacts, session context from the most recent recap, and options to continue or advance. Or use checkpoint-in-forma with a name argument to create a named subdirectory.

### Skipping stages

| Stage | Safe to skip when |
|---|---|
| ideating-in-forma | Direction is obvious. Bug fixes, minor iterations, well-defined tickets. |
| user-testing-in-forma | Change is cosmetic, low-risk, doesn't affect task completion. |
| recap-in-forma | Session was straightforward, no decisions worth preserving. |
| thinking-in-forma | The decision is obvious or the hunch isn't worth structured analysis. |

Never skip framing-in-forma. Even simple fixes benefit from a clear frame.

### Good to know

**Auto-save.** All skills save their output immediately. Wireframes and test results use versioned files (`wireframes-v1.md`, `wireframes-v2.md`, etc.) — each version is its own file. Other artifacts overwrite in place.

**Any skill can be the entry point.** checkpoint-in-forma is optional — run framing-in-forma directly if you don't need the status check.

**Flat directory model.** Skills operate on the current working directory. No required project structure — just `cd` into a directory and start.

---

## Dialogue patterns

Skills don't generate output in one shot. Most open a conversation — presenting options, incorporating your reactions, and converging on a final artifact.

**Absorb.** Some skills take input and produce output without back-and-forth. User testing runs persona walkthroughs against your wireframes. Recap captures session thinking. You give the agent material, it processes it, done.

**Dialogue + autonomy.** Framing-in-forma and ideating-in-forma open with structured engagement. Framing-in-forma asks clarifying questions before drafting. Ideating-in-forma presents approaches with trade-offs, then auto-develops all of them — you re-engage to compare, combine, and commit. Challenge an option and the agent rethinks rather than defends. Reject everything and it asks what's wrong — usually revealing a requirement that wasn't in the brief.

**Structured thinking.** Thinking-in-forma works before, during, or between design stages. Without artifacts, it decomposes problems and assesses level of effort. With artifacts, it frames the question (hunch, what-if, or decision), runs structured analysis, and optionally applies changes. Dialogue scales with ambiguity: vague instincts get more back-and-forth to sharpen the question, clear decisions get autonomous comparison.

**Iterate.** Wireframing-in-forma and user-testing-in-forma form a loop. User-testing-in-forma surfaces issues; wireframing-in-forma fixes them. Wireframing-in-forma caps at about 3 rounds — if the structure isn't converging, the problem is upstream in the concept.

---

## Design principles

### Design is thinking, not decoration

Forma optimizes for decisions. The system treats design as increasingly specific commitments — from problem framing to interaction model to screen structure — where each stage forces a decision before the next begins. Jumping to wireframes before articulating the core interaction model produces layouts that encode no real design bet.

### Opinionated defaults, flexible execution

The workflow has a recommended flow that produces tested wireframes. You can run the full pipeline, skip stages, or jump in at any point. But when a stage runs, it runs with opinion — ideating-in-forma names what each approach prioritizes and sacrifices, user-testing-in-forma simulates specific people with specific behaviors. The system would rather be wrong and specific than right and vague.

### Artifacts over conversations

Every stage writes a durable file — brief, concept, wireframes, test results — that persists across sessions and can be read without context from the conversation that produced it. Design work is interrupt-heavy; artifacts carry the thinking forward so you don't re-derive decisions.

### Specificity over flexibility

Every stage pushes toward concrete, falsifiable statements. A concept direction names its key bet and the assumption it rests on, wireframes commit to specific screen structures, test results validate against specific behavior patterns. "Tabbed inbox with badge count on unread, swipe-to-archive" is actionable. "Clean, intuitive interface" is not.

### Honest feedback, not validation

The system challenges, not confirms. Ideating-in-forma pressure-tests your direction by naming what it sacrifices. User-testing-in-forma simulates real users who miss things, get confused, and say blunt things. If a wireframe has a fundamental problem, the system says so. It also flags diminishing returns — telling you to re-run ideating-in-forma rather than continuing to adjust wireframes past the point of structural improvement.

### Traceability

Every concept names its key bet. Test results explicitly validate or contradict that bet. Session debriefs log what was decided and rejected. This prevents the most common failure mode: forgetting why something was decided and revisiting it endlessly.

### Why ASCII wireframes

ASCII wireframes are intentionally low-fidelity — no color to debate, no border radius to bikeshed. The medium forces attention on information hierarchy, interaction flow, and screen structure. They're also fast to generate and iterate on, which changes how you work: you stop protecting wireframes from criticism because replacing them costs almost nothing. And they live in the same medium as everything else — markdown files, versionable with git, diffable in PRs, readable by AI agents.

---

## Limitations

- **Not a pixel-perfect design tool.** ASCII wireframes define structure, not visual design.
- **Not a replacement for real user research.** Simulated persona walkthroughs catch structural friction, but they're behavioral archetypes, not real people.
- **Not a project management system.** No task tracking, no timeline, no team coordination. It's a design thinking tool for one person moving through a design problem.
- **Not for visual-heavy design work.** Branding, illustration, motion design, data visualization — the text-based pipeline doesn't have much to offer. It's strongest when the problem is structural.
