# Design: Restore versioning, drop design-log

## Context

The quickflow design toolkit currently has two auxiliary tracking mechanisms with overlapping purposes:
- **Session notes** (`sessions/YYYY-MM-DD-HHMM.md`) — capture reasoning, decisions, and open threads from design conversations
- **Design log** (`design-log.md`) — an append-only chronological index of artifact versions

The design log was introduced to compensate when full versioning was removed from wireframing and user-testing skills. But losing versioned artifacts (separate files per version) means you can't revert to earlier wireframes if a direction proves infeasible, and you can't review how test results evolved. The design log provides a thin record of what versions existed, but not the content itself.

**Decision:** Restore separate-file versioning to wireframes and test-results, remove design-log entirely, keep sessions for reasoning. This is cleaner — versioned files *are* the history, sessions capture the *why*.

## Changes

### Wireframing skill (`skills/wireframing/SKILL.md`)

- Each version writes to a new file: `wireframes-v1.md`, `wireframes-v2.md`, etc.
- Skill checks for highest existing `wireframes-v*.md` and increments
- Same version-increment rule: only increment when a different skill has run since last save; within-session iterations overwrite the current version file
- Remove all `design-log.md` append logic
- When addressing test results, include `**Addressing:** test-results-v{M}` on the next line

### User-testing skill (`skills/user-testing/SKILL.md`)

- Each version writes to a new file: `test-results-v1.md`, `test-results-v2.md`, etc.
- Same version-increment rule as wireframing
- Remove all `design-log.md` append logic
- `**Tested against:** wireframes-v{M}` references the file name now

### Thinking-partner skill (`skills/thinking-partner/SKILL.md`)

- Remove design-log reference from Act section
- When thinking-partner modifies wireframes or test-results, it creates the next versioned file
- Session notes remain unchanged

### Checkpoint skill (`skills/checkpoint/SKILL.md`)

- Remove `design-log.md` references
- Scan for `wireframes-v*.md` and `test-results-v*.md` files
- Reconstruct timeline from version headers and "Addressing"/"Tested against" lines
- Update file naming convention table

### Guide (`docs/guide.md`)

- Update "Auto-save" note to reflect versioned file creation

### README (`README.md`)

- Update skills table output column to `wireframes-v{N}.md` and `test-results-v{N}.md`
