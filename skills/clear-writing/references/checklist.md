# Verification And Output

Run this pass on every draft before you deliver it. Checks are ordered from mechanical to judgment.

## Mechanical checks

Search the draft for each pattern. Every hit outside code blocks and quoted text is a violation.

### Both registers

| Search for | Violation | Fix |
|---|---|---|
| `—` or `--` | Em dash | Comma, period, parentheses, or two sentences |
| `[Your`, `[Insert`, `[Add`, `XX-XX` | Unfilled placeholder | Fill it in or delete the sentence |
| `citeturn`, `oaicite`, `oai_citation`, `grok_card` | Chat markup leak | Strip the token |
| `utm_source=chatgpt`, `utm_source=claude`, `utm_source=perplexity`, `referrer=grok` | AI tool URL parameter | Strip the parameter, keep the URL |
| `e.g.`, `i.e.`, `etc.` | Latin abbreviation | "for example", "that is", name the items |
| `could potentially`, `may eventually`, `might ultimately` | Hedge stack | Pick one |
| `serves as`, `boasts`, `features` (verb) | Copula avoidance | `is` or `has` |
| `experts believe`, `studies show`, `research suggests` | Vague attribution | Name the source or cut the claim |
| Tier 1 words from `word-tables.md` | Slop vocabulary | Replace |

### Instructional register only

| Search for | Violation | Fix |
|---|---|---|
| `'ll`, `'re`, `'ve`, `n't`, `it's` | Contraction (Rule 4.2) | Expand it |
| `has been`, `have been`, `had been` | Present or past perfect (Rule 3.4) | Simple past or simple present |
| `has` or `have` plus past participle | Present perfect (Rule 3.4) | Simple past |
| `should`, `would`, `may`, `might`, `could` | Unapproved modal (Rule 3.2) | See the modal ladder in `ste-rules.md` |
| `is being`, `are being`, `was being` | Progressive passive (Rules 3.4, 3.5) | Active, simple tense |
| `, making`, `, allowing`, `, enabling`, `, ensuring` | "-ing" clause as verb (Rule 3.5) | New sentence with a real subject |
| `;` | Semicolon (Rule 8.1) | Two sentences |
| ` if `, ` when ` mid-sentence | Trailing condition (Rule 5.4) | Move the condition to the start, add a comma |
| `simply`, `easily`, `seamlessly`, `robust` | Filler with no fact | Delete |

## Countable checks

**Instructional register:**

1. **Sentence length.** Count words in each sentence. Procedural limit 20, descriptive limit 25, notes 25. Backticked commands, numbers with units, and identifiers count as one word each (Rule 8.6).
2. **Paragraph size.** Six sentences maximum per paragraph (Rule 6.6).
3. **Multi-word nouns.** Any noun chain over three words gets broken with prepositions (Rule 2.1).
4. **Instructions per sentence.** One, unless the actions are simultaneous (Rule 5.2).

**Voiced prose:**

5. **Sentence length spread.** If most sentences fall between 15 and 25 words, the rhythm is metronomic. Add short sentences of 3 to 8 words and let some run past 25.
6. **Paragraph length spread.** If every paragraph is 3 to 5 sentences, vary it. Some should be one sentence.
7. **Heading density.** More than three headings in under 300 words means the piece is over-structured.
8. **Hashtags.** Six or more on a short social post is a hard flag.
9. **Vocabulary diversity.** On general prose over 200 words, a type-token ratio below 0.40 is worth a second look. Broaden the content, do not thesaurus the words.

## Judgment checks

**Instructional register:**

10. **Classification.** Is each passage cleanly procedural or descriptive? Procedures in imperative, descriptions never in imperative.
11. **Voice.** For any passive sentence: is the agent truly unknown, and is the passage descriptive? Otherwise make it active (Rule 3.6).
12. **Condition placement.** Every "if" and "when" stands before its command, with a comma (Rule 5.4).
13. **Warnings.** Command or condition first, risk second (Rules 7.2, 7.3).
14. **Completeness.** Articles present, "that" present after "make sure", no telegraph style (Rule 4.2).

**Both registers:**

15. **Synonym rotation.** One term per concept across the whole document (Rules 1.11, 9.4). Scan for check/verify/confirm, config/settings, run/execute.
16. **Untouchables intact.** Code, identifiers, quoted errors, and proper nouns unchanged.

