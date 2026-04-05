# 内容创作命令

## 用法
```
/create-content <平台> <主题>
```

## 支持平台
- `x` / `twitter` - X/Twitter 推文
- `公众号` / `wechat` - 微信公众号文章
- `小红书` / `xhs` - 小红书笔记
- `thread` - X/Twitter 长推文

## 功能
基于知识库内容，为指定平台生成适配的内容。

## 创作流程

1. **查询知识库**
   - 搜索 wiki/ 中相关概念和摘要
   - 提取关键观点和证据

2. **内容生成**
   - 根据平台特点调整风格
   - 控制字数和格式
   - 添加相关标签

3. **存储位置**
   - X → `x/YYYY-MM-DD-主题.md`
   - 公众号 → `公众号/YYYY-MM-DD-主题.md`
   - 小红书 → `小红书/YYYY-MM-DD-主题.md`

## 平台风格指南

### X/Twitter
- 单条推文 ≤280 字符
- Thread 每条独立可读
- 使用 emoji 增加可读性
- 重点用「」强调

### 公众号
- 标题吸引眼球
- 开头 3 秒抓住注意力
- 分段短小，多用小标题
- 结尾引导互动

### 小红书
- 标题带数字和 emoji
- 图文结合
- 口语化表达
- 标签 #话题#

## 示例
- `/create-content x 巴菲特投资哲学`
- `/create-content 公众号 AI Agent 入门指南`
- `/create-content thread Karpathy 知识库方法论`
