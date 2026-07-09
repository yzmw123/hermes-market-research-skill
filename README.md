# Hermes Market Research Skill

> Hermes Agent 技能：行业市场调研 + 销售拜访准备

## 版本

**v2.0.0** — 2026-07-09

## 功能

- **陌生行业快速建模型**：从零了解一个行业，15 章深度报告（A-P 框架）
- **销售拜访准备**：搜政策+招投标+案例，生成聊天话题和话术
- **HTML 报告渲染**：左目录右正文，来源链接可点击跳转原网页

## 触发方式

| 你说什么 | 触发什么 |
|---|---|
| "帮我调研 XX 行业" | 快速建模型（默认，假设你不懂这个行业） |
| "我要拜访 XX 客户" | 销售拜访准备 |

## 输出

- `~/Downloads/{行业}-行业深度调研报告-{日期}.md`
- `~/Downloads/{行业}-行业深度调研报告-{日期}.html`（可点击来源链接）
- `~/Downloads/{行业}-销售拜访准备-{日期}.md`（仅拜访模式）

## 安装

```bash
# 复制到 Hermes skills 目录
cp -r hermes-market-research-skill ~/.hermes/skills/research/market-research/

# 或在 Hermes 中直接加载
```

## 文件结构

```
market-research/
├── SKILL.md                              # 技能定义（主文件）
├── references/
│   ├── industry-onboarding-template.md   # 陌生行业建模型模板 (A-P)
│   ├── evidence-workflow.md              # 证据侦察指南
│   ├── methods.md                        # 分析方法论
│   ├── reporting.md                      # 报告写作规范
│   ├── structure-patterns.md             # 报告结构模式
│   ├── quality.md                        # 质量控制标准
│   └── sales-visit-prep.md               # 销售拜访指南
├── scripts/
│   ├── render_html.py                    # MD→HTML 渲染脚本
│   ├── validate_skill.py                 # 技能验证
│   └── run_evals.py                      # 评估运行
└── evals/
    └── evals.json                        # 评估用例
```

## v2.0 更新

- **默认路由变更**：调研=不懂行业，不再需要额外触发词
- **报告框架 A-P**：15 章固定结构，覆盖从行业定义到切入机会
- **硬性质量标准**：≥20 招中标样本、≥10 公司详情、市场规模三档估算
- **来源链接可点击**：render_html.py 支持 `[text](url)` → HTML 链接
- **置信度标注**：不确定信息必须标"低置信度/需验证"

## 许可

MIT
