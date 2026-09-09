# Use Cases By Register

STE was built for aircraft maintenance manuals. Its properties (one meaning per word, short sentences, condition-first commands) transfer to any text where misreading has a cost. By the end of Issue 8, 64% of registered STE users were outside aerospace and defense.

Each case names its register, its STE classification where it has one, and the adaptations.

## Error messages and CLI output

Register: instructional, procedural. The highest-value target. An error message is a 2am instruction to a stressed reader.

Pattern: state what happened in simple past, state the cause if known, give the command or condition to fix it.

> **Before:** Oops! Something went wrong while attempting to establish a connection. Please ensure your credentials are properly configured and try again.
>
> **After:** Connection to the database failed. The password for user `app` was not correct. Set `DB_PASSWORD` and connect again.

No "Oops", no "Please ensure", no apology filler.

## Runbooks and standard operating procedures

Register: instructional, procedural, leaning strict. This is STE's home turf. An on-call runbook is a maintenance manual.

- Every step imperative, one instruction per step, conditions first.
- Warnings before the step, command first, risk second.
- The 20-word limit enforced hard. An operator under pager stress reads each sentence once.

## Incident reports and postmortems

Register: instructional, descriptive. Simple past only. A timeline in present perfect ("we have identified...") hides when things happened.

> **Before:** We have identified an issue that may have impacted some users' ability to access the service.
>
> **After:** Between 14:02 and 14:31 UTC, 12% of requests failed. A deploy at 14:00 removed the cache warmup step.

Hedges like "may have impacted" are banned. The report states what is known and says "unknown" for the rest. This reads more honest because it is.

## Commit messages and pull request descriptions

Register: instructional. Imperative subject, descriptive body.

Convention already matches STE: imperative subject line, plain past facts in the body. Apply the substitution table and the 25-word limit to the body. Delete "this PR aims to".

## API changelogs and release notes

Register: mixed. Entries are instructional and descriptive. A release announcement's opening paragraph is voiced prose.

One entry, one change, one sentence where possible. "Breaking:" entries follow the warning pattern, command first: "Update your calls to `v2/users`. The `name` field split into `first_name` and `last_name`."

## Instructions for AI agents: prompts, AGENTS.md, skills

Register: instructional, procedural. A system prompt is a procedure executed by a reader that cannot ask questions, which is the exact reader STE was designed for.

- One instruction per sentence keeps rules independently quotable and hard to half-follow.
- One word, one meaning stops the model from treating "check", "verify", and "validate" as three different operations.
- Condition-first ("If the build fails, stop") beats trailing conditions, which models drop.
- No "should". A model reads "should" as optional. Write "must" or delete the rule.

## Support macros and status-page updates

Register: instructional, descriptive. The 25-word limit applies. Non-native readers are the majority of many user bases.

No "we sincerely apologize for any inconvenience this may have caused". Write: "The API was down for 18 minutes. Uploads made during this time were saved and will process today."

## UI copy and empty states

Register: instructional, procedural, with hard length limits.

Buttons and labels are technical names and are exempt. Body copy follows the rules: "No projects yet. Create a project to start." Nothing else survives at this length anyway.

## Translation and localization prep

Register: instructional, strict.

STE's original purpose was making English readable for non-native maintenance crews, and it doubles as pre-editing for machine translation. One meaning per word plus complete grammar (articles, "that") removes most translation ambiguity. If your docs get localized, this cuts the error rate and the cost.

## README files

Register: mixed, and this is the most common place people get it wrong.

The opening paragraph, the "why I made it" section, and any project-status commentary are voiced prose. They need a person's voice, varied rhythm, and first-person opinion. Applying the 20-word cap here produces the flat robotic README that the AI-pattern half exists to prevent.

Installation, usage, configuration, and environment variables are instructional. They get the caps, the imperative, and the condition-first rule.

## Blog posts, social posts, announcements

Register: voiced prose. The STE half does not apply.

Governed by `ai-patterns.md` and the context and voice profiles. Vary sentence length deliberately. Keep first person. Repeat a word when it is the right word, but never rotate synonyms to avoid repeating.

## Where none of this fits

Marketing pages, launch copy, brand writing.

STE deletes persuasion on purpose. The AI-pattern rules still apply, because slop is slop, but do not impose sentence caps or vocabulary discipline. Write those in the owner's voice, then use the instructional rules for the docs the landing page links to.
