# blog-writing — OpenClaw SEO Blog Writing Skill

> An OpenClaw skill for producing publication-ready SEO blog articles end-to-end: research → outline → write → optimize → QA → review.

---

## English

### What It Does

`blog-writing` is a structured 7-phase workflow skill for AI-assisted SEO content production. It covers everything from keyword research to automated QA — and enforces quality gates before any draft is handed off for human review.

**Phases:**
1. **Research** — keyword analysis, competitive SERP review, search intent classification
2. **Outline** — structured heading hierarchy, FAQ planning, internal link targets
3. **Write** — body content following readability, keyword density, and brand voice standards
4. **Optimize** — SEO checklist, AI writing pattern elimination, GEO/AEO authority signals
5. **Link Verification** *(mandatory)* — every URL tested, dead/moved links replaced, source quality tiered
6. **Automated QA** *(mandatory)* — runs content-qa skill's QA runner if available, produces a pass/fail report
7. **Review** — spawns a review sub-agent against the QA-passed draft

### Key Features

- **Comparison table standard** — required for all best-of / alternatives articles
- **External link proportionality** — 12–18 links for 5–7 product comparisons, 16–24 for 8+
- **AI pattern blocklist** — eliminates "delve", "leverage", "seamlessly", em-dash overuse, and 20+ other AI tells
- **GEO/AEO optimization** — statistics with sources, expert citations, self-contained answer blocks for AI search engines
- **Year-in-title rules** — comparison articles get years; evergreen how-to articles don't
- **Automated QA runner** — shell-based when available, produces Markdown + JSON reports, PASS/FAIL verdict

### Requirements

- [OpenClaw](https://openclaw.ai) installed and configured
- Optional but recommended: [`content-qa`](https://clawhub.ai) skill for automated QA
- Optional but recommended: [`seo-geo-qa`](https://clawhub.ai) skill for technical SEO analysis
- Your own SEO config file if using automated QA tools

### Installation

```bash
# Via ClaWHub (recommended)
clawhub install blog-writing

# Or manually — copy SKILL.md into your OpenClaw workspace skills folder
cp SKILL.md ~/.openclaw/workspace/skills/blog-writing/SKILL.md
```

### Usage

Trigger this skill by asking your OpenClaw agent to write a blog article. The agent reads `SKILL.md` and follows the full phase sequence automatically.

**Important — always spawn the writing sub-agent with `security: "full"`:**

```
sessions_spawn(
  task: "Write a blog article about [topic] targeting keyword [keyword]",
  runtime: "subagent",
  security: "full"
)
```

> Without `security: "full"`, exec approval gates will block Phase 5 (link verification) and Phase 6 (QA runner). The sub-agent will silently skip both and deliver an unverified draft.

### Output

- Draft saved to your configured blog directory (e.g., `blog/seo/{slug}.md`)
- QA report saved to your configured reports directory (if QA tools available)
- Cross-links added to related existing articles

### Customization

Edit `SKILL.md` to adapt:
- Word count targets per article type
- Internal/external link thresholds
- Blocked AI writing patterns list
- File paths for your project structure
- QA configuration paths

---

## 中文

### 这个 Skill 做什么

`blog-writing` 是一个结构化的 7 阶段工作流 Skill，用于 AI 辅助 SEO 内容生产。覆盖从关键词调研到自动化 QA 的完整流程，并在交付人工审核前强制执行质量门控。

**7 个阶段：**
1. **调研** — 关键词分析、竞品 SERP 研究、搜索意图分类
2. **大纲** — 标题层级结构、FAQ 规划、内链目标规划
3. **写作** — 按可读性、关键词密度、品牌语气标准撰写正文
4. **优化** — SEO checklist、消除 AI 写作模式、GEO/AEO 权威信号
5. **链接验证**（强制）— 测试每一条 URL，替换死链/跳转链接，来源质量分级
6. **自动化 QA**（强制）— 如果有 content-qa skill，运行 QA runner，生成通过/失败报告
7. **审核** — 对通过 QA 的草稿派生一个审核 Sub-agent

### 核心特性

- **比较表标准** — 所有 best-of / alternatives 类文章必须包含比较表
- **外链比例规范** — 5-7 个产品对比需 12-18 条外链，8 个以上需 16-24 条
- **AI 写作模式黑名单** — 消除 "delve"、"leverage"、"seamlessly"、em-dash 滥用等 20+ 个 AI 特征词
- **GEO/AEO 优化** — 带来源的数据统计、专家引用、独立可被 AI 搜索引擎提取的答案块
- **标题年份规则** — 比较类文章带年份，常青型 how-to 文章不带
- **自动化 QA runner** — 如有工具则基于 Shell 脚本，输出 Markdown + JSON 报告，PASS/FAIL 判定

### 依赖

- 已安装并配置 [OpenClaw](https://openclaw.ai)
- 可选推荐：[`content-qa`](https://clawhub.ai) skill（提供自动化 QA）
- 可选推荐：[`seo-geo-qa`](https://clawhub.ai) skill（提供技术 SEO 分析）
- 如使用自动化 QA 工具，需要你自己的 SEO 配置文件

### 安装

```bash
# 通过 ClaWHub 安装（推荐）
clawhub install blog-writing

# 或手动安装 — 将 SKILL.md 复制到你的 OpenClaw workspace skills 目录
cp SKILL.md ~/.openclaw/workspace/skills/blog-writing/SKILL.md
```

### 使用方法

让你的 OpenClaw agent 写博客文章即可触发此 Skill。Agent 会读取 `SKILL.md` 并自动按完整阶段顺序执行。

**重要 — 必须用 `security: "full"` 派生写作 Sub-agent：**

```
sessions_spawn(
  task: "写一篇关于 [主题] 的博客文章，目标关键词 [关键词]",
  runtime: "subagent",
  security: "full"
)
```

> 不带 `security: "full"` 的话，exec 审批门会阻塞第 5 阶段（链接验证）和第 6 阶段（QA runner）。Sub-agent 会静默跳过这两个阶段，交付一个未验证的草稿。

### 输出产物

- 草稿保存至你配置的博客目录（如 `blog/seo/{slug}.md`）
- QA 报告保存至你配置的报告目录（如有 QA 工具）
- 自动在相关已有文章中添加交叉链接

### 自定义

编辑 `SKILL.md` 以适配：
- 各文章类型的目标字数
- 内链/外链数量阈值
- 禁用的 AI 写作模式列表
- 你项目的文件路径结构
- QA 配置文件路径

---

## File Structure

```
blog-writing-skill/
├── README.md     ← This file (EN + ZH)
└── SKILL.md      ← The skill definition (OpenClaw reads this)
```

## License

MIT

## Related Skills

| Skill | Purpose |
|-------|---------|
| `content-qa` | QA checklist and review agent (recommended) |
| `seo-geo-qa` | Technical SEO + GEO QA runner (recommended) |
| `content-production` | Produce → review → revise workflow |
| `seo-audit` | Full-site technical SEO audit |
| `seo-geo` | GEO optimization for AI search engines |
| `competitor-alternatives` | Comparison page structure guide |
| `copy-editing` | Multi-pass editing framework |

## Contributing

This is a generic/universal version of the blog-writing skill. It's designed to work with any website or blog, not just specific companies or products.

When contributing:
- Keep examples generic ("your website", "your product")
- Avoid hardcoded file paths — use configurable examples
- Maintain broad compatibility across different blog setups
- Test with different OpenClaw configurations

---

*Built for the OpenClaw AI agent ecosystem. Works best when combined with complementary content skills.*