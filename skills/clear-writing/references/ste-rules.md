# The STE Rule Catalog

53 rules in 9 sections, paraphrased from ASD-STE100 Issue 9 with software examples. These govern **instructional** register. The official wording is in the free standard at asd-ste100.org.

When reporting violations, cite only rule numbers that appear in this file. Do not cite from memory. The numbering is unintuitive and models invent it. Tested: an agent without this file cited "Rule 3.1: short sentences". The real Rule 3.1 is about verb forms.

## Two levels of strictness

| Level | When | What applies |
|---|---|---|
| **Pragmatic** (default) | Docs, READMEs, error messages. The user wants clear text. | All structural rules. Domain words stay, so "idempotent" and "webhook" are legal. |
| **Strict** | The user names STE, ASD-STE100, or compliance | Structural rules plus full vocabulary discipline. Tell the user that full compliance needs the official dictionary. |

## Section 1: Words (1.1 to 1.14)

| Rule | Instruction |
|---|---|
| 1.1 | Use only approved words, technical nouns, or technical verbs. |
| 1.2 | Use an approved word only as its listed part of speech. |
| 1.3 | Use an approved word only with its approved meaning. |
| 1.4 | Use only the approved forms of verbs and adjectives. |
| 1.5 | You can use domain words as technical nouns ("webhook", "commit", "endpoint"). |
| 1.6 | Use an unapproved word only when it is a technical noun or part of one. |
| 1.7 | Do not use technical nouns as verbs. |
| 1.8 | Use the technical nouns of your project or industry. |
| 1.9 | When you pick a technical noun, pick a short and clear one. |
| 1.10 | No regional, slang, or jargon words as technical nouns. |
| 1.11 | One item, one name. Do not call it "config" here and "settings" there. |
| 1.12 | You can use domain verbs as technical verbs ("deploy", "compile", "merge"). |
| 1.13 | Do not use technical verbs as nouns. |
| 1.14 | Use American English spelling. |

In pragmatic mode, rules 1.5, 1.8, and 1.12 do the heavy lifting. Your domain vocabulary is legal. The ones agents break are 1.7, 1.11, and 1.13.

**Before:** You can webhook the event, then do a deploy.
**After:** Send the event to the webhook. Then deploy the service.

## Section 2: Multi-word nouns (2.1 to 2.2)

| Rule | Instruction |
|---|---|
| 2.1 | Write multi-word nouns of three words or fewer. |
| 2.2 | When a technical noun needs more than three words, write it in full once, then give a short form or hyphenate the units. |

Break long noun chains with prepositions (of, on, in, for):

**Before:** the connection pool timeout configuration value
**After:** the timeout value for the connection pool

## Section 3: Verbs (3.1 to 3.7)

| Rule | Instruction |
|---|---|
| 3.1 | Use only the verb forms that the dictionary gives. |
| 3.2 | Use only: infinitive, imperative, simple present, simple past, simple future, past participle as adjective. |
| 3.3 | Use the past participle only as an adjective ("the cached response"). |
| 3.4 | No auxiliary verbs for complex constructions. No present perfect, no "is to be installed". |
| 3.5 | Use an "-ing" form only as a technical noun or inside one ("logging", "the mounting bracket"), never as a verb. |
| 3.6 | Active voice. In descriptive text, passive is legal only when the agent is unknown. |
| 3.7 | Describe an action with a verb, not a noun. Write "compress the file", not "perform compression of the file". |

**Before:** The migration has completed and the table is being rebuilt.
**After:** The migration is complete. The database rebuilds the table.

**Before:** The flag can be set in the config file, making restarts unnecessary.
**After:** You can set the flag in the config file. Then a restart is not necessary.

**Before:** The temperature must be adjusted.
**After:** Adjust the temperature.

### The modal ladder

Approved: `can`, `will`, `must`. Banned: `should`, `would`, `may`, `might`, `could`.

| You wrote | STE writes |
|---|---|
| should (requirement) | must |
| should (recommendation) | Delete it, or state it as fact: "X is better because Y." |
| may / might / could (possibility) | can |
| may (permission) | can |
| would (hypothetical) | Restructure: "If X occurs, Y occurs." |

The standard rejects "could" even for possibility. Write "an explosion can occur", never "could occur".

This matters double for agent instructions. Models read "should" as optional.

## Section 4: Sentences (4.1 to 4.5)

| Rule | Instruction |
|---|---|
| 4.1 | Write short and clear sentences. |
| 4.2 | Do not omit words or use contractions to shorten sentences. Keep articles, keep "that". |
| 4.3 | Use a vertical list for complex text. |
| 4.4 | Use connecting words between sentences on related topics ("Then", "As a result"). |
| 4.5 | Put an article (the, a, an) or a demonstrative adjective (this, these) before nouns where applicable. |

Rule 4.2 is the anti-terseness rule. STE is short sentences with complete grammar, not telegraph style:

**Wrong shortening:** Ensure file exists before running.
**STE:** Make sure that the file exists before you run the command.

## Section 5: Procedural writing (5.1 to 5.5)

| Rule | Instruction |
|---|---|
| 5.1 | Maximum 20 words per sentence. Warnings and cautions included. |
| 5.2 | One instruction per sentence, unless two actions happen at the same time. |
| 5.3 | Write instructions in the imperative: "Run the migration." |
| 5.4 | Put a required condition before the command, divided by a comma: "If the build fails, read the log." |
| 5.5 | Notes give information, never instructions. Notes get the 25-word limit. |

