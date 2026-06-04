# Output Templates

本文件定义 `skill-siphon` 的常用输出格式。

## Analyze-only Output

当没有 target skill 时使用：

```md
# Source Skill Review

## 1. Skill Profile

## 2. Workflow

## 3. Reusable Patterns

## 4. Limitations And Risks

## 5. Possible Uses
```

## Target Adoption Round Output

当有 target skill 且正在逐轮讨论候选时使用：

```md
## 候选发现 <编号>：<名称>

### 发现

### 来源证据

### 可迁移价值

### 适配判断

| 维度 | 判断 |
|---|---|
| 适配度 | 高 / 中 / 低 |
| 风险 | 低 / 中 / 高 |
| 上下文成本 | 低 / 中 / 高 |
| 范围影响 | 无 / 小 / 中 / 大 |

### 初步建议

### 你的选择

A. 采纳
B. 暂定
C. 深挖当前方向
D. 跳过
```

## Integration Review Output

所有 rounds 结束后，Final Summary 之前使用：

```md
# Integration Review

## 1. 已采纳项整合

说明哪些采纳项可以合并、哪些需要保留独立。

## 2. 暂定项二次分析

逐项判断暂定项应升级、合并、降级还是跳过。

## 3. 重复与合并

识别相似、重叠或可合并的 pattern。

## 4. 冲突与边界检查

检查是否有规则冲突、职责重叠、scope 扩张或 target skill 过重。

## 5. 整合后建议清单

这是 Final Summary 的唯一输入。
```

## Final Adoption Summary

Integration Review 完成后使用：

```md
# Skill Adoption Summary

## 1. 整合后采纳项

只列合并后的采纳项，不重复罗列原始 rounds。

## 2. 暂定项处理结果

说明每个暂定项最终升级、合并、降级、跳过，或仍需用户决策。

## 3. 已跳过项

## 4. Recommended Adoption Plan

说明建议如何吸收到 target skill：

- 应写入 `SKILL.md` 的内容。
- 应写入 `references/` 的内容。
- 应作为 optional workflow 的内容。
- 不应写入但可作为人工参考的内容。

## 5. Decisions Needed

列出还需要用户决策的问题。

## 6. Optional Apply Plan

只有用户要求实施时才执行。
```

## Multi-source Index Output

多个 source skill 时使用：

```md
# Source Skill Index

| Source | Main Value | Strong Patterns | Risk | Deep Priority |
|---|---|---|---|---|
| ... | ... | ... | ... | high / medium / low |

## Suggested Deep Pass Options

- Option 1: ...
- Option 2: ...
- Option 3: ...
```

## Apply Plan Output

用户明确要求应用修改时，先输出简短执行计划：

```md
# Apply Plan

## Files To Change

## Changes

## Validation

## What Will Not Be Changed
```

## Skill Optimization Review Output

没有 source、只优化 target skill 时使用：

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
