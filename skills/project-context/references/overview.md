# OVERVIEW.md

The living technical reference. It answers "how does this project work right now?" for a person or an agent who has never seen the code.

Present tense only. If a sentence contains "used to", "we changed", "previously", or "as of version 2", it belongs in `MEMORY.md` or `CHANGELOG.md` instead.

## Who it is for

Someone about to make their first change. They need the mental model, not the source. Write what the code cannot tell them quickly: the flow, the invariants, the boundaries, and the rules that are enforced by convention rather than by types.

## Sections

Use the ones the project needs. Order roughly like this:

| Section | What goes in it |
|---|---|
| Opening | One paragraph: what the project is and what it is for |
| Stack | Frameworks, database, hosting, notable services, test tools |
| Core flow | The main path through the system, numbered |
| Project structure | A directory tree, plus where documentation lives |
| Data model | Tables or collections and their important fields |
| Auth | How identity works and what must always be scoped |
| API routes | Method, path, what it accepts, what it returns |
| App routes | Pages and what each one shows |
| Important commands | The actual commands, in a code block |
| Environment | Variable names, with a note on which are required |
| Current limits | What the project does not do yet |

A small utility might only need the opening, stack, structure, and commands. Keep the file proportional to the project.

## The rules that matter most

Most of the value in this file is in the invariants. These are the sentences that stop someone from breaking something silently.

Write them plainly, near the flow they govern:

> The raw URL should always be saved before optional metadata processing begins. Metadata failures must not cause the bookmark itself to be lost.

> Every bookmark, collection, and tag query must be scoped by `user_id`. Cross-account access is considered a security bug.

> Do not deploy without explicit confirmation.

## Keeping it accurate

Update `OVERVIEW.md` when a completed change made something in it wrong or incomplete. That means:

- A route was added, removed, or changed its contract
- A field, table, or index changed
- A step in the core flow moved, or a new step appeared
- A command changed, or a new one is now required
- An environment variable was added or renamed
- A stated limit is no longer true
- An invariant changed

Do not update it for renames inside a module, refactors that preserve behavior, styling work, or comment edits. Nothing in the file became wrong, so nothing needs to change.

## Editing style

Edit in place. Rewrite the sentence that is now wrong rather than appending a correction after it. A file that accumulates "note: this changed in July" lines stops being a description of the present.

Keep paragraphs tight and specific. Name real paths, real function names, real thresholds. `src/lib/notes/category-similarity.ts` reuses an existing category at or above 0.70 cosine similarity is useful. "There is some similarity checking" is not.

When behavior has a reason worth recording, put the behavior here and the reason in `MEMORY.md`. Do not duplicate the full argument in both files.

## Pointing at the other docs

Include a short block naming the other context files, so a new reader knows where the rest of the knowledge lives:

```md
Project documentation lives in `/DOCS`.

- `/DOCS/OVERVIEW.md`: current architecture and behavior
- `/DOCS/MEMORY.md`: significant decisions and rejected alternatives
- `/DOCS/ERRORS.md`: difficult bugs, failed approaches, and reusable fixes
- `/DOCS/ROADMAP.md`: planned work
- `README.md`: user-facing project documentation
- `CHANGELOG.md`: release history
```
