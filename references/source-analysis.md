# Source Skill Analysis

本文件定义分析 source skill 的维度。

## Read Order

读取 source 前必须先确认 source 是用户明确提供的。不要因为 target skill 已知，就自行选择其它 skill 作为 source。

优先读取：

1. `SKILL.md`
2. `agents/openai.yaml`
3. 顶层资源目录结构：`references/`、`scripts/`、`assets/`
4. 与当前 focus 相关的 reference 或 script

不要默认全量读取所有资源文件。

## Skill Profile

为 source skill 建立 profile：

- 名称和一句话用途。
- 触发场景。
- 明确不适用场景。
- 用户输入。
- 输出或修改对象。
- 是否会写文件、运行脚本、调用工具。
- 资源结构。
- 主要受众。

## Workflow Analysis

拆解 workflow：

- 入口判断：什么时候触发。
- Context gathering：先读什么、后读什么。
- Clarification：什么时候问用户，问什么。
- Execution：主要步骤。
- User confirmation：哪些动作需要用户确认。
- Validation：如何检查结果。
- Delivery：如何汇报结果。
- Fallback：遇到缺失、失败、冲突时怎么办。

## Reusable Patterns

重点寻找可迁移模式：

- 触发描述写法。
- 渐进式披露和 reference loading。
- 多模式 workflow。
- 分阶段访谈或澄清。
- 用户确认机制。
- 候选池 / 决策池 / checklist。
- 输出模板。
- 文件结构和命名策略。
- 质量门槛。
- dry-run / validation / forward-testing。
- 风险边界和 forbidden actions。
- 多输入规模控制策略。

## Risk Notes

分析风险：

- 是否过度复杂。
- 是否依赖 source skill 的特定领域。
- 是否会让 target skill 的 `SKILL.md` 过长。
- 是否会导致频繁打断用户。
- 是否会把建议误变成自动执行。
- 是否会越界替其它专业文档做决定。
- 是否有不可迁移的工具、脚本、平台假设。

## Transfer Fit

如果有 target skill，对每个候选 pattern 判断：

- Fit：与 target 目标是否一致。
- Value：能解决 target 的什么真实问题。
- Risk：会不会带来复杂度或边界问题。
- Context Cost：是否显著增加 token 消耗。
- Placement：应放入 `SKILL.md`、`references/`、template、checklist，还是不放。
- Adoption Type：可直接采纳、需要改写、只作为 optional，或不建议采纳。

注意：Adoption Type 是分析建议，不是用户最终选择。用户最终选择通过 adoption rounds 完成。

## Skill Optimization Lens

当用户要求优化 target skill，或在 Integration Review 中判断候选是否值得吸收时，额外检查：

- Trigger accuracy：description 是否包含触发词、使用条件、跳过条件。
- Workflow control：步骤是否有进入条件、出口条件和失败处理。
- Context economy：`SKILL.md` 是否过长，是否重复 references，是否默认加载过多材料。
- Safety / confirmation gates：写文件、覆盖、安装、发布、不可逆操作是否需要确认。
- Reference structure：references 是否由 `SKILL.md` 一层直接引用，是否存在深链。
- Output discipline：输出格式是否稳定，是否会过度总结或机械罗列。
- Validation readiness：是否能通过 dry checks 或 eval 验证 skill 行为。