**Voiced prose:**

17. **Read aloud.** If a text-to-speech engine could read it without sounding odd, it is too uniform.
18. **Paragraph reshuffle.** Can you swap two body paragraphs without breaking the piece? If yes, there is no argument, only a list.
19. **Treadmill test.** Name the one fact each paragraph adds. If you cannot, cut it.
20. **First person.** If the piece is supposed to have a voice, does it have opinions and reactions, or is it relentlessly neutral?

## Severity tiers

For a quick pass or triaging a large document, prioritize by tier. Use P0 and P1 for quick passes. A full audit covers all three.

### P0: credibility killers, fix immediately

- Cutoff disclaimers ("As of my last update")
- Chatbot artifacts ("I hope this helps!", "Great question!")
- Chat markup leaks and AI tool URL parameters
- Unfilled placeholders
- Vague attributions without sources ("Experts believe")
- Significance inflation on routine events
- Hashtag stuffing on `linkedin` and `investor-email`. Severity varies by profile, and it drops to P2 on `blog` and `technical-blog` where a launch post may legitimately stack tags.

### P1: obvious AI smell, fix before publishing

- Word-table violations (delve, leverage, harness, robust)
- Template phrases and slot-fill constructions
- "Let's" transition openers
- Synonym cycling within a paragraph
- Formulaic openings ("In the rapidly evolving world of...")
- Bold overuse
- Em dash frequency above one per 1,000 words
- Generic future-narrative closers
- Social endorsement closers ("This one is worth your time:")
- Hedge-stacked predictions
- Real and actual adjective inflation
- Bullet lists of bare noun phrases
- Tier 3 phrase clustering, three or more distinct phrases

### P2: stylistic polish, fix when time allows

- Generic conclusions ("The future looks bright")
- Compulsive rule of three
- Uniform paragraph length
- Copula avoidance
- Transition phrases (Moreover, Furthermore, Additionally)
- Hashtag stuffing on `blog` and `technical-blog`
- Tier 3 phrase repetition, a single phrase twice or more

## Output format

### Write mode

Return the text, then a short note on the register you classified it as and the self-check result.

### Rewrite mode, the default

Four sections.

**1. Issues found.** Every pattern identified, with the offending text quoted.

**2. Rewritten version.** The full rewritten content. Preserve the original structure, intent, and all specific technical details. Change only what the guidelines require.

**3. What changed.** A brief summary of the major edits. Not every word.

**4. Second-pass audit.** Re-read your own rewrite from section 2. Identify anything that survived the first pass: recycled transitions, lingering inflation, copula avoidance, filler. Fix them, return the corrected text inline, and note what changed. If the rewrite is clean, say so.

### Detect mode

Two sections.

**1. Issues found.** Every pattern identified, with the offending text quoted, grouped by severity. In instructional register, report each as rule number, offending text, compliant rewrite. Cite only rule numbers that appear in `ste-rules.md`.

**2. Assessment.** For each flag, note whether it is a clear problem or a judgment call. Some AI-associated patterns are effective writing in small doses. Uniform paragraph length is a problem, a well-placed "however" is not. Call out which flags to definitely fix and which are worth a second look but may be fine in context. If the text is clean, say so.

When the user asked for STE compliance, end with: "No tool can guarantee ASD-STE100 compliance. Final approval rests with the writer. The official standard is a free download at asd-ste100.org."

### Edit mode

After editing in place, return a short report, not the full file.

**1. Edits made.** The changes, each with the file location and the before and after. Only the spans you touched.

**2. Verification.** Confirm you re-read the file and the flagged patterns are resolved. Note anything you deliberately left alone because it was already human or intentional.

## Tone calibration

The goal is writing that sounds like a person wrote it. Direct. Specific. The writing should demonstrate confidence, not assert it.

1. **Vary sentence length** in voiced prose. Mix short with long. Fragments are fine.
2. **Be concrete.** Replace vague claims with numbers, names, dates, or examples.
3. **Have a voice** where appropriate. First person, stated preferences, real reactions.
4. **Cut the neutrality.** Humans have opinions. If the piece is supposed to take a position, take it.
5. **Earn your emphasis.** Do not tell the reader something is interesting. Make it interesting.

If the original writing is already strong, say so and make only the necessary cuts. Do not over-edit for the sake of it.
