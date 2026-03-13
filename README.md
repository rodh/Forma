# QuickFlow

A structured design practice for AI coding agents.

QuickFlow gives your AI coding agent a design workflow. You describe what you want to build, and a series of skills walks you through briefing, concept exploration, wireframing, and usability testing — all in structured dialogue, all saved to markdown files that persist between sessions. Pick up where you left off, refine what exists, or branch into a new direction.

Works with Claude Code, Codex, and any AI coding agent that reads markdown.

## What a session looks like

> **Platform syntax:** Claude Code uses `/skill-name`, Codex CLI uses `$skill-name`. Examples below use plain skill names — add your platform's prefix.

You're building a team notifications feature. Start a design directory:

```
quickflow-status STASH-team-notifications
```

The agent creates `STASH-team-notifications/` and drops you in. Now brief it:

```
design-briefing
We need team notifications for our project management app. Users miss
updates on tasks they're assigned to or watching. Need real-time alerts,
a notification center, and digest options for people who don't want
constant interruptions.
```

The agent asks clarifying questions — what platforms, how many users, any existing notification patterns? You go back and forth until the brief is solid. It saves `brief.md`.

Now explore the concept space:

```
concept-forming
```

The agent reads your brief, generates multiple approaches, surfaces tensions between them, and works with you to land on a direction. It saves `concept.md`.

Wireframe the key screens:

```
wireframing notification center, alert toast, digest settings
```

ASCII wireframes for each screen, saved to `wireframes.md`. The agent critiques its own layouts and asks if anything needs revision.

Test it with AI personas:

```
user-testing
```

The agent generates realistic user personas, then walks each one through the wireframes — finding usability issues, confusing flows, and missed edge cases. Results go to `test-results.md` and `personas.md`.

Something off? Go back to any stage. The old version gets archived automatically before the new one overwrites it.

Done for the day? Capture where you left off:

```
quickflow-recap
```

Next session, run `quickflow-status` in the same directory — it reads your artifacts, shows what's done, surfaces open threads, and asks where you want to pick up.

## Try it

```
git clone https://github.com/rodh/QuickFlow.git
```

**Claude Code:**

```
cd your-project
quickflow-status my-first-design
```

**Codex CLI:**

```
cd your-project
$quickflow-status my-first-design
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
| quickflow-status | Check status, resume, or create a design directory | — |
| concept-branching | Branch into an alternative design direction | sibling directory with copied artifacts |
| quickflow-recap | Capture session decisions and open threads | `sessions/YYYY-MM-DD-HHMM.md` |

## Learn more

- [Quick start](docs/quickstart.md) — scenario-based examples for different project types
- [Guide](docs/guide.md) — the full workflow in depth
- [Philosophy](docs/philosophy.md) — why design practice matters for AI agents

## License

MIT
