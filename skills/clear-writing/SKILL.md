---
name: clear-writing
version: 1.0.0
description: |
  Write and edit text that is clear to a tired reader and does not read as
  machine-generated. Combines ASD-STE100 Simplified Technical English for
  instructional text with an AI-pattern audit for prose that carries a voice.
  Use for documentation, READMEs, setup guides, runbooks, error messages,
  release notes, incident reports, commit messages, agent instructions, blog
  posts, and social posts. Also use when the user says "remove AI-isms",
  "make this sound less like AI", "de-slop", "clean up this writing", "audit
  this for AI tells", "STE", "Simplified Technical English", "make this
  readable", or "write for non-native readers".
license: MIT
compatibility: claude-code cursor codex gemini-cli opencode
metadata:
  merged_from: simple-english 1.0.0, avoid-ai-writing 3.15.0
  standard: ASD-STE100 Issue 9 (2025-01-15)
---

# Clear Writing

Two jobs, one skill.

**Write clearly.** Text that a tired reader, often not a native English speaker, cannot misread on the first pass. The rules come from ASD-STE100 Simplified Technical English, the controlled language aerospace manufacturers use for maintenance manuals.

**Remove the machine.** Text that does not read as LLM output. Not because AI writing is forbidden, but because the patterns are vague, padded, and unfalsifiable. Cutting them makes writing better whoever produced it.

These two jobs mostly agree. Both hate filler, hedging, inflated verbs, and vague claims. They disagree about exactly one thing, and Step 1 exists to settle it.

## Step 1: Classify The Register

Do this before anything else. It decides which ruleset governs.

| | **Instructional** | **Voiced prose** |
|---|---|---|
| Reader is | executing something | being informed or persuaded |
| Examples | docs, setup guides, runbooks, error messages, CLI output, API reference, parameter docs, UI copy, troubleshooting steps, agent instructions and prompts, incident reports, commit bodies, support macros | README opening and "why I made it", blog posts, social posts, announcements, release note narrative, essays, personal writing |
| Governed by | `references/ste-rules.md` | `references/ai-patterns.md` |
| Rhythm | Uniform. Predictable is correct. | Varied. Uniform is the tell. |

One document holds both. A README's opening paragraph is voiced prose. Its install steps are instructional. Classify per section, not per file.

### The one real conflict

| Question | Instructional | Voiced prose |
|---|---|---|
| Sentence length | Hard caps: 20 words procedural, 25 descriptive | Mix 3-word fragments with 25-word sentences. Uniformity in the 15 to 25 band is the strongest AI signal there is. |
| Same word repeated | Repeat it. One concept, one word. | Repeat when it is the right word, vary when variation is natural. Never rotate synonyms to avoid repeating. |
| Sentence shape | Parallel and predictable | Deliberately uneven. Fragments allowed. Questions allowed. |
| Personality | None. It is not the reader's problem. | Required where the piece is supposed to have a voice. First person, stated opinions, reactions. |

Both are right for their own register. A runbook step read at 2am should be metronomic. A README intro that reads metronomic sounds like a bot wrote it.

### Inside instructional, classify again

STE splits instructional text one level further, and every sentence-level rule depends on it:

| | Procedural | Descriptive |
|---|---|---|
| Purpose | Tell the reader what to do | Explain what a thing is or does |
| Verb form | Imperative: "Install the pump." | Simple present, past, or future |
| Sentence limit | 20 words (Rule 5.1) | 25 words (Rule 6.3) |
| Unit rule | One instruction per sentence (5.2) | One topic per paragraph (6.5), six sentences maximum (6.6) |

Do not mix them in one passage. A "Getting started" section is procedural. An "Architecture" section is descriptive. A note inside a procedure is descriptive: 25 words, no imperative.

## Step 2: Pick The Mode

| Mode | When | What you return |
|---|---|---|
| **write** | Producing new text | The text, then the self-check |
| **rewrite** (default on existing text) | The user wants it fixed | Issues, rewritten version, what changed, second-pass audit |
| **detect** | "flag only", "audit", "scan", "what's wrong with this" | Issues grouped by severity, plus an assessment of which are judgment calls. No rewriting. |
| **edit** | The user names a file and wants it fixed in place | Minimal targeted edits with the Edit tool, then a short report. Not the full file. |

Default to rewrite when handed existing text and given no instruction. Full output formats are in `references/checklist.md`.

In **edit** mode, change the flagged spans and nothing else. Leave passages that are already human alone. Never rewrite quoted material, code blocks, or text attributed to someone else. On a large file, confirm which section to clean first. Re-read the file afterward and confirm the patterns are resolved.

**Iterating.** Rewrite mode already runs one corrective second pass, and that pass counts as pass two. Cap at two passes. A third costs a full regeneration and rarely finds anything.

## Step 3: Fix Your Vocabulary Before Drafting

This one step prevents more problems than any rule below it.

Pick ONE verb for the check / verify / confirm / validate concept. Pick ONE noun for config / settings / options. Use no other word for those concepts anywhere in the document. Same for run / execute / invoke / launch, show / display / render, and delete / remove / drop.

In instructional text this is Rule 1.11, and it is mandatory. In voiced prose it is the cure for synonym cycling, which is the habit of rotating "developers, engineers, practitioners, builders" through one paragraph to avoid repeating a word. Human writers repeat the clearest word.

## What Both Registers Ban

These apply everywhere. No register earns them.

**Slop vocabulary.** Full tables in `references/word-tables.md`, tiered by how reliably each word signals machine output. Tier 1 words get replaced on sight. Tier 2 words get flagged when two or more land in one paragraph. Tier 3 words only get flagged at density.

