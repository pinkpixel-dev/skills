---
name: pickup
description: Find and read the latest relevant handoff document so the current session can continue previous work.
argument-hint: "Optional project or task to pick up"
disable-model-invocation: true
---

Find and read the most recent relevant handoff document created by the `handoff` skill.

The handoff is stored in the temporary directory of the user's OS, not the current workspace.

If the user passed arguments, use them to identify the project or task they want to resume. Otherwise, use the current working directory and available session context to identify the relevant handoff.

If multiple handoff documents exist, prefer the most recent one that matches the current project or requested task. Do not select an unrelated handoff merely because it is newer. If the correct handoff cannot be determined reliably, ask the user which one to use.

Read the selected handoff document in full. Use its **Resume here** section to identify the next action, and consult the referenced planning documents, roadmaps, and other artifacts as needed.

Preserve the instructions, constraints, decisions, and task status recorded in the handoff. Do not assume that incomplete work has been completed or that previously completed work needs to be redone.

Briefly tell the user which handoff was loaded and what task is being resumed, then continue with the next action described in the handoff.

Do not modify or delete the handoff document.
