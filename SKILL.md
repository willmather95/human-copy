---
name: human-copy
description: Strip detectable AI patterns from written content. Catches vocabulary tells, structural patterns, promotional language, and stylistic tics that flag text as machine-generated. Based on Wikipedia's AI signs research + academic studies on LLM detection. Use when the user says 'does this sound AI', 'human check', 'AI slop check', 'clean the copy', 'flag without rewriting' (detect mode), or 'sound human'. Mandatory gate after any content generation (ads, copy, emails, social, blog posts) and before publishing anything live.
triggers:
  - "does this sound AI"
  - "human check"
  - "AI slop check"
  - "clean the copy"
  - "flag without rewriting"
  - "sound human"
  - "detect AI patterns"
  - "remove AI tells"
---

# Human Copy Gate

Every piece of written content passes through this gate before publishing. No exceptions. Blog posts, email sequences, landing page copy, social content, ad scripts - all of it.

This is not about "making it sound human." It's about eliminating the specific, documented patterns that trained readers and detection tools use to identify AI-generated text.

## Modes

- **Rewrite (default):** Run 7 passes + output structured audit (4 sections). Produces cleaned copy.
- **Detect:** Flag patterns with quoted text, tier, and severity. No rewrite. Triggers: `/human-copy --detect`, "flag without rewriting", "audit this content", "scan for AI tells without changing it". Use when auditing client content, when patterns might be intentional, or when you want a quick scan without alteration.

## When to Run

- After any content-generation step: ad copy, email copy, sales pages, blog posts, social posts, landing pages, newsletters
- After any blog post, article, or long-form content
- After repurposing or atomizing content (atomized output inherits parent patterns)
- Before publishing anything to a live site

## The 7 Passes

Run all 7 passes on the content. Fix every violation. No "this one's fine" exceptions.

### Pass 1: Vocabulary Purge (3-Tier Sensitivity)

Tiered flagging reduces over-correction. Tier 1 fires always. Tier 2 fires only when 2+ words cluster in the same paragraph. Tier 3 fires only at high density (3+ per 100 words).

**TIER 1 - Always flag and replace. Validated against real production usage.**

| AI Word | Replace With |
|---------|-------------|
| delve/delving | dig into, explore, look at, examine |
| tapestry (figurative) | DELETE - say what you mean |
| vibrant | DELETE or use a specific descriptor |
| crucial/pivotal/vital | important, or DELETE if the sentence works without it |
| foster/fostering | build, create, grow, start |
| landscape (figurative) | scene, market, space, world |
| meticulous/meticulously | careful, precise, obsessive |
| underscore (verb) | show, prove, reveal, make clear |
| showcase/showcasing | show, display, demonstrate |
| testament (figurative) | proof, evidence, sign |
| intricate/intricacies | complex, detailed, layered |
| garner | get, earn, win, attract |
| groundbreaking | new, first |
| renowned | famous, well-known, respected |
| leverage (verb) | use |
| utilize | use |
| boasts | has |
| nestled | DELETE - travel brochure language |
| Additionally (starting a sentence) | Also, And, Plus, or just start the next sentence |
| Furthermore | DELETE - just continue |
| Moreover | DELETE - just continue |
| Notably | DELETE |
| In conclusion / In summary / Overall | DELETE - just end |
| It is worth noting | DELETE |

**TIER 2 - Flag when 2+ cluster in the same paragraph. Single use may be intentional.**

