# Forma

**Opinionated design thinking skills for AI agents.**

Forma gives your AI coding agent a design thinking workflow — frame problems, explore solutions, wireframe interfaces, test with simulated users, and iterate on what you've built. Works with Claude Code, Codex, and any AI coding agent that reads markdown.

It runs as an opinionated workflow: each stage produces a persistent artifact that survives across sessions and engages in structured dialogue rather than one-shot generation. Run the stages in order, or jump to the one you need — the workflow adapts either way. You pick up any design exactly where you left off.

## Try it

```
git clone https://github.com/rodh/Forma.git
```

Start from scratch:

**Claude Code:**

```
/framing-in-forma
```

**Codex CLI:**

```
$framing-in-forma
```

Or jump in anywhere:

**Claude Code:**

```
/user-testing-in-forma [screenshot.png]
```

**Codex CLI:**

```
$user-testing-in-forma [screenshot.png]
```

## Skills

> Skill names shown without prefix. Use `/` for Claude Code, `$` for Codex CLI.

### Design loop

| Skill | What it does | Output |
|-------|-------------|--------|
| framing-in-forma | Distill raw context into a working frame through dialogue | `frame.md` |
| ideating-in-forma | Explore the solution space, develop all approaches to wireframe depth, pick or combine | `ideation.md`, `approaches.md`, `wireframes.md`, `exploration/` |
| wireframing-in-forma | Generate ASCII wireframes from the concept | `wireframes.md` |
| user-testing-in-forma | AI persona usability walkthroughs | `test-results.md`, `personas.md` |

### Iteration and session management

| Skill | What it does | Output |
|-------|-------------|--------|
| status-in-forma | Check status, resume, or create a design directory | — |
| log-in-forma | Capture session decisions and open threads | `sessions/YYYY-MM-DD-HHMM.md` |
| thinking-in-forma | Understand problems, evaluate effort, reason through design decisions | `sessions/YYYY-MM-DD-HHMM.md` |

## Example session

> **Platform syntax:** Claude Code uses `/skill-name`, Codex CLI uses `$skill-name`. This example uses `/` — swap for your platform's prefix.

```
▶ /framing-in-forma
  [notifications-requirements.md]  [current-save-flow.png]

  Teams need to be notified when a teammate saves content to a shared
  topic. Currently saves are silent. Want push + in-app notifications
  with controls to avoid noise.

  Before drafting — two questions:
  - Per-topic mute, global quiet hours, or both?
  - All shared topics notify by default, or opt-in?

> Per-topic mute only. Default on, opt-out.

  ✓ Frame saved → frame.md


▶ /ideating-in-forma

  Three directions:

  A. Activity feed — passive tab per topic.
     Low interruption, low timeliness.
  B. Smart digest — batched summary.
     Quiet, but delays awareness by hours.
  C. Notify-on-save — push per save, per-topic mute.
     Immediate, but noisier.

> Explore all three.

  A: New "Activity" tab            C: Inline notification banner
  ┌───────────────────────┐        ┌───────────────────────┐
  │ Design Systems        │        │ ┌───────────────────┐ │
  │ [Saves] [Activity]    │        │ │ Sarah saved "Q3   │ │
  │ ┌───────────────────┐ │        │ │ OKRs" [Mute▾] [x] │ │
  │ │ Sarah: Q3 OKRs    │ │        │ │ [View]             │ │
  │ │ 2h ago            │ │        │ └───────────────────┘ │
  │ │ James: Brand doc  │ │        │ ★ Design Systems  (3) │
  │ │ yesterday         │ │        │   Product Research (1)│
  │ └───────────────────┘ │        │   Brand Guidelines    │
  └───────────────────────┘        └───────────────────────┘

  B: Daily digest notification
  ┌───────────────────────┐
  │ Today's Activity      │
  │ ┌───────────────────┐ │
  │ │ Design Systems    │ │
  │ │ 3 new saves today │ │
  │ │ Product Research  │ │
  │ │ 1 new save today  │ │
  │ └───────────────────┘ │
  └───────────────────────┘

  A and B are pull-based — user checks for updates.
  C is push-based — updates come to the user.

  ✓ All three developed → exploration/

> C — mute controls inline is exactly right.

  ✓ Concept locked → ideation.md
  Direction: notify-on-save with inline mute controls.
  Key bet: users will manage noise themselves if controls are
  within reach.


▶ /user-testing-in-forma

  3 personas walked through the design independently.
  Consensus issue: mute toggle is discoverable but "mute duration"
  isn't — all 3 expected a way to mute temporarily, not just on/off.
  Recommendation: add a duration picker (1h, 1d, forever) to the
  mute action.

  ✓ Test results saved → test-results.md


▶ /wireframing-in-forma fix the mute duration issue

  ┌──────────────────────────────────┐
  │ ┌──────────────────────────────┐ │
  │ │ Sarah saved "Q3 OKRs"        │ │
  │ │ to Design Systems       [x]  │ │
  │ │  [View]  [Mute ▾]            │ │
  │ │  ┌─────────────────────────┐ │ │
  │ │  │ Mute for 1 hour        │ │ │
  │ │  │ Mute for 1 day         │ │ │
  │ │  │ Mute forever           │ │ │
  │ │  └─────────────────────────┘ │ │
  │ └──────────────────────────────┘ │
  │  ★ Design Systems            (3) │
  │    Product Research          (1) │
  │    Brand Guidelines              │
  └──────────────────────────────────┘

  ✓ Wireframes updated → wireframes.md


▶ /user-testing-in-forma

  3 personas re-tested the updated wireframe.
  No critical issues. Minor: consider "Unmute" confirmation.

  ✓ Test results saved → test-results.md

  This cycle repeats as needed:

           │
           ▼
  ┌──────────────────────────┐◄─────┐
  │  wireframing-in-forma    │      │
  └────────────┬─────────────┘      │
               ▼                    │
  ┌──────────────────────────┐  ┌───┴─────────────┐
  │  user-testing-in-forma   │─►│ Issues found?   │
  └────────┬────────┘    │ Refine & retest │
           │              └─────────────────┘
           │ (passes)
           ▼
  ┌─────────────────────────────────┐
  │ Ready to implement              │
  │ → Hand off to your build tools  │
  └─────────────────────────────────┘
```

## Learn more

[Guide](docs/guide.md) — scenario patterns, design principles, and the full workflow

## License

MIT
