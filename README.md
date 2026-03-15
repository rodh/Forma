# Forma

**A structured design practice for AI coding agents.**

Forma is a set of skills that give your coding agent a design workflow — shape ideas, wireframe solutions, test with simulated users, and iterate on what you've built. Works with Claude Code, Codex, and any AI coding agent that reads markdown.

It runs as an opinionated workflow: each stage produces a persistent artifact that survives across sessions and engages in structured dialogue rather than one-shot generation. Run the stages in order, or jump to the one you need — the workflow adapts either way. You pick up any design exactly where you left off.

## What a session looks like

> **Platform syntax:** Claude Code uses `/skill-name`, Codex CLI uses `$skill-name`. This example uses `/` — swap for your platform's prefix.

```
> /checkpoint STASH-team-notifications

  No design named "STASH-team-notifications" found. Create it? (y/n)

> y

  Created STASH-team-notifications/. Ready for design-briefing.

> /design-briefing
  [STASH-92.md]  [topics-screen-current.png]

  Teams need to be notified when a teammate saves content to a shared
  topic. Currently saves are silent — teammates only discover new content
  when they open the topic. Want push + in-app notifications with controls
  to avoid noise.

  agent: Reading ticket and screenshot...

  Before drafting — a few things to clarify:
  - The ticket says "controls to avoid noise" but doesn't specify scope.
    Per-topic mute? Global quiet hours? Both?
  - Should all shared topics notify by default, or only ones the user
    explicitly follows?

> Per-topic mute only — keep it simple. All shared topics notify by default,
  following is opt-out not opt-in.

  Clear.

  ✓ Brief saved → brief.md
  Problem: shared saves are invisible. Users miss teammate contributions.
  Key constraint: notification fatigue — per-topic mute, not global.
  Open question: notification grouping when a teammate saves multiple items quickly.

> /concept-forming

  Three directions:

  A. Activity feed — passive. A "what's new" tab per shared topic.
     Prioritizes: low interruption. Sacrifices: timeliness.
  B. Smart digest — batched. Daily/weekly summary of shared topic activity.
     Prioritizes: noise control. Sacrifices: real-time awareness.
  C. Notify-on-save — active. Push + in-app per save, with per-topic mute.
     Prioritizes: immediacy. Sacrifices: quiet if team is active.

  Which direction, or push back?

> C, but I want the mute controls to be really prominent — not buried in settings

  ✓ Concept saved → concept.md
  Direction: notify-on-save with inline mute controls.
  Key bet: users will manage noise themselves if controls are within reach.

> /wireframing notification banner, topic screen with mute toggle, notification center

  ┌──────────────────────────────────┐
  │ Topics                       [≡] │
  │ ┌──────────────────────────────┐ │
  │ │ Sarah saved "Q3 OKRs"        │ │
  │ │ to Design Systems       [x]  │ │
  │ │  [View]  [Mute topic ▾]      │ │
  │ └──────────────────────────────┘ │
  │  ★ Design Systems            (3) │
  │    Product Research          (1) │
  │    Brand Guidelines              │
  └──────────────────────────────────┘

  Mute toggle is on the banner itself — no settings detour.
  Notification center and other screens also drafted.

  Banner should push the list down, not overlay it.

> Right — update to push layout instead of overlay

  [revised wireframes with push layout]

  ✓ Wireframes saved → wireframes.md

> /user-testing

  3 personas walked through the design independently.
  Consensus issue: mute toggle is discoverable but "mute duration" isn't —
  all 3 personas expected a way to mute temporarily, not just on/off.
  Recommendation: add a duration picker (1h, 1d, forever) to the mute action.

  ✓ Test results saved → test-results.md
```

## Try it

```
git clone https://github.com/rodh/Forma.git
```

**Claude Code:**

```
cd your-project
checkpoint my-first-design
```

**Codex CLI:**

```
cd your-project
$checkpoint my-first-design
```

## Skills

> Skill names shown without prefix. Use `/` for Claude Code, `$` for Codex CLI.

### Design loop

| Skill | What it does | Output |
|-------|-------------|--------|
| design-briefing | Distill raw context into a working brief through dialogue | `brief.md` |
| concept-forming | Explore the solution space, land on a concept direction | `concept.md`, `approaches.md` |
| wireframing | Generate ASCII wireframes from the concept | `wireframes.md` |
| user-testing | AI persona usability walkthroughs | `test-results.md`, `personas.md` |

### Iteration and session management

| Skill | What it does | Output |
|-------|-------------|--------|
| checkpoint | Check status, resume, or create a design directory | — |
| concept-branching | Branch into an alternative design direction | sibling directory with copied artifacts |
| recap | Capture session decisions and open threads | `sessions/YYYY-MM-DD-HHMM.md` |

## Learn more

- [Quick start](docs/quickstart.md) — scenario-based examples for different project types
- [Guide](docs/guide.md) — the full workflow in depth
- [Philosophy](docs/philosophy.md) — why design practice matters for AI agents

## License

MIT
