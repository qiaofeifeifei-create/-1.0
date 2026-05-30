# 电气知识库 · 代理规则

## 系统架构

```
workspace/
  raw/                  # 原始材料 — 原文转录，YAML frontmatter，不改动
  inspection/           # 巡检报告 — 定期审计输出（P0/P1/P2/P3 分级）
  knowledge/
    areas/              # 领域知识 — 电气工程 Atomic Notes，115 条，相互链接
    resources/
      digest/           # 消化记录 — 结构化摘要、概念抽取、冲突标记
      concepts/         # 概念卡片 — 跨来源的独立概念定义（id, aliases, sources）
      topics/           # 元主题页 — 知识系统本身的设计（Thesis, Structure, Tensions）
      notes/            # 外部捕获笔记 — 文章/视频/播客的结构化摘要
    projects/           # 进行中项目 — 有明确目标和截止时间的事项
    archives/           # 归档 — 暂时不用但需要保留的内容
    index.md            # 统一索引 — 跨层导航，[[wikilinks]] 引用
  outputs/              # 输出产物 — index.html + article/infographic/pdf/ppt/memo/social
  AGENTS.md             # 本文件：系统规则
```

## 数据流

```
外部数据（HTML/网页/视频/播客/文档）
       ↓ 摄取（ingestion）
    raw/*.md                                     ← 原文保留，YAML frontmatter 元信息
       ↓ 消化（digestion — AI 做四项工作）
    knowledge/resources/digest/*.md               ← 结构化摘要 + 概念抽取 + 冲突标记
       ↓ 抽取概念，映射到已有概念库
    knowledge/resources/concepts/*.md             ← 独立概念卡片（Atomic）
       ↕ 组织主题，更新主题页
    knowledge/areas/*.md                          ← 领域主题页（115 条 Atomic Notes）
    knowledge/resources/topics/*.md               ← 元主题页（知识系统设计）
    knowledge/resources/notes/*.md                ← 外部捕获笔记
       ↓ 索引
    knowledge/index.md                            ← 统一索引
       ↓ 编译（build）
    outputs/index.html                            ← 可交互的知识库应用
    outputs/article/...                           ← 按技能类型输出
```

## 代理职责

### 1. 摄取代理

**触发条件**：新的外部材料需要入库

- 将原始材料转录为 `raw/*.md`，保留原文全部信息，不改动
- 添加 YAML frontmatter（source, source_url, extracted_at, content_type）
- 遇到无法直接提取的文件（YouTube、音频、JS 渲染页面等），使用 pi-skills 工具处理

### 2. 消化代理

**触发条件**：raw/ 层有新文件或更新时

- 为每份 raw 生成结构化摘要 → 写入 `digest/`
- 抽取原子概念，映射到已有概念库（concepts/），必要时新建概念卡片
- 更新或创建主题页（areas/、topics/）
- 更新总索引（areas/_index.md、knowledge/index.md）
- 消化原则：增量处理、来源追溯、先概念后主题、持续迭代
- 遵循 Atomic Notes：每条笔记一个主题，标题清晰可检索，可独立理解
- 发现冲突时标记，不要偷偷覆盖

### 3. 输出代理

**触发条件**：需要基于知识系统生成内容

- 先读取 index，再定位相关主题、概念、摘要
- 不要直接凭印象作答
- 输出中明确区分：已知结论 / 推断 / 待确认问题
- 尽量引用具体来源文件
- 根据任务目标选择最合适的输出形式（article/infographic/pdf/ppt/memo/social）
- 输出写入对应的 `outputs/` 子目录

### 4. 巡检代理

**触发条件**：定期审计或指定巡检时

- 扫描目录结构，检查断链、孤岛文件、重复概念
- 检查定义冲突、缺来源支持、过时内容
- 先出报告（写入 `digest/_audit-*.md`），不要默认自动改
- 每个问题给证据、建议动作、优先级
- 按照 P0（立即）/ P1（尽快）/ P2（迭代）/ P3（建议）分级

## 实体 Schema

### areas 主题页

```yaml
---
title: string          # 页面标题
tags: [string]         # 标签列表
related: [string]      # 关联页面
source_type: string    # 来源类型
source_url: string     # 来源 URL
captured_at: date      # 捕获日期
status: string         # complete | partial | shell_only
---
```

条目格式：`**ID**: XXXX | **标签**: \`tag1\`, \`tag2\``

### 概念卡片

```yaml
---
id: concept-xxx
title: string
type: concept
created_at: date
updated_at: date
aliases: [string]
related: [string]      # 关联概念 id
sources: [string]      # 来源 id
---
## Definition
## Why It Matters
## Where It Appears
## Notes
```

### 捕获笔记

```yaml
---
id: summary-yyyy-mm-dd-author-topic-NNN
source_id: string
title: string
type: summary
created_at: date
topics: [string]
concepts: [string]
---
## Core Idea
## Key Points
## Evidence
## Open Questions
```

## 质量要求

- **内容完整性**：wiki 条目内容必须与 raw/ 原文一致，不得压缩或扩展
- **来源追溯**：每条知识必须携带来源引用（source_url / source_id）
- **冲突标记**：发现版本冲突时在 digest/ 中记录，不偷偷覆盖
- **巡检记录**：每次巡检产出书面报告（`digest/_audit-*.md`）
- **管道完整性**：任何一层更新时必须评估对下游的影响
