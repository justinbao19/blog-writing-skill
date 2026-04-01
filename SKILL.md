---
name: blog-writing
version: 2.1.0
description: "Complete SEO blog article writing workflow: research → outline → write → optimize → review. Use for ALL blog content production. Covers keyword strategy, content structure, internal linking, AI writing avoidance, readability standards, and link verification. Works with content-production skill (mandatory review) and content-qa skill (QA agent)."
---

# SEO Blog Writing — Complete Workflow

## When to Use
- Writing any blog article (comparison, how-to, listicle, guide, thought piece)
- Creating long-form SEO content (2000+ words)
- Producing content for any website or blog

## Execution Model (IMPORTANT)

This skill requires running shell commands (Phase 5 link verification, Phase 6 QA runner). It **must** be executed in a context with full exec permissions.

**Always spawn the writing subagent with `security: "full"`:**
```
sessions_spawn(
  task: "[full article brief]",
  runtime: "subagent",
  security: "full"   ← REQUIRED — without this, exec approval gates block Phase 5 & 6
)
```

If running in main session directly (fallback only), exec permissions are already sufficient — proceed normally.

**Never spawn without `security: "full"` — the subagent will silently skip QA and deliver an unverified draft.**

## Pre-Flight
1. Read your product documentation for current facts
2. Read your brand guidelines for voice and red lines
3. Check your internal links map for linking targets
4. Check your content plan for where this article fits in the topic cluster

---

## Phase 1: Research (Before Writing)

### Keyword Research
1. **Primary keyword** — The exact phrase you want to rank for (e.g., "best project management tools 2026")
2. **Secondary keywords** — Related phrases to include naturally (3-5)
3. **Long-tail variants** — Question-form queries for FAQ section

### Competitive Analysis
For the primary keyword, search Google and analyze top 5 results:
- Word count of each
- H2/H3 structure
- What they cover that you should cover
- What they miss that you can fill (content gap)
- External links they use (authority sources)

Run QA analysis if you have the content-qa and seo-geo-qa skills installed:
```bash
# Via unified QA runner (recommended):
skills/content-qa/scripts/run_qa.sh path/to/draft.md --keyword "your primary keyword"

# Or call SEO analyzer directly:
python3 skills/seo-geo-qa/scripts/seo_qa_runner.py path/to/draft.md --config your-seo-config.json --keyword "your primary keyword"
```

Use the SERP gap analyzer for debugging specific competitive gaps:
```bash
python3 skills/seo-geo-qa/scripts/serp_gap_analyzer.py "your primary keyword" path/to/draft.md
python3 skills/seo-geo-qa/scripts/serp_gap_analyzer.py "your primary keyword" path/to/draft.md --urls https://competitor1.com https://competitor2.com
```

### Search Intent Classification
| Intent Type | Signal | Article Approach |
|-------------|--------|-----------------|
| Informational | "what is", "how to" | Definitive guide, answer-first |
| Comparison | "best", "vs", "alternatives" | Structured comparison, table-heavy |
| Commercial | "review", "pricing" | Detailed evaluation, honest pros/cons |
| Navigational | brand name | Product-focused, feature deep-dive |

### Output: Research Brief
Save to your planning directory before writing:
```markdown
## Research Brief: [Title]
- Primary keyword: 
- Secondary keywords: 
- Search intent: 
- Target word count: 
- Top 5 competitor URLs + word counts
- Content gaps to exploit
- Internal links to include
- External authority sources identified
```

---

## Phase 2: Outline

### Standard Article Structure
```
# H1 — Contains primary keyword, under 60 chars

Opening hook (150-200 words)
- Define the problem/question
- Why this matters now
- What this article covers

## Quick Comparison Table (for comparison articles)

## Detailed Reviews / Sections (bulk of article)
### H3 subsections as needed

## How We Tested / Methodology

## How to Choose / Decision Framework

## FAQ (4-6 questions, schema-markup ready)

## Further Reading (internal + external links)
```

