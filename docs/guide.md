# Forma Guide

Forma is a design toolkit for rapid iteration — a set of skills that give your coding agent a design practice. It optimizes for decisions, not pixels — each stage forces a commitment before the next one begins.

For usage patterns and examples, see the [Quick Start](quickstart.md).

---

## How the stages connect

Each skill reads the previous stage's artifact, does its work through dialogue or structured processing, and writes a file to the current directory.

**Design briefing** opens a dialogue with you to distill messy input into a problem statement, constraints, known context, open questions, and an opinionated first instinct. It asks clarifying questions one at a time — probing for gaps, surfacing ambiguity, and testing assumptions — before synthesizing the brief. This is the foundation everything else builds on.

**Concept forming** explores the solution space. It presents genuinely different approaches — not three flavors of the same idea, but different interaction models with different trade-offs. After presenting approaches, it offers a choice: rapid-explore all approaches to wireframe depth (recommended), pick one to develop through dialogue, explore one deeper, or branch into parallel pipelines.

**Rapid exploring** auto-develops all approaches from concept-forming to wireframe depth without user dialogue. It reads `approaches.md`, autonomously resolves tensions for each approach based on its stated priorities, generates concept directions and full ASCII wireframes, and saves each to `exploration/{approach-slug}.md`. After all approaches are materialized, it presents a comparison summary and lets you pick one or combine elements from several into a single direction that promotes to `concept.md` and `wireframes.md`. Use this when you want to visually compare all directions before committing — faster than exploring each one manually, at the cost of human nuance in tension resolution.

**Wireframing** translates the concept into screen structure using ASCII art. The constraint of ASCII keeps the focus on information architecture and interaction flow rather than visual polish. Iteration is capped at three rounds — if the structure isn't stable by then, the problem is in the concept, not the layout.

**User testing** runs simulated usability walkthroughs with behavioral personas (generated from the brief, provided by you, or loaded from `personas.md` in the project directory). Each persona encounters the design independently, reacts based on their specific behavior patterns, and surfaces friction that generic review misses. Results include consensus issues, a highest-leverage fix recommendation, and an explicit check against the concept's key bet.

**Concept branching** creates sibling variant directories for exploring alternative directions. It copies the brief and personas into a new directory, letting you re-run concept-forming with a different constraint or branch into an approach you didn't choose the first time. Useful when you want to compare two directions side by side without losing work.

---

## What you can brief

The design-briefing stage is deliberately format-agnostic. The agent expects messy, incomplete, mixed-abstraction input — that's the whole point. Here's what works:

- **Tickets and tasks.** Jira tickets, Linear issues, GitHub issues, Trello cards. Structured or not — design-briefing extracts the problem statement and constraints from whatever format they're in.
- **Conversations.** Slack threads, Discord messages, email chains, meeting transcripts. The back-and-forth often contains the real requirements buried in debate and context-switching.
- **Product documents.** PRDs, one-pagers, strategy decks (pasted as text), roadmap excerpts. Partial documents work fine — the agent identifies what's covered and flags what's missing.
- **User feedback.** Customer verbatims, support tickets, NPS comments, app store reviews, user interview notes. Direct quotes are especially useful because they ground the brief in real language rather than abstracted requirements.
- **Data and metrics.** Analytics summaries, funnel drop-off numbers, heatmap observations, A/B test results. Quantitative context helps the brief distinguish between "users say they want X" and "users actually do Y."
- **Visual references.** Screenshots, photos of whiteboards, existing wireframes, mockups, competitor UI screenshots, sketches on paper. Images are first-class input — the agent reads them directly and extracts layout patterns, interaction cues, and visual hierarchy into the brief.
- **Existing UI.** Descriptions of current screens, component inventories, design system audit notes. Useful when the design task is modifying something that already exists.
- **Personal observations.** "I keep running into this problem" or "every time I try to do X, the app makes me do Y first." A frustration described in your own words is a perfectly valid starting point.

