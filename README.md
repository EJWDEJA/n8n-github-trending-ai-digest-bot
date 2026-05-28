# 基于 n8n 与 DeepSeek 的 GitHub 趋势榜 AI 智能筛选与邮件日报系统

这是一个利用低代码流水线引擎 **n8n** 编排，深度融合 **DeepSeek-v4-flash** 大语言模型与 SMTP 服务的云端全自动情报订阅系统。系统每天定时抓取 GitHub Trending 榜单的异构 HTML/文本数据，通过大模型实施智能解析、翻译、价值筛选及热度成因分析，最终实现高价值开源项目的个性化邮件日报精准投递。

## 🚀 核心架构与功能特性
- **定时调度触发（Chronos 层）**：利用 `Schedule Trigger` 配置特定的时间轮询机制，实现每日固定时段的自动化资产盘点。
- **异构数据抓取**：通过 `HTTP Request` 节点高并发请求 GitHub 官方原生 Trending 页面，捕获一手社区动态。
- **大模型动态提示词编排（AI 控制层）**：深度集成 `Basic LLM Chain` 与 `DeepSeek Chat Model`，精心设计角色扮演（科技圈资深主编）提示词拓扑。促使 AI 执行三大核心逻辑：
  1. **智能收敛**：从海量冗余数据中筛选最具爆炸性、实用性的 Top 3 开源项目。
  2. **本地化翻译与链接回溯**：完成高品质的中文意译，并精准回溯其 GitHub 原始 URL。
  3. **热度成因微观剖析**：提供一句话通俗化原理解析，一针见血指出项目爆火的底层逻辑。
- **SMTP 通道封装（分发层）**：借助 `EmailSend` 节点，将大模型输出的结构化文本（文本/HTML 格式）无缝封装，通过标准邮件传输协议高效触达用户终端。

## 🛠 技术栈
- **Workflow Automation**: n8n
- **LLM Engine**: DeepSeek-v4-flash (via LangChain Node)
- **Framework**: LangChain Integration (`chainLlm` / `lmChatDeepSeek`)
- **Protocols**: HTTP (Data Fetch) / SMTP (Email Delivery)
- **Data Architecture**: Structured JSON

## 📦 如何部署与使用
1. 下载本项目中的 `workflow.json` 文件。
2. 在您的 n8n 工作流画布空白处直接按 `Ctrl + V`（或导入 JSON），即可一键复现完整的 AI 节点网络拓扑。
3. **节点配置调整**：
   - 在 `DeepSeek Chat Model` 节点中配置您的个人 DeepSeek API Key。
   - 在 `Send an Email` 节点中配置您的发件/收件邮箱及 SMTP 授权凭证。
