---
id: manifest-2026-05-30
title: 知识系统快照
type: manifest
created_at: 2026-05-30
status: initial-complete
---

# 知识系统快照

## 系统架构

```
raw/ → knowledge/{areas,resources} → outputs/
       ↑                            ↕
   inspection/              .claude/rules/
```

## 目录结构（PARA）

```
workspace/
├── .claude/rules/knowledge-system.md   # 系统规则（身份、设计哲学、操作规范）
├── AGENTS.md                            # 代理规则（角色、数据流、schema）
├── raw/                                 # 原始材料（10 文件，原文不改动）
├── knowledge/
│   ├── areas/                           # Areas — 电气工程领域（11 文件，115 条目）
│   ├── resources/
│   │   ├── digest/                      #   消化记录（10 文件）
│   │   ├── concepts/                    #   概念卡片（5 文件）
│   │   ├── topics/                      #   元主题（2 文件）
│   │   └── notes/                       #   捕获笔记（2 文件）
│   ├── projects/                        # Projects — 进行中事项（空）
│   ├── archives/                        # Archives — 归档（空）
│   └── index.md                         # 统一索引
├── inspection/                          # 巡检报告（2 文件）
├── outputs/                             # 输出产物（index.html + 6 子目录）
└── MANIFEST.md                          # 本文件
```

## 文件清单（46 文件）

| 层 | 数量 | 内容 |
|-----|------|---------|
| `raw/` | 10 | 电气工程原始资料，原文转录，YAML frontmatter |
| `knowledge/areas/` | 11 | 10 个领域主题页 + `_index.md`，共 115 条目 |
| `knowledge/resources/digest/` | 10 | 每份 raw 对应一份消化记录 |
| `knowledge/resources/concepts/` | 5 | 4 概念卡片 + 模板 |
| `knowledge/resources/topics/` | 2 | 1 元主题 + 模板 |
| `knowledge/resources/notes/` | 2 | 1 捕获笔记 + 模板 |
| `inspection/` | 2 | 巡检报告 + 模板 |
| `outputs/` | 1 | index.html（54KB, 758 行，暗色主题） |
| 规则 | 2 | AGENTS.md + .claude/rules/knowledge-system.md |
| **总计** | **46** | |

## 架构决策记录

1. **采用 PARA**：Areas（长期领域）+ Resources（参考资料）+ Projects（项目）+ Archives（归档）
2. **稳定目录结构 > 方法论正确**：重点不是选最正确的方法，而是给 AI 稳定可预测的组织规则
3. **管道思维**：raw → digest → concepts ↔ areas/topics/notes → index → outputs
4. **文件即真理**：Markdown + YAML frontmatter 是源，应用是编译产物
5. **增量优先**：不批量重建，只处理变化部分
6. **巡检只出报告不自动修**：保证人做判断
7. **冲突显式标记**：不静默覆盖

## 角色定义

> 你不是一次性内容生成器。你是这个系统的维护者。

## 数据流

```
外部数据 → raw/（摄取）
  → resources/digest/（消化：摘要 + 概念抽取 + 冲突标记）
  → resources/concepts/（概念卡片）
  ↔ areas/ + resources/topics/ + resources/notes/（主题页）
  → knowledge/index.md（索引）
  → outputs/（编译输出）
```

## 巡检状态

| 优先级 | 问题 | 状态 |
|--------|------|------|
| P0 | 跨层链接路径错误 | ✅ 已修复 |
| P0 | 死链接占位符 | ✅ 已修复 |
| P1 | AGENTS.md 过时 | ✅ 已修复 |
| P2 | 索引职责重叠 | ✅ 已修复 |
| P3 | digest YAML schema 统一 | ⬜ 待处理 |
| P3 | source_url 单一 | ⬜ 待处理 |

## 待办

- [ ] P3-8：digest 文件统一 `id:` + `updated_at` 前注
- [ ] 用 pi-skills 从外部文章/视频/播客摄取新内容
- [ ] 新增 LLM / AI 相关领域页面
- [ ] 首次实际输出任务（article/infographic/memo 等）
