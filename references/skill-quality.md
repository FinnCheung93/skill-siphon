# Skill Quality

本文件用于在没有 source skill 时优化 target skill，也用于 Integration Review 时判断候选是否值得吸收。

需要更完整的 skill 设计术语、信息层级、拆分判断和失败模式时，读取 [skill-design-principles.md](skill-design-principles.md)。本文件只保留高频质量镜头。

## Core Idea

好 skill 不是内容越多越好，而是能在正确时机把 agent 的行为约束到正确路径上。

优先优化行为控制，而不是堆知识。

准则约束风险，不替 agent 固定判断路径。

给 agent 的文件应是轻量工作协议，不是厚重操作手册。它应该固定入口、节奏、边界、确认点和记录机制，把具体判断空间留给 agent。

skill 的根目标是提高过程可预测性：不是让每次输出相同，而是让 agent 每次按同一类可靠过程推进。

## Quality Lens

### 1. 触发准确性

`description` 必须控制触发，包含：

- 用户可能会怎么说。
- 什么情况下应使用。
- 什么情况下不应使用或应停下确认。

不要把关键触发条件只写在正文里，因为正文只有触发后才会加载。

如果 skill 只需要用户手动调用，优先考虑降低自动触发成本；如果 agent 或其它 skill 需要主动发现它，才让触发描述承担 model-invoked 职责。实操上，`disable-model-invocation: true` 表示 user-invoked；省略它并保留 model-facing `description` 表示 model-invoked。

### 2. 结构合理性

Skill 分三层：

- `description`：负责触发。
- `SKILL.md`：负责主 workflow、硬规则、出口条件。
- `references/`：负责详细模板、分析维度、可选流程。

多数执行型 skill 的 `SKILL.md` 应像 workflow controller，不应像知识库。但纯 reference skill 或 reference-heavy skill 也可以是合理形态：如果它的目标是提供一组平级审查规则、术语或判断镜头，而不是驱动一串步骤，就不应因为“没有流程”被判为结构问题。

对 `AGENTS.md`、项目治理文件或其它 agent-facing 文件也适用同一原则：只固定如何安全进入任务、如何保持上下文、如何避免误改、如何记录和自进化，不承载 PRD、Specs、实现计划或任务拆解。

`SKILL.md` 优先承载当前调用路径必需的步骤、硬规则和高频判断；低频解释、术语、模板和长清单应下沉到 reference，并用清楚的读取条件连接。对 reference-only skill，重点检查其平级规则是否完整、共置、可应用，而不是强行补 workflow。

### 3. 渐进式引用

- `SKILL.md` 直接引用需要的 reference。
- 避免深层引用，例如 `SKILL.md -> A -> B -> C`。
- 长内容放入 references，但必须说明何时读取。
- 不要默认全量读取 references、scripts、assets。

引用文字本身要写清触发条件。一个重要 reference 没被读取，通常先修 pointer wording，再考虑把内容拉回 `SKILL.md`。

### 4. 出口条件

workflow 的关键步骤必须有进入和退出条件：

- source 缺失时停下。
- target 缺失时切换模式或询问。
- 用户未授权写文件时只输出计划。
- 多 source 超出阈值时先 Index Pass。
- 暂定项必须在 summary 前二次分析。

优先使用 loop、gate、checkpoint，而不是厚重 SOP。Loop 约束工作节奏，gate 阻止越界，checkpoint 保证可恢复；具体工具和实现路径交给 agent 判断。

每个关键步骤都应有可检查的完成标准。完成标准越模糊，越容易让 agent 提前收尾；先收紧标准，再考虑拆分步骤或隐藏后续步骤。

### 5. 安全与确认

不可逆或高影响动作必须有 confirmation gate：

- 写文件、覆盖、删除、发布、安装、迁移。
- 修改 source skill。
- 自动把建议应用到 target skill。
- 生成可能被当成权威的文件。

Completion checklist 应明确禁止事项，而不只是正向步骤。

容易误解、越权或提前执行的位置都应设置 hard gate。例如：source 缺失、角色团确认、写文件授权、Final Summary 前 Integration Review。

### 6. 上下文经济性

检查：

- `SKILL.md` 是否过长。
- 是否重复了 references 的内容。
- 是否存在无行为价值的解释。
- 是否能用一句硬规则替代一段说明。
- 是否把 rarely used 的细节拆到 reference。

同时检查 context load 和 cognitive load：自动触发的内容会消耗模型上下文，手动触发的内容会消耗用户记忆。拆分 skill 前先判断这笔成本是否值得。

### 7. 指令有效性

优先写清 WHY、边界和失败处理，少写空泛的 ALWAYS / NEVER。

好的指令应回答：

- 为什么这条规则存在？
- 什么时候适用？
- 什么时候不适用？
- 违反时会造成什么风险？

优先使用能唤起稳定行为的 leading word：用一个准确概念压缩反复解释，但只在它确实改变 agent 行为时保留。

### 8. 可验证性

优化后应能用 dry checks 验证：

- 该触发时会触发。
- 不该行动时会停下。
- 缺输入时会问。
- 有授权时才改文件。
- 多 source 时不会爆上下文。
- 输出格式符合预期。

### 9. 开放任务的动态生成

如果任务对象高度开放，不要维护固定场景表、固定角色库、固定槽位表或固定问题清单。

更好的方式：

- 先理解当前对象、真实语境、主要风险和期望输出。
- 再由 agent 动态生成角色、路径、候选、问题或审查顺序。
- Skill 只规定生成约束和确认闸门，不规定固定库。

判断标准：固定清单是否会让 agent 更像查表执行器？如果会，改成动态生成规则。

### 10. 交互推进

访谈、拷打、评审、adoption rounds 等多轮交互应单点深入：

- 能从材料、文件、代码或上下文里得到的信息，不问用户。
- 必须问时，一次只问一个当前最阻塞的问题。
- 问题后给推荐回答方向、回答结构或判断标准。
- 沿用户回答继续推进，不把开场变成问卷。

### 11. 输出克制

输出只保留完成当前任务所必需的内容，复杂度交给 agent 按场景判断。

### 12. 修剪纪律

每条规则都应通过三问：是否仍相关、是否重复、是否改变行为。无法通过的内容应删除、合并或下沉，不要因为“看起来完整”而保留。

### 13. 失败模式

审查 skill 时主动寻找：提前完成、重复定义、旧内容沉积、主文件蔓延、无效指令。先修局部完成标准和单一权威来源，再考虑拆分结构。

## Optimization Review Output

```md
# Skill Optimization Review

## 1. 关键问题

## 2. 触发与边界

## 3. Workflow 控制

## 4. Reference 结构

## 5. 安全与确认

## 6. 建议修改

## 7. 需要用户决策
```
