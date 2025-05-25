# 智能舆情分析系统

本项目改自尚硅谷的MCP课程资料，视频地址： https://www.bilibili.com/video/BV1jDVUzSEnz

项目旨在构建一个智能舆情分析系统，输入用户自然语言，实现自动化的新闻检索、情感分析和邮件推送。

## 🚀 功能特性

- **智能新闻检索**：基于Serper API（Google Search封装）进行关键词新闻搜索
- **AI情感分析**：使用大语言模型对新闻内容进行情感倾向分析
- **自动报告生成**：生成Markdown格式的舆情分析报告
- **邮件推送服务**：支持将分析报告作为附件发送邮件
- **MCP架构**：基于Model Context Protocol实现工具调用和会话管理

## 📁 项目结构

```
newAnalys-mcp/
├── README.md              # 项目说明文档
├── pyproject.toml         # 项目配置文件
├── server.py              # MCP服务器端，提供工具函数
├── client.py              # MCP客户端，处理用户交互
├── qwen_api_test.py       # API测试文件
├── google_news/           # 新闻搜索结果存储目录
├── sentiment_reports/     # 情感分析报告存储目录
├── llm_outputs/           # 对话记录存储目录
└── .env                   # 环境变量配置文件（需自行创建）
```

## 🛠 环境配置

### 1. 安装依赖

本项目基于uv包管理器，首先使用下面命令同步依赖：

```shell
cd newAnalys-mcp
uv sync
```

### 2. 环境变量配置

在项目根目录创建 `.env` 文件，配置以下环境变量：

```env
# 大语言模型配置
DASHSCOPE_API_KEY=your_dashscope_api_key
BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
MODEL=qwen-plus

# 新闻搜索API配置
SERPER_API_KEY=your_serper_api_key

# 邮件服务配置
SMTP_SERVER=smtp.qq.com
SMTP_PORT=465
EMAIL_USER=your_email@qq.com
EMAIL_PASS=your_smtp_vaild_code
```

### 3. API密钥获取

- **DashScope API Key**：访问 [阿里云DashScope](https://dashscope.console.aliyun.com/) 获取
- **Serper API Key**：访问 [Serper.dev](https://serper.dev/) 获取
- **邮箱授权码**：在邮箱设置中开启SMTP服务并获取授权码

## 🎯 使用方法

### 启动系统

```shell
# 激活虚拟环境
source .venv/bin/activate  # Linux/Mac
# 或
.venv\Scripts\activate     # Windows

# 运行客户端
uv run ./client.py
```

### 交互示例

启动后，您可以使用自然语言进行查询：

```
你: 分析一下理塘丁真的最新新闻情况，并发送报告到 example@email.com

🤖 AI: 我将为您搜索理塘丁真的最新新闻，进行情感分析，并将报告发送到指定邮箱...
```

系统会自动执行以下流程：
1. 🔍 搜索相关新闻
2. 📊 进行情感分析
3. 📝 生成分析报告
4. 📧 发送邮件通知

## 🔧 核心工具

### 1. search_google_news
- **功能**：根据关键词搜索Google新闻
- **参数**：keyword (搜索关键词)
- **输出**：前5条新闻的标题、描述和链接

### 2. analyze_sentiment
- **功能**：对文本内容进行情感分析
- **参数**：text (文本内容), filename (保存文件名)
- **输出**：Markdown格式的分析报告

### 3. send_email_with_attachment
- **功能**：发送带附件的邮件
- **参数**：to (收件人), subject (主题), body (正文), filename (附件文件名)
- **输出**：邮件发送状态

## 📊 输出文件

- **新闻数据**：`google_news/google_news_YYYYMMDD_HHMMSS.json`
- **分析报告**：`sentiment_reports/sentiment_关键词_YYYYMMDD_HHMMSS.md`
- **对话记录**：`llm_outputs/查询内容_YYYYMMDD_HHMMSS.txt`

## 🔍 技术栈

- **Python 3.12+**
- **MCP (Model Context Protocol)**：工具调用框架
- **OpenAI API**：大语言模型接口
- **httpx**：异步HTTP客户端
- **smtplib**：邮件发送服务

## 📝 注意事项

1. 确保所有API密钥配置正确
2. 邮箱需要开启SMTP服务并使用授权码
3. 网络环境需要能够访问相关API服务
4. 建议在虚拟环境中运行项目

## 🤝 贡献

欢迎提交Issue和Pull Request来改进项目！

## 📄 许可证

本项目基于MIT许可证开源。
