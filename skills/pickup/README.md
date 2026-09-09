# Pickup

Pickup is an agent skill and Claude plugin that finds and loads the most recent relevant handoff document created by `handoff`, allowing a fresh agent session to resume work immediately.

It reads the saved project state, identifies your next task, and continues without requiring you to re-explain context.

## Why I made it

Writing a good handoff document only solves half of the problem.

When you open a fresh terminal or switch agents, you still have to tell the new agent where the file lives, ask it to read the notes, and make sure it does not ignore your constraints. If you forget to point it to the handoff, the agent starts from scratch anyway.

I built `pickup` to close that loop. Instead of manually copying paths or summarizing your goals in chat, you run one command: `/pickup:pickup`. The incoming agent looks up the right handoff file in your temporary directory, reads the working state, and immediately takes the next step.

## How It Works

When invoked, `pickup` follows a structured sequence:

1. **Locate:** Searches the operating system temporary directory for handoff files created by the `handoff` skill.
2. **Match:** Identifies the correct document based on your active working directory, git branch, or an optional task name you provide. If multiple files match, it chooses the newest relevant document. If the match is ambiguous, it asks you which one to load instead of guessing.
3. **Inspect:** Reads the handoff document in full. It uses the **Resume here** section to determine the next action and reviews recorded constraints, decisions, and unverified work.
4. **Report and Execute:** Tells you which handoff file was loaded and what task is resuming, then continues execution. It preserves recorded decisions and does not redo tasks marked as complete.

## How to Use It

### In Claude Code

Start your fresh session and run:

```shell
/pickup:pickup
```

If you have multiple tasks or projects saved, pass an optional keyword to help match the right document:

```shell
/pickup:pickup "auth-flow"
```

### In Other Agents

If you use Codex, Antigravity, or custom agent setups, call the skill directly:

```text
Use the pickup skill to find our latest handoff document and continue our previous work.
```

## The Workflow Loop

`handoff` and `pickup` work together to create a reliable handover lifecycle:

1. **Active Session:** You work on features, debug issues, or make architectural decisions.
2. **End of Session:** Run `/handoff:handoff` before closing your session. A structured snapshot is saved to your OS temporary directory.
3. **Fresh Session:** Open a clean session in your project and run `/pickup:pickup`.
4. **Immediate Progress:** The new agent loads the snapshot, reads the next steps, and picks up exactly where you stopped.

Pair `pickup` with the [`handoff`](../handoff/README.md) skill to maintain continuity across models, context resets, and development sessions.
