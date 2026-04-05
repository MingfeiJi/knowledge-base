# 内容采集命令

## 用法
```
/fetch-content <URL或关键词>
```

## 功能
从指定 URL 或搜索关键词获取内容，自动整理成 Markdown 格式存入知识库。

## 执行步骤

1. **判断输入类型**
   - URL: 直接抓取页面内容
   - 关键词: 先搜索找到相关来源，再抓取

2. **内容抓取策略**
   - 公开网页: 使用 WebFetch + Jina
   - 需登录/动态网页: 使用 Web Access (CDP 浏览器)
   - 社交媒体: 优先 Web Access

3. **内容处理**
   - 提取标题、作者、日期
   - 转换为 Markdown 格式
   - 添加 frontmatter 元数据

4. **存储位置**
   - 文章 → `raw/articles/`
   - 播客 → `raw/podcasts/`
   - 论文 → `raw/papers/`

5. **输出格式**
```markdown
---
source_url:
author:
published:
fetched: YYYY-MM-DD
tags: []
---

# 标题

[内容正文]
```

## 示例
- `/fetch-content https://example.com/article`
- `/fetch-content AI大模型最新进展`
- `/fetch-content Karpathy 最新播客`
