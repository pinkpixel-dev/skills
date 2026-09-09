# Profiles

Two independent axes.

**Context profiles** set how strict to be, based on the audience. **Voice profiles** set how the prose should sound. You can write blunt for a blog or warm for docs.

## Context profiles

If no context is given, auto-detect from content cues.

| Profile | What it is |
|---|---|
| `linkedin` | Short-form social. Punchy fragments and visual formatting matter. |
| `blog` | Default. Standard long-form prose. All rules at full strength. |
| `technical-blog` | Long-form with code, architecture, APIs. Technical terms get a pass. |
| `investor-email` | High-trust audience. Tighten everything. Promotional language is the biggest risk. |
| `docs` | Documentation, READMEs, guides. Clarity over voice. |
| `casual` | Slack messages, internal notes, quick replies. Only the worst offenders. |

Register and context are related but not the same. Register (instructional versus voiced prose, set in `SKILL.md`) decides which ruleset governs. Context decides how hard to enforce it. The `docs` profile almost always means instructional register, and `linkedin` almost always means voiced prose, but a docs page can open with a voiced paragraph.

### Tolerance matrix

Rules not listed apply at full strength across all profiles.

| Rule | linkedin | blog | technical-blog | investor-email | docs | casual |
|------|----------|------|----------------|----------------|------|--------|
| Em dashes | relaxed (2/post OK) | strict | strict | strict | relaxed | skip |
| Bold overuse | relaxed (bold hooks OK) | strict | strict | strict | relaxed | skip |
| Emoji in headers | relaxed (1-2 end-of-line OK) | strict | strict | strict | skip | skip |
| Excessive bullets | skip (lists work on LinkedIn) | strict | relaxed (technical lists OK) | strict | skip (lists are docs) | skip |
| Hedging | strict | strict | relaxed ("may" is accurate in technical) | strict | relaxed | skip |
| Word table (full list) | strict | strict | **partial** (see below) | strict | relaxed | P0 only |
| Promotional language | relaxed (some sell is expected) | strict | strict | **extra strict** | strict | skip |
| Significance inflation | strict | strict | strict | **extra strict** | relaxed | skip |
| Copula avoidance | skip | strict | relaxed | strict | skip | skip |
| Uniform paragraph length | skip (short-form) | strict | strict | strict | relaxed | skip |
| Numbered list inflation | relaxed | strict | relaxed | strict | skip | skip |
| Rhetorical questions | relaxed (1 as hook OK) | strict | strict | strict | strict | skip |
| Transition phrases | skip (short-form) | strict | strict | strict | relaxed | skip |
| Generic conclusions | skip | strict | strict | **extra strict** | skip | skip |
| Hashtag stuffing | strict | strict | strict | **extra strict** | skip (no hashtags in docs) | skip |
| Bullet-NP lists | strict | strict | relaxed (technical option lists OK) | strict | relaxed (parameter lists OK) | skip |
| Tier 3 phrase clustering | strict | strict | strict | **extra strict** | relaxed | skip |
| Future-narrative closers | strict | strict | strict | **extra strict** | skip | skip |
| Social endorsement closers | strict (the LinkedIn share-post tell) | strict | strict | strict | skip | relaxed (1 OK in a DM) |
| Hedge-stacked predictions | strict | strict | relaxed ("could" is hedged accuracy) | **extra strict** | relaxed | skip |
| Real/actual inflation | strict | strict | strict | **extra strict** | relaxed | skip |

**Technical-blog word table exceptions.** These have legitimate technical meaning and are not flagged in technical context: `robust`, `comprehensive`, `seamless`, `ecosystem`, `leverage` when discussing actual platform leverage or APIs, `facilitate`, `underpin`, `streamline`. Still flag: `delve`, `tapestry`, `beacon`, `embark`, `testament to`, `game-changer`, `harness`.

**"Extra strict"** means flag even borderline instances. In an investor email a single "thriving ecosystem" can undermine the whole message.

**"Skip"** means do not audit this category for this profile. The rule does not apply or is not worth the edit.

**Wall-of-text replies are not in this matrix on purpose.** A plain issue comment auto-detects to `blog`, so scoping that rule by profile would fire it on continuous long-form prose. The scoping lives in the rule's own judgment instead.

### Auto-detection cues

| Signal | Inferred context |
|---|---|
| Under 300 words plus hashtags or mentions | `linkedin` |
| Code blocks, API references, or technical architecture | `technical-blog` |
| Salutation ("Hi [name]", "Dear") plus investor or fundraising language | `investor-email` |
| Step-by-step instructions, parameter docs, README structure | `docs` |
| No strong signals | `blog`, the safest default, where all rules apply |

If auto-detection feels wrong, say which profile you are using and why. The user can override.

## Voice profiles

Voice is optional. If the writer does not name one, infer it from the input's existing register and do not impose a persona on text that already has one.

Each profile is a set of concrete targets, not a vibe.

**`casual`.** Contractions throughout, since their absence reads stiff. Short sentences, averaging 14 words or fewer. Fragments allowed. At least one first-person or concrete-anecdote touch. Near-zero jargon. Keep warm hedges such as "honestly" and "I think", cut corporate ones such as "it's worth noting". Used for blog posts, social, community.

**`professional`.** Active voice for most sentences. Vary sentence length and avoid three in a row within a few words of each other. One concrete claim per paragraph: a number, a name, a date. Never "experts say". Make the ask explicit. Low tolerance for hedging. Used for LinkedIn, investor email, sponsor pitches.

**`technical`.** Prefer plain copulatives ("X is Y") over inflated substitutes ("serves as", "stands as a testament to"). One idea per sentence, imperative mood for instructions. Jargon is fine but define it on first use. Tables and lists only where the content is genuinely list-shaped. Used for docs and technical blog.

**`warm`.** Address the reader directly and acknowledge them at least once. Cut intensifiers ("very", "truly", "incredibly") in favor of stronger verbs. No performative-empathy openers ("I completely understand how you feel"). Medium sentences of 15 to 20 words for an unhurried cadence. Used for mentorship, onboarding, thank-yous.

**`blunt`.** Lead with the claim and cut the "It's important to note that" windup. Use periods for emphasis. No padding to hit a rule of three. Near-zero hedging, and flag "may / could / potentially" stacks. Short declaratives with the occasional long sentence for contrast. Used for decision memos, thought leadership, hard feedback.

### Calibrating to a sample

If the writer gives you a sample of their own writing, analyze its sentence-length pattern, contraction rate, paragraph openings, and recurring word choices, then match those instead of a named profile. Do not upgrade their vocabulary. If they write "stuff" and "things", keep that register.

### How voice composes with context

Voice sets the target and context sets how hard to enforce it.

A voice target always applies, even where a context profile would skip that category. `technical` voice still prefers plain copulatives in a `casual` context that otherwise ignores copula avoidance.

Where both axes govern the same rule and agree, they reinforce. `blunt` voice wants near-zero em dashes and `blog` context is already strict, so it stays a hard edit.

Where they disagree, resolve toward the stricter of the two. A `warm` voice on `docs` still does not get decorative tables.

Sensible default pairings: casual with casual, professional with linkedin or investor-email, technical with docs or technical-blog.
