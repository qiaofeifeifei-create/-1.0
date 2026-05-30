---
id: concept-incremental-processing
title: 增量处理
type: concept
created_at: 2026-05-30
updated_at: 2026-05-30
aliases:
  - incremental compilation
  - 增量编译
related:
  - file-over-app
  - source-traceability
  - atomic-notes
sources:
  - summary-2026-05-30-digestion-principles
---

# 增量处理

## Definition

每次只处理新增或变更的原始材料，不做全局重做。消化层（digest/）记录每次处理的元数据，避免重复劳动。与"一次性完美分类"相反——先交付、再迭代。

## Why It Matters

知识库是持续生长的，不是一次性工程。如果每次新增内容都要重新处理全部已有材料，系统就无法扩展。增量处理让维护成本与新增量成正比，而非与总存量成正比。

## Where It Appears

- 消化原则：第 1 条"以增量方式处理新增内容"
- raw/ → digest/ → areas/ 流程中，digest/ 记录已处理状态
- 与"持续迭代"（第 5 条）配合使用

## Notes

增量处理的前提是每条知识必须可独立标识（Atomic Notes），否则无法判断"哪些是新的"。