You can combine these freely. A typical briefing might include a Jira ticket, two Slack messages that add context the ticket missed, and a note about what you noticed when you tried the current flow yourself. Design-briefing sorts it out — extracting the problem, inferring constraints, identifying gaps, and producing a structured brief that downstream stages can build on.

The key design choice: design-briefing would rather you paste in too much raw context than too little. Thin input produces thin briefs. When the context is genuinely sparse, the brief says so explicitly — it names what's missing rather than padding with assumptions.

---

## Dialogue patterns

Skills don't generate output in one shot. Most open a conversation — presenting options or structure, incorporating your reactions, and converging on a final artifact. Understanding which skills work which way helps you calibrate how much to engage at each stage.

**Three interaction modes:**

**Absorb.** Some skills take input and produce output without back-and-forth. User testing runs persona walkthroughs against your wireframes. Concept branching copies and diverges. Recap captures session thinking. Checkpoint reads artifacts and orients you. You give the agent material, it processes it, done. These skills are transactional — the quality of the output depends on the quality of the input, not on mid-process conversation.

**Dialogue.** Design-briefing and concept-forming open with structured engagement and expect you to react. Design-briefing asks clarifying questions one at a time before drafting the brief — probing gaps, testing assumptions, and surfacing requirements you hadn't articulated. Concept-forming presents 2-4 concept directions with explicit trade-offs and expects you to push back or choose. The conversation typically converges in 2-3 exchanges. Two responses matter here:
- **Challenge an option** — the agent rethinks rather than defends. If you say "approach B feels too complex," it doesn't argue for B — it revisits what made B seem necessary and looks for simpler alternatives.
- **Reject everything** — the agent treats this as a signal that the real constraint hasn't surfaced yet. Instead of generating more options, it asks what's wrong with all of them. The answer usually reveals a requirement that wasn't in the brief.

**Iterate.** Wireframing presents structure and accepts directed feedback — move this section, break this into two screens, show the empty state. Each round produces a revised wireframe you can react to again. This is capped at about 3 rounds. After that, the agent flags diminishing returns: either the wireframe is structurally sound and remaining issues are visual (handle those downstream), or the problems are upstream in the concept and further wireframe tweaking won't fix them.

**How feedback gets incorporated.** Across all modes, the agent doesn't defend its output. A challenge to a concept direction means rethinking the direction, not producing a better justification for it. A request to restructure a wireframe means restructuring, not explaining why the current structure is actually fine. The agent treats your reactions as constraints, not objections to overcome.

**Convergence signals.** The agent tells you when to stop iterating. This shows up as explicit flags: "this is a visual polish issue, not a structural one" or "this problem traces back to the concept — re-run concept-forming instead of continuing to adjust wireframes." These signals prevent the common failure mode where you keep refining an artifact past the point of structural improvement, burning time on changes that belong in a different stage.

---

## Session continuity

The system reconstructs context from artifacts, not conversation history. When you run checkpoint in a directory with existing artifacts, it reads every artifact, detects the current stage, and orients you.

Artifacts carry the decisions. Session recaps (recap) carry the thinking between artifacts. Git history preserves iteration history. Resumption isn't a special feature — it's a side effect of how the system already works.

---

## Limitations

- **Not a pixel-perfect design tool.** ASCII wireframes define structure, not visual design.
- **Not a replacement for real user research.** Simulated persona walkthroughs catch structural friction, but they're behavioral archetypes, not real people.
- **Not a project management system.** No task tracking, no timeline, no team coordination. It's a design thinking tool for one person moving through a design problem.
- **Not for visual-heavy design work.** Branding, illustration, motion design, data visualization — the text-based pipeline doesn't have much to offer. It's strongest when the problem is structural.

---

## See also

- [Quick Start](quickstart.md) — Usage patterns, examples, and which stages to skip
- [Philosophy](philosophy.md) — Design principles, why ASCII wireframes, refine vs. fork
