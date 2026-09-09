# AI Pattern Catalog

Named patterns that make text read as machine-generated. These govern **voiced prose**, and the mechanical ones apply to instructional text too.

`SKILL.md` summarizes the highest-frequency patterns under "What Both Registers Ban". This file holds the full version of each, including the carve-outs that keep them from firing on legitimate writing.

Word-level replacements live in `word-tables.md`. Strictness by audience lives in `profiles.md`.

## Formatting

**Em dashes.** Replace with commas, periods, parentheses, or two sentences. Target zero. Hard maximum one per 1,000 words. Applies to headings, not just body prose. Catch both the Unicode em dash and the double-hyphen substitute.

**Bold overuse.** Strip bold from most phrases. One bolded phrase per major section at most, or none. If something is important enough to bold, restructure the sentence to lead with it instead.

**Emoji in headers.** Remove entirely. No `## 🚀 What This Means`. Social posts may use one or two sparingly, at the end of a line, never mid-sentence.

**Excessive bullet lists.** Convert bullet-heavy sections into prose. Bullets only for genuinely list-like content: feature comparisons, step-by-step instructions, API parameters.

**Curly quotation marks.** A weak paste-from-chat signal, meaningful mainly in plain-text contexts like code comments, commit messages, or plaintext drafts where nothing auto-curls. Treat as corroborating, never conclusive. Word, Google Docs, macOS, and iOS curl quotes by default, so most human prose contains them. Do not flag curly apostrophes on their own. Replace with straight quotes in plain text and code. Leave them in finished publications and in locale-correct punctuation such as French guillemets or German quotes.

**Immaculate typography in casual registers.** Same weak tier, scoped to register. Perfect spacing, punctuation, and capitalization where humans type fast (issue comments, chat, DMs) is corroborating evidence, not proof. A careful human types a flawless comment and a rushed one types a sloppy one. The inverse is worth flagging the other direction: when editing a human's casual text, preserve their typos, contractions, and idiosyncratic capitalization. Smoothing the rough edges erases the fingerprint that marks the text as theirs.

## Sentence structure

**"It's not X, it's Y".** Rewrite as a direct positive statement. Maximum one per piece, only if it serves the argument. This includes the **split-sentence form**, where the negation and the correction fall in two separate sentences instead of pivoting on one dash: "The headline isn't the speed. The real story is Y." Read alone each sentence looks innocent, which is exactly why the split version slips past a check tuned to the joined phrasing. Flag it the same way. AI also stacks the negation across several options before the reveal: "It's not the price. It's not the features. It's the trust." The multi-negation countdown is the same move inflated. Cut straight to the positive claim.

**Hollow intensifiers.** Cut `genuine`, `genuinely`, `real` as in "a real improvement", `truly`, `quite frankly`, `to be honest`, `let's be clear`, `it's worth noting that`. State the fact.

**Vague endorsement.** Cut or replace `worth reading`, `worth paying attention to`, `worth a look`, `worth exploring`, `worth checking out`, `worth your time`. These substitute a generic thumbs-up for a specific reason. Say why something matters.

**Hedging.** Cut `perhaps`, `could potentially`, `it's important to note that`, `to be clear`. Make the point directly.

**Missing bridge sentences.** Each paragraph should connect to the last. If paragraphs could be rearranged without the reader noticing, add connective tissue.

**Compulsive rule of three.** Vary groupings. Use two items, four items, or a full sentence. Maximum one "adjective, adjective, and adjective" pattern per piece.

## Template phrases

Slot-fill constructions signal that a sentence was generated, not written. If a phrase has a blank where a noun or adjective could go and still sound the same, it is too generic.

