# Multi-source Strategy

本文件定义多个 source skill 的处理方式。

## Principle

多个 source skill 时，不追求一次性读完。先建立索引，再选择深挖对象或 pattern 类别。

目标是控制上下文，而不是最大化读取量。

## Source Count Rules

### 1-2 个 source

可以直接 deep analysis。

读取：

- 每个 source 的 `SKILL.md`
- `agents/openai.yaml`
- 资源目录结构
- 与用户 focus 相关的 references

### 3-5 个 source

先做 Index Pass。

Index Pass 输出：

```md
| Source | Main Value | Strong Patterns | Risk | Deep Priority |
|---|---|---|---|---|
| ... | ... | ... | ... | high / medium / low |
```

然后建议 deep order，并等待用户选择：

- 从 high priority 开始。
- 聚焦某个 pattern 类别。
- 比较两个最相关 source。
- 暂停在 index summary。

### 超过 5 个 source

默认只做 Index Pass，不 deep analysis。

必须让用户选择 focus 后再继续：

- 选择 1-2 个 source 深挖。
- 选择一个 pattern 类别，例如访谈、校验、模板、workflow。
- 选择一个 target pain point，例如“降低上下文消耗”。

## Index Pass Read Limit

Index Pass 只读取：

- `SKILL.md`
- `agents/openai.yaml` 如果存在
- 顶层目录结构
- reference 文件名列表
- script 文件名列表
- asset 文件名列表

除非文件名不足以判断价值，否则不要读取 reference 正文。

## Deep Pass

Deep Pass 可以读取：

- source 的相关 reference。
- source 的脚本说明或脚本代码。
- target skill 的相关章节。
- 先前 adoption rounds 的候选和用户决策。

Deep Pass 必须服务于一个明确问题，不要泛泛展开。

## Cross-source Comparison

多个 source 的对比应以 pattern 为单位，而不是以文件为单位。

推荐维度：

- 哪个 source 的 workflow 更清晰？
- 哪个 source 的用户确认机制更好？
- 哪个 source 的 reference loading 更节省上下文？
- 哪个 source 的 checklist 更可迁移？
- 哪些 pattern 可以合并？
- 哪些 pattern 彼此冲突？
