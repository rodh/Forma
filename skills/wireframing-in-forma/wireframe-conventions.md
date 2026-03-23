# Wireframe Conventions

## Component Labels

Label structural components inline so users can reference them by ID (e.g., "I want A1 and B3").

- **Format:** `// {Letter}{Number}: {Short Name}` as a right-side annotation on the first content line of the component
- **Letter:** Approach letter (A/B/C) when in a multi-approach context; omit the letter for standalone wireframing
- **Number:** Sequential across all screens in the approach, not per-screen (A1, A2, ... A7 continues into Screen 2)
- **What to label:** Structural components — distinct UI regions that represent a design decision: navigation bars, content areas, cards, form sections, action groups, modals, sidebars, filter panels
- **What to skip:** Page-level headers, individual buttons, single text lines, decorative elements
- **Short names:** 2-3 words max, descriptive of function (e.g., "Alert Card", "Tab Bar", "Filter Panel")

```
┌──────────────────────────────────────┐
│ MyApp        [Settings] [Log out]    │
│                                      │
│ ┌──────────────────────────────────┐ │
│ │ ★ 3 items need review           │ │ // A1: Alert Card
│ │ [Review now]                     │ │
│ └──────────────────────────────────┘ │
│                                      │
│ Name       Status    Due             │ // A2: Task Table
│ ──────────────────────────────────── │
│ Q3 OKRs    Pending   Mar 30         │
│ Brand doc  Done      Mar 15         │
│                                      │
│ [* Add Task *]                       │ // A3: Action Bar
└──────────────────────────────────────┘
```

## Interactive Elements

`[Button]` `[* Primary *]` `[___input___]` `(dropdown v)` `(o) Selected` `[x] Checked` `[ON|off]` `[ Active Tab ]` `<Link>`

## Width Tiers

- **Narrow (~50 chars):** Mobile, modals, cards
- **Standard (~72 chars):** Web pages, forms, dashboards — **default**
- **Wide (~90 chars):** Dense dashboards, multi-column, data tables

Add `// Width: Standard (~72 chars)` at the top of each wireframe. Multi-column at wide tier: represent columns proportionally. Mixed flows can use different widths per screen.

## Stubs

Stubs are lightweight placeholders for screens not yet fully wireframed.

```
Screen 4: Empty State — Task List
What the user sees when they have no tasks yet.
- Illustration placeholder area
- "No tasks yet" heading + helper text
- [* Create First Task *] primary action
- Link to import from existing tool
```
