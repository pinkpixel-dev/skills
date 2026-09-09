---
name: project-context
version: 1.0.0
description: |
  Read and maintain a project's durable context files: OVERVIEW.md (how the
  project works now), MEMORY.md (decisions and rejected alternatives), and
  ERRORS.md (failed approaches worth remembering). Use at the start of a
  session, before changing an existing design, before debugging something that
  looks familiar, and after finishing work that made one of those files wrong.
  Also use when the user says "log this decision", "add this to memory",
  "write this up in ERRORS", "update the overview", "what did we decide about
  X", "did we try this before", or asks to set these files up in a new project.
license: Apache-2.0
compatibility: claude-code cursor codex gemini-cli opencode
---

# Project Context: Read Before You Change, Write After You Learn

A project carries three kinds of knowledge that code does not hold on its own:

| File | Question it answers | Tense |
|---|---|---|
| `OVERVIEW.md` | How does this project work right now? | Present |
| `MEMORY.md` | Why is it built this way, and what did we turn down? | Past, dated |
| `ERRORS.md` | What already failed, and what worked instead? | Past, dated |

All three live in `/DOCS`. `README.md` and `CHANGELOG.md` stay at the repository root.

The point of these files is to stop the same conversation from happening twice. An agent that reads them does not re-propose a rejected design or re-debug a solved problem. An agent that writes to them leaves the next session in better shape than it found it.

They only work if they stay small enough to trust. Most of this skill is about what **not** to write.

## Read Phase

Read before you change code, not after you break something.

### What to read, and when

| Situation | Read |
|---|---|
| Starting a session in an unfamiliar repository | `OVERVIEW.md` in full |
| About to change existing behavior, structure, or a data model | `MEMORY.md`, filtered |
| About to propose an alternative to something already built | `MEMORY.md`, filtered |
| Debugging, or picking an approach to a hard problem | `ERRORS.md`, filtered |
| Touching tests, build config, emulators, or CI | `ERRORS.md`, filtered |
| Answering "why is it like this?" | `MEMORY.md` |
| Answering "what does this do?" | `OVERVIEW.md` |

### Filter, do not dump

These files grow. A real `MEMORY.md` on a project six months in can pass 700 lines, and reading all of it to answer one question wastes the context you need for the actual work.

Read the headings first, then read only the entries that match:

```bash
grep -n "^#\{2,3\} " DOCS/MEMORY.md
grep -in "reminder\|push\|cron" DOCS/MEMORY.md
sed -n '281,300p' DOCS/MEMORY.md
```

Entry titles are written to be greppable for exactly this reason. Read `OVERVIEW.md` in full the first time, because it is the map. After that, grep it too.

### When a file contradicts the code

The code wins as a description of what happens. The file wins as a description of what was intended. If they disagree, say so out loud before you change anything, then fix the file as part of the work.

### Never quietly reverse a logged decision

If the task asks for something `MEMORY.md` already rejected, stop and say which entry covers it and what its stated reason was. The user may still want the change, and reasons expire. But the reversal has to be deliberate, and it needs a new entry recording why the old reason no longer holds.

## Write Phase

Write after the work is done and verified, not while you are still guessing.

### The qualification bar

Ask one question per file. If the answer is no, write nothing.

**MEMORY.md:** Would a competent contributor, seeing only the code, plausibly change this back without knowing what it cost?

**ERRORS.md:** Would this waste more than an hour of someone's time again?

**OVERVIEW.md:** Did this change make something the file currently says untrue or incomplete?

### What does not qualify

These are the four ways the files rot:

- **Turning `MEMORY.md` into a changelog.** "Added the reminders page" is a changelog line. It has no decision, no reasoning, and no rejected alternative.
- **Turning `ERRORS.md` into a bug tracker.** A bug you found and fixed in ten minutes is not a lesson. It is a commit.
- **Turning `OVERVIEW.md` into a history.** "We used to store this in Redis, then moved to SQLite" belongs in `MEMORY.md`. `OVERVIEW.md` says where it lives now.
- **Logging routine implementation.** Naming a variable, picking a loop, splitting a component that had to be split. There was no fork in the road, so there is nothing to record.

When in doubt, leave it out. A short file that people read beats a long file that people skip.

### Dates

Run `date` before writing a dated entry. Do not guess, and do not reuse a date you saw earlier in the conversation.

Use absolute dates in `YYYY-MM-DD` form as `## ` section headings. Never write "last week", "recently", or "in the previous session" inside an entry. Those stop meaning anything within a month.

If a section for today's date already exists, add to it instead of creating a second one.

### Ordering

Check the existing file and match it. The examples in this repository run oldest first. Newest first also works. What breaks a file is mixing the two, which happens when an agent appends without looking.

### Entry formats

Keep the exact field labels. They are what makes the files greppable and scannable.

`MEMORY.md`:

```md
### Decision: <short imperative statement of what was decided>

What was decided: <one or two sentences, specific, naming real files or routes>

Why: <the reason that would otherwise be lost>

Rejected: <the alternative, and what was wrong with it>
```

`ERRORS.md`:

```md
### Note: <short statement of the trap, not the symptom>

What did not work: <the approach and the actual observed failure>

What worked instead: <the fix, specific enough to repeat>

Note for next time: <the general lesson, one sentence>
```

Detailed rules, quality bars, and worked examples for each file:

- `references/memory.md`
- `references/errors.md`
- `references/overview.md`
- `references/examples.md` for side-by-side good and bad entries

### Writing style

These files are read under pressure by someone who is already confused. Write accordingly.

- Name real files, routes, functions, and thresholds. `getOrCreateCategory` in `src/lib/notes/category-service.ts` is useful. "the category logic" is not.
- Include the number that matters: the timeout, the similarity threshold, the version you pinned.
- Say what actually happened, not what usually happens.
- Plain language, active voice, short sentences.
- No em dashes. No filler adjectives. No "seamless", "robust", "comprehensive", "leverage".
- Do not claim you verified something you inferred.

## Bootstrapping A Project

When a project has none of these files, do not invent content for them.

1. Create `/DOCS` if it does not exist.
2. Copy `templates/OVERVIEW.md`, `templates/MEMORY.md`, and `templates/ERRORS.md` into it.
3. Fill in `OVERVIEW.md` from what the code actually shows: stack, main flow, structure, data model, routes, commands, environment, current limits. Leave a `TODO` marker anywhere you would have to guess.
4. Leave `MEMORY.md` and `ERRORS.md` empty apart from their headers. They fill up from real work.

Backfilling `MEMORY.md` with decisions you reconstructed after the fact produces confident, wrong history. If the user wants past decisions captured, ask them what they remember and write down what they say, not what you inferred.

## Session Checklist

Start of session, when prior context could matter:

- [ ] `OVERVIEW.md` read, or grepped for the area being touched
- [ ] `MEMORY.md` checked for decisions covering this area
- [ ] `ERRORS.md` checked for prior attempts at this problem

End of a task:

- [ ] Did anything in `OVERVIEW.md` become untrue? Fix it.
- [ ] Was there a real fork in the road with a rejected option? Log it in `MEMORY.md`.
- [ ] Did anything take more than two attempts or have a surprising cause? Log it in `ERRORS.md`.
- [ ] `date` run before writing any dated entry.
- [ ] Nothing logged that is really a changelog line, a fixed bug, or routine implementation.
