# Forma

**A structured design practice for AI coding agents.**

Forma is a set of skills that give your coding agent a design workflow — shape ideas, wireframe solutions, test with simulated users, and iterate on what you've built. Works with Claude Code, Codex, and any AI coding agent that reads markdown.

It runs as an opinionated workflow: each stage produces a persistent artifact that survives across sessions and engages in structured dialogue rather than one-shot generation. Run the stages in order, or jump to the one you need — the workflow adapts either way. You pick up any design exactly where you left off.

## Try it

```
git clone https://github.com/rodh/Forma.git
```

Start from scratch:

**Claude Code:**

```
/design-briefing
```

**Codex CLI:**

```
$design-briefing
```

Or jump in anywhere:

**Claude Code:**

```
/user-testing [screenshot.png]
```

**Codex CLI:**

```
$user-testing [screenshot.png]
```

## Skills

> Skill names shown without prefix. Use `/` for Claude Code, `$` for Codex CLI.

### Design loop

| Skill | What it does | Output |
|-------|-------------|--------|
| design-briefing | Distill raw context into a working brief through dialogue | `brief.md` |
| concept-forming | Explore the solution space, develop all approaches to wireframe depth, pick or combine | `concept.md`, `approaches.md`, `wireframes.md`, `exploration/` |
| wireframing | Generate ASCII wireframes from the concept | `wireframes.md` |
| user-testing | AI persona usability walkthroughs | `test-results.md`, `personas.md` |

### Iteration and session management

| Skill | What it does | Output |
|-------|-------------|--------|
| checkpoint | Check status, resume, or create a design directory | — |
| recap | Capture session decisions and open threads | `sessions/YYYY-MM-DD-HHMM.md` |

## Example session

> **Platform syntax:** Claude Code uses `/skill-name`, Codex CLI uses `$skill-name`. This example uses `/` — swap for your platform's prefix.

```
▶ /design-briefing
  [notifications-requirements.md]  [current-save-flow.png]

  Teams need to be notified when a teammate saves content to a shared
  topic. Currently saves are silent. Want push + in-app notifications
  with controls to avoid noise.

  Before drafting — two questions:
  - Per-topic mute, global quiet hours, or both?
  - All shared topics notify by default, or opt-in?

> Per-topic mute only. Default on, opt-out.

  ✓ Brief saved → brief.md


▶ /concept-forming

  Three directions:

  A. Activity feed — passive tab per topic.
     Low interruption, low timeliness.
  B. Smart digest — batched summary.
     Quiet, but delays awareness by hours.
  C. Notify-on-save — push per save, per-topic mute.
     Immediate, but noisier.

> Explore all three.

  All three developed to wireframe depth → exploration/

  A and B are pull-based — user checks for updates.
  C is push-based — updates come to the user.

> C — mute controls inline is exactly right.

  ✓ Concept locked → concept.md
  Direction: notify-on-save with inline mute controls.
  Key bet: users will manage noise themselves if controls are
  within reach.


▶ /user-testing

  3 personas walked through the design independently.
  Consensus issue: mute toggle is discoverable but "mute duration"
  isn't — all 3 expected a way to mute temporarily, not just on/off.
  Recommendation: add a duration picker (1h, 1d, forever) to the
  mute action.

  ✓ Test results saved → test-results.md
```

## Learn more

[Guide](docs/guide.md) — scenario patterns, design principles, and the full workflow

## License

MIT
