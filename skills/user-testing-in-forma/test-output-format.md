# Test Output Format

## Internal Process

Before writing any output, mentally walk through each screen per persona — first impressions, task attempts, friction points, what they'd say out loud. This internal walkthrough is the raw material for every section below. Do not output the walkthrough itself.

## Output Order

After the personas list, produce the following sections in this order:

### Action items

Always use three sections (omit any that would be empty). Number items sequentially as AI-{n} — these IDs are stable references across test iterations.

Each action item gets 1–2 evidence bullets showing which persona hit it and how. Format:

```
- **AI-{n}.** Brief description — why it matters.
  - *Evidence:* Persona (trait) observed behavior or specific failure.
  - *Evidence:* Persona (trait) observed behavior or specific failure.
```

- **Resolved from previous test:** Items the current wireframes have addressed. Preserve original AI-{n} IDs. (Empty on first test run.)
- **Remaining issues:** Items still present from prior tests. Preserve original AI-{n} IDs. Re-state why each still matters. (Empty on first test run.)
- **New findings:** Issues found in this test. On first run, this contains all items. On subsequent runs, continue numbering from max prior ID + 1.

### What works

Short list of design positives grounded in persona behavior — what the design gets right and why it works for these users. Format:

```
- **Short label.** What works and which persona behavior confirms it.
```

### Consensus issues

What problems did multiple personas hit? Numbered list, each with evidence. Below each issue, an indented sub-bullet with the verdict — ***Fix now*** or ***Defer*** — leading the line, followed by a short rationale. "Fix now" means worth addressing before moving to the next stage. "Defer" means real but acceptable — state what absorbs the risk.

### Highest-leverage fix

One recommendation, bolded, with 2–4 bullets on what it accomplishes. End with a readiness assessment: where the design stands and a clear next step (iterate wireframes, move to prototype, run another targeted test, etc.).

If the concept from the ideating-in-forma skill included a key bet, report whether the internal walkthroughs validated or contradicted it.

### Adoption

One line per persona — would they adopt this over their current workflow, and why? Format:

```
- **Persona name:** Adopts / Hesitant / Unlikely — reason tied to their current workflow.
```