- "a [adjective] step towards [adjective] AI infrastructure" becomes the specific capability, benchmark, or outcome
- "a [adjective] step forward for [noun]" follows the same rule: say what actually changed
- "Whether you're [X] or [Y]" is a false-breadth construction. Pick the audience you are actually addressing, or cut. "Whether you're a startup founder or an enterprise architect" means everyone, which means nothing.
- "I recently had the pleasure of [verb]-ing" is a review and social pattern. Just say what happened: "I talked to", "I read", "I attended".

## Transition phrases

- "Moreover", "Furthermore", "Additionally": restructure so the connection is obvious, or use "and", "also", "on top of that"
- "In today's [X]", "In an era where": cut, or state specific context
- "It's worth noting that", "Notably": state the fact
- "Here's what's interesting", "Here's what caught my eye", "Here's what stood out": reader-steering frames. Let the content signal its own importance. If you need a lead-in, make it specific: "The revenue number matters because..." not "Here's the interesting part."
- "In conclusion", "In summary", "To summarize": your conclusion should be obvious
- "When it comes to": talk about the thing directly
- "At the end of the day": cut
- "That said", "That being said": cut, or use "but", "yet", "however". Do not overuse any one of them.

## Structural issues

**Uniform paragraph length.** Vary deliberately. Include some one and two sentence paragraphs and some longer ones. If every paragraph is roughly the same size, fix it.

**Formulaic openings.** If the piece opens with broad context before getting to the point ("In the rapidly evolving world of..."), rewrite to lead with the news or the insight. Context can come second.

**Suspiciously clean grammar.** Do not sand away all personality. Deliberate fragments, sentences starting with "And" or "But", comma splices for effect: if the natural voice uses them, keep them.

**Excessive structure.** More than three headings in under 300 words is almost always AI trying to look organized. Merge sections or use prose transitions. Eight or more bullet points in under 200 words means the content should be a paragraph. Formulaic section headers ("Overview", "Key Points", "Summary", "Conclusion", "Introduction") are default scaffolding. Use headers that tell the reader something specific about what follows.

**Numbered list inflation.** "Three key takeaways", "Five things to know", "Here are the top seven". AI defaults to numbered lists because they are structurally safe. Use them only when the content genuinely has that many discrete parallel items. If you are padding to hit a number, the list should not exist.

**Inline-header lists.** Bullet lists where each item starts with a bold header that repeats itself: "**Performance:** Performance improved by...". Strip the bold header and write the point directly. If the list items need headers, they should probably be paragraphs.

**List-label periods.** In bulleted lists where each item leads with a short label, LLMs end the label with a period and run the explanation as a separate sentence. A person writing the same list almost always uses a colon. Strongest form is bold labels (`**Intros.**` where a human writes `**Intros:**`). Weaker but still a tell is the same shape without bold. The colon reads as "here is what this label means". The period reads as a sentence that the following clause then contradicts by continuing. Fix the period to a colon and lowercase the start of the gloss, or drop the label and write the point as a plain sentence. Carve-outs: when the label span is a full sentence on its own, the period is correct. For the unbolded form, flag only when the leading fragment is clearly a label, meaning a one to four word noun phrase with no verb.

**Title case headings.** AI over-capitalizes: "Strategic Negotiations And Key Partnerships" instead of "Strategic negotiations and key partnerships". Use sentence case for subheadings. Title case only for the piece's main title, if at all.

**Hyphenated-pair overuse.** "A high-quality, well-architected, future-proof solution." Two distinct problems. First, density: strings of hyphenated adjectives piled on one noun. Cut to the modifier that matters. Second, the attributive and predicate error: a compound is hyphenated before the noun ("a high-quality report") but not after a linking verb ("the report is high quality"). AI frequently hyphenates the predicate form. Adapted from `blader/humanizer` P26.

