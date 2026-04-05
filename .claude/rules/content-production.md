# 内容生产规则

## 内容生产链路

```
输入源 → 采集 → 编译 → 创作 → 发布
  │         │       │       │       │
  │         │       │       │       └─ 社交平台
  │         │       │       └─ x/ 公众号/ 小红书/
  │         │       └─ wiki/
  │         └─ raw/
  └─ URL / 搜索 / 推荐
```

## 输入源优先级

### AI 领域优质信息源
1. **一手信息**
   - OpenAI Blog / Anthropic Blog / Google AI Blog
   - arXiv 论文
   - 官方文档和 Changelog

2. **意见领袖**
   - Andrej Karpathy (@karpathy)
   - Yann LeCun (@ylecun)
   - Jim Fan (@DrJimFan)
   - 国内: 李沐, 宝玉 (@dotey)

3. **高质量播客**
   - Lex Fridman Podcast
   - Acquired
   - Latent Space

4. **社区讨论**
   - Hacker News
   - Reddit r/MachineLearning
   - Twitter/X AI 话题

## 采集策略

### 按内容类型
| 类型 | 工具 | 存储位置 |
|---|---|---|
| 网页文章 | WebFetch + Jina | raw/articles/ |
| 社交媒体 | Web Access (CDP) | raw/articles/ |
| 播客转录 | Podwise / Whisper | raw/podcasts/ |
| PDF 论文 | Claude 直接读取 | raw/papers/ |
| 视频字幕 | yt-dlp + Whisper | raw/podcasts/ |

### 反爬处理
- 需登录: 使用 Web Access (复用 Chrome 登录态)
- 动态加载: 使用 CDP 浏览器等待渲染
- 限流: 控制请求频率，使用代理

## 编译策略

### 增量优先
- 每次只处理新增的 raw 文件
- 全量编译仅在结构大改时执行

### 概念提取
- 识别核心术语和概念
- 建立概念间的关联
- 更新索引文件

## 创作策略

### 平台适配
- 了解各平台算法偏好
- 调整内容长度和格式
- 选择最佳发布时间

### 内容复用
- 一份长内容可拆解为多个平台版本
- Thread → 公众号 → 小红书

## Q&A 沉淀

每次复杂问答都应沉淀:
```markdown
---
question: "问题"
asked_at: YYYY-MM-DD
sources: [[[来源1]], [[来源2]]]
---

# 问题标题

## TL;DR

## 详细回答

## 证据/来源

## 不确定性
```

存储位置: `outputs/qa/QA-YYYYMMDD-关键词.md`