| AI Word | Replace With |
|---------|-------------|
| bolstered | strengthened, backed, supported |
| enhance/enhancing | improve, sharpen, strengthen |
| enduring | lasting, permanent, long-running |
| interplay | relationship, connection, tension |
| align with | match, fit, support |
| encompassing | covering, including |
| navigate (figurative) | handle, deal with, manage |
| facilitate | help, enable, make possible |
| comprehensive | thorough, complete, full |
| robust | strong, solid, reliable |
| innovative | new, original, clever |
| resonate/resonating | connect, hit home, land |
| embody/embodying | represent, show, be |
| cultivate/cultivating | build, grow, develop |
| seamless/seamlessly | smooth, clean, or DELETE |
| streamline/streamlined | simplify, speed up |
| empower/empowering | enable, help, give |
| holistic | whole, full, end-to-end |
| strategic | planned, deliberate, or DELETE |
| dynamic (adj) | specific descriptor or DELETE |
| transformative | big, major, or DELETE |
| revolutionary | new, first, or DELETE |
| paradigm shift | big change |
| synergy/synergize | fit, work together |
| holistic approach | full picture |
| endeavor (noun) | effort, project, try |
| commence | start |
| ascertain | find out, check |
| myriad | many, or a specific number |
| plethora | many, or a specific number |
| pivotal | important |
| quintessential | classic, typical |
| multifaceted | layered, many-sided |
| paramount | most important, top |
| imperative | must, critical |
| unwavering | steady, firm, constant |
| invaluable | very useful, rare |
| arguably | DELETE - pick a side |
| aforementioned | this, that (already named) |

**TIER 3 - Flag ONLY at high density (3+ instances per 100 words). Common words that over-index in AI.**

| AI Word | Replace With |
|---------|-------------|
| important | specific reason, or DELETE |
| significant | specific magnitude, or DELETE |
| various | list them, or DELETE |
| many | specific number, or DELETE |
| often | specific frequency, or DELETE |
| typically | specific case, or DELETE |
| generally | specific case, or DELETE |
| particularly | DELETE or specific |
| especially | DELETE or specific |
| essentially | DELETE |
| ultimately | DELETE |
| fundamentally | DELETE |
| effectively | DELETE |
| potentially | DELETE |
| increasingly | specific trend, or DELETE |
| thereby | so, which |
| whereas | but, while |
| hence | so |
| thus | so |
| indeed | DELETE |
| furthermore | DELETE (also Tier 1 sentence-start) |
| nonetheless | but, still |
| moreover | DELETE |
| consequently | so |
| accordingly | so |
| evidently | DELETE |
| certainly | DELETE |
| undoubtedly | DELETE |
| inherently | DELETE |
| profoundly | specific magnitude |
| considerably | specific magnitude |
| substantially | specific magnitude |
| relatively | DELETE |
| virtually | almost |

**Context-dependent - check each use:**

| Word | OK When | Kill When |
|------|---------|-----------|
| serves as | Technical description | Replacing "is" for no reason |
| stands as | Physical standing | Figurative ("stands as a symbol") |
| reflects | Literal reflection | "reflects broader trends" |
| highlights | You're literally highlighting | "highlights the importance of" |
| represents | Data/statistics | "represents a shift in" |
| commitment to | Contractual/legal | "commitment to excellence" |
| boasts | Never OK | Always |
| nestled | Never | Always - travel brochure language |
| in the heart of | Geographic accuracy | Figurative ("in the heart of the community") |

### Pass 2: Structural Pattern Removal

**Kill the rule of three.** AI defaults to "X, Y, and Z" triads constantly. If you see three adjectives, three examples, or three parallel phrases, break the pattern. Use two. Or four. Or one strong one.

Before: "Heritage, craftsmanship, and authenticity define the brand."
After: "Craftsmanship defines the brand."

**Kill negative parallelisms.** "Not just X, but also Y" and "It's not about X - it's about Y" are AI signatures.

Before: "It's not just a hat - it's a statement of who you are."
After: "It's a hat that says something."

**Kill "despite" conclusions.** "Despite [challenges], [subject] continues to [positive outcome]" is the most common AI article ending.

Before: "Despite the challenges of competing with mass-market brands, HBH continues to grow its loyal customer base."
After: DELETE the whole paragraph. End on something specific.

**Kill superficial analysis phrases.** Present participle phrases that add fake depth:

