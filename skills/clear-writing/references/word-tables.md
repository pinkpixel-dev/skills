# Word Tables

Merged vocabulary lists. The tier system comes from AI-pattern research and reduces false positives on words that are fine alone but suspicious in clusters. The plain-language table at the end comes from STE and covers phrase-level padding the tiers do not reach.

**Tiers:**

- **Tier 1** appears 5 to 20 times more often in AI text than human text. Replace on sight.
- **Tier 2** is legitimate alone. Two or more in one paragraph is a strong signal. Flag together.
- **Tier 3** is normal English that AI overuses. Flag only at density, roughly 3% or more of total words.

**Match inflected forms.** Each entry covers the listed word and its variants: adverb (`-ly`), gerund (`-ing`), plural, comparative, and conjugations. So `genuine` also flags `genuinely`, `leverage` also flags `leveraging`, `meticulous` covers `meticulously`. When a variant carries a separate honest sense, such as `real` meaning factual rather than the intensifier in "a real improvement", judge by context instead of matching blindly.

The tables give defaults, not mandates. If a flagged word is clearly the right choice in context, keep it.

## Tier 1: always replace

| Replace | With |
|---|---|
| delve / delve into | explore, dig into, look at |
| deep dive / dive into | look at, examine, explore |
| landscape (metaphor) | field, space, industry, world |
| tapestry | (describe the actual complexity) |
| realm | area, field, domain |
| paradigm | model, approach, framework |
| embark | start, begin |
| beacon | (rewrite entirely) |
| testament to | shows, proves, demonstrates |
| robust | strong, reliable, solid |
| comprehensive | thorough, complete, full |
| cutting-edge | latest, newest, advanced |
| leverage (verb) | use |
| utilize | use |
| pivotal | important, key, critical |
| marking a pivotal moment | (state what happened) |
| underscores | highlights, shows |
| meticulous / meticulously | careful, detailed, precise |
| seamless / seamlessly | smooth, easy, without friction |
| game-changer / game-changing | describe what specifically changed and why it matters |
| hit differently / hits different | (say what specifically changed, or cut) |
| watershed moment | turning point, shift (or describe what changed) |
| the future looks bright | (cut, say something specific or nothing) |
| only time will tell | (cut, say something specific or nothing) |
| nestled | is located, sits, is in |
| vibrant | (describe what makes it active, or cut) |
| thriving | growing, active (or cite a number) |
| despite challenges... continues to thrive | (name the challenge and the response, or cut) |
| showcasing | showing, demonstrating (or cut the clause) |
| unpack / unpacking | explain, break down, walk through |
| bustling | busy, active (or cite what makes it busy) |
| intricate / intricacies | complex, detailed (or name the specific complexity) |
| complexities | (name the actual complexities, or use "problems" or "details") |
| ever-evolving | changing, growing (or describe how) |
| enduring | lasting, long-running (or cite how long) |
| daunting | hard, difficult, challenging |
| holistic / holistically | complete, full, whole (or describe what is included) |
| actionable | practical, useful, concrete |
| impactful | effective, significant (or describe the impact) |
| learnings | lessons, findings, takeaways |
| thought leader / thought leadership | expert, authority (or describe their actual contribution) |
| best practices | what works, proven methods, standard approach |
| at its core | (cut, just state the thing) |
| synergy / synergies | (describe the actual combined effect) |
| interplay | relationship, connection, interaction |
| in order to | to |
| due to the fact that | because |
| serves as | is |
| features (verb) | has, includes |
| boasts | has |
| presents (inflated) | is, shows, gives |
| commence | start, begin |
| ascertain | find out, determine, learn |
| endeavor | effort, attempt, try |
| keen (as intensifier) | interested, eager, enthusiastic (or cut) |
| genuinely / genuine (as intensifier) | (cut, just state the fact) |
| symphony (metaphor) | (describe the actual coordination or combination) |
| embrace (metaphor) | adopt, accept, use, switch to |

## Tier 2: flag when two or more appear in one paragraph