### Heading Rules
- **One H1** per article, contains primary keyword
- **H2s** match search queries where possible
- **H3s** for subsections within H2s
- Never skip levels (H1 → H3 is wrong)
- Headings describe content, not for styling

---

## Phase 3: Write

### Opening (First 100 Words — Critical)
- Primary keyword appears in first 100 words
- Direct answer or clear hook (no throat-clearing)
- Set expectation for what reader will learn

### Body Writing Standards

**Word Count by Type:**
| Type | Minimum | Target |
|------|---------|--------|
| Comparison / Listicle | 2,500 | 3,000-3,500 |
| How-to Guide | 1,500 | 2,000-2,500 |
| Thought Piece | 1,000 | 1,500-2,000 |
| Product Comparison (vs) | 2,000 | 2,500-3,000 |

**Keyword Density:**
- Primary keyword: 1-2% (natural, never stuffed)
- Secondary keywords: 0.5-1% each
- Check: keyword should feel invisible to the reader

**Paragraph Structure:**
- Max 3-4 sentences per paragraph
- One idea per paragraph
- Short sentences mixed with longer ones
- Use bullet points and numbered lists for scanability

**Readability Target:**
- Flesch Reading Ease: 60-70 (standard/conversational)
- Grade level: 8-10 (accessible but not dumbed down)
- Sentence length: average 15-20 words, max 35

### Internal Linking Strategy

| Word Count | Internal Links Min | Target |
|-----------|:-----------------:|:------:|
| < 1500 | 2 | 3-5 |
| 1500-2500 | 3 | 5-8 |
| 2500-3500 | 5 | 8-12 |
| 3500+ | 7 | 10-15 |

- Link with descriptive anchor text (not "click here")
- Link to related blog posts in the same topic cluster
- Link to product/feature pages where natural
- Follow hub-spoke pattern from your internal links map
- Consult your internal linking strategy document

### External Linking Standards (Proportional)

| Content Type | External Links Min | Rationale |
|-------------|:-----------------:|-----------|
| Comparison / Best-of (8+ products) | 16-24 | Each product: official site + 1 authority source |
| Comparison / Best-of (5-7 products) | 12-18 | Same ratio |
| Alternatives page | 10-15 | Each alternative + authority sources |
| How-to guide | 5-10 | Claims need sources, fewer entities |
| Thought piece | 3-8 | Fewer claims, more perspective |

**The principle:** Every entity mentioned gets a link. Every factual claim gets a source. Don't link for the sake of linking.
- Prefer: official sites > media reviews > research papers
- Avoid: personal blogs, paywalled content, temporary pages
- Never link to competitors' comparison articles (link to their product page)
- **All links must be verified** (Phase 5)

### Authority Signals (GEO/AEO Optimization)
These boost visibility in AI search engines (ChatGPT, Perplexity, Google AI Overviews):

| Signal | Impact | How |
|--------|--------|-----|
| Statistics with sources | +37% | "According to [Source], X% of users..." |
| Quotations (expert quotes) | +30% | "As [Name], [Title] at [Company], notes..." |
| Authoritative tone | +25% | Write with demonstrated expertise, not hedge language |
| Authoritative citations | +40% | Link to research, not just claims |
| Clear definitions | +20% | Definition in first paragraph of each section |
| FAQ with schema | +30-40% | Natural Q&A format at bottom |
| "Last updated" date | +freshness | Include at bottom of article |

