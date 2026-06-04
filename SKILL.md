---
name: skill-siphon
description: Analyze, review, and improve Codex skills by extracting reusable patterns from source skills or applying skill-quality heuristics to a target skill. Use when the user wants to learn from another skill, compare multiple skills, optimize an existing skill, absorb patterns into a target skill, or create an adoption plan before modifying skill files.
metadata:
  version: v1.2.2
  updated: 2026-06-04
---

# Skill Siphon

把目标理解为“萃取、评估、吸收或优化 skill 的行为设计”，不是复制文件。

## Modes

- **Analyze-only**：只有 source skill；分析它的 profile、workflow、patterns 和风险。
- **Target adoption**：有 source + target；从 source 提炼候选，通过 adoption rounds 决定是否吸收进 target。
- **Target optimization**：只有 target；基于 [skill-quality.md](references/skill-quality.md) 做质量审查和优化建议，不假装参考外部 source。
- **Apply mode**：只有用户明确要求写文件、应用修改或生成 patch 时才进入。

## Hard Rules

- 先通过 Intake Gate；source、target、focus、写文件授权缺失时先停下。
- 先分析，不吸收；先建议，不修改。
- 不自行选择 source；用户没给 source 时，只能做 target optimization 或询问。
- “优化 target skill”不等于允许修改文件。
- 有 source + target 时，使用 adoption rounds；不要一次性给最终改造方案。
- 每轮只讨论一个候选，用 `A. 采纳 / B. 暂定 / C. 深挖当前方向 / D. 跳过`。
- Final Summary 前必须先做 Integration Review，合并重复项、处理暂定项、检查冲突和冗余。
- 不静默修改 source skill 或 target skill；不可逆或写文件动作必须先确认。

## Workflow

### 1. Intake Gate

先判断输入是否足够：

| 情况 | 行为 |
|---|---|
| 只有 source | Analyze-only |
| 只有 target，用户要求优化 | Target optimization |
| 有 source + target | Target adoption |
| 用户说“参考某 skill 优化 target”但没给 source | 询问 source，不要猜 |
| 多个 source | 先按 [multi-source.md](references/multi-source.md) 做 Index Pass |
| 用户未授权写文件 | 只输出分析、rounds、review、summary 或 apply plan |

读取本地 skill 时，先读 `SKILL.md`、`agents/openai.yaml` 和资源目录结构；不要默认全量读取 references、scripts、assets。

### 2. Index / Analysis

- 分析 source：用 [source-analysis.md](references/source-analysis.md)。
- 优化 target：用 [skill-quality.md](references/skill-quality.md)。
- 多 source：用 [multi-source.md](references/multi-source.md)。

### 3. Candidate Pool

提炼少量高价值候选，不追求穷尽。候选可来自触发描述、workflow、访谈/澄清、reference loading、确认机制、模板、validation、fallback 和安全边界。

### 4. Adoption Rounds

有 source + target 时，按 [adoption-rounds.md](references/adoption-rounds.md) 逐个候选推进。`采纳` 只表示进入最终清单，不立即执行。

### 5. Integration Review

所有 rounds 后，先整合再总结：

- 合并重复或相似的采纳项。
- 二次分析暂定项。
- 检查规则冲突、职责重叠、scope 扩张和 target 过重。
- 判断内容应放入 `SKILL.md`、`references/`、optional workflow，还是不吸收。

### 6. Summary / Apply

使用 [output-templates.md](references/output-templates.md) 输出 review、summary 或 apply plan。只有用户明确要求实施时，才修改文件；修改前说明将改哪些文件、不会改什么、如何验证。

涉及创建、重构或实质修改 skill 文件时，联动 `skill-creator` 做结构校验、`agents/openai.yaml` 同步和必要的 forward-testing；不要复制 `skill-creator` 的流程细节。

## Reference Loading

- source 分析：`references/source-analysis.md`
- skill 质量优化：`references/skill-quality.md`
- 多 source 控制：`references/multi-source.md`
- adoption rounds：`references/adoption-rounds.md`
- 输出格式：`references/output-templates.md`

## Completion Checklist

- 是否通过 Intake Gate，没有擅自选择 source？
- 是否区分 Analyze-only、Target adoption、Target optimization、Apply mode？
- 是否没有静默修改任何 skill？
- 是否避免一次性过度读取 references/scripts/assets？
- adoption rounds 是否使用 `A/B/C/D`？
- Final Summary 前是否完成 Integration Review？
- 是否检查误触发、越权、过度加载、规则冲突和 target 过重？
- 如修改文件，是否说明路径并完成可用 validation？
