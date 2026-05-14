# human-copy eval checklist

## Criteria

1. Does the output identify and replace at least 3 specific banned vocabulary words from the Pass 1 list (delve, tapestry, vibrant, crucial, foster, landscape, meticulous, underscore, showcase, testament, etc.)? (Fails: accepting content with banned words intact. Fails: flagging words not on the list. Must cite the specific word found and its replacement.)
   - Source: SKILL.md Pass 1 Vocabulary Purge table. Wikipedia AI signs research + Kobak et al. (2024) excess vocabulary analysis. These are the strongest statistical signals.

2. Does the output catch and fix structural AI patterns - specifically the rule of three ("X, Y, and Z" triads), "not just X, but also Y" parallelisms, and "despite [challenges], [subject] continues to [positive]" conclusions? (Must flag at least one structural pattern if present in input.)
   - Source: SKILL.md Pass 2 Structural Pattern Removal. These are harder to catch than vocabulary but equally detectable by trained readers.

3. Does the output replace em dashes with single hyphens, and curly quotes with straight quotes? (Zero tolerance - every em dash and curly quote must be replaced. Fails if any remain in the output.)
   - Source: SKILL.md Pass 6 Em Dash and Formatting Purge. Em dashes are the highest-signal AI tell. Curly quotes are a ChatGPT signature.

4. Does the output restore simple copula constructions where AI inflated them? ("serves as" -> "is", "boasts" -> "has", "features" -> "has", "stands as" -> "is".) Must fix at least one copula inflation if present in input.
   - Source: SKILL.md Pass 3 Copula Restoration. AI avoids "is/are/has" and replaces with fancier alternatives.

5. Does the output vary sentence rhythm - no 5+ consecutive sentences of similar length (15-25 words)? (Must include at least one fragment or short punch sentence if the input was monotonous. Fails: uniform medium-length sentences throughout.)
   - Source: SKILL.md Pass 4 Sentence Rhythm Check. AI writes uniform medium-length sentences. Human writing mixes short and long.

6. Does the output inject specificity where the input was vague? (At least one instance of replacing an adjective with a number, metric, or concrete detail. "Premium materials" -> "1.2mm genuine split suede". Fails: leaving vague claims untouched.)
   - Source: SKILL.md Pass 5 Specificity Injection. Numbers beat adjectives. "Growing community" means nothing. "400 repeat buyers" means everything.

7. Does the final copy pass the "would a person say this out loud" test? (No textbook phrasing, no meta-commentary about the article itself, no "I hope this helps" artifacts, no "challenges and future outlook" sections.)
   - Source: SKILL.md Pass 7 The Human Test. Five-point check for artifacts that survive the mechanical passes.

## Test Inputs

- "Clean this product description: 'Heritage Brand Hats delves into the rich tapestry of western culture, showcasing vibrant designs that serve as a testament to meticulous craftsmanship. Additionally, the brand fosters a community of hat enthusiasts who navigate the evolving landscape of western fashion. It's not just a hat - it's a statement of who you are. Despite the challenges of competing with mass-market brands, HBH continues to grow its loyal customer base through innovative approaches and robust quality standards.'"
- "Human-check this blog intro: 'In today's rapidly evolving digital landscape, businesses must leverage cutting-edge AI tools to enhance their online presence. Furthermore, understanding the intricate interplay between search engine optimization and artificial intelligence is crucial for maintaining a competitive edge. This comprehensive guide delves into the pivotal role that AI-powered answer engines play in shaping the future of digital marketing, underscoring the need for a robust strategy that encompasses both traditional and innovative approaches.'"
- "Run human-copy on this email sequence opener: 'We are thrilled to welcome you to our vibrant community of forward-thinking entrepreneurs! Your decision to join showcases your commitment to fostering growth and navigating the challenges of building a business. Moreover, our meticulously crafted resources will help you cultivate the skills needed to garner success in today's competitive landscape. We look forward to embarking on this journey with you.'"
