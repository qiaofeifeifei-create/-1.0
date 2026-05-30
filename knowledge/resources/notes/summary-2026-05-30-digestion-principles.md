---
id: summary-2026-05-30-digestion-principles
source_id: conversation-2026-05-30-digestion
title: 知识消化层的设计原则
created_at: 2026-05-30
type: summary
topics:
  - knowledge-system
  - digestion-workflow
concepts:
  - incremental-processing
  - atomic-notes
  - source-traceability
  - conflict-marking
---

## Core Idea

消化层不是"再写一遍摘要"，而是把原始材料编译成可复用的知识结构。原始材料是输入，摘要、概念、主题页、索引是编译产物。

## Key Points

1. **增量处理**：只处理新增或指定的 raw 文件，不做全局重做。
2. **来源追溯**：每条结论尽量带来源 ID，确保可回溯。
3. **先概念后主题**：先抽取原子概念，再映射到已有概念库，最后组织主题页。
4. **人机分工**：人负责判断，AI 负责整理和联结。
5. **持续迭代**：不追求一次性完美分类，持续迭代就够。
6. **Atomic Notes**：每条笔记只表达一个明确主题，标题必须是清晰可检索的名词短语，脱离上下文也能独立理解。

## Evidence

- 用户原始定义："消化是这套系统的核心。它做的不是'再写一遍摘要'，而是把原始材料编译成可以复用的知识结构。"
- "AI 在消化阶段做四件事：为每份 raw 生成结构化摘要；抽取概念并映射到已有概念库；更新主题页或创建新主题页；更新总索引。"
- "如果发现内容与现有知识冲突，标记冲突，不要偷偷覆盖。"

## Open Questions

- 概念库（concept inventory）当前散落在各 wiki 页面中，是否需要独立的全局概念索引？
- raw/ 与 areas/ 之间的版本差异如何系统性地跟踪？
- 外部捕获内容（notes/）与 areas/ 之间的双向链接如何维护？

## 相关条目

- [[电气基础理论]]
- [[电力系统]]
- [[电气自动化]]
- [[弱电与智能化]]

## Source

- 对话记录 2026-05-30，用户定义的消化阶段工作流
