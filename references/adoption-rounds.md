# Adoption Rounds

本文件定义有 target skill 时的多回合吸收决策流程。

## Purpose

Adoption rounds 的目标不是立即改 target skill，而是帮助用户逐个判断 source skill 中的发现是否值得进入最终考虑。

每轮只讨论一个候选发现，避免一次性输出过多建议造成上下文和决策负担。

进入 adoption rounds 的前提是：用户已经明确提供 source skill 和 target skill。缺少 source 时，不要创建候选发现。

## Round Structure

每一轮使用以下结构：

```md
## 候选发现 <编号>：<名称>

### 发现
一句话说明这个 pattern 是什么。中文输出时，除必要术语外使用中文。

### 来源证据
指出它来自 source skill 的哪个部分，例如 `SKILL.md`、`references/...`、workflow、checklist、script 使用方式。

### 可迁移价值
说明它能给 target skill 带来什么改进。

### 适配判断
| 维度 | 判断 |
|---|---|
| 适配度 | 高 / 中 / 低 |
| 风险 | 低 / 中 / 高 |
| 上下文成本 | 低 / 中 / 高 |
| 范围影响 | 无 / 小 / 中 / 大 |

### 初步建议
说明建议收入采纳清单、暂定、深挖当前方向，还是跳过。

### 你的选择
A. 采纳
B. 暂定
C. 深挖当前方向
D. 跳过
```

如果用户用英文交流，可以将标题和判断值改为英文；如果用户用中文交流，不要输出 `Fit: high` 这类不必要的英文表格。

## Decision Meanings

### 采纳

收入采纳清单，最后统一汇总。不要立即修改 target skill。

使用场景：

- 价值明确。
- 与 target skill 目标一致。
- 不明显扩大 scope。
- 不显著增加上下文负担。

### 暂定

收入待判断清单，最后结合其它发现做二次分析。

使用场景：

- 方向有价值，但可能与其它候选重复。
- 可能让 target skill 变重。
- 需要看完其它候选后再判断优先级。
- 需要用户额外取舍。

### 深挖当前方向

继续围绕当前发现展开，而不是进入下一个候选。

可以做的动作：

- 读取 source skill 的相关 reference。
- 读取 target skill 的对应章节。
- 展开 fit / risk / context cost。
- 生成改造前后的对照。
- 拆成更小候选。

深挖后必须再次回到四个选择：采纳、暂定、深挖当前方向、跳过。

呈现时仍使用编号：

- `A. 采纳`
- `B. 暂定`
- `C. 深挖当前方向`
- `D. 跳过`

### 跳过

忽略该发现，不进入最终汇总。

使用场景：

- 与 target skill 不匹配。
- 过度复杂。
- 只是 source 的领域特例。
- 会破坏 target skill 的边界。

## End-of-Rounds Handling

所有候选处理完后：

1. 汇总已采纳项。
2. 汇总暂定项。
3. 先输出独立的 Integration Review，不要直接进入 final summary。
4. 在 Integration Review 中对暂定项做二次分析：
   - 是否与已采纳项重复？
   - 是否应该合并？
   - 是否应该降级为 optional？
   - 是否会让 target skill 变重？
   - 是否需要用户再次决策？
5. 在 Integration Review 中同时检查已采纳项：
   - 是否多个采纳项其实是同一个规则？
   - 是否存在相互矛盾的规则？
   - 是否存在职责重叠？
   - 是否应该合并为一个更清晰的改动？
   - 是否应拆到 `SKILL.md` 和 `references/` 的不同位置？
6. 基于整合后的清单输出 final adoption summary。
7. 等用户明确要求后，才执行修改。

Final summary 不能机械罗列 rounds 中的原始决定；它必须使用 Integration Review 后的合并、去重、冲突处理结果。