| Replace | With |
|---|---|
| harness | use, take advantage of |
| navigate / navigating | work through, handle, deal with |
| foster | encourage, support, build |
| elevate | improve, raise, strengthen |
| unleash | release, enable, unlock |
| streamline | simplify, speed up |
| empower | enable, let, allow |
| bolster | support, strengthen, back up |
| spearhead | lead, drive, run |
| resonate / resonates with | connect with, appeal to, matter to |
| revolutionize | change, transform, reshape (or describe what changed) |
| facilitate / facilitates | enable, help, allow, run |
| underpin | support, form the basis of |
| underpinning / underpinnings | basis, foundation, what supports |
| nuanced | specific, subtle, detailed (or name the actual nuance) |
| crucial | important, key, necessary |
| multifaceted | (describe the actual facets, or cut) |
| ecosystem (metaphor) | system, community, network, market |
| myriad | many, numerous (or give a number) |
| plethora | many, a lot of (or give a number) |
| encompass | include, cover, span |
| catalyze | start, trigger, accelerate |
| reimagine | rethink, redesign, rebuild |
| galvanize | motivate, rally, push |
| augment | add to, expand, supplement |
| cultivate | build, develop, grow |
| illuminate | clarify, explain, show |
| elucidate | explain, clarify, spell out |
| juxtapose | compare, contrast, set side by side |
| paradigm-shifting | (describe what actually shifted) |
| transformative / transformation | (describe what changed and how) |
| cornerstone | foundation, basis, key part |
| paramount | most important, top priority |
| poised (to) | ready, set, about to |
| burgeoning | growing, emerging (or cite a number) |
| nascent | new, early-stage, emerging |
| quintessential | typical, classic, defining |
| overarching | main, central, broad |
| quietly | cut, or name the concrete contrast |
| deeply | cut, or name what specifically runs deep |

**On `deeply`:** significance collocations only, such as "deeply integrated", "deeply committed", "deeply rooted". Literal uses like "deeply nested" or "cares deeply" never count toward a cluster.

## Tier 3: flag only at high density

Normal words. Flag only when the text is saturated with them, which signals that AI filled space with vague praise instead of specifics.

| Word | What to do |
|---|---|
| significant / significantly | Replace some with specifics: numbers, comparisons, examples |
| innovative / innovation | Describe what is actually new |
| effective / effectively | Say how, or cite a metric |
| dynamic / dynamics | Name the actual forces or changes |
| scalable / scalability | Describe what scales and to what |
| compelling | Say why it compels |
| unprecedented | Name the precedent it breaks (or cut) |
| exceptional / exceptionally | Cite what makes it an exception |
| remarkable / remarkably | Say what is worth remarking on |
| sophisticated | Describe the sophistication |
| instrumental | Say what role it played |
| world-class / state-of-the-art / best-in-class | Cite a benchmark or comparison |

## Tier 3 phrases: flag at repetition or in clusters

Multi-word boilerplate that is individually unobjectionable but stacks heavily in generated content. Crypto, web3, DePIN, and AI infrastructure reviews are the worst offenders.

Two triggers. **Repetition:** two or more uses of the same phrase. This is a lower threshold than single-word Tier 3, because a two-word match repeated twice is already stronger evidence than re-using "significant". **Clustering:** three or more distinct phrases from this table in one piece, even when each appears once. That is the shape LLMs take when they vary their own boilerplate to seem less repetitive.

| Phrase | What to do |
|---|---|
| emerging sector / emerging space / emerging category | Name the actual sector or what is emerging about it |
| the integration of (X with Y) | Describe what is being integrated and what changes for the user |
| the intersection of (X and Y) | Pick the specific overlap that matters or cut the framing |
| community-driven | Name what the community does. "Community-driven" alone is filler |
| long-term sustainability | Cite the time horizon and the constraint. "Long-term" is hand-waving |
| user engagement | Name the action. "Engagement" is a wrapper around clicks, comments, retention |
| decentralized compute | Specify the architecture or cut. The phrase is a category label, not a claim |
| (sustainable) reward emissions | Cite the emission schedule and the sink |
| tokenized incentive structures | Describe the actual mechanism (vesting, gauge, bonded LP) |
| designed for long-term [X] | Cut "designed for". Either it is or it is not. Then state the property |

## Plain-language substitutions

From STE. These are phrase-level padding, mostly outside the tier system. If the word carries no fact, delete it instead of replacing it.

| Slop | Write instead |
|---|---|
| prior to | before |
| ensure | make sure that |
| in the event that | if |
| when it comes to | for |
| as needed, as necessary | (state the condition) |
| it is worth noting that | (delete) |
| it's important to, crucially | (delete, state the fact) |
| simply, just, easily, effortlessly | (delete) |
| powerful, performant | (delete, or give the measurable property) |
| functionality | function, feature |
| enables you to, allows you to | you can |
| is designed to, aims to | (delete, say what it does) |
| gracefully handles | (say what it does: "retries three times, then stops") |
| out of the box | by default |
| under the hood | internally |
| blazingly fast | fast (give the number) |
| addresses the issue, tackles | corrects the fault, removes the error |
| and/or | Pick one, or write "X, or Y, or both" |
| e.g. / i.e. / etc. | for example / that is / (name the items) |

Already covered above and not repeated here: `leverage`, `utilize`, `in order to`, `due to the fact that`, `robust`, `comprehensive`, `seamless`, `delve`, `dive into` in Tier 1; `streamline`, `facilitate`, `plethora`, `myriad` in Tier 2; `state-of-the-art` in Tier 3.