**Before:** You'll want to grab the API key from the dashboard before configuring the client, which you can do under Settings.
**After:** Get the API key from the dashboard, under Settings. Then configure the client with this key.

## Section 6: Descriptive writing (6.1 to 6.6)

| Rule | Instruction |
|---|---|
| 6.1 | Give information gradually: one new fact per sentence. |
| 6.2 | Use key words and phrases to give the text a logical structure. |
| 6.3 | Maximum 25 words per sentence. |
| 6.4 | Group related information in paragraphs. |
| 6.5 | One topic per paragraph. |
| 6.6 | Maximum six sentences per paragraph. |

No imperative in descriptive text. Descriptions explain, procedures instruct.

## Section 7: Safety instructions (7.1 to 7.3)

| Rule | Instruction |
|---|---|
| 7.1 | Use a word that shows the risk level. "WARNING" means injury, "CAUTION" means damage. |
| 7.2 | Start with a clear command or condition. |
| 7.3 | Then give the risk or the possible result. |

Never bury the instruction after the explanation. The pattern transfers directly to destructive CLI flags, irreversible migrations, and dangerous API options.

**Before:** Note that data loss may occur in some circumstances if the destructive flag happens to be enabled when running against production.
**After:** CAUTION: Do not use the `--force` flag against production. The flag deletes rows that do not match the source.

## Section 8: Punctuation and word count (8.1 to 8.7)

| Rule | Instruction |
|---|---|
| 8.1 | All standard punctuation is legal except the semicolon. Write two sentences instead. |
| 8.2 | Use hyphens to connect words that act as one unit. |
| 8.3 | Parentheses are legal for references, item numbers, abbreviations, plural forms, explanations, alternatives. |
| 8.4 | In a vertical list, the lead-in colon ends a sentence for word count. |
| 8.5 | Text inside parentheses counts as one word. |
| 8.6 | Count as one word each: numbers, numbers with units, abbreviations, alphanumeric identifiers, quoted text, titles, labels, proper nouns. |
| 8.7 | A hyphenated word counts as one word. |

Rule 8.6 matters for software text. `sqlpipe run --config sqlpipe.yaml` in backticks is quoted text and counts as one word. Long identifiers do not blow your sentence budget.

## Section 9: Writing practices (9.1 to 9.4, GR-1 to GR-8)

| Rule | Instruction |
|---|---|
| 9.1 | When a word-for-word replacement does not work, restructure the sentence. |
| 9.2 | Use each approved word correctly: approved meaning, approved part of speech. |
| 9.3 | Do not build phrasal verbs. "Go down" becomes "decrease". "Set up" becomes "install" or "configure". |
| 9.4 | Keep one consistent style and terminology through the whole document. |

General recommendations GR-1 to GR-8: keep the conjunction "that", be careful with "with", give pronouns clear referents, prefer "this + noun" over bare "this", avoid false friends, avoid Latin abbreviations, use inclusive language, and use the possessive apostrophe form only when you are sure it is correct. GR-8 says that if you are unsure, do not use it, because non-native readers find it hard.

GR-6 for software docs: "e.g." becomes "for example", "i.e." becomes "that is", and "etc." gets deleted. Name the items or write "and more".

## Vocabulary discipline

The official dictionary holds about 900 approved words and about 1,200 banned words with alternatives. It is copyrighted by ASD and is not reproduced here. Its mechanics apply without it: **one word, one meaning, one part of speech.**

Known part-of-speech rulings, useful as patterns:

| Word | Ruling |
|---|---|
| test, check, work | Noun only. "Do a test", not "test the pump". "Check that X" becomes "make sure that X". |
| oil | Noun only as used in STE examples. For the verb, the dictionary gives "lubricate". |
| help | Verb only. For the noun, the dictionary gives "aid": "with the aid of". |
| fall | "To move down by gravity" only, never "decrease". |
| follow | "To come after" only, never "obey". Write "obey the instructions". |
| above, below | Physical positions only. For limits write "more than", "less than". |

### Consistency pass

Collapse these rotations to one term each (Rules 1.11 and 9.4):

- check / verify / confirm / validate / ensure: pick one
- config / configuration / settings / options: pick one
- delete / remove / drop / destroy: one per meaning, kept consistent
- error / issue / problem / failure: "error" for errors, "failure" for failed operations
- run / execute / invoke / launch: pick one
- show / display / render / present: pick one

## Full example

**Before, real unedited AI output:**

> **Connection timeouts.** If sqlpipe hangs or fails with `dial tcp: i/o timeout`, check that the host running sqlpipe can reach the Postgres port (usually 5432) — this is often a security group or firewall rule blocking the connection. If you're connecting to a managed database (RDS, Cloud SQL, etc.), confirm the instance allows connections from sqlpipe's IP. You can also try increasing `source.connect_timeout_seconds` in your config, since a slow network path can trip the default timeout even when the connection eventually succeeds.

**After.** Classified procedural, verb fixed to "make sure", conditions first, one instruction per sentence:

> **Connection timeouts.** sqlpipe stops with `dial tcp: i/o timeout` when it cannot reach the Postgres port (5432 by default).
>
> 1. Make sure that the host that runs sqlpipe can reach the Postgres port. A firewall or security group usually blocks it.
> 2. If the database is managed (RDS, Cloud SQL), make sure that the instance accepts connections from the IP of sqlpipe.
> 3. If the network is slow, increase `source.connect_timeout_seconds` in the configuration.

What changed: 40-word sentences split under 20, "you're" expanded, "check" and "confirm" collapsed to "make sure that", every condition moved before its command, "etc." removed, em dash removed, code and error strings untouched.
