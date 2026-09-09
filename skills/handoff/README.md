# Handoff

Handoff is an agent skill and Claude plugin that compacts your active session into a structured handoff document, stored in your operating system temporary directory.

It preserves your working state, task progress, and technical decisions so a fresh agent can continue your work without losing context.

## Why I made it

Long agent sessions get messy.

As a conversation stretches across hours, context windows fill up with tool outputs, abandoned approaches, and conversational noise. Reasoning gets sluggish, costs climb, or you decide to switch models or start a fresh terminal.

Starting a fresh session usually comes with an annoying penalty. You either spend ten minutes typing out a manual status update, or you let the new agent guess where you left off. When that happens, the incoming agent often repeats mistakes you already fixed, refactors files you told it not to touch, or misinterprets your architecture.

I built `handoff` to create a clean exit ramp. When you wrap up a session or hit a natural stopping point, `handoff` writes an honest snapshot of where things stand. It records what actually works, what remains broken, and exactly what to do next. Because it saves to your OS temporary directory, it never pollutes your git history with temporary markdown notes.

## What It Captures

A handoff document contains concrete sections that an incoming agent needs:

| Section | What it records | Why it matters |
|---|---|---|
| **Resume here** | The specific next task, entry files to read first, and hard constraints | Gives the next agent an immediate starting point without re-analyzing the whole repo |
| **Task status** | Completed, in-progress, blocked, and not-started work | Prevents the new agent from redoing finished tasks or assuming incomplete work is done |
| **Planning documents** | Paths to relevant specs, roadmaps, and architecture records | Points the agent to source-of-truth documents instead of guessing intent |
| **Skills used and suggested** | Tools called in the current session and recommendations for next steps | Keeps helpful workflows and sub-skills active across sessions |
| **Instructions and constraints** | User preferences, boundaries, and files that must not be changed | Preserves your rules and implementation requirements |
| **Decisions and rationale** | Chosen technical approaches and rejected alternatives | Stops the next agent from proposing approaches you already considered and discarded |
| **Current working state** | Active git branch, modified files, and running local processes | Provides grounded environment context before the agent runs any commands |
| **Verification and known issues** | Tests that passed, tests that failed, and known regressions | Separates verified code from unverified changes |
| **Open questions and blockers** | Decisions that require user confirmation or external dependencies | Identifies items that need human input before the agent can move forward |

## How to Use It

### In Claude Code

Run the skill at the end of a session or before clearing context:

```shell
/handoff:handoff
```

You can also pass an optional hint describing what the next session should focus on:

```shell
/handoff:handoff "implement password reset flow and add unit tests"
```

When you provide a hint, the skill tailors the **Resume here** and **Task status** sections to prioritize that objective.

### In Other Agents

If you use Codex, Antigravity, or custom agent setups, invoke the skill through your agent interface:

```text
Use the handoff skill to summarize this session for the next agent. Next focus: refactor database queries.
```

## Storage and Privacy

Handoff files follow strict storage and privacy boundaries:

- **OS Temporary Directory:** Saved to `/tmp` on Linux and macOS, or `%TEMP%` on Windows. Files stay outside your project directory and do not clutter your git repository.
- **Redaction:** Secrets, API keys, passwords, and sensitive tokens are automatically redacted.
- **Honest Records:** The skill records what was actually checked and verified. If a test was not run, or a file path is unknown, the document says so directly.

Pair `handoff` with the [`pickup`](../pickup/README.md) skill to load your saved state in your next session.