**Bullet lists of bare noun phrases.** Five or more consecutive bullets where each is a short adjective-plus-noun phrase with no verb: "Stable mining efficiency / Reliable pool connectivity / Optimized RandomX performance". Reads as a marketing one-pager because that is the shape LLMs default to when summarizing features. The tell is the symmetry: every item the same grammatical shape, parallel in length, none of them checkable. A genuine list of observations has varying length, occasional verbs, and at least one item that does not fit. Convert to prose, or rewrite items as full claims. "Failed shares stayed under 1% across a 12-hour run" beats "Low failed share rates". This does not apply to genuine list content such as changelog entries, todo lists, parameter docs, or ingredient lists, where bare noun phrases are correct. Ask whether the bullets summarize claims (rewrite) or enumerate items (leave).

## Inflation and false significance

**Significance inflation.** "Marking a pivotal moment in the evolution of...", "a watershed moment for the industry". These inflate routine events into history-making ones. State what happened and let the reader judge. If the sentence still works after you delete the inflation clause, delete it.

**Generic future-narrative closers.** "May become one of the most important narratives of the next market cycle", "could become the defining trend of the coming decade", "is poised to become the next major chapter in [X]". AI defaults to this shape when it needs to land a closing thought without committing to a falsifiable claim. Grammatically a prediction, containing no testable content. The pattern is: modal (may, could, will, is poised to) plus "become" plus "one of the most [adjective]" plus a noun from the set narrative, story, trend, theme, chapter, movement, force. Fix by picking the falsifiable version. "DePIN compute may exceed AWS spot pricing for embarrassingly parallel workloads by 2027" is a prediction. The original is not.

**Hedge-stacked predictions.** "Could potentially create", "may eventually unlock", "might ultimately transform". Either word alone is acceptable. The stack is the tell. Each hedge cancels the next, leaving a sentence that asserts nothing while sounding cautious. Pick one.

**Real and actual adjective inflation.** "Real on-chain tokenomics", "actual reward sustainability", "genuine utility", "true product-market fit". Using `real`, `actual`, `genuine`, or `true` as an empty intensifier on an abstract noun implies the rest of the field is fake, without naming what makes this instance the real one. Distinct from hollow intensifiers, which are sentence-level hedges. This is the noun-modifier form. **Carve-out:** if the sentence names what the fake version is, leave it. "Real on-chain settlement, not bridged IOUs" is honest contrastive writing. The tell is the unsaid contrast. Fix by dropping the adjective and adding the specific claim.

**Novelty inflation.** AI treats established concepts as if the speaker invented them: "He introduced a term", "She coined the phrase", "a concept nobody's naming". Most ideas in a conversation are applications of existing concepts. Two problems. It is factually risky: if the concept has a Wikipedia page, claiming novelty makes the writer look uninformed. And it flatters the subject in a way that reads promotional. Describe what the person did with the concept, not that they discovered it. Related framings to flag: "the failure mode nobody's naming", "a problem nobody talks about", "the insight everyone's missing", "what nobody tells you about". Also flag **invented labels**: pseudo-analytical compound terms coined mid-sentence and never defined ("the supervision paradox", "the context-collapse problem", "a coordination tax"). Naming a concept is not explaining it. Source: tropes.fyi (Invented Labels).

**Promotional language.** Tourism-brochure prose: "nestled within the breathtaking foothills", "a vibrant hub of innovation", "a thriving ecosystem". Replace with plain description: "is a town in the Gonder region", "has 12 startups". If you would not say it in conversation, cut it.

**Formulaic challenges.** "Despite challenges, [subject] continues to thrive", "While facing headwinds, the organization remains resilient". A non-statement. Name the actual challenge and the actual response, or cut.

**False concession structure.** "While X is impressive, Y remains a challenge". AI uses this to sound balanced without weighing anything. Both halves are vague. Either make the concession specific or pick a side and argue it.

**False ranges.** Pairing unrelated extremes for breadth: "from the Big Bang to dark matter", "from ancient civilizations to modern startups". Sweeping and empty. List the actual topics or pick the one that matters.

## Manufactured credibility

**Vague attributions.** "Experts believe", "Studies show", "Research suggests", "Industry leaders agree", without naming the expert, study, or leader. Cite a specific source or drop the attribution and state the claim directly.

**Vague third-party validation.** Pointing at an unnamed external authority, usually with a generic superlative: "an outside party measuring the same models everyone runs and putting us on top", "independent testing confirms", "third-party benchmarks show we lead". The authority is faceless and the claim unfalsifiable. Name the source, the test, and the result: "On Stanford's HELM leaderboard (April 2026 run), we ranked first on reasoning latency." If you cannot name it, cut the claim. **Carve-out:** specifically attributed, checkable validation is legitimate. A named benchmark, a linked report, a dated audit. The tell is the vagueness, not the act of citing outside proof. Distinct from notability name-dropping, which piles on specific names. This is the inverse move, where the authority is deliberately unnamed, which is both harder to check and easier to invent.

**Notability name-dropping.** Piling on prestigious citations to manufacture credibility: "cited in The New York Times, BBC, Financial Times, and The Hindu". If a source matters, use it with context: "In a 2024 NYT interview, she argued...". One specific reference beats four name-drops. Related: **historical analogy stacking**, rapid-fire lists of past technologies to borrow their weight ("like the printing press, the telegraph, and the internet before it"). The montage substitutes for the argument. Name the one parallel that does analytical work. Source: tropes.fyi (Historical Analogy Stacking).

**Superficial -ing analyses.** Strings of present participles as pseudo-analysis: "symbolizing the region's commitment to progress, reflecting decades of investment, and showcasing a new era of collaboration". These say nothing. The same move appears without the -ing, as declarative meaning-telling that glosses a mundane subject as profound: "this represents a broader shift", "the decision symbolizes a commitment to excellence". If the significance is real, show it with a specific consequence. Adapted from `Aboudjem/humanizer-skill` P40.

## Filler and padding

**Filler phrases.** "It is important to note that", "In terms of", "The reality is that". Strip mechanical padding that adds words without meaning.

**Generic conclusions.** "The future looks bright", "Only time will tell", "One thing is certain", "As we move forward". Filler disguised as conclusions. Cut them. If the piece needs a closing thought, make it specific to the argument.

**Copula avoidance.** AI avoids "is" and "has" by substituting fancier verbs: "serves as", "features", "boasts", "presents", "represents". These sound like a press release. Default to "is" or "has" unless a more specific verb genuinely adds meaning.

**Synonym cycling.** AI rotates synonyms to avoid repeating a word: "developers... engineers... practitioners... builders" in one paragraph. Human writers repeat the clearest word. If the same noun or verb appears three times in a paragraph and it is the right word, keep all three. Forced variation reads as thesaurus abuse.

**Parenthetical hedging.** "(and, increasingly, Z)", "(or, more precisely, Y)", "(and perhaps more importantly, W)". AI inserts asides to sound nuanced without committing. If the aside matters, give it a sentence. If not, cut it.

**Speculative scenario openers.** "Imagine a world where...", "Picture a future in which...". AI opens with a hypothetical that lists desirable outcomes instead of making a claim. The scenario does the persuading and no evidence is offered. Cut the hypothetical and state the real claim. **Carve-out:** fiction, a thought experiment with a stated payoff, and instructional "imagine you have a sorted array" are fine. Flag only the world-scenario opener that stands in for an argument. Source: tropes.fyi (Imagine a World Where).

**Rhetorical question openers.** "But what does this mean for developers?", "So why should you care?", "What's next?". AI uses these to stall before the point. If you know the answer, say it. Rhetorical questions are earned by strong setup, not dropped as section transitions.

**Infomercial engagement hooks.** Punchy fragment-hooks that tee up a reveal: "The catch?", "The kicker?", "Here's the thing.", "The best part?", "Plot twist:", "The result?". These fake momentum around ordinary information. Distinct from rhetorical-question openers (which stall before a point) and chatbot artifacts (which perform helpfulness): these are mid-flow teasers that pad the rhythm. Delete the hook and state the thing. Adapted from `Aboudjem/humanizer-skill` P41.

