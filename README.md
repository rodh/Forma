# SlashDesign

A platform-agnostic skill pack for rapid design iteration — brief, explore concepts, wireframe, and test with AI personas.

Works with any agent platform that supports the [Agent Skills specification](https://agentskills.io/specification): Claude Code, Codex CLI, and others.

## Install

**Claude Code:**

```
claude plugin add rod-howard/slash-design
```

**Codex CLI:**

```
git clone https://github.com/rod-howard/slash-design.git
cp -r slash-design/skills/* ~/.agents/skills/
```

Or copy into a project-local `.agents/skills/` directory.

## Workflow

```
design-briefing → concept-forming → wireframing → user-testing
                              ↑          |
                              | (refine) |
                              +──────────+
```

### Skills

| Skill | What it does | Output |
|-------|-------------|--------|
| quickflow-status | Check status, resume, or create a design directory | — |
| design-briefing | Distill raw context into a working brief | `brief.md` |
| concept-forming | Explore the solution space, land on a concept | `concept.md` |
| wireframing | Generate ASCII wireframes | `wireframes.md` |
| user-testing | AI persona usability walkthroughs | `test-results.md`, `personas.md` |
| quickflow-recap | Capture session decisions and open threads | `sessions/YYYY-MM-DD-HHMM.md` |

### Invocation syntax

Depends on your platform:

| Platform | Syntax | Example |
|----------|--------|---------|
| Claude Code | `/skill-name` | `/design-briefing I want to build...` |
| Codex CLI | `$skill-name` | `$design-briefing I want to build...` |

### Quick example

```
mkdir my-app && cd my-app

design-briefing
I want to build a personal content saving app that captures stuff fast,
organizes it with AI, and helps me use it later.

concept-forming
wireframing home screen, save flow, topic briefing
user-testing
```

Any skill can be the entry point — quickflow-status is optional. Skills operate on the current working directory.

## How it works

- **Flat directory model.** No required project structure. `cd` into any directory and run skills.
- **Auto-save.** Every skill saves immediately. Existing artifacts are versioned to `archive/` before overwrite.
- **Dialogue-driven.** Shaping and testing are conversations — push back, redirect, refine.
- **Self-contained skills.** Each skill carries its own context, archive protocol, and communication style. No platform-specific orchestration required.

## Docs

See [docs/quickstart.md](docs/quickstart.md) for scenario-based examples.

## License

MIT
