# 知识库编译规范 (CLAUDE.md)

基于 Karpathy 的 "LLM Knowledge Bases" 方法论。

## 目录结构

```
知识库-鸣老师/
├── raw/                    # 原始资料，不修改
│   ├── articles/           # Web Clipper 剪藏
│   ├── podcasts/           # Podwise 导出
│   ├── papers/             # 论文
│   ├── books/              # 书籍笔记
│   └── buffett-letters/    # 巴菲特信件（已编译的知识库）
│
├── wiki/                   # 编译产物，LLM 维护
│   ├── indexes/            # 索引
│   │   ├── All-Sources.md      # 来源清单
│   │   ├── All-Concepts.md     # 概念清单
│   │   └── Glossary.md         # 术语表
│   ├── concepts/           # 概念条目
│   └── summaries/          # 逐篇摘要
│
├── outputs/                # 运行时输出
│   ├── qa/                 # 问答沉淀
│   └── health/             # 健康检查报告
│
├── x/                      # X 平台成品
├── 公众号/                  # 公众号成品
└── 小红书/                  # 小红书成品
```

## 编译规范

### 1. 摘要模板 (wiki/summaries/)

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
（3句话内概括核心观点）

## 核心结论
-

## 关键证据
-

## 相关概念
- [[概念1]]
- [[概念2]]

## 疑点/待验证
-

## 原文引用
>
```

### 2. 概念条目模板 (wiki/concepts/)

```markdown
---
aliases: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# 概念名称

## 定义
（一句话定义）

## 详细解释
（2-3段解释）

## 关键特征
-

## 典型例子
-

## 相关概念
- [[]]

## 来源引用
- [[wiki/summaries/来源摘要]]
```

### 3. Q&A 模板 (outputs/qa/)

```markdown
---
question: "问题"
asked_at: YYYY-MM-DD
sources:
  - [[来源1]]
  - [[来源2]]
---

# 问题标题

## TL;DR
（简短回答）

## 详细回答


## 证据/来源
（链接回原始来源）

## 不确定性/待验证
-
```

### 4. 健康检查模板 (outputs/health/)

```markdown
---
check_date: YYYY-MM-DD
---

# 健康检查报告 - YYYY-MM-DD

## 一致性问题
（定义冲突的概念）

## 完整性问题
（缺定义/例子/来源的条目）

## 孤岛笔记
（入链出链少于2的笔记）

## 建议操作
- [ ]
```

## 命名规则

1. **摘要文件**: `S-XXX 原标题.md` (如 `S-001 Karpathy LLM知识库.md`)
2. **概念文件**: `C-XXX 概念名.md` (如 `C-001 内在价值.md`)
3. **Q&A 文件**: `QA-YYYYMMDD-关键词.md`
4. **健康报告**: `Health-YYYYMMDD.md`

## 编译流程

### 增量编译（每次新增 raw 后执行）

1. **读取** raw/ 中新增/修改的文件
2. **生成摘要** → 存入 wiki/summaries/
3. **提取概念** → 更新 wiki/concepts/
4. **更新索引** → 更新 wiki/indexes/

### 健康检查（每周执行）

1. 检查概念定义一致性
2. 检查条目完整性
3. 识别孤岛笔记
4. 生成报告 → outputs/health/

## 索引文件格式

### All-Sources.md

```markdown
# 来源索引

## 按类型

### 文章
| ID | 标题 | 作者 | 日期 | 摘要 |
|---|---|---|---|---|

### 播客
...

### 论文
...

## 按时间
...

## 按主题
...
```

### All-Concepts.md

```markdown
# 概念索引

| ID | 概念 | 定义 | 相关来源数 | 最后更新 |
|---|---|---|---|---|
```

## API 配置

使用云雾 API 进行 LLM 调用：

```python
from openai import OpenAI

client = OpenAI(
    api_key="sk-TzMsxrBRuxyDRKO0hQAu2SCVHIaCa6NJ5diWjqXLyMbJOfJj",
    base_url="https://yunwu.ai/v1"
)

# 推荐模型
# - 编译任务: kimi-k2.5, claude-sonnet-4-20250514
# - 快速任务: gpt-4o-mini, deepseek-chat
```

## 同步规则

- 本地 Obsidian → GitHub 仓库
- 同步频率: 每日自动 / 手动触发
- 忽略文件: `.obsidian/`, `.trash/`, `.DS_Store`
