---
id: topic-llm-knowledge-system
title: LLM 知识系统
type: topic
updated_at: 2026-05-30
related:
  - concept-incremental-processing
  - concept-atomic-notes
  - concept-source-traceability
  - concept-file-over-app
sources:
  - summary-2026-05-30-digestion-principles
---

# LLM 知识系统

## Thesis

LLM 知识系统不是知识库应用，而是以文件为中心、人机协作的知识管线。它的核心是将原始材料"编译"为结构化的知识层，可增量维护、可追溯来源、可脱离 LLM 独立使用。

## Main Structure

### 1. 系统目标

构建一个**持久化的中间层**，介于原始资料（raw/）和输出产物（outputs/）之间。这个中间层由三类实体组成：

- **概念卡片**（concepts/）——跨来源的独立概念定义，是知识的最小原子
- **主题页面**（areas/ + topics/）——围绕一个主题组织的知识集合
- **捕获笔记**（notes/）——外部材料的结构化摘要，携带完整来源信息

### 2. 核心机制

**消化（Digestion）** 是系统的核心操作，将原始材料编译为知识层：

1. 读取 raw 文件
2. 生成结构化摘要
3. 抽取概念并映射到概念库（concepts/）
4. 更新或创建主题页（areas/ / topics/）
5. 更新总索引（_index.md）

消化遵循四条原则：增量处理、来源追溯、先概念后主题、持续迭代。

### 3. 典型流程

```
外部材料 → notes/（捕获笔记）
  ↓ 抽取概念
concepts/（概念卡片）
  ↓ 组织主题
areas/ + topics/（主题页面）
  ↓ 索引
_index.md（总索引）
  ↓ 编译
outputs/（HTML 等产物）
```

## Tensions

- **粒度 vs 可管理性**：Atomic Notes 要求细粒度，但过多小文件会增加维护成本。当前 areas/ 以"子模块"为单位组织条目，每个条目可视为 Atomic Note，但并非每个条目都对应一个独立文件。
- **概念库的位置**：concepts/ 与 areas/ 之间可能存在重叠——一个概念可以被多个主题页引用。concepts/ 当前只包含元概念（关于知识系统本身），领域级概念仍分布在 areas/ 中。
- **LLM 的角色**：LLM 负责整理和联结，人负责判断。这个分工在实践中需要不断校准——LLM 能做的"整理"范围在不断扩展。
