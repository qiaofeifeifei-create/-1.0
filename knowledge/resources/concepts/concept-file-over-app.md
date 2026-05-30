---
id: concept-file-over-app
title: File Over App
type: concept
created_at: 2026-05-30
updated_at: 2026-05-30
aliases:
  - 文件优先
  - file-as-source-of-truth
related:
  - incremental-processing
  - atomic-notes
sources:
  - summary-2026-05-30-digestion-principles
---

# File Over App

## Definition

文件（Markdown + YAML frontmatter）是唯一的知识源，应用（HTML、搜索界面、可视化）是编译产物。文件可直接用编辑器修改、被 Git 跟踪、被 LLM 处理；应用只是视图层，随时可以重建。

## Why It Matters

这是整个管线架构的基石。如果知识只存在于应用数据库中，它就绑定到了特定工具。以文件为中心意味着：编辑器可以换、UI 可以重写、搜索可以替换——但数据始终安全地存在于普通文件中。

## Where It Appears

- 管线结构：raw/ → digest/ → areas/（文件） → outputs/（编译产物）
- areas/ 的 frontmatter 和 Markdown 正文
- notes/ 的 YAML 元数据 + wikilinks
- 消化原则中"人负责判断，AI 负责整理和联结"——因为文件格式让人和 AI 都能读写

## Notes

Karpathy 的 "File Over App" 原则：任何应用都会过时，但纯文本文件永远不会。HTML 应用可以被重构十次，只要 wiki 文件在，知识就在。
