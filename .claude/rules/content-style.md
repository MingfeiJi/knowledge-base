# 内容风格规则

## 写作原则

### 1. 简洁清晰
- 一句话一个观点
- 避免冗余修饰
- 用具体代替抽象

### 2. 结构化
- 使用标题分层
- 善用列表和表格
- 逻辑递进清晰

### 3. 可追溯
- 每个观点标注来源
- 区分事实和观点
- 保留原文引用

## 命名规范

### 文件命名
- 摘要: `S-XXX 标题.md`
- 概念: `C-XXX 概念名.md`
- Q&A: `QA-YYYYMMDD-关键词.md`
- 健康报告: `Health-YYYYMMDD.md`

### 标签命名
- 使用小写
- 多词用连字符: `ai-agent`
- 分类标签: `type/article`, `topic/investing`

## Frontmatter 规范

### 必填字段
```yaml
---
title: 标题
created: YYYY-MM-DD
---
```

### 可选字段
```yaml
---
source_url: URL
author: 作者
published: 发布日期
updated: 更新日期
tags: [tag1, tag2]
aliases: [别名1, 别名2]
---
```

## 链接规范

### 内部链接
- 使用 `[[文件名]]` 格式
- 概念链接: `[[C-001 内在价值]]`
- 带显示文本: `[[C-001 内在价值|内在价值]]`

### 外部链接
- 使用 `[文本](URL)` 格式
- 重要链接添加存档
