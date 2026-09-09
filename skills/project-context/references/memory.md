# MEMORY.md

The decision log. It exists so nobody has to re-argue a settled question, and so a future contributor can tell the difference between a deliberate constraint and an accident.

## What belongs here

An entry qualifies when all three are true:

1. A real fork in the road existed. At least one other option was on the table.
2. The reason is not visible in the code. Reading the implementation would not reveal it.
3. Reversing it later without knowing the reason would cost something.

Typical qualifying decisions:

- Ordering that protects the user's data, like saving raw input before optional enrichment runs
- Picking one library, service, or hosting target over a named alternative
- Deliberately not building something, and the conditions that would change that
- A threshold or limit calibrated against real data
- Scope boundaries, like keeping a feature single-level instead of nested
- A destructive-versus-reversible tradeoff, like soft delete instead of hard delete
- Pinning a dependency version to work around a specific bug

## What does not belong here

- Feature announcements. That is `CHANGELOG.md`.
- Planned work. That is `ROADMAP.md`.
- How something currently works. That is `OVERVIEW.md`.
- A bug and its fix, unless the fix locked in a design constraint.
- Naming, formatting, file splits, and other choices with no rejected alternative.
- Anything you inferred rather than watched happen.

## Structure

```md
# Memory

## 2026-08-04

### Decision: Save bookmarks before metadata extraction

What was decided: A submitted URL is saved as a bookmark before title, description, favicon, or site metadata is fetched.

Why: Saving the bookmark is the user's primary action. A slow, blocked, or malformed remote website should not cause the user to lose the URL they were trying to save.

Rejected: Fetching metadata first and only creating the bookmark after extraction succeeds. That makes a secondary network operation part of the critical save path.
```

Date headings are `## YYYY-MM-DD`. Entry headings are `### Decision: ` followed by a statement of what was decided, not a topic. "Decision: Keep collections single-level" is greppable. "Decision: Collections" is not.

Several decisions on the same day share one date heading.

## Field rules

**What was decided.** Present tense, specific, and concrete enough to check against the code. Name the route, file, function, table, or field. If a number decides the behavior, put the number here.

**Why.** The reason that the code cannot show. Usually a user-facing consequence, a cost, or a constraint from outside the codebase. One or two sentences.

**Rejected.** Name the alternative and say what was wrong with it. This field is what stops the decision from being reopened next month. An entry with no `Rejected:` line is usually not a decision, it is a note.

You can have more than one `Rejected:` line when several options were considered.

## Optional fields

Add these only when they carry real information:

- `Revisit when:` the concrete condition that should reopen the decision. Useful for "not yet" decisions.
- `Supersedes:` the date and title of the entry this replaces.

## Reversing a decision

Do not edit or delete the old entry. Write a new one on today's date that names the old decision and says what changed:

```md
### Decision: Move search to Meilisearch

What was decided: Search now runs through Meilisearch instead of database queries.

Why: The vault passed 40,000 notes and multi-term queries were taking over two seconds. The original reason for staying database-backed was scale, and that reason expired.

Rejected: Adding more indexes. Tried it first, and it helped single-term queries only.

Supersedes: 2026-08-29, "Keep search database-backed for now".
```

The old entry stays. It is the record of what was true then, and the reasoning in it is often still worth reading.

## Session summaries

Optional, and only if the project actually uses them. When the user says the session is ending, a short summary can go at the end of `MEMORY.md`:

```md
### Session Summary: 2026-08-29

Worked on:
- Search filtering
- Archive behavior

Completed:
- Added archived-only search mode
- Added tests for restore behavior

In progress:
- Search result highlighting

Decisions made:
- Keep search database-backed for now

Next session priorities:
- Finish highlighting
- Check mobile search layout
```

Keep them short. A summary that lists every file touched is a `git log` with extra steps.
