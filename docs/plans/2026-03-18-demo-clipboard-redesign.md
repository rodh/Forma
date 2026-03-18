# Demo Clipboard Redesign

## Context

The original demo-clipboard.md targeted a desktop activity log with 3 personas and 5+ screens. This was too slow for a 5-minute demo. Redesigning for speed while keeping all 5 pipeline steps live.

## Changes from Original

| Dimension | Original | Revised |
|-----------|----------|---------|
| Topic | Activity / audit log | Mobile notification center |
| Platform | Desktop (wide wireframes) | Mobile (narrow, less to generate) |
| Screens | 5+ (list, filters, detail, export, settings) | 3 (list, detail, settings) |
| Personas | 3 (admin, team lead, compliance) | 2 (power user, casual user) |
| Iteration fixes | 3 findings | 2 findings |
| Briefing strategy | Short input + many follow-ups | Front-loaded input to minimize follow-ups |

## Demo Topic: Mobile Notification Center

**Why this topic:** Every SaaS user understands notifications. It generates genuine persona tension (power user wants granular control, casual user wants simplicity). Simple to brief, 3 screens keeps wireframe generation fast.

### Screens

1. **Notification list** -- scrollable feed, unread badges, grouped by time (today/earlier)
2. **Notification detail / action** -- expanded view with context + primary action button
3. **Notification settings** -- per-category toggles for in-app, email, push channels

### Personas

1. **Power user** -- wants granular control, filters, mark-all-read
2. **Casual user** -- wants simplicity, overwhelmed by too many settings

### Key tension

Granular control vs. simplicity. Settings screen is where this shows up most.

## Step-by-Step Clipboard Content

### STEP 1: Design Briefing

**Initial input (front-loaded to minimize follow-ups):**

> We need a notification center for our B2B SaaS mobile app. Right now notifications are email-only and users miss critical updates -- project assignments, deadline changes, @mentions in comments. Two user types feel this differently: power users who want granular control over what notifies them and how, and casual users who just want to know when something needs their attention without being overwhelmed. The app already has a bottom tab bar, standard iOS/Android patterns. Three screens: a notification list, a detail/action view, and notification settings. Success looks like: users check the notification center instead of relying on email.

**Backup answers:**

- Users/affected: "Power users who want control, casual users who want simplicity"
- Trigger: "Users missing critical updates because email-only notifications get buried"
- Scope: "Just the mobile notification center -- list, detail, and settings. Not the notification delivery backend."
- Constraints: "Standard mobile app with bottom tab bar. iOS/Android conventions."
- Success: "Users open the notification center instead of relying on email"

### STEP 2: Concept Forming

- Open questions: "List screen shows all notifications grouped by today/earlier. Detail screen shows context + primary action. Settings screen has per-category toggles for in-app, email, and push."
- Choose approach: "The standard feed approach -- chronological list with category filters. Don't need anything fancy like an inbox-zero model or priority-based grouping."
- Trade-offs: "Simplicity over power. Default settings should be sensible so casual users never touch settings. Power users can dig in if they want."

### STEP 3: User Testing Round 1

- Personas: "Generate them from the brief. Two personas: a power user who wants granular control, and a casual user who just wants simplicity."

### STEP 4: Wireframing Iteration

- Template: "Based on the user testing findings: 1) Add a mark-all-read button to the list screen header 2) Simplify the settings screen -- group toggles by category with sensible defaults shown"
- Adapt to actual test-results-v1.md findings from dry run.
- Only 2 fixes to keep iteration fast.

### STEP 5: User Testing Round 2

- No input expected -- auto-picks up wireframes-v2 and existing personas.

## Dry Run Strategy

1. Run through all 5 steps once (unrecorded)
2. Check test-results-v1.md for actual findings
3. Update Step 4's wireframing input to reference real findings
4. Re-run with screen recording for the final take