- "...highlighting the importance of..."
- "...underscoring the need for..."
- "...emphasizing the role of..."
- "...reflecting broader trends in..."
- "...contributing to the ongoing..."
- "...symbolizing the enduring..."
- "...marking a significant shift..."
- "...setting the stage for..."
- "...shaping the future of..."

DELETE all of these. If the point matters, make it a sentence. If it doesn't, cut it.

**Kill legacy/significance inflation.** Phrases that puff up importance:

- "pivotal moment in the history of"
- "indelible mark on"
- "deeply rooted in"
- "rich cultural heritage"
- "enduring legacy"
- "plays a vital role in"
- "key turning point"
- "evolving landscape"
- "focal point of"

### Pass 3: Copula Restoration

AI avoids simple "is/are/has" constructions. It replaces them with fancier alternatives. Reverse this.

| AI Construction | Human Construction |
|----------------|-------------------|
| serves as | is |
| stands as | is |
| functions as | is |
| represents | is |
| marks | is |
| features | has |
| offers | has, gives |
| boasts | has |
| holds the distinction of being | is |
| remains | is (usually) |

Before: "The snapback serves as a bridge between western heritage and modern street style."
After: "The snapback is western heritage made for the street."

### Pass 4: Sentence Rhythm Check

AI writes in uniform medium-length sentences. Human writing has rhythm - short punchy sentences mixed with longer flowing ones. Check for:

**Monotonous length.** If 5+ consecutive sentences are similar length (15-25 words each), break the pattern. Add a 3-word sentence. Or a 40-word one.

**Missing fragments.** Real human writing uses fragments for emphasis. "Built different." "No shortcuts." "Period." AI almost never generates fragments.

**Missing one-word paragraphs.** Sometimes a single word is the paragraph. AI doesn't do this.

**Every sentence starts with subject-verb.** AI defaults to "The [noun] [verb]..." pattern. Mix it up. Start with a time reference, a prepositional phrase, an action.

Before: "The hat is made from genuine suede. The brim develops a natural patina over time. The construction uses heavyweight materials."
After: "Genuine suede. That's the brim. Over time it develops a patina - gets softer, richer, more yours. The kind of hat that doesn't wear out. It wears in."

### Pass 5: Specificity Injection

AI generalizes. Humans specify. Every claim should pass the "like what?" test. If a reader would ask "like what?" after your sentence, you failed.

Before: "HBH uses premium materials in all their products."
After: "The suede on an HBH brim is 1.2mm genuine split - thick enough to hold shape, thin enough to curve how you want it."

Before: "The brand has a growing community of loyal customers."
After: "400 people keep coming back. Some are on their third hat."

**Numbers beat adjectives.** "Premium" means nothing. "1.2mm genuine split suede" means everything. "Growing" means nothing. "400 repeat buyers" means everything.

### Pass 6: Em Dash and Formatting Purge

**Em dashes.** Replace every em dash with a single hyphen, a period, or restructure the sentence. AI overuses em dashes for dramatic pauses and parenthetical insertions. This is the single highest-signal tell.

**Curly quotes.** Replace all curly quotation marks ("" '') with straight quotes ("" ''). Curly quotes are a ChatGPT signature.

**Excessive boldface.** Remove bold from body copy unless it's a term being defined for the first time. AI bolds key phrases like a PowerPoint deck.

**Title case in headings.** Use sentence case. "How suede ages" not "How Suede Ages."

**Markdown artifacts.** Remove any `**bold**`, `*italic*`, `###`, or backtick formatting that leaked from AI output.

### Pass 7: The Human Test

Read the final copy and check:

1. **Would a person actually say this out loud?** Read it aloud. If you stumble or it sounds like a textbook, rewrite.

2. **Does every paragraph earn its place?** If you can delete a paragraph and nothing is lost, delete it. AI pads content. Humans write tight.

3. **Is there a single original observation?** Something specific, unexpected, or opinionated that no AI would generate. A detail from the founder's experience. A customer quote. A number nobody else publishes. If every sentence could appear in a generic article on the same topic, it's AI slop.