**Filler that carries no fact.** "It is worth noting that", "it's important to", "the reality is that", "in terms of", "at the end of the day". Delete and state the fact.

**Hedging and modal stacking.** "Could potentially", "may eventually", "might ultimately". Each hedge cancels the next and the sentence asserts nothing. Pick one. In instructional text go further and use the modal ladder in `references/ste-rules.md`: only `can`, `will`, and `must` survive. A model reads "should" as optional, and so does a tired human.

**Vague claims where a specific one belongs.** "Experts believe", "studies show", "independent testing confirms", "significantly faster". Name the expert, the study, the benchmark, the number. If you cannot name it, cut the claim rather than dressing it up.

**Inflated verbs for "is" and "has".** "Serves as", "features", "boasts", "presents", "represents". These sound like a press release. Default to `is` and `has` unless a specific verb genuinely adds meaning.

**Em dashes.** Replace with commas, periods, parentheses, or two sentences. This includes headings. Catch both the Unicode em dash and the double-hyphen substitute.

**Semicolons in instructional text.** Rule 8.1. Write two sentences.

**Latin abbreviations.** "e.g." becomes "for example". "i.e." becomes "that is". Delete "etc." and name the items or write "and more".

**Unfilled placeholders and tool leakage.** `[Your Name]`, `2025-XX-XX`, `citeturn0search0`, `utm_source=chatgpt.com`. These are fingerprints, not patterns. Their presence is near-proof that generated text was pasted without cleanup. Strip them whatever else the text looks like.

## Untouchables

Leave these exact, even when they break a vocabulary rule. They are technical names (Rules 1.5 and 8.6).

- Code blocks, inline code, identifiers, CLI commands, flags, file paths
- Quoted error messages and log lines
- Product names, API endpoint names, config keys
- Numbers with units
- Quoted material and text attributed to someone else

Each of these counts as one word against a sentence limit, so a long identifier does not blow your budget.

**Self-reference escape hatch.** When writing about writing patterns, quoted examples of bad writing are exempt. Flag only the author's own prose, never the specimens.

**Preserve a human's rough edges.** When editing someone's casual text, keep their typos, contractions, and odd capitalization. Smoothing those away erases the fingerprint that marks the text as theirs. Over-polishing pushes human writing toward the machine profile, which is the opposite of the job.

## Step 4: Self-Check Before You Deliver

Not optional. Four searches, then read.

1. **Count words** in your three longest sentences. Over the cap in instructional text, split them. Under 15 words in every sentence of voiced prose, vary them.
2. **Search** for: `'ll`, `'re`, `n't`, `has been`, `have been`, `should`, `;`, `e.g.`, `i.e.`, `etc.`, `, making`, `, allowing`, `, enabling`, `—`, `--`. In instructional text every hit outside code is a violation. Contractions are fine in voiced prose and expected in a casual voice.
3. **Search every `if` and `when`.** In instructional text each one stands at the start of its sentence, before the command, with a comma. "Increase the timeout if the network is slow" becomes "If the network is slow, increase the timeout."
4. **Search for the words you did not pick** in Step 3. Replace every hit.

Then read it once as the reader. For voiced prose, read it aloud. If it could be read by a text-to-speech engine without sounding odd, it is too uniform.

Full audit pass, with the severity tiers and the searchable pattern list, is in `references/checklist.md`.

## When To Rewrite Instead Of Patch

If voiced prose has five or more flagged vocabulary hits across several categories, three or more distinct pattern categories triggered, and uniform sentence and paragraph length, patching individual phrases will not fix it. The structure itself is generated. State the core point in one sentence and rebuild from there.

Two writer-side tests that catch this before you start editing:

**Paragraph reshuffle.** Can you swap two body paragraphs without breaking the piece? If order does not matter, you have a list of points, not an argument.

**Treadmill test.** For each paragraph, name the one fact or turn it contributes. If you cannot, cut it. If you could cut 40% and lose nothing, the piece restates its premise instead of advancing it.

## Limits

This skill is for technical facts, instructions, and honest prose. Do not apply the STE half to marketing copy, launch posts, or brand writing. It deletes persuasion by design. When someone asks for it on marketing text, say so and offer it for the docs the landing page links to.

The AI-pattern half is a writing-quality tool, not a verdict. The patterns are more common in LLM output, but humans on deadline, in unfamiliar genres, or writing in a second language produce the same shapes. Detector audits have found false-positive rates above 60% on non-native English writers (Liang et al., Stanford, *Patterns* 2023) and misclassification above 70% on open-source detectors (Jabarian and Imas, BFI Working Paper 2025-116, 2025). Signals, not proof. Never make them the sole basis for a decision about a person.

This is an unofficial aid. It is not affiliated with or endorsed by ASD or STEMG, and no tool can guarantee STE compliance. ASD-STE100 is a registered trademark of ASD. The official standard is a free download at asd-ste100.org. Full compliance needs the official dictionary, which is copyrighted and not reproduced here.

## References

| File | What is in it |
|---|---|
| `references/ste-rules.md` | The 53-rule catalog, the modal ladder, part-of-speech rulings, a full before-and-after example |
| `references/ai-patterns.md` | The complete AI-pattern catalog, roughly 50 named patterns with fixes and carve-outs |
| `references/word-tables.md` | Merged slop vocabulary: Tier 1, 2, and 3 words, boilerplate phrases, and plain-language substitutions |
| `references/profiles.md` | Context profiles and the tolerance matrix, auto-detection cues, voice profiles |
| `references/use-cases.md` | Register-by-register adaptations: error messages, runbooks, incident reports, commits, release notes, agent instructions, UI copy, translation prep |
| `references/checklist.md` | The full verification pass, severity tiers P0 to P2, and the output format for every mode |
