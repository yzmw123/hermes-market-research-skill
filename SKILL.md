---
name: market-research
description: "用户要求调研行业、市场、产品、竞品、公司、市场机会或商业论证时使用；也用于判断某方向是否值得做、是否有机会、如何进入、如何对标。同时支持销售拜访准备——当用户提到「拜访客户」「见客户」「出差拜访」等场景时，搜索行业动态+政策+招投标+案例，生成聊天话题和销售话术。所有输出基于公开资料，形成可溯源报告。"
version: 0.11.0
---

# Market Research

## Purpose

Use this skill to turn vague market, industry, product, or competitor research requests into evidence-backed research outputs.

Core principle: **research is not template filling; research is decision support from available evidence.**

Do not begin by writing a fixed table of contents. Begin by clarifying the decision, scouting what evidence exists, then choose the report structure based on evidence density.

## When Not to Use

Do not run the full workflow when the user is only discussing how the skill should work, brainstorming a research process, or asking for a quick opinion. In those cases, stay conversational.

Do not use this skill for academic literature reviews unless the user frames the task as market/product/industry research.

## Operating Contract

A good run produces these artifacts, unless the user explicitly asks for a lighter output:

1. A confirmed research-question rewrite.
2. An evidence map showing which search directions are strong, weak, or unavailable.
3. An internal Finding-Card collection (used by the agent to organize evidence, **not** included in the final report).
4. An adaptive formal Markdown report saved under `~/Downloads/`, with chapters chosen from evidence clusters and professional report structure patterns.
5. A polished HTML version of the same report saved under `~/Downloads/`.
6. A source index, structure rationale, and a list of key blind spots.

If public sources cannot support a credible report, produce a blind-spot report or validation plan instead of padding weak sections.

## 工作流调度

**核心原则：用户让你做行业调研报告 → 默认就是不了解这个行业。不需要用户额外说"我不熟悉"。**

收到用户请求后，先判断属于哪种场景：

| 触发信号 | 路由 |
|---|---|
| "拜访"、"见客户"、"出差去XX"、"明天去XX公司"、"准备见XX行业的" | → **销售拜访准备工作流**（见下方） |
| **"调研"、"研究"、"分析"、"有没有机会"、"市场空间"、"竞品"、"招标格局"、"出报告"、"行业报告"** | → **陌生行业快速建模型工作流**（默认路由，见下方）。即使用户没说"我不熟悉"，也默认走此流程，因为要求调研本身就意味着需要建立认知。 |
| 不确定 | 用 `clarify` 问用户，但**不要问"你是不是不熟悉这个行业"**（这是废话），只确认：行业名称、ToG/ToB/ToC、重点方向。 |

**澄清环节只确认三件事（不要多问）**：
1. 行业名称和范围（用户可能用口语描述，需要校准）
2. ToG / ToB / ToC？（影响数据源选择）
3. 有没有特别想了解的重点方向？（有就深挖，没有就全覆盖）

## 陌生行业快速建模型工作流（Industry Onboarding Report）

### 触发条件

**默认路由**。当用户提出行业调研/研究/分析/出报告需求时自动进入，不需要用户额外说"我不熟悉"。

### 核心定调

### 关键区别 vs 标准调研

| 标准调研 | 陌生行业快速建模 |
|---|---|
| 用户已经懂行业，要判断是否进入 | 用户不懂行业，要先建立认知 |
| 从证据集群出发，动态生成章节 | 从行业基础知识开始，逐步展开 |
| 报告像咨询/投研报告 | 报告像行业教科书 + 咨询报告的结合体 |
| 可以跳过基础概念 | **必须解释基础概念**，不能假设用户知道 |

### 报告必须回答的 15 个问题

加载 `references/industry-onboarding-template.md` 获取完整模板（A-P 结构）。核心框架：

1. 这个行业是干什么的？解决什么问题？服务谁？
2. 行业里的核心业务流程是什么？
3. 谁是主管部门、采购方、建设方、使用方、验收方？
4. 这个行业主要有哪些产品、系统、平台、服务？
5. 主要技术底座是什么？包括数据、平台、软件、硬件、信创、AI 等。
6. 一年市场总盘子大概多大？请给出估算方法、样本来源、低/中/高三档，不允许只给空泛数字。
7. 近 2-3 年主要采购项目有哪些？按省级、市级、区县级、专项类拆分。
8. 龙头公司是谁？有没有上市公司？上市公司市值、营收、相关业务占比大概如何？非上市公司要说明行业位置和强势区域。
9. 竞争格局是什么？平台厂商、集成商、数据服务商、数据库厂商、本地厂商分别卡在哪一层？
10. 当前政策趋势是什么？哪些政策会直接带来预算和项目？
11. 当前技术趋势是什么？哪些技术变化会带来新机会？
12. 当前业务痛点是什么？省级、市级、区县级客户分别关心什么？
13. 如果我们要切入，最现实的切入点是什么？不建议做什么？
14. 重点专项方向请单独展开，包括市场需求、客户痛点、典型项目、竞品、产品形态、交付内容、验收方式。
15. 最后给出：行业吸引力评分、竞争强度评分、切入难度评分、机会窗口评分、建议动作。

### 硬性要求

- **不允许只写结论，必须解释行业基本概念。** 用户不懂这个行业，不能假设他们知道术语。
- **不允许只堆政策，必须说明政策如何转化成项目和预算。** 每条政策后面要有"这意味着什么"。
- **不允许只列公司名，必须说明公司所在层级、优势区域、典型项目、上市情况、财务体量。**
- **市场规模必须给估算方法，不能凭空写数字。** 必须展示低/中/高三档和推导过程。
- **至少统计 20 个近年招中标样本**，形成项目金额区间表。
- **至少列 10 家相关厂商**，区分平台层、应用层、数据服务层、数据库/信创层、本地集成商。
- **对不确定信息必须标明"低置信度/需验证"**，不能伪装成确定事实。
- **输出要能服务客户拜访，不是学术报告。**

### 报告结构（A-P 固定框架）

加载 `references/industry-onboarding-template.md` 获取完整 A-P 章节定义和每章写作指南。

### 产出物

- Markdown：`~/Downloads/{行业}-行业深度调研报告-{日期}.md`
- HTML：`~/Downloads/{行业}-行业深度调研报告-{日期}.html`（左目录右正文，来源链接可点击跳转原网页）
- 不单独生成销售拜访简报（拜访问题已内嵌在第 O 章）

## 销售拜访准备工作流（Sales Visit Preparation）

### 触发条件

用户说出类似以下内容时，自动进入此工作流：

- "我今天要拜访电力行业的客户"
- "明天去见一个能源集团的领导"
- "下周出差去XX，帮我准备一下"
- "给我找点XX行业的谈资"
- "帮我想想跟XX客户聊什么"

### 步骤 1：意图澄清（必须）

使用 `clarify` 工具向用户确认关键信息。分两轮进行：

**第一轮：确认行业和客户画像**

```python
clarify(
    question="你要拜访哪个行业的客户？请选择或输入：",
    choices=[
        "电力/能源（电网、发电集团、新能源）",
        "制造业（机械、电子、汽车零部件等）",
        "政府/政务（数字化、智慧城市、信创）",
        "其他行业（请在下轮补充说明）"
    ]
)
```

如果用户选"其他行业"，用开放式 clarify 追问具体行业。

**第二轮：确认拜访目标和你的产品**

```python
clarify(
    question="这次拜访的目的是什么？你主要卖什么产品或服务？",
    choices=[
        "初次拜访/建立关系 —— 主要为了认识人、了解对方需求",
        "方案汇报/演示 —— 已经有接触，这次去讲方案",
        "关系维护 —— 老客户，需要找话题保持联系",
        "其他（请补充说明）"
    ]
)
```

两轮 clarify 跑完后，再追问一句（对话中直接问，不需要 clarify 工具）：
- 客户的具体单位/角色（如"XX省电网公司调度中心"）
- 有什么特别想了解或不想涉及的话题

在得到用户确认前，不开始搜索。

### 步骤 2：信息侦察

基于确认的行业和客户类型，多方向搜索公开信息。使用以下搜索策略：

```bash
# 1. 近期行业新闻（最近 30 天）
autocli google search "XX行业 最新 新闻 2026" --limit 10
autocli google search "XX行业 政策 发布 2026" --limit 5

# 2. 招投标信息
autocli google search "XX行业 招标 中标 2026" --limit 10
# 如果有中国政府采购网等专业平台的访问权限，优先使用

# 3. 各地案例
autocli google search "XX行业 案例 数字化 智能化 项目" --limit 10
autocli google search "site:gov.cn XX行业 试点 示范" --limit 5

# 4. 客户/竞品动态（如果能定位到具体客户）
autocli google search "XX公司 新闻 动态 2026" --limit 5
```

**搜索优先级**：
1. 政策/监管变化 → 最容易引发客户讨论的话题
2. 招投标/项目动态 → 展示你对市场的了解
3. 同行/竞争对手动态 → 客户最在意的信息
4. 技术/行业趋势 → 展示专业深度
5. 本地/区域新闻 → 拉近距离

### 步骤 3：生成销售拜访简报

搜索完成后，生成一份简报，保存到 `~/Downloads/{行业}-销售拜访准备-{日期}.md`。

简报结构：

```markdown
# {行业}销售拜访准备 — {日期}

## 客户背景（如有）
- 单位/角色：
- 拜访目的：
- 我们的产品/服务：

## 行业近期动态速览

### 🔥 政策/监管（最近 30 天）
| 日期 | 政策/文件 | 来源 | 关键内容 | 可聊点 |
|---|---|---|---|---|

### 📰 行业新闻
| 日期 | 标题 | 来源 | 一句话要点 | 可聊点 |
|---|---|---|---|---|

### 🏗️ 招投标/项目动态
| 日期 | 项目名称 | 金额 | 甲方 | 中标方 | 可聊点 |
|---|---|---|---|---|---|

### 📍 各地案例/试点
| 地区 | 案例概述 | 关键做法 | 可聊点 |
|---|---|---|---|

## 🗣️ 聊天话题清单

### 请教类话题（优先使用 — 姿态低、对方愿意说）
1. **话题标题**
   - 话题引子：（一句话怎么开口）
   - 为什么问这个：（让对方觉得你做了功课）
   - 你希望对方说什么：（预判对方的回答方向）
   - 你可以接什么：（对方说完后你如何接话、转到你的产品）

2. ...

### 行业动态类话题（展示你对市场的了解）
1. ...

### 案例参考类话题（借别人的经验引出自己的方案）
1. ...

## 💬 销售话术建议

### 开场白（3 个版本）
1. 正式版：...
2. 自然版：...
3. 请教版：...

### 关键转场话术
- 从闲聊转到正事：...
- 从政策/新闻转到我们的方案：...
- 对方提竞品时：...

### 常见问题应答
| 客户可能问 | 建议回答 |
|---|---|

## 注意事项
- 本次拜访的 3 个核心话题：
- 避免提及的话题：
- 需要带的东西：
```

### 步骤 4：输出与交付

**对话中输出**：行业简报的核心发现（3-5 条） + 聊天话题的要点列表（5-10 个） + 文件路径。

**文件保存**：
- Markdown 简报：`~/Downloads/{行业}-销售拜访准备-{日期}.md`
- 不生成 HTML（销售简报以快速阅读为主，Markdown 即可）

不需要写正式的行业调研报告，也不需要 Finding Cards。这个工作流的目的是**快速准备谈资**，不是深度研究。

### 话题设计原则

**核心原则：以请教姿态切入，不是以推销姿态切入。**

| ✅ 好话题 | ❌ 差话题 |
|---|---|
| "最近看到XX政策出来了，你们这边有感受到什么变化吗？" | "我们有一个XX产品，能帮你们解决XX问题" |
| "XX地的XX项目是你们做的吗？我们最近在研究这个案例" | "你们的竞争对手XX已经上了我们的系统" |
| "你们行业最近XX技术很火，你实际接触下来觉得靠谱吗？" | "你们现在用的XX方案太落后了" |
| "听说你们最近在搞XX，方便分享一下思路吗？" | "我给你们介绍一下我们的产品" |

**话题来源优先级**：
1. 客户自己的新闻/动态（体现你真的关注对方）
2. 客户所在行业的最新政策（体现市场敏感度）
3. 同行的案例和做法（引发对比和讨论）
4. 行业技术趋势（请教对方怎么看）

**绝对禁止**：
- 不要编造客户内部信息（"听说你们..."必须以公开来源为依据）
- 不要假装知道客户的痛点（可以说"行业普遍存在XX问题，你们这边是不是也..."）
- 不要把竞品说得一无是处（客观对比，不要说坏话）

## Workflow

### 1. Calibrate the Question (Interactive)

Before searching, rewrite the user's request into a researchable decision question using **interactive clarification**.

Check for vague words such as "有前景", "有机会", "空间大", "适合", "先进", "值得做". Present the decision scenarios as selectable options via the `clarify` tool.

**Step 1: Present decision scenario options**

Use `clarify` with up to 4 choices. Default options: 投资/入局判断、产品/方向选型、销售/标书/提案素材、其他/组合场景。具体措辞根据用户原问题动态调整。

**Step 2: If user selects "其他/组合场景", ask for free-text input**

Use open-ended `clarify`: "请简述你的具体决策场景（1-2句话）".

**Step 3: Present the rewritten research question for confirmation**

```markdown
基于你的选择，我建议把原问题：
"{用户原话}"

重写为：
"{可调研问题}"

这份调研主要回答：
1. ...
2. ...
3. ...

不回答：
- ...

**确认无误请回复"确认"，或提出修改意见。**
```

Wait for explicit confirmation before proceeding to evidence scout.

Detailed guidance: read `references/evidence-workflow.md` when the framing is ambiguous.

### 2. Scout Evidence Before Planning the Report

Run a short evidence scout before drafting the report outline.

Use available search tools. In this Hermes environment, `web_search` may be unavailable; prefer:

```bash
autocli google search "关键词" --limit 10 --format json
autocli read "URL" -f text
```

Search across likely evidence channels: policy/procurement, company sites, docs, pricing, cases, reviews, social/community discussion, hiring pages, filings, funding/news, reports, demos, changelogs.

When the topic is broad or the user expects a full report, also run **structure scouting**: open 2-5 paid report TOCs (e.g. Cir.cn), 3-5 short industry-analysis articles (e.g. chinabgao.com/info), and 1-3 authoritative institutional reports when available (especially CAICT/中国信通院 for digital economy, AI, data governance, industrial internet, telecom, government digitalization). Record TOCs/articles as **structure evidence only**; treat institutional reports as factual evidence within their domain, while still checking critical numbers against original sources.

Produce an evidence map:

```markdown
| Direction | Evidence density | Evidence quality | Continue? | Reason |
|---|---:|---:|---|---|
| 招投标 | 高 | 中高 | 是 | 有大量中标公告，可看采购品类和供应商 |
| 用户评论 | 低 | 低 | 否 | 公开讨论很少，不适合硬写用户洞察 |
```

Do not write a report before producing the evidence map.

Detailed guidance: read `references/evidence-workflow.md`.

### 3. Choose the Research Path

Choose the path from the evidence map, not from a fixed ToG/ToB/ToC template.

Common paths: signal report; product/competitor teardown; market opportunity judgment; hypothesis and validation plan; blind-spot report.

Detailed method selection: read `references/methods.md`.

### 4. Deepen Only High-Value Evidence Channels

Deepen the evidence channels marked "continue" in the evidence map. Do not chase every possible dimension.

Convert findings into Finding Cards as an **internal organizing tool**. Each card must include: one-sentence finding, type (fact/inference/judgment/recommendation), evidence, confidence, limits, and decision impact.

**Finding Cards are for the agent's internal use only.** Use them to organize evidence clusters before writing the formal report; do not include cards as-is in final output.

Detailed card and report rules: read `references/reporting.md`.

### 5. Draft the Report Dynamically

Cluster Finding Cards by topic as an internal preparatory step. Then choose an **adaptive formal report structure** from the evidence clusters and the pattern bank in `references/reporting.md` / `references/structure-patterns.md`.

**报告写作规范：**
- 以连续正文分析为主，表格只做辅助（每张表前后必须有解释）
- 每个章节有明确的研究问题、分析过程、证据说明和阶段性结论
- 所有大判断必须解释"为什么"，不能只写结论
- 对拿不到的数据，写成"研究限制与假设/关键盲区"，不要假装已充分验证
- 报告语气像正式咨询/投研/产业调研报告，而非公众号文章、AI 总结、项目建议书或销售方案
- 结论必须从前文推导，而非先验给出
## HTML 生成规则（所有调研报告必须遵守）

### 渲染脚本
`scripts/render_html.py` — 独立 Python 脚本，输入 Markdown，输出完整 HTML。

```bash
python scripts/render_html.py <input.md> <output.html> [--theme THEME]
```

### 可用主题
| 主题 | 适用行业 |
|---|---|
| `tech` | AI、软件、互联网、数据治理（默认） |
| `cict` | 数字政府、信通院、数字经济、政务 |
| `industry` | 工业制造、能源、基建 |

脚本自动基于报告正文关键词频次选主题。

### 强制样式规则（已写入脚本）

#### 1. h1 hero 标题必须可见
不用渐变文字，直接用单色 `color:var(--accent)`。

#### 2. 来源引用 `[S1]` 必须带链接
正文字 `[S1]` → `<a href="#ref-S1">`；来源索引表格第一列自动插入 `id="ref-S1"`。

#### 3. 目录固定在左侧
sidebar 用 `position:fixed; left:0; height:100vh`，正文区域在右侧。

#### 4. 表格有可见边框
`border:1px solid var(--bd-strong)`，表头下方 `2px solid var(--accent)` 强调。

#### 5. 重点内容颜色区分
- `strong`：渐变背景 + 白色文字（pill 风格）
- `em`：左边框 + accent 色
- `[S1]` 引用：highlight 色 + 悬停反转为深色

#### 6. 输出到本地
HTML 保存到 `~/Downloads/<topic>-调研报告.html`。对话中只回复文件路径 + 概述。

#### 7. Markdown 兼容性
- `**bold**` 含空格自动转标准 bold
- `[S1]` 自动转内部锚点链接（跳转到文末来源索引表格对应行）
- **`[文本](url)` Markdown 链接自动转为可点击 HTML 链接**（`target="_blank"` 新窗口打开）。来源索引的"链接"列必须使用此格式，确保读者能直接跳转到原网页。

### 如何新增/修改主题
在 `scripts/render_html.py` 的 `THEMES` 字典中增加/修改色板定义即可。

---

## 本地文件输出

- Markdown：`~/Downloads/{topic>-调研报告.md`
- HTML：`~/Downloads/{topic>-调研报告.html`
Detailed output rules: read `references/reporting.md`; when the structure is hard to choose, read `references/structure-patterns.md`.

### 6. Verify Before Final Delivery

Fact-check before finalizing. Focus on:

- Numbers, dates, company names, product names, policy titles, funding amounts.
- Comparative claims such as “第一”, “唯一”, “最大”, “领先”.
- Causal claims.
- Claims based on one source or marketing material.

Downgrade unverifiable claims to inference, move them to blind spots, or delete them.

Detailed quality rules: read `references/quality.md`.

## Research Boundaries

ToG / ToB / ToC are evidence-entry points, not report templates.

- ToG public evidence may show policies, standards, procurement intentions, budgets, tender awards, supplier patterns, and pilot programs. It usually cannot show internal scoring, expert relationships, dark prices, or unwritten access rules.
- ToB public evidence may show positioning, pricing, docs, cases, hiring signals, public technical content, filings, and review-site complaints. It usually cannot show a specific company's internal procurement process, true ROI model, renewal rate, churn, or private architecture.
- ToC public evidence may show app-store reviews, social-media language, ranking signals, pricing, version history, public ads, and community complaints. It usually cannot show true CAC/LTV, retention, silent churn, recommendation algorithms, or internal A/B results.

When a requested dimension is structurally unavailable, say so early and propose a validation route.

## References

Load these only when needed:

- `references/evidence-workflow.md` — question calibration, evidence scout, ToG/ToB/ToC source channels.
- `references/methods.md` — DBS, Superpowers, gstack, Lenny, and PM-skills methods as analysis lenses.
- `references/reporting.md` — adaptive formal report structure, evidence use rules, section title conventions, **HTML output style guide (Agent generates HTML directly, no script needed)**.
- `references/structure-patterns.md` — structure patterns learned from Cir.cn paid report TOCs, chinabgao short articles, and CAICT/中国信通院 reports; use TOCs/articles as structure inspiration and CAICT as authoritative domain evidence when relevant.
- `references/quality.md` — confidence scoring, hallucination control, fact-checking, eval prompts.
- `references/sales-visit-prep.md` — 销售拜访准备的详细指南：搜索策略、话题设计模式、话术模板库、常见行业话术示例。
- `references/industry-onboarding-template.md` — **陌生行业快速建模型模板**：A-P 15 章报告结构定义、每章写作指南、15 个必须回答的问题、硬性要求清单。

## Common Failure Modes

- Starting with a fixed outline without evidence scouting.
- Treating paid report TOCs as factual market evidence instead of structure inspiration.
- Forcing the old 11-chapter template when evidence only supports 4-6 meaningful chapters.
- Treating ToG/ToB/ToC as templates rather than evidence-entry points.
- Padding weak sections with "暂无数据".
- Turning marketing copy into facts.
- Writing internal procurement, CAC/LTV, retention, or评标细则 as if public sources can reveal them.
- Skipping the evidence map.
- Producing only a chat answer when the user asked for local Markdown + HTML files.
- **Outputting Finding Cards or strategy cards as the final report structure instead of writing a formal chapter-by-chapter industry report.**
- **Writing a "memo" or "evidence summary" when the user expects a full industry research report with connected analysis between chapters.**
- Forgetting to version-bump after skill updates. Update version on any non-trivial change.
- **After a research session, only producing a chat response or Markdown file when the SKILL requires BOTH `md` AND `html` files saved locally.** A chat-only or md-only answer is a protocol failure — the user expects a full evidence-backed report with local artifacts.
- **行业入门报告写成政策摘要或新闻摘要。** 当用户说"我不熟悉这个行业"时，报告必须从基本概念讲起，不允许假设用户知道术语、流程、参与角色。第一版被用户批评"内容单薄，像新闻摘要"就是犯了这个错误——正确的做法是先用 B-D 章建立行业基础认知，再展开分析。
- **报告内容太薄。** 如果用户不熟悉行业，一篇 3000 字的报告是不够的。行业入门报告应达到 15000-40000 字（含表格），覆盖 A-Q 全部章节。20+ 招中标样本、10+ 公司详情、市场规模三档估算是最低标准。
- **来源索引链接不可点击。** render_html.py 已支持 markdown 链接 `[text](url)` 自动转为可点击 HTML 链接。来源索引的"链接"列中必须写完整的 `[名称](https://url)` 格式，确保读者能直接跳转到原网页。