### Content Extractability (for AI Citation)
AI systems extract passages, not pages. Each key point should work standalone:
- Lead every section with a direct answer (don't bury it)
- Keep key answer passages to 40-60 words
- Tables beat prose for comparison content
- Numbered lists beat paragraphs for process content
- Self-contained answer blocks that work without surrounding context

### Comparison Article Specifics
For "Best X" / "X Alternatives" / "X vs Y" articles:
- **Always include a comparison table** at the top
- Each entry needs: Name, Price, Key Feature, Platforms, Best For
- **Be honest about competitors** — acknowledge strengths
- **Be honest about your product's weaknesses** — builds trust, ranks better
- Position your product appropriately based on real merits
- Include anchor IDs for each product section

---

## Phase 4: Optimize

### SEO Checklist (Before Review)
- [ ] H1 contains primary keyword, under 60 chars
- [ ] Meta description drafted: 150-160 chars, includes keyword
- [ ] Primary keyword in first 100 words
- [ ] Primary keyword in at least one H2
- [ ] URL slug is keyword-rich and clean
- [ ] At least one table or list (featured snippet opportunity)
- [ ] FAQ section present (schema markup ready)
- [ ] "Last updated: [Month Year]" at bottom
- [ ] Internal links ≥ 3
- [ ] External links ≥ 10
- [ ] All images have alt text (when applicable)

### AI Writing Pattern Avoidance

**CRITICAL: Content must not read like AI wrote it.**

Common AI patterns to eliminate:
| Pattern | Example | Fix |
|---------|---------|-----|
| Em-dash overuse | "The tool — which is powerful — works well" | Use commas or periods instead. Max 3 em-dashes per article. |
| "Delve into" | "Let's delve into the features" | "Here's what it does" / "Let's look at" |
| "Landscape" | "In today's software landscape" | Cut it. Be specific. |
| "Leverage" | "Leverage AI to improve" | "Use AI to improve" |
| "Tapestry/Mosaic" | "A rich tapestry of features" | Just describe the features. |
| "Revolutionize" | "Revolutionizing how you work" | "Changes how you work" |
| "Game-changer" | "This is a game-changer" | Say what it actually changes. |
| "Seamlessly" | "Seamlessly integrates" | "Integrates" or "works with" |
| "Robust" | "A robust set of features" | "A full set of features" or just list them. |
| "Elevate" | "Elevate your workflow experience" | "Improve" or describe the specific improvement. |
| "Navigate" (metaphor) | "Navigate your productivity challenges" | "Deal with" / "Handle" / "Manage" |
| "Harness" | "Harness the power of AI" | "Use AI to..." |
| "Paradigm" | "A paradigm shift" | Describe the actual change. |
| "Synergy" | "Create synergy between..." | "Works well with" or describe specifically. |
| "Holistic" | "A holistic approach" | "A complete approach" or be specific. |
| "At the end of the day" | Filler | Cut it. |
| "Without further ado" | "Without further ado, here's..." | Just start. |
| Triple-adjective stacking | "Powerful, intuitive, and elegant" | Pick one. Prove it. |
| Rhetorical questions | "But what if there was a better way?" | State the better way. |
| "In conclusion" / "In summary" | "In conclusion, X is the best" | Just make your point. |

**Self-check:** Read the article out loud. If any sentence sounds like a press release, rewrite it.

---

## Phase 5: Link Verification (MANDATORY)

**Never deliver content without verifying every link.**

### Process
1. Extract all URLs from the article
2. Test each with `web_fetch` or `curl -sI`
3. Check for: 404, 403, redirects to wrong content, paywalls
4. For non-obvious external sources, run a source-quality spot check

### Source Quality Spot Check
For external sources that are not obviously authoritative, check whether they are worth citing:
- **AITDK traffic page:** `https://aitdk.com/traffic/<domain>` for traffic / keyword / domain-age hints when accessible
- **Ahrefs Backlink Checker:** use as a quick proxy for domain strength / backlink profile
- **Search evidence:** `site:domain.com`, branded query, and recent indexed pages if third-party tools are blocked

Do **not** require perfect metrics. The goal is to catch weak, stale, spammy, or irrelevant sources before they land in the article.

### When Links Fail
- Search for alternative source supporting the same claim
- Prioritize: Official sites > Research > Major publications
- Update surrounding text if needed
- Document changes:
```markdown
**Original:** https://broken-link.com (404)
**Replacement:** https://working-link.com
**Reason:** Original returned 404
**Verified:** ✅ Same data confirmed
```

### Quote & Attribution Verification (CRITICAL)
- If citing a review → verify the quote exists AND the article's overall tone matches your framing
- **Tone match test:** Read the first 3 paragraphs of the source article. Is it positive, negative, or neutral?
  - Source is positive → quote freely
  - Source is negative → either don't quote, or frame honestly: "Even [Source]'s critical review acknowledged..."
  - Source is neutral → quote with accurate framing
- Don't pull positive fragments from negative reviews — readers click through and lose trust
- Statistics must match their cited source exactly (number, date, methodology)
- "According to [Source]" → verify Source actually says that

---

## Phase 6: Automated QA (MANDATORY — runs before human review)

**After completing Phase 5, ALWAYS run the QA runner before spawning a review agent or delivering the draft. Do not skip this. Do not ask whether to run it.**

If you have the content-qa skill installed:
```bash
skills/content-qa/scripts/run_qa.sh path/to/article.md --keyword "primary keyword"
```

### What happens automatically (if QA tools are available)
1. All links verified (liveness + source quality tiering)
2. Dead links, weak sources, moved links flagged
3. FAQ count, external link count, SERP gap checked
4. Markdown + JSON report saved
5. Verdict: PASS or FAIL

### If QA tools are not available
Manually verify:
- All external links work (no 404s, 403s, redirects to wrong content)
- Primary keyword appears in H1 and first 100 words
- Article meets minimum word count for its type
- FAQ section is present for comparison articles
- At least the minimum number of internal and external links

### If FAIL
- Fix critical issues (dead links, missing required elements)
- Re-run until PASS
- Max 3 rounds — if still failing, escalate with the report

### If PASS
- Proceed to Phase 7 (human review)
- Include the QA report link in the review handoff

---

## Phase 7: Review (Auto-Spawn)

If you have the content-production skill, always spawn a review agent after Phase 6 passes. The review agent should use content-qa skill checklist if available.

**Review must check:**
- QA runner verdict is PASS (if available) or manual verification complete
- SEO checklist complete
- Brand voice compliance
- Factual accuracy (pricing, features)
- AI writing patterns eliminated
- Readability standards met

---

## File Conventions

### Where to Save
Adapt these paths to your project structure:
- Research briefs: `blog/plan/brief-{slug}.md` 
- Article drafts: `blog/seo/{slug}.md` or `blog/{slug}.md`
- Article images: handled in website repo, not workspace

### Slug Format
- Lowercase, hyphen-separated
- Match target URL path: `/blog/{slug}`

### Title Year Rules

| Article Type | Include Year? | Reason |
|-------------|:----------:|------|
| **Comparison** (best X, X alternatives) | ✅ Yes | Year is part of search keywords ("best tools 2026") |
| **Educational / How-to** | ❌ No | Search intent is evergreen, year limits article lifespan |
| **Problem/scenario** | ❌ No | Same as above |
| **Feature announcement** | ❌ No | Features aren't searched by year |
| **Thought pieces** | ❌ No | Same as above |

- Educational articles use freshness signals at bottom: "Last updated: [Month Year]"
- Comparison articles update year + content annually in Q1
- Focus on content freshness signals rather than title years for evergreen content

---

## Related Skills
These OpenClaw skills work well with blog-writing:
- `content-production` — Produce → review → revise workflow
- `content-qa` — QA checklist and review agent  
- `seo-audit` — Technical SEO checks for the whole site
- `seo-geo` — GEO optimization for AI search engines
- `competitor-alternatives` — Comparison page structure
- `schema-markup` — JSON-LD implementation
- `copy-editing` — Multi-pass editing framework