# Forma

**Opinionated design thinking skills for AI agents.**

Forma gives your AI coding agent a design thinking workflow — frame problems, explore solutions, wireframe interfaces, test with simulated users, and iterate on what you've built. Works with Claude Code, Codex, and any AI coding agent that reads markdown.

It runs as an opinionated workflow: each stage produces a persistent artifact that survives across sessions and engages in structured dialogue rather than one-shot generation. Run the stages in order, or jump to the one you need — the workflow adapts either way. You pick up any design exactly where you left off.

## Install

### Claude Code

```sh
git clone https://github.com/rodh/Forma.git ~/.local/share/forma
for skill in ~/.local/share/forma/skills/*-in-forma; do
  ln -s "$skill" ~/.claude/skills/$(basename "$skill")
done
```

Each skill must be a direct child of `~/.claude/skills/` so Claude Code can discover it. Symlinks keep them updatable with `git pull`.

### Codex CLI

```sh
git clone https://github.com/rodh/Forma.git ~/.local/share/forma
for skill in ~/.local/share/forma/skills/*-in-forma; do
  ln -s "$skill" ~/.codex/skills/$(basename "$skill")
done
```

Each skill must be a direct child of `~/.codex/skills/` so Codex can discover it. Symlinks keep them updatable with `git pull`.

## Skills

> Skill names shown without prefix. Use `/` for Claude Code, `$` for Codex CLI.

### Design loop

| Skill | What it does | Output |
|-------|-------------|--------|
| framing-in-forma | Distill raw context into a working brief through dialogue | `brief.md` |
| ideating-in-forma | Explore the solution space, present approaches as text, pick or combine | `concept.md`, `approaches.md` |
| wireframing-in-forma | Generate ASCII wireframes from the concept | `wireframes.md` |
| user-testing-in-forma | AI persona usability walkthroughs | `test-results.md`, `personas.md` |
| autorun-in-forma | Autonomous full pipeline — brief to tested wireframes, no interaction | `run-YYYY-MM-DD-HHMM/` (all artifacts) |

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

  ✓ Brief saved → brief.md


▶ /ideating-in-forma

  Three directions:

  A. Activity feed — passive tab per topic.
     Low interruption, low timeliness.
  B. Smart digest — batched summary.
     Quiet, but delays awareness by hours.
  C. Notify-on-save — push per save, per-topic mute.
     Immediate, but noisier.

> C — mute controls inline is exactly right.

  ✓ Concept locked → concept.md
  Direction: notify-on-save with inline mute controls.
  Key bet: users will manage noise themselves if controls are
  within reach.


▶ /wireframing-in-forma

  Key screens:

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

  Stubs:

  Screen 3: Empty State — No Notifications
  What the user sees with no recent activity.
  - "All caught up" message
  - Link to notification settings

  Screen 4: Muted Topic — Visual Treatment
  How a muted topic appears in the sidebar.
  - Muted icon indicator
  - Dimmed unread count
  - [Unmute] action on hover

  ✓ Key screens + stubs saved → wireframes.md


▶ /user-testing-in-forma

  3 personas walked through the key screens + stubs.
  Consensus issue: mute toggle is discoverable but "mute duration"
  isn't — all 3 expected a way to mute temporarily, not just on/off.
  Recommendation: add a duration picker (1h, 1d, forever) to the
  mute action.

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
