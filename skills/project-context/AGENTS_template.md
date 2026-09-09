# AGENTS.md

## Important Rules

1. Ask, don't assume. If something is unclear, ask before writing code. Never make silent assumptions about intent, architecture, or requirements.
2. Simplest solution first. Implement the simplest thing that could work. Do not add abstractions or flexibility that were not explicitly requested.
3. Don't touch unrelated code. If a file or function is not directly part of the current task, do not modify it just because it could be improved.
4. Flag uncertainty explicitly. If you are not confident about an approach or technical detail, say so before proceeding.
5. Do not change files unless you understand the project structure and intent.
6. Use a direct, friendly, engaged tone.
7. Update documentation only when the completed task actually changes documented behavior, usage, setup, architecture, public-facing information, release history, or other documented facts.
8. Use available tools, documentation, project files, and other reliable sources before guessing.
9. Check current framework and API documentation when versions, packages, or behavior may have changed.
10. Prefer modern, maintainable solutions over outdated patterns.
11. Do not leave mocks, placeholders, stubs, or temporary implementations in finished work unless explicitly requested.
12. Keep large codebases modular. Application/source files in a normal multi-file project should usually stay reasonably sized when splitting them improves clarity, maintenance, reuse, or separation of concerns. Do not refactor working code solely to satisfy an arbitrary line count.

    This guideline does not apply when the task intentionally calls for a small fixed-file structure or self-contained artifact, such as CodePen projects, single-file demos, prototypes, generated files, configuration files, data files, documentation, or scripts that are clearer as one file.

13. Write useful tests when the change warrants them. Do not run large test suites after every tiny edit.
14. Do not run browser automation or end-to-end checks by default. Use them for initial scaffolds, explicit requests, or changes that genuinely require browser-only verification.
15. Design and implement with mobile, keyboard, touch, mouse, and accessibility in mind.
16. If the repository has no license and the project owner has specified a preferred license, create that license. Otherwise, ask before choosing one.

## Design Preferences

Use this section to describe the project's default visual direction.

Example:

- Prefer a clean, minimal interface.
- Avoid unnecessary decoration.
- Use accessible contrast and obvious interaction states.
- Keep layouts responsive.
- Do not add visual effects that were not requested.
- Reuse the existing design system before introducing new patterns.

Replace these examples with the actual project's design rules.

## Communication Preferences

Be direct, useful, and clear.

When editing code:

- Preserve working prompts, copy, and logic unless the requested change requires altering them.
- Do not randomly improve unrelated sections.
- Explain important tradeoffs.
- Mention uncertainty instead of pretending to know.
- Match response length to task complexity.

When debugging:

1. Identify the likely root cause.
2. Explain the fix plainly.
3. Make the smallest relevant change.
4. Mention tradeoffs or follow-up checks.

When building features:

1. Keep the MVP practical.
2. Suggest enhancements only when they are genuinely useful.
3. Favor maintainable structure over clever complexity.
4. Do not add features that were not requested.

## Default Session Behavior

Before changing code:

1. Read the relevant project documentation.
2. Understand the existing structure.
3. Check `/DOCS/MEMORY.md` and `/DOCS/ERRORS.md` for prior decisions and failed approaches that affect this task.
4. Inspect the relevant implementation before proposing changes.

If the task changes architecture, project behavior, a significant workflow, or an important implementation decision, update the appropriate documentation after the work is complete.

If something is unclear and the ambiguity could materially change the implementation, ask before proceeding.

## Writing Style

Use the `clear-writing` skill for documentation, guides, release notes, error messages, commit bodies, agent instructions, and any prose written on behalf of the project owner. It covers both halves of the job: writing that a tired reader cannot misread, and prose that does not read as machine-generated.

The skill classifies each passage first, because the rules differ. Instructional text such as setup steps and error messages gets hard sentence limits and one word per concept. Voiced prose such as a README opening or a release announcement gets varied rhythm and a real voice. A README holds both.

Beyond the skill, match the voice defined here instead of defaulting to generic AI writing.

Customize this section with the owner's preferences.

Suggested defaults:

