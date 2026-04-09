# seo-blog-writer

> Zero-friction SEO article writer. Provide a topic + domain — the skill auto-discovers product context, researches keywords, analyzes competitors, writes the article, verifies all links, and delivers publication-ready content. Works for any site, any industry, any CMS.

---

## English

### What It Does

`seo-blog-writer` is a fully automated 5-phase SEO content production skill. Give it a topic and a domain — it figures out the rest.

**Phases:**
0. **Context Discovery** — crawls your site to auto-detect product, brand voice, existing content, and competitors. One human confirmation gate before writing starts.
1. **Research Brief** — keyword intelligence, competitive gap analysis, linking strategy, article blueprint
2. **Content Generation** — writes the full article with verified statistics, proper structure, and integrated links
3. **AI Pattern Prevention** — scans for and eliminates AI writing tells, aligns with detected brand voice
4. **Quality Assurance** — multi-dimensional scoring (SEO / Content / Linking / Brand), link verification, factual accuracy checks
5. **Delivery Package** — final article + schema markup + QA report + promotion checklist

### Key Features

- **Zero hardcoded dependencies** — works for any site, any industry, any CMS
- **Minimum viable input** — just `topic` + `domain` to start
- **Three modes** — Express (5-10min), Standard (15-20min), Expert (25-35min)
- **One human checkpoint** — confirms keyword, structure, and plan before a single word is written
- **Verified claims only** — every statistic and quote is confirmed against source before inclusion
- **GEO/AEO optimized** — structured for AI search citation (ChatGPT, Perplexity, Google AI Overviews, Claude)
- **AI pattern blocklist** — eliminates 20+ AI writing tells automatically
- **Full link verification** — every URL tested, dead links replaced with alternatives
- **Schema markup** — auto-generates Article + FAQPage JSON-LD

### Requirements

- [OpenClaw](https://openclaw.ai) installed and configured
- No additional paid tools required — uses built-in `web_search` and `web_fetch`

### Installation

```bash
# Via ClaWHub (recommended)
clawhub install seo-blog-writer

# Or manually
cp SKILL.md ~/.openclaw/workspace/skills/seo-blog-writer/SKILL.md
```

### Usage

**Minimum input:**
```
Write a blog article about "best email apps for productivity 2026" for https://yoursite.com
```

**With options:**
```
Write an SEO article:
- topic: "gmail alternatives for privacy-conscious users"
- domain: "https://yoursite.com"
- mode: "expert"
- product_context: "docs/product-brief.md"   ← skip auto-discovery
```

**Important — always spawn the writing sub-agent with `security: "full"`:**
```
sessions_spawn(
  task: "Write a blog article about [topic] for [domain]",
  runtime: "subagent",
  security: "full"
)
```

> Without `security: "full"`, exec approval gates will block the QA phase. The sub-agent will silently skip verification and deliver an unverified draft.

### Modes

| Mode | Time | Quality Target | Best For |
|------|------|---------------|----------|
| **Express** | 5-10 min | 65+ score | Quick turnaround |
| **Standard** | 15-20 min | 75+ score | Most articles |
| **Expert** | 25-35 min | 85+ score | High-stakes keywords |

### Output

```
seo-output/{article-slug}/
├── article.md                 ← Final article with frontmatter
├── qa-report.md               ← Score breakdown + link verification
├── schema-markup.json         ← JSON-LD for CMS integration
├── research-brief.md          ← Research + competitive analysis (Standard+)
├── promotion-checklist.md     ← Post-publish marketing tasks (Standard+)
├── internal-links-strategy.md ← Hub-spoke linking plan (Expert only)
└── optimization-opportunities.md ← Future enhancements (Expert only)
```

### Failure Recovery

Built-in resilience for common failure scenarios:
- JS-heavy sites that block crawling → questionnaire fallback
- Competitors that block fetching → search snippet proxy
- Low keyword confidence → presents alternatives at confirmation gate
- Failed link verification → auto-searches for replacement sources
- QA score below threshold → specific improvement roadmap

---

## 中文

### 这个 Skill 做什么

`seo-blog-writer` 是一个全自动 5 阶段 SEO 内容生产 Skill。提供一个话题和域名，它自动处理其余一切。

**5 个阶段：**
0. **上下文发现** — 爬取你的站点，自动检测产品信息、品牌语气、现有内容和竞品。写作开始前唯一一次人工确认。
1. **调研摘要** — 关键词洞察、竞品差距分析、链接策略、文章蓝图
2. **内容生成** — 用已验证的数据、正确结构和集成链接写完整文章
3. **AI 模式清除** — 扫描并消除 AI 写作特征词，对齐检测到的品牌语气
4. **质量保证** — 多维度评分（SEO / 内容 / 链接 / 品牌），链接验证，事实准确性检查
5. **交付包** — 最终文章 + Schema 标记 + QA 报告 + 推广 checklist

### 核心特性

- **零硬编码依赖** — 适用于任何站点、任何行业、任何 CMS
- **最小输入** — 只需 `topic` + `domain` 即可开始
- **三种模式** — 快速（5-10分钟）、标准（15-20分钟）、专家（25-35分钟）
- **唯一人工确认节点** — 在写第一个字之前确认关键词、结构和计划
- **仅包含已验证声明** — 每条数据和引用都在纳入前经过来源确认
- **GEO/AEO 优化** — 针对 AI 搜索引用结构化（ChatGPT、Perplexity、Google AI Overviews、Claude）
- **AI 写作模式黑名单** — 自动消除 20+ 个 AI 特征词
- **完整链接验证** — 测试每一条 URL，用替代来源替换死链
- **Schema 标记** — 自动生成 Article + FAQPage JSON-LD

### 依赖

- 已安装并配置 [OpenClaw](https://openclaw.ai)
- 无需额外付费工具 — 使用内置的 `web_search` 和 `web_fetch`

### 安装

```bash
# 通过 ClaWHub 安装（推荐）
clawhub install seo-blog-writer

# 或手动安装
cp SKILL.md ~/.openclaw/workspace/skills/seo-blog-writer/SKILL.md
```

### 使用方法

**最小输入：**
```
为 https://yoursite.com 写一篇关于"2026年最佳效率邮件应用"的博客文章
```

**带选项：**
```
写一篇 SEO 文章：
- topic: "注重隐私用户的 Gmail 替代品"
- domain: "https://yoursite.com"
- mode: "expert"
- product_context: "docs/product-brief.md"   ← 跳过自动发现
```

**重要 — 必须用 `security: "full"` 派生写作 Sub-agent：**
```
sessions_spawn(
  task: "为 [domain] 写一篇关于 [topic] 的博客文章",
  runtime: "subagent",
  security: "full"
)
```

> 不带 `security: "full"` 的话，exec 审批门会阻塞 QA 阶段。Sub-agent 会静默跳过验证，交付未验证的草稿。

---

## File Structure

```
blog-writing-skill/
├── README.md     ← This file (EN + ZH)
└── SKILL.md      ← The skill definition v2.2.0 (OpenClaw reads this)
```

## License

MIT

## Related Skills

| Skill | Purpose |
|-------|---------|
| `seo-geo` | GEO optimization for AI search engines |
| `content-qa` | Additional QA workflows |
| `competitor-alternatives` | Specialized comparison page structures |
| `programmatic-seo` | Scale across multiple pages |
| `copy-editing` | Detailed editing and refinement |

---

*Built for the OpenClaw AI agent ecosystem. Zero hardcoded dependencies — works for any site, any industry, any CMS.*