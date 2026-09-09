# ERRORS.md

The debugging log. It exists so the same trap does not cost a second afternoon.

This is not a bug tracker. Most bugs are found, fixed, committed, and forgotten, which is correct. Only a small fraction earn an entry here.

## What belongs here

An entry qualifies when at least one is true:

1. It took more than two real attempts to solve.
2. The root cause was somewhere other than where the symptom appeared.
3. The behavior is environment-specific and will recur on another machine, another connection, or another runner.
4. A reasonable next approach would fail the same way.

Typical qualifying failures:

- A default that silently does the wrong thing, like `fetch()` with no timeout hanging on a server that accepts the connection and never responds
- Ordering bugs, like normalizing a value after the uniqueness check instead of before it
- Test failures caused by shared state rather than the code under test
- A setting that is connection-scoped or process-scoped and does not carry over, like SQLite foreign-key enforcement in a standalone script
- Toolchain and environment traps: emulator graphics backends, symlinked dependency trees, a hand-started server picking up the real `.env`
- An API whose response shape is not what the documentation implies

## What does not belong here

- Ordinary bugs found and fixed quickly
- Typos, syntax errors, missing imports
- Anything already prevented by a test that now exists, unless the trap can return in a new form
- A rant about a library
- Failures you did not actually reproduce

## Structure

```md
# Errors

## 2026-08-12

### Note: URL normalization must happen before duplicate lookup

What did not work: Querying for an existing bookmark using the raw submitted URL and normalizing only before insert. URLs that differed only by a fragment or removable tracking parameters passed the duplicate check and were inserted twice.

What worked instead: Normalize first, then use `normalized_url` for both lookup and insert.

Note for next time: Validation and normalization order matters. Any uniqueness rule based on transformed data must use the transformed value before the existence check.
```

Date headings are `## YYYY-MM-DD`. Entry headings are `### Note: ` followed by the trap, stated as a fact.

Title the trap, not the symptom. "Note: vector_top_k has no distance column" is findable by someone hitting it. "Note: search was broken" is not.

## Field rules

**What did not work.** The approach you took and what you actually observed. Include the error text, the file and line, or the specific wrong output. Vague failure descriptions do not help the next reader recognize their own situation.

**What worked instead.** The fix, specific enough to apply without rediscovering it. Name functions, flags, config keys, and commands exactly. If the fix has a prerequisite, say so.

**Note for next time.** One sentence, generalized past this instance. This is the part that transfers. "Remote metadata is untrusted network work, so every fetch path needs an explicit timeout" is worth more than the timeout value itself.

## Traps that bite twice

When something recurs, do not open a second entry. Update the existing one and say so in the title or the note:

```md
### Note: vector_top_k has no distance column (bit us twice)
```

A repeat is a signal that the note was not findable enough. Fix the title while you are there.

## Ruling out a regression

When a failure might be pre-existing rather than caused by your change, prove it before you write anything down. Re-run the failing test alone. If it passes, run the full suite against a clean baseline checkout or worktree.

That result is worth an entry, because the next person will assume a regression too:

```md
### Note: The e2e suite has a pre-existing flaky failure in full serial runs

What did not work: Treating a single full-suite failure as a regression. Three consecutive runs each failed one test, but not the same one, and every one of them passed when run alone.

What worked instead: A worktree at the last commit, with no new work in it, failed the same way. Note that the worktree needs its `node_modules` on the same filesystem, because a symlink to the main checkout makes the bundler panic.

Note for next time: The suite runs serially against one shared database with no retries, so ordering sensitivity shows up as a moving failure. Re-run the failing test alone, then check a baseline worktree before blaming a change.
```
