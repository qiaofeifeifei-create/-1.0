---
id: concept-source-traceability
title: 来源追溯
type: concept
created_at: 2026-05-30
updated_at: 2026-05-30
aliases:
  - 溯源
  - source tracking
related:
  - atomic-notes
  - conflict-marking
sources:
  - summary-2026-05-30-digestion-principles
---

# 来源追溯

## Definition

每条知识结论都必须携带来源引用，可以是原始文档 ID、URL、对话记录。没有来源的知识不进入 wiki。冲突标记本身就是一种特殊的溯源——标注"这个说法来自版本 A，那个说法来自版本 B"。

## Why It Matters

知识库的可信度取决于可追溯性。没有来源的知识会逐渐退化为"可能对的"的模糊记忆。当发现两个来源相互矛盾时，溯源能力决定了是能解决冲突还是无声地保留错误。

## Where It Appears

- areas/ 中每个条目的 `source_url` + `captured_at` 字段
- digest/ 中的 `conflicts` 段
- notes/ 中的 `Source` 段
- 消化原则第 2 条"每条结论尽量带来源"

## Notes

溯源粒度：raw 文件级别（source_url） > 条目级别（source_id） > 段落级别（引用标记）。当前系统在 areas/ 中做到的是文件级溯源，notes/ 中做到的是条目级溯源。
