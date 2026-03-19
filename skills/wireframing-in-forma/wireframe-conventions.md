# Wireframe Conventions

## Alignment Rules

1. **Build from a ruler line.** Start each box with its full top border (`┌──...──┐`) as the ruler. All subsequent lines must match its total character count — content lines, separators, and bottom border.
2. **Content stays inside.** If text exceeds box width, wrap at word boundary. Never push the right border outward.
3. **Nesting.** Inner boxes fit entirely within the outer box, with at least 1 space of padding on each side.

## Spacing Rules

1. **Blank lines between sections.** Inside any box, separate distinct content groups with a padded blank line (`│` + spaces + `│`). Navigation, content area, and actions should always have blank lines between them.
2. **No content on border lines.** Lines with `┌`, `└`, `├`, and separator `─` characters carry only border characters. Content starts on the next line.
3. **Section labels get their own line.** Labels like "FILTERS", "RESULTS", or section headers sit on their own line with a blank line after them before content begins.

## Interactive Elements

- Buttons: `[Button Label]`
- Primary buttons: `[* Button Label *]`
- Text inputs: `[___placeholder text___]`
- Dropdowns: `(dropdown label v)`
- Radio buttons: `(o) Selected  ( ) Unselected`
- Checkboxes: `[x] Checked  [ ] Unchecked`
- Toggle: `[ON|off]` or `[on|OFF]`
- Tabs: `[ Active ] [ Inactive ] [ Inactive ]`
- Links: `<Link Text>`

## Width Tiers

Choose a width tier based on the content being wireframed:
- **Narrow (~50 chars):** Mobile screens, single components, modals, cards
- **Standard (~72 chars):** Web pages, forms, single-column layouts, simple dashboards
- **Wide (~90 chars):** Dense dashboards, multi-column layouts, admin panels, data tables

Standard is the default. For multi-column layouts at wide tier, represent columns proportionally (e.g., sidebar + main + aside as ~20 + ~48 + ~20 chars). Add a width annotation comment at the top of each wireframe: `// Width: Standard (~72 chars)`. The user can override by requesting a specific tier. Mixed flows can use different widths per screen (e.g., narrow for a mobile modal, wide for a dashboard).