**Hashtag stuffing.** Long trailing hashtag blocks, six or more on a short post, are near-universal in LLM social content and rare in thoughtful human posts. The block usually mixes a project tag with broad category tags (#AI #Crypto #Web3 #Innovation #FutureTech) that do nothing for discoverability. **Why six?** LinkedIn and X organic engagement plateaus past three to five tags. Human posts exceeding five are usually launch posts trading reach for engagement, while LLM posts default to 10 to 15. Six is where false positives drop below false negatives. Treat six or more as a hard flag and five as a soft tell on `linkedin` and `investor-email`. Fix with two or three specific tags, or none.

## Chat and model leakage

**Chatbot artifacts.** "I hope this helps!", "Certainly!", "Absolutely!", "Great question!", "Feel free to reach out", "Let me know if you need anything else". Conversational tics from chat interfaces, not writing. Remove entirely. Also watch for "In this article, we will explore..." and "Let's dive in!", which are meta-narration.

**Sycophantic tone.** "Great question!", "Excellent point!", "You're absolutely right!", "That's a really insightful observation". Distinct from chatbot artifacts: sycophancy validates the reader rather than performing helpfulness.

**Acknowledgment loops.** "You're asking about", "The question of whether", "To answer your question". AI restates the prompt before answering. The reader knows what they asked. Related: opening a section by summarizing the previous section.

**"Let's" constructions.** "Let's explore", "Let's take a look", "Let's break this down", "Let's examine". A false-collaborative opener that delays the point. Flag any "let's + verb" functioning as a transition rather than a genuine invitation to act.

**Reasoning chain artifacts.** "Let me think step by step", "Breaking this down", "To approach this systematically", "Step 1:", "Here's my thought process", "First, let's consider". Chain-of-thought scaffolding leaking into published prose. State the conclusion, then the evidence. Also watch for numbered reasoning steps that read like internal monologue rather than an argument for an audience.

**Cutoff disclaimers.** "While specific details are limited based on available information", "As of my last update", "I don't have access to real-time data". Model limitations leaking into prose. Find the information or remove the hedge. Never publish a sentence admitting the writer did not look something up.

**Speculative gap-filling.** When the model lacks a fact it fills the gap with hedged speculation dressed as background: "maintains a relatively low public profile", "is believed to have", "likely began his career in", "appears to have studied". Guesses formatted as statements. Distinct from cutoff disclaimers, which admit the gap. This hides it behind plausible filler, which is worse, because the reader cannot tell what is known from what is invented. Cut the speculation or replace it with a sourced fact. Adapted from `blader/humanizer` P21.

**Unfilled placeholders.** `[Your Name]`, `[INSERT SOURCE URL]`, `[Describe the specific section]`, `2025-XX-XX`, `<!-- Add citation if available -->`. Near-definitive evidence that generated boilerplate was pasted without editing. Humans use placeholders in templates but rarely ship them. Treat any visible placeholder as a publishing bug. Catch the obvious shapes: `\[(?:Your|Insert|Add|Enter|Describe|Specify|Choose)[^\]]+\]`, `\b\d{4}-XX-XX\b`, and HTML or Markdown comments with placeholder verbs.

**Chatbot citation markup leaks.** `citeturn0search0`, `contentReference[oaicite:0]{index=0}`, `oai_citation`, `[attached_file:1]`, `grok_card`. Not patterns, fingerprints. Their presence is essentially proof the text came from a specific chat tool and was pasted without cleanup. Strip every token. If a citation was meaningful, replace it with a real reference. Worth catching even when nothing else reads as AI. Adapted from `Aboudjem/humanizer-skill` P34.

**AI-tool URL parameters.** `utm_source=chatgpt.com`, `utm_source=copilot.com`, `utm_source=openai`, `utm_source=claude.ai`, `utm_source=perplexity.ai`, `referrer=grok.com`. Same logic as citation leaks. Strip the parameter and keep the URL. Adapted from `Aboudjem/humanizer-skill` P35.

## Emotion and emphasis

**Emotional flatline.** AI claims emotions as a structural crutch without conveying them: "What surprised me most", "I was fascinated to discover", "What struck me was", "I was excited to learn", "The most interesting part", and the bare header variant "Interesting part of the project:". Two problems. It is tell-don't-show: if the thing is genuinely surprising, the reader should feel that from the content. And these are massively overused as list introductions. This is not always AI. It is also lazy human writing on autopilot. Flag it either way. The fix is not "never say surprised", it is that if you claim an emotion the writing around it should earn it. Related: "hit differently" and "hits different", trendy colloquialisms used as a shortcut to sound relatable without earning the beat.

**Confidence calibration phrases.** "It's worth noting that", "Interestingly", "Surprisingly", "Importantly", "Significantly", "Notably", "Certainly", "Undoubtedly", "Without a doubt". These signal how the reader should feel instead of letting the fact speak. Also "Here's what's interesting" and "Here are the parts I found interesting", which pre-interpret importance. One "notably" in 2,000 words is fine. Three in 500 is emphasis stacking. Flag by density. Related **persuasive-authority tropes**: "the real question is", "at its core", "fundamentally", "make no mistake", "the truth is". Same move, but they assert depth or stakes instead of feeling. Cut the trope and lead with the substance. Adapted from `blader/humanizer` P27.

**Self-labeling significance.** After describing several items, the writer points back at one and labels it contrarian, clever, surprising, counterintuitive, or key: "That last move is the contrarian one", "This is the interesting part", "That third bullet is the real story". The label does the work the content was supposed to do. If a move is genuinely contrarian, the reader recognizes it. Distinct from confidence calibration (which front-loads the cue) and emotional flatline (which prefaces a single claim). This back-points after the fact, usually as "[that / this / the Xth / the last] [noun] is the [adjective] one". Signal adjectives: contrarian, clever, surprising, counterintuitive, interesting, key, important, unusual, smart, brilliant, real, actual. Cut the labeling sentence and let the explanation do the work. Before: "Two separate indexes for tiered storage. That last move is the contrarian one. Co-locating related data usually helps cache locality." After: "Two separate indexes for tiered storage. Co-locating related data usually helps cache locality, but splitting the indexes is what makes the hot path cheap."

**Social endorsement closers.** The curatorial sign-off appended to posts that share something, usually a colon teeing up a link: "This one is worth your time:", "This one's a must-read:", "Do yourself a favor and read this.", "Bookmark this.", "Don't sleep on this one.", "Thank me later." It performs a recommendation without giving a reason to click. The endorsement is generic and demonstrative-anchored, so it could sit under any link. Distinct from the bare "worth [verb]ing" entry (a single weak word inside a sentence) and from infomercial hooks (mid-flow teasers): this is the whole closing line. Say what the thing is and who it is for, then drop the call to action. If you cannot name a specific reason, the share needs no sign-off.

## Conversational register

**Wall-of-text replies.** In conversational registers (issue and PR comments, chat, DMs, casual email) humans break a reply at thought boundaries. LLMs default to a single dense block regardless of length. The tell: reply-length text, roughly under 150 words, with four or more sentences delivered as one unbroken paragraph. Break at thought boundaries, one idea per line-group. Observed in the wild: a maintainer called out an assisted-sounding reply with "I prefer to talk human to human", and the dense block shape was the tell, not any single word. Distinct from paragraph-length uniformity, which is about long-form prose where every paragraph is the same size. This is about short text having zero breaks. **Carve-out:** a single dense paragraph is correct in formal long-form registers such as a blog intro, a docs paragraph, or a deliberately tight one-paragraph email. This fires only in conversational reply registers. Never flag continuous long-form prose just because it lacks internal breaks.

**Recap-flattery opener.** Replying to a person by summarizing their own work back at them with praise before getting to the point: "Thanks for all the legwork here, the migration script and the rollback plan you worked through are what made this possible." The reader already knows what they did. The recap performs appreciation instead of conveying information. Distinct from a genuine thank-you, which is short and moves on. Distinct from sycophantic tone (generic validation of the reader) and acknowledgment loops (restating the prompt): those echo the question or context, this echoes the other person's own work back at them. Substance first. If thanks is warranted, one plain clause: "Thanks for the legwork, this looks right to me, one comment below."

## Rhythm and uniformity

These are patterns in how the text flows as a whole. AI text is metronomic. Human text has varied rhythm.

**Structure is the number one detection signal.** Detection tools, including Pangram which trains a classifier on 28M human documents, weight structural regularity higher than vocabulary. Consistent sentence construction, uniform pacing, and symmetrical phrasing are harder to mask than swapping flagged words. Fix every Tier 1 word and leave the rhythm untouched, and the text still reads as generated.

- **Sentence length uniformity.** If most sentences run 15 to 25 words, the text sounds robotic. Mix short punchy sentences of 3 to 8 words with longer flowing ones over 20. Fragments work. Questions break the monotony.
- **Paragraph length uniformity.** If every paragraph is 3 to 5 sentences and roughly the same size, vary deliberately. Some should be one sentence.
- **Vocabulary repetition versus synonym cycling.** AI either repeats mechanically or cycles conspicuously. Human writers repeat when the word is right and vary when it is natural. There is no formula.
- **Read-aloud test.** If the text could be read by a text-to-speech engine without sounding odd, it is too uniform.
- **Missing first-person perspective.** Where appropriate the writer should have opinions, preferences, and reactions. AI is relentlessly neutral. If the piece is supposed to have a voice, the absence of "I think" or a stated preference is itself a tell.
- **Over-polishing.** Aggressively editing out every irregularity pushes human writing toward AI statistical profiles. Natural disfluency, idiosyncratic word choices, and uneven pacing keep text out of that classification. Applying every rule at maximum strictness creates the very uniformity you are trying to avoid.

**Vocabulary diversity.** In pieces over 200 words, look at how much vocabulary the text uses. The type-token ratio, distinct word types divided by total tokens, is a classical stylometric signal readable by eye. Human prose at this length usually lands around 0.50 to 0.65 in English. AI text trends flatter, sometimes under 0.40 when the model locks onto a small vocabulary loop. A low ratio is not proof: narrow topics, technical reference material, and second-language writing all compress vocabulary legitimately. But on general prose where you expect range, below 0.40 is worth a second look. The fix is rarely to thesaurus the text. It is to broaden the what: name specific things, cite specific cases, replace a re-used abstract noun with the concrete instance behind it.

**Paragraph-reshuffle immunity.** A writer-side diagnostic. Can you swap two body paragraphs without breaking the piece? If order does not matter, you have written a list of points, not an argument that builds. AI prose often fails this, because each paragraph is a self-contained module with no load-bearing connection to its neighbors. The fix is structural: establish a through-line where each paragraph depends on the one before it. If the paragraphs are genuinely independent, decide whether the piece should be an explicit list, or whether it is missing a thesis. Adapted from `Aboudjem/humanizer-skill` P38.

**Treadmill effect.** Read each paragraph and ask what is actually new here. AI prose frequently restates the premise in fresh words instead of advancing it: lots of motion, no distance covered. The tell is that you could cut 40 to 60% and lose no information. For each paragraph, name the one fact, claim, or turn it contributes. If there is not one, cut it. If there is, lead with it and drop the throat-clearing. Adapted from `Aboudjem/humanizer-skill` P43.
