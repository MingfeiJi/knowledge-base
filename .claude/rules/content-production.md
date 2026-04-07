# 内容生产规则

## 核心原则

**raw = 原汁原味的完整内容**
- 文章：全文，一字不改
- 播客：逐字稿，包括语气词、停顿、互动
- 视频：完整字幕或转写
- 不要摘要，不要提炼，保留所有细节

**wiki = 编译提炼后的精华**
- 这里才做总结、提取、关联
- 保留原文引用，标明出处

**平台内容 = 有血有肉的表达**
- 讲人话，有温度
- 用故事和例子，不要堆术语
- 金句要能脱口而出

---

## 采集策略

### 1. 文章采集

**目标**：获取完整全文

| 来源类型 | 工具 | 注意事项 |
|---|---|---|
| 普通网页 | WebFetch / Jina Reader / curl+python | 确保获取正文全部 |
| 付费墙 | Chrome 浏览器手动 | 登录后复制 |
| 微信公众号 | 手动复制或 API | 图片需单独处理 |
| Twitter/X Thread | 浏览器扩展 | 保留完整线程 |

### 2. 播客/视频采集

**目标**：获取完整逐字稿（Transcript）

| 来源 | 获取方式 |
|---|---|
| YouTube | yt-dlp 下载字幕，或官方 Transcript |
| 播客 | Podwise / Snipd / 官方 Transcript |
| B站 | 字幕下载工具 |
| 无字幕视频 | Whisper 本地转写 |
| 第三方转录网站 | singjupost.com, metacast.app 等 |

**逐字稿要求**：
- 包含说话人标识
- 保留语气词、停顿
- 不要"整理"成书面语

### 3. 优质信息源

**AI 领域一手信息**
- OpenAI Blog / Anthropic Blog / Google AI Blog
- arXiv 论文 / 官方文档

**意见领袖**
- Andrej Karpathy, Yann LeCun, Jim Fan
- 国内: 李沐, 宝玉 (@dotey)

**高质量播客**
- Lex Fridman / Acquired / Latent Space / No Priors

---

## 写作规则

### 讲人话

❌ "RLVR 是针对自动可验证奖励进行强化学习训练的方法"
✅ "简单说，就是让 AI 做数学题，对了奖励，错了惩罚"

### 用故事开头

❌ "本文介绍 Claude Code 的最佳实践"
✅ "上周我用 Claude Code 写了个爬虫，3 小时的活 20 分钟搞定"

### 金句要能脱口而出

❌ "LLM 呈现参差不齐的性能表现"
✅ "AI 上一秒是博士，下一秒被小学生难住"

### 举具体例子

❌ "上下文窗口很重要"
✅ "上下文就像 AI 的工作记忆。塞太多，它就开始犯迷糊"

### 有节奏感

- 长句短句交替
- 重点单独一行
- 留白让人喘息

---

## 工具配置

### yt-dlp 下载字幕
```bash
yt-dlp --write-auto-sub --sub-lang en --skip-download "VIDEO_URL"
```

### Whisper 本地转写
```bash
whisper audio.mp3 --model medium --language en
```

### 网页内容提取 (Python)
```python
import urllib.request, re, html
# ... 提取 <p> 标签内容，清理 HTML
```

---

## 质量检查

采集后：
- [ ] 内容是否完整？（不是摘要）
- [ ] 格式正确？（frontmatter 完整）
- [ ] 来源标注？

写作后：
- [ ] 开头能抓人？
- [ ] 有具体例子？
- [ ] 读出来顺口？
- [ ] 小白能看懂？
