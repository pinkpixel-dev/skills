---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.

The handoff should be concise but actionable. Preserve the information needed to continue the work without requiring the next agent to reconstruct the conversation.

## Resume here

Begin the document with a short "Resume here" section that tells the incoming agent:

* What the current work is and its intended outcome.
* Which documents or files should be read first.
* The specific task to continue with.
* Any important instructions or constraints that must not be overlooked.
* Any blockers or decisions that must be resolved before proceeding.

## Task status

Include a "task status" section that clearly distinguishes completed, in-progress, blocked, and not-started work. For each relevant task, capture:

* **Task:** What the task is and its intended outcome.
* **Status:** Completed, in progress, blocked, or not started.
* **Completed work:** What has been accomplished so far and how it was done, including important implementation decisions, commands, tools, or approaches when relevant.
* **Incomplete work:** What is unfinished, blocked, or still needs verification.
* **Remaining work:** What is left to do and the planned approach for completing it.
* **Next action:** The specific next step the incoming agent should take.

Keep the task list accurate to the current conversation. Do not mark work as completed unless it was actually completed, and do not invent plans or implementation details. If a plan is not yet established, say so.

## Planning documents and roadmaps

Include a "planning documents and roadmaps" section listing the locations of any planning documents, roadmaps, specs, ADRs, or other project documents relevant to the current work or the next session.

Include their paths or URLs and a brief description of what each contains. Prioritise documents the next agent should read before continuing. If a relevant document is mentioned but its location is unknown, say so rather than inventing a path.

## Skills used or requested

Include a "skills used or requested" section listing any skills the user explicitly requested during this session and any skills actually used.

For each, include the skill name, location if known, and its purpose. Distinguish skills that were **requested**, **used**, or both. Do not claim a skill was used merely because it was mentioned or recommended.

## Suggested skills

Include a "suggested skills" section naming which skills the next agent should call the Skill tool for, and briefly explain why each would be useful for the remaining work.

Keep this separate from skills already used or requested. Do not invent skill names or locations.

## User instructions and constraints

Preserve any session-specific instructions, preferences, or constraints that could affect how the next agent should continue.

Examples include requirements about implementation approach, technologies, dependencies, files that should not be changed, UI or behavior that must be preserved, testing expectations, and scope limitations.

Distinguish explicit user instructions from decisions or assumptions made by the agent.

## Decisions and rationale

Summarise important decisions made during the session, especially when alternatives were considered.

Include the chosen approach and the reason for it when known. Reference an existing ADR, plan, or other artifact instead of duplicating its contents.

Do not present an unresolved discussion as a final decision.

## Current working state

When known, include:

* The relevant working directory and branch.
* Important files created or modified.
* Whether there are uncommitted changes.
* Any running processes or development servers relevant to continuing.
* The current implementation state.

Do not invent repository state or claim to have inspected files, branches, or processes that were not actually checked.

## Verification and known issues

Record what was actually tested or verified, what passed, what failed, and what has not yet been tested.

Include relevant commands and results when useful. Distinguish implemented work from verified work, and note any known bugs, regressions, or unresolved errors.

## Open questions and blockers

List unresolved questions, decisions needed from the user, external dependencies, and blockers.

For each, explain what is needed to move forward. Do not treat ordinary remaining work as a blocker.

## Artifact references

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

For task status, provide a concise summary and point to the relevant artifact for details.

## Privacy and accuracy

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

Do not invent file paths, skill names, decisions, completed work, test results, or plans. If something is unknown or was not verified, say so.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the document accordingly.
