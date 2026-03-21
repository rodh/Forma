---
name: thinking-in-forma
description: Use when you need to reason through a design decision, understand a ticket, explore a hunch, or compare options — works with or without existing artifacts
---

**Workflow context:** Thinking partner — works before, during, or between design stages. Adapts to whatever context exists.

## 1. Read context

Read all design artifacts in CWD (`brief.md`, `concept.md`, `wireframes.md`, `test-results.md`, `personas.md`, `research/`, latest `sessions/` note) plus any user-provided input. Note what exists and what doesn't — this determines behavior.

## 2. Frame

Detect the thinking pattern from `$ARGUMENTS` and context.

**Orient ("help me understand this ticket/problem"):**
- Triggered by: ticket content, task descriptions, "what is this asking" questions, or raw context with no existing artifacts.
- Decompose into: (1) what's being asked, (2) the actual problem underneath, (3) what it connects to, (4) level of effort (quick fix → full design loop).
- If research is needed, conduct and present separately. Save substantial findings to `research/{topic-slug}.md` (self-contained: title, date, question, findings, sources).
- **Output:** structured understanding with level-of-effort recommendation

**Hunch ("something feels off"):**
- Present compact design state summary (one sentence per artifact), then ask "what's nagging you?"
- One question per message. Allow 1-2 rounds to get from vague → specific. Surface artifact tensions as options if they can't articulate it.
- **Output:** a precise statement of the issue

**What-if ("what if we tried..."):**
- Restate the idea as a testable proposition
- One quick check: "Is that a fair restatement?" (skip if clearly accurate)
- **Output:** the proposition to trace

**Decision ("should we X or Y"):**
- Acknowledge the options. If only one stated, ask for the alternative.
- Frame as "[X] vs [Y] given [relevant context from artifacts]"
- **Output:** the framed decision

**Research ("look into X", "how does Y work", "what are the patterns for Z"):**
- Triggered by: competitor/pattern inquiries, focused factual questions, "look into", "how does X handle", "what are the approaches for".
- Conduct research autonomously — no Frame stop, no session note.
- Save findings to `research/{topic-slug}.md` with: title, date, question, findings, key takeaways (2-3 bullets), sources (if applicable).
- Present a summary with key takeaways. The research artifact is the only output.
- **Skip Think, Act, and Capture** — the saved artifact is the deliverable.

**STOP after Frame** (Orient/Hunch/What-if/Decision only). Present the framed output and wait for the user to confirm or adjust before proceeding to Think. Research skips this stop.

If ambiguous, ask one AskUserQuestion: **A. Understand something** (orient), **B. Surface something** (hunch), **C. Explore a what-if**, **D. Decide between options**, **E. Research something** (research). If the user needs a different skill, say so directly.

## 3. Think

**Orient pattern — three-part analysis:**

1. **Breakdown** — decompose the problem into constituent parts, name each clearly
2. **Landscape** — what exists already, what's new, what's uncertain. Integrate any external research.
3. **Effort assessment** — what level of design engagement each part warrants (light touch vs. full design loop)

End with 2-3 labeled next moves reflecting the actual situation, not a generic menu.

**Hunch/What-if/Decision patterns — four-part analysis:**

1. **What the artifacts say** — pull relevant content, quote specific lines/sections
2. **What's at stake** — concrete downstream effects on each artifact if we go one way vs another
3. **Strongest argument for each side** — steel-man all positions (even for hunches: steel-man "it's actually fine" vs "there's a real problem")
4. **What we'd need to believe** — the assumption about user behavior each direction rests on

**Dialogue pacing:**

| Pattern | Delivery | Exchanges |
|---------|----------|-----------|
| Orient | Full breakdown, then ask what to dig into | 1 (focused) to 2-3 (complex) |
| Hunch | Pause after tensions, check in after each analysis piece | 2-3 |
| What-if | Four-part analysis as one block, then "worth pursuing or dead end?" | 1 |
| Decision | Four-part analysis as one block, then "which way are you leaning?" Pressure-test before Act. | 1 |
| Research | Autonomous — research, save artifact, present summary | 0 (no stops) |

Each pause = **stop and wait** — do not continue to the next phase in the same message. Prefer labeled options (A/B/C) over open-ended questions.

## 4. Act

If thinking leads to artifact changes: list each file and proposed change, get approval per file via AskUserQuestion (approve / reject / modify), then apply. Archive wireframes/test-results before overwriting.

If orient pattern produced findings ready for a brief: name what would carry into framing-in-forma and let the user decide. Don't auto-invoke.

If no changes needed: skip to Capture.

## 5. Capture

Write session note to `sessions/YYYY-MM-DD-HHMM.md` (create directory if needed):

- **Type:** Thinking
- **Session summary** — 2-3 sentences
- **Trigger** — the user's opening statement
- **Frame** — the precise question or decomposition arrived at
- **Analysis** — key points from Think (compressed)
- **Resolution** — what was decided or understood
- **Artifact changes** — what was modified, or "None"
- **Research output** — filename and one-line description (if saved to `research/`)
- **Feeds forward** — findings for future skills (orient pattern only)
- **Open threads** — anything surfaced but not resolved

## Rules

- Be direct. No preamble, no filler. Labeled bullets for discrete items, prose for narrative.
- Quote artifacts, don't summarize — the user needs to see exactly what you're referencing.
- Steel-man all positions. Don't lead the user toward a predetermined answer.
- YAGNI: if thinking resolves without needing artifact changes, don't invent changes to make.
- If thinking reveals an upstream problem (concept-level, not wireframe-level), name it. Don't patch downstream artifacts to work around a concept issue.
- **Never deliver Frame and Think in the same response.** Each phase ends with the user's input before the next begins.
- Orient is for understanding, not designing — decompose and assess, don't jump to solutions.
- Don't skip thinking because it "seems obvious." The user invoked it for a reason.
- Research must be clearly labeled and separated from analysis — factual vs. assessment.

$ARGUMENTS
