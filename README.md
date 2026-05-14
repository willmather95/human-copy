# human-copy

A filter that strips AI fingerprints from your writing before you publish. Drop it into any LLM workflow.

## The fingerprint

Modern AI writing has a predictable signature. Expert annotators misclassify just 1 in 300 AI-generated articles ([Russell, Karpinska & Iyyer, 2025](https://arxiv.org/abs/2501.15654)). The tells:

- **Vocabulary:** "delve", "tapestry", "leverage", "robust", "seamless", "comprehensive", "vibrant". 100+ flagged terms across a 3-tier sensitivity model.
- **Structural patterns:** rule-of-three triads, "not just X, but also Y" parallelisms, "despite challenges, X continues to grow" conclusions.
- **Copula avoidance:** "serves as" instead of "is", "boasts" instead of "has".
- **Em dashes.** The single highest-signal tell.
- **Generic conclusions** about "the evolving landscape" of any topic.

If your content has these, trained readers (and detection tools) clock it as AI before they read the substance. Authority gone before sentence one.

## What this does

7 passes. Every piece of written content runs through them before it goes live:

1. **Vocabulary purge.** 3-tier word list. Tier 1 always fires. Tier 2/3 fire on density.
2. **Structural pattern removal.** Kills triads, negative parallelisms, "despite" conclusions, superficial-analysis participles.
3. **Copula restoration.** "serves as" becomes "is". "boasts" becomes "has".
4. **Sentence rhythm check.** No 5+ monotone sentences in a row. Fragments allowed. One-word paragraphs allowed.
5. **Specificity injection.** Adjectives become numbers. "Premium materials" becomes "1.2mm split suede".
6. **Em dash and formatting purge.** Zero tolerance. Curly quotes to straight. No leftover markdown.
7. **The human test.** Read it aloud. Does a person actually say this?

Output: a structured 4-section audit (flags table, rewrite, change summary, second-pass scan).

## Before / after

A typical AI-generated business intro:

**Before** (80 words):

> In today's rapidly evolving digital landscape, organizations must leverage cutting-edge AI tools to enhance their competitive positioning. Furthermore, understanding the intricate interplay between automation and human creativity is crucial for fostering sustainable growth. This comprehensive guide delves into the pivotal role that AI-powered platforms play in reshaping the future of modern enterprise, underscoring the need for a robust strategy that encompasses both traditional and innovative approaches. Despite the challenges of digital transformation, forward-thinking organizations continue to garner significant value by embracing these groundbreaking technologies.

`12+ AI tells. 80 words. 0 specific claims.`

**After** (43 words):

> AI tools are competitive table stakes now. Companies that embrace them are pulling ahead. The catch: "embracing AI" isn't a strategy deck. It's one person picking one workflow per quarter and rebuilding it with AI. Strategy is cheap. The doing is the work.

`0 AI tells. 43 words. Same point as the Before, said by a human.`

The first reads like a corporate blog post nobody finishes. The second reads like a real person who's seen this play out.

## Use it

Platform-neutral. Works anywhere you can give an LLM persistent instructions.

**Claude Code (skill):**

```bash
git clone https://github.com/willmather95/human-copy.git ~/.claude/skills/human-copy
```

The target path must not already exist. Then in any Claude Code session: `/human-copy`, or activate via triggers like "does this sound AI", "human check", "AI slop check", "clean the copy", "flag without rewriting", "sound human".

**Claude.ai (Projects or custom skills):**

Paste the body of `SKILL.md` into your Project's custom instructions or a custom skill. Same trigger phrases work.

**Gemini (Gems):**

Create a custom Gem. Paste the body of `SKILL.md` into the Gem's **Instructions** field. Note: if it exceeds the instruction-length limit, paste the load-bearing core (the 7 passes + the Tier 1 vocabulary table) instead of the full file. Send content with "human check this" or "audit this for AI tells".

**Codex (or any agentic CLI):**

Drop `SKILL.md` into your agent's instructions file (`AGENTS.md`, `.codex/instructions.md`, or whatever your tool reads). Reference it when running passes.

**Plain LLM chat (ChatGPT, Claude, Gemini, etc.):**

Paste the body of `SKILL.md` as a system prompt or first message. Then paste your content and ask it to run the 7 passes.

## Modes

- **Rewrite (default).** Runs all 7 passes. Outputs cleaned copy plus the structured audit.
- **Detect.** Flags AI patterns with severity ratings, no rewrite. Trigger: `--detect` or "flag without rewriting".

## Sources

- Wikipedia, [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing). Community-maintained.
- Kobak et al. (2024), [Delving into LLM-assisted writing in biomedical publications through excess vocabulary](https://arxiv.org/abs/2406.07016).
- Russell, Karpinska & Iyyer (2025), [People who frequently use ChatGPT for writing tasks are accurate detectors of AI-generated text](https://arxiv.org/abs/2501.15654).

## The standard

If a trained reader would flag your text as AI-generated, it fails the gate. Rewrite until it passes.

## License

MIT. Fork it.

## Credit

Built from my own writing workflow.

Will Mather
