# Clear Writing

Clear Writing is an agent skill and Claude plugin designed to write and edit technical copy that is easy to read and free of machine-generated fluff.

It brings two distinct writing disciplines together in one place:

1. **ASD-STE100 Simplified Technical English** for instructional copy (runbooks, documentation, error messages, and agent instructions).
2. **An anti-AI pattern audit** for voiced prose (README openings, blog posts, essays, and release announcements).

Instructional text needs strict structure and predictable sentence length. Voiced prose needs varied rhythm and genuine personality. This skill classifies what you are writing first, then applies the right ruleset.

## Why I made it

Most technical writing suffers from one of two problems.

The first problem is inconsistency in technical documentation. An engineer uses three different verbs for the same action across two paragraphs, stacks modal verbs like "could potentially", and buries critical commands after long explanations. ASD-STE100 solved this decades ago for aerospace maintenance manuals. It keeps instructions unambiguous, especially for tired readers and non-native English speakers.

The second problem is the wave of generic LLM text. Generated drafts tend to settle into a predictable cadence: uniform 15-to-25 word sentences, inflated verbs like "serves as" or "boasts", and empty transitions like "in today's digital landscape" or "delve into".

I built this skill because I wanted a tool that handles both. When I write a setup guide, I want metronomic clarity. When I write an introduction, I want direct human writing that sounds like a real person built the project.

## The Two Registers

Clear Writing classifies text into one of two registers before applying rules:

| Register | Used for | Governed by | Key rules |
|---|---|---|---|
| **Instructional** | Docs, setup guides, runbooks, error messages, API docs, agent instructions | ASD-STE100 rules | 20 words max per procedural sentence, 25 per descriptive sentence. One instruction per sentence. Imperative verbs. Condition first. |
| **Voiced prose** | README intros, blog posts, essays, release narratives | AI pattern catalog | Varied sentence lengths (short fragments mixed with longer lines). First-person voice when natural. No marketing filler or buzzwords. |

Single documents often contain both registers. For example, a README introduction is voiced prose, while its installation and configuration sections are instructional.

## Operating Modes

You can invoke Clear Writing in four modes:

| Mode | What it does | Expected output |
|---|---|---|
| `rewrite` (default) | Fixes existing text | Flagged issues, rewritten text, change summary, and a second-pass audit |
| `write` | Drafts fresh copy from your notes or requirements | Drafted text followed by an audit checklist |
| `detect` | Scans text without changing it | Categorized issues grouped by severity (P0, P1, P2) |
| `edit` | Applies targeted edits directly to a named file | Minimal in-place edits using file tools, followed by a summary |

If you provide text without specifying a mode, the skill defaults to `rewrite`.

## What Both Registers Ban

Certain patterns degrade writing regardless of register:

- **Slop words:** Terms like "delve", "tapestry", "seamless", "robust", "cutting-edge", "game-changing", "plethora", and "testament".
- **Empty filler:** Phrases like "it is important to note that", "at the end of the day", and "in terms of".
- **Hedging:** Stacking modals like "could potentially" or "might possibly".
- **Inflated verbs:** Writing "serves as" or "features" when "is" or "has" works.
- **Em dashes:** Use commas, periods, colons, or parentheses instead.
- **Semicolons in instructions:** Split the thought into two sentences.
- **Latin abbreviations:** Write "for example" instead of "e.g.", "that is" instead of "i.e.", and name items instead of ending with "etc.".
- **Tool leakage:** Unfilled placeholders like `[Your Name]` or residual AI artifacts.