- Clear
- Human
- Direct
- Technically credible
- Not stiff or corporate
- No unnecessary hype
- No filler
- Preserve the author's meaning
- Prefer straightforward language over buzzwords

If the project has specific banned words, punctuation preferences, terminology, or tone rules, list them here.

## Documentation

### Documentation Location

Recommended structure:

- `README.md` remains at the repository root.
- `CHANGELOG.md` remains at the repository root.
- All other project documentation lives in `/DOCS`.

This can include:

- `OVERVIEW.md`
- `MEMORY.md`
- `ERRORS.md`
- `ROADMAP.md`
- `RELEASE.md`
- setup guides
- architecture notes
- troubleshooting docs
- migration notes
- tutorials
- reference docs

When looking for project documentation or reference material, check `/DOCS` before assuming it does not exist.

### Documentation Rules

Three durable context files live in `/DOCS` and each has a separate job:

- `OVERVIEW.md`: how the project works right now
- `MEMORY.md`: significant decisions, reasoning, and rejected alternatives
- `ERRORS.md`: failed approaches and difficult bugs worth remembering

Read them before changing existing behavior, before proposing an alternative to something already built, and before debugging a problem that may have been hit before.

Write to them after the work is done and verified, when a real decision was made or an approach failed in a way that would cost time again. Do not log routine implementation, ordinary fixed bugs, or feature announcements.

Keep `OVERVIEW.md` accurate as the living technical reference. Fix the sentence that became wrong instead of appending a correction after it.

Use the `project-context` skill for entry formats, the bar for what qualifies, and worked examples. Use the `clear-writing` skill for the prose itself.

If the repository uses session summaries, add one to `/DOCS/MEMORY.md` when the owner says the session is ending.

If the project maintains a roadmap, update `/DOCS/ROADMAP.md` only when the direction of the project or planned work actually changes.

## Release Workflow

Customize this section for the repository.

A safe default workflow:

1. Review `git status`.
2. Preserve unrelated work.
3. Confirm no private files or secrets are tracked or staged.
4. Determine whether application/source code changed.
5. Only bump the application version if the project's versioning policy requires it.
6. Update the changelog only when the change belongs in release history.
7. Update release notes and user-facing documentation when needed.
8. Provide a concise release summary and suggested commit message.
9. Do not commit, push, publish, or deploy unless explicitly authorized.

## Versioning

Use semantic versioning if the project follows it:

`MAJOR.MINOR.PATCH`

Suggested interpretation:

- `PATCH`: bug fixes and small backwards-compatible improvements.
- `MINOR`: new backwards-compatible features or capabilities.
- `MAJOR`: breaking changes or destructive migrations.

Do not bump versions for documentation-only changes, comments, formatting, CI configuration, repository housekeeping, or other non-code maintenance unless the repository explicitly follows a different policy.

If one file is the source of truth for the version, document it here.

## Git & GitHub

Customize these rules for the repository.

Recommended defaults:

- Never commit unless explicitly requested.
- Never push unless explicitly requested.
- Never deploy unless explicitly requested.
- Do not rewrite unrelated history.
- Preserve unrelated working-tree changes.
- Before an authorized commit, inspect the exact diff.
- Before an authorized push, confirm repository, branch, remote, and intended changes.

If the repository uses a branch strategy, document it here.

Example:

- `main` is production.
- Feature and fix branches merge into `dev`.
- `dev` is tested before promotion to `main`.

## Destructive Actions

Require explicit confirmation before:

- deleting files
- overwriting important existing code
- dropping database data
- running destructive migrations
- removing dependencies when impact is unclear
- publishing or deploying
- sending external messages
- making irreversible changes

When possible, explain exactly what will be affected before performing the action.

## Dependencies

- Prefer existing dependencies and shared utilities before adding a package.
- Add dependencies only when they improve correctness, maintenance, security, or delivery.
- Prefer current stable releases.
- Do not upgrade unrelated dependencies unless compatibility or security requires it.
- Explain significant additions or upgrades.

## Completion Summary

After a coding task, provide a short summary containing:

- Files changed
- What was modified
- Files intentionally not touched
- Follow-up needed
- Suggested commit message, if useful

Do not claim tests passed unless they were actually run.
Do not claim something was verified if it was only inferred.
