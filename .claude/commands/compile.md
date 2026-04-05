# 知识库编译命令

## 用法
```
/compile [增量|全量]
```

## 功能
将 raw/ 目录的原始资料编译成 wiki/ 的结构化知识。

## 编译流程

### 增量编译（默认）
只处理新增/修改的 raw 文件：

1. **扫描变更** - 对比上次编译时间，找出新增文件
2. **生成摘要** - 为每个新文件生成结构化摘要
3. **提取概念** - 识别并更新概念条目
4. **更新索引** - 更新 All-Sources.md 和 All-Concepts.md

### 全量编译
重新处理所有 raw 文件（耗时较长）

## 输出位置
- 摘要 → `wiki/summaries/S-XXX 标题.md`
- 概念 → `wiki/concepts/C-XXX 概念名.md`
- 索引 → `wiki/indexes/`

## 摘要模板
```markdown
---
source: [[raw/articles/原文件名]]
source_url:
author:
created: YYYY-MM-DD
tags: []
---

# 标题

## TL;DR
（3句话概括）

## 核心结论
-

## 关键证据
-

## 相关概念
- [[C-XXX 概念]]

## 疑点/待验证
-
```

## 示例
- `/compile` - 增量编译
- `/compile 全量` - 全量重建