4. **Does it have an opinion?** AI hedges. "Some prefer X, while others prefer Y." Humans pick a side. "X is better. Here's why."

5. **Are there any "I hope this helps" artifacts?** Collaborative phrasing, meta-commentary about the article itself, disclaimers about limitations, or sign-off language.

6. **Is there a "challenges and future outlook" section?** Delete it. Write a specific ending about what's next, or just end.

## Project-Specific Voice Overlay (optional)

After the 7 passes, if a project-specific voice or tone guide exists, apply it on top of the cleaned base. The 7 passes produce text free of AI signatures; a voice overlay adds personality, vocabulary preferences, and tone on top of that clean substrate.

## Quick Reference Card

For fast editing, scan for these instant-kill patterns:

```
CTRL+F these phrases - if found, rewrite:

"serves as a"
"stands as a"
"testament to"
"rich tapestry"
"vibrant community"
"plays a crucial role"
"in the heart of"
"it's important to note"
"despite these challenges"
"not just X, but also Y"
"highlighting the importance"
"underscoring the need"
"reflecting broader trends"
"commitment to excellence"
"In summary"
"In conclusion"
"Overall"
"Additionally,"  (starting a sentence)
"Furthermore,"
"Moreover,"
"Notably,"
"It is worth noting"
```

## Structured Audit Output

Every run (Rewrite or Detect) outputs 4 sections in this order. Makes review scannable.

### Section 1 - Flags

Table of every pattern caught. One row per flag.

| # | Quoted Text | Pattern Category | Tier | Severity |
|---|-------------|------------------|------|----------|
| 1 | "serves as a bridge" | Copula avoidance | Tier 1 | High |
| 2 | "robust framework" | Vocabulary cluster | Tier 2 | Medium |

Pattern categories: Vocabulary (Tier 1/2/3), Copula avoidance, Rule of three, Negative parallelism, Despite-conclusion, Superficial analysis phrase, Significance inflation, Rhythm uniformity, Missing fragments, Em dash, Formatting artifact, Chatbot opener, Generic conclusion.

Severity: High (must fix) / Medium (fix if easy) / Low (judgment call).

### Section 2 - Rewrite (Rewrite mode only)

Clean version of the full text. For Detect mode, this section is skipped.

### Section 3 - Change Summary (Rewrite mode only)

Bullet list: what was cut, what was swapped, what was restructured, word count delta.

### Section 4 - Second-Pass Audit

Re-scan the rewrite (or original in Detect mode). Flag any AI patterns that survived the first edit. Common survivors: recycled transitions, lingering inflation ("significant"), copula swaps that snuck through ("remains", "holds"). If clean, note: "Second pass clean."

**For Detect mode:** Section 4 is the primary signal. It shows which flags from Section 1 are judgment calls vs. hard problems.

## Grading (Diagnostic Scale)

- **A** = Caught real AI patterns, copy reads human after fixes
- **B** = Caught some patterns, missed others, or over-corrected (made it stilted)
- **C** = Missed obvious AI tells, or copy still reads as AI after the pass

## Chain Position

- Fires AFTER any content creation skill
- Fires BEFORE publishing, deploying, or sharing content
- Can run independently on any text: `/human-copy [paste text or file path]`
- Chains: content skill -> human-copy -> publish

## Sources

Based on:
- Wikipedia's "Signs of AI writing" (community-maintained)
- Kobak et al. (2024) "Delving into LLM-assisted writing" - excess vocabulary analysis
- Juzek & Ward (2025) "Why Does ChatGPT Delve So Much?" - lexical overrepresentation
- Reinhart et al. (2025) "Do LLMs write like humans?" - grammatical/rhetorical style variation
- Russell, Karpinska & Iyyer (2025) - detection accuracy by LLM familiarity
- Author's writing rules: no em dashes, short declarative sentences, Altman-style

## The Standard

If a trained reader would flag this text as AI-generated, it fails the gate. Rewrite until it passes.
