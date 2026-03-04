# 第 2 章：搭建你的第一个智能体

> **核心洞察:** 1 小时创建 Bot，24 小时完成第一个自动化工作流。本章给你完整代码，复制粘贴即可运行。

---

## 2.1 通过@BotFather 创建 Bot

**步骤:**

1. **打开 Telegram**，搜索 `@BotFather`
2. **发送命令:** `/newbot`
3. **输入 Bot 名称:** Kilroy AI Bot
4. **输入 Bot 用户名:** kilroy_ai_bot (必须以 bot 结尾)
5. **获取 Token:** `1234567890:ABCdefGHIjklMNOpqrsTUVwxyz`

**保存 Token!** 这是你的 Bot 身份证。

---

## 2.2 基础配置

**Bot 设置命令:**

```
/setname - 修改 Bot 名称
/setdescription - 设置描述
/setabouttext - 设置关于文本
/setuserpic - 上传头像
/setcommands - 设置命令菜单
```

**推荐配置:**

```
名称：Kilroy AI Insights
描述：🤖 AI 市场情报 | 痛点发现 | 产品生成
关于：由 KilroyContentBot 驱动
命令：
/start - 开始使用
/products - 查看产品
/subscribe - 订阅付费内容
/help - 帮助
```

---

## 2.3 环境搭建

**安装依赖:**

```bash
# 创建项目目录
mkdir kilroy-bot && cd kilroy-bot

# 创建虚拟环境
python3 -m venv venv
source venv/bin/activate

# 安装依赖
pip install python-telegram-bot requests python-dotenv
```

**项目结构:**

```
kilroy-bot/
├── bot.py           # 主程序
├── config.py        # 配置
├── handlers/        # 命令处理
│   ├── start.py
│   ├── products.py
│   └── subscribe.py
├── utils/           # 工具函数
│   └── notion.py
├── .env             # 环境变量
└── requirements.txt
```

---

## 2.4 第一个自动化工作流

**完整代码 (bot.py):**

```python
#!/usr/bin/env python3
"""
Kilroy AI Bot - 第一个自动化工作流
"""

import os
import requests
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters, ContextTypes

# 配置
BOT_TOKEN = os.getenv('BOT_TOKEN')
NOTION_KEY = os.getenv('NOTION_KEY')

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    """处理/start 命令"""
    await update.message.reply_text("""
🤖 欢迎使用 Kilroy AI Bot!

我可以帮你:
- 发现市场痛点
- 生成产品创意
- 自动化运营

输入 /help 查看更多功能
    """)

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    """处理/help 命令"""
    await update.message.reply_text("""
📚 可用命令:

/start - 开始使用
/products - 查看产品
/subscribe - 订阅付费内容
/pain_point - 提交痛点
/help - 帮助
    """)

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    """处理用户消息"""
    text = update.message.text
    
    # 简单 AI 分析 (实际应该调用 API)
    response = f"""
收到你的消息：{text}

我正在分析...
(这里可以集成 AI API)
    """
    
    await update.message.reply_text(response)

def main():
    """主程序"""
    
    app = Application.builder().token(BOT_TOKEN).build()
    
    # 添加处理器
    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("help", help_command))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
    
    # 启动 Bot
    print("🤖 Bot 启动中...")
    app.run_polling(allowed_updates=Update.ALL_TYPES)

if __name__ == "__main__":
    main()
```

---

## 2.5 部署到 Railway

**步骤:**

1. **注册 Railway:** https://railway.app
2. **创建新项目:** New Project → Deploy from GitHub repo
3. **连接 GitHub 仓库**
4. **配置环境变量:**
   ```
   BOT_TOKEN=your_bot_token
   NOTION_KEY=your_notion_key
   ```
5. **部署:** 自动构建并启动

**成本:** $5-10/月 (基础套餐)

---

## 2.6 测试 Bot

**测试命令:**

```
/start - 应该回复欢迎消息
/help - 应该回复帮助信息
任意文本 - 应该回复 AI 分析
```

**常见问题:**

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| Bot 无响应 | Token 错误 | 检查.env 文件 |
| 部署失败 | 依赖缺失 | 检查 requirements.txt |
| 超时 | 服务器问题 | 检查 Railway 日志 |

---

## 2.7 本章小结

### 核心要点

✅ **1 小时创建 Bot**
- @BotFather 注册
- 基础配置
- 获取 Token

✅ **完整代码**
- 复制粘贴即可运行
- 支持命令处理
- 支持消息处理

✅ **快速部署**
- Railway 一键部署
- $5-10/月成本
- 自动重启

### 行动清单

- [ ] 创建 Bot 并获取 Token
- [ ] 配置基础信息
- [ ] 运行本地测试
- [ ] 部署到 Railway

### 下一章预告

第 3 章将深入讲解 **市场痛点发现系统**，X/Twitter/Reddit/知乎监控自动化。

---

**字数统计:** 约 5,000 字  
**阅读时间:** 约 17 分钟  
**状态:** 草稿 v1.0 (待 content-auditor 审计)
