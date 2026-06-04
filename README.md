# Skill 吸星大法

> 分析、审查、对比和优化 Codex Skills 的方法型 Skill。适合用来拆解一个 Skill 为什么有效、哪里容易误触发、哪些行为模式值得吸收。

<p>
  <img src="https://img.shields.io/badge/Codex-Skill-blue" />
  <img src="https://img.shields.io/badge/version-v1.2.2-green" />
  <img src="https://img.shields.io/badge/language-中文-orange" />
  <img src="https://img.shields.io/badge/license-all_rights_reserved-lightgrey" />
</p>

## 它适合做什么

- 分析一个 Skill 的触发条件、工作流、边界和风险
- 对比多个 Skills，提炼可复用的行为设计模式
- 审查一个目标 Skill 的质量，并给出优化建议
- 从优秀 Skill 中提炼候选改法，但不直接照搬
- 在正式改写前形成清晰的采纳清单和执行计划

## 什么时候使用

当你想要认真研究一个 Skill，而不是简单复制它时，可以使用这个 Skill。

典型场景包括：

- “帮我分析这个 Skill 为什么好用”
- “参考 A Skill，看看 B Skill 能吸收什么”
- “审查一下这个 Skill 有没有误触发、越权或过重的问题”
- “帮我优化这个 Skill，但先不要改文件”

## 使用方式

把本目录作为 Codex skill 安装或放入你的 skills 目录中。

入口文件：

```text
SKILL.md
```

## 工作方式

这个 Skill 会优先区分任务模式：

- 只有 source：做分析
- 只有 target：做质量审查
- 有 source 和 target：做候选提炼与采纳判断
- 明确授权写文件：才进入修改模式

它的重点是先判断、再建议、最后才执行，避免把“学习别人的 Skill”变成机械复制。

## 目录结构

```text
skill-siphon/
  SKILL.md
  agents/
  references/
```

## 授权说明

No license is provided. All rights reserved.
