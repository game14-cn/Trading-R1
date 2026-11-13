# 更新日志

简体中文 | [English](docs/en/CHANGELOG.md)

## [0.1.1] - 2026-11-09

- 报告：PDF 改用 Noto Sans 字体，并包含 Noto Sans SC 与 KR，因此能够呈现中文、日文、韩文文本，以及货币
  符号、分数和箭头等常用符号。
- 导出：终端和 `trading-r1 export` 在报告无法生成 PDF 时会说明原因，并提供 HTML 页面。
- 公式改用 Markdown 书写，不再使用 LaTeX。
- Telegram：报告标题由任务名（或 Trading-R1）加上日期组成；表格中的每一行渲染成一行文字。

## [0.1.0] - 2026-11-04

Trading-R1 的首个正式版本，由 [Tauric Research](https://tauric.ai/) 出品的金融研究与分析终端。

- 提出一个问题，智能体会拉取市场数据、阅读网页、完成计算，并写出一份带引用的报告。
- 68 个工具与 17 个工作流技能：公司、市场与宏观数据；估值、风险、投资组合、统计、固定收益与衍生品。
- 模型：Tauric、OpenAI、Anthropic、Gemini、vLLM 与 Ollama。
- 报告可输出为 PDF、Markdown 或 HTML 页面，并发送到 Telegram、邮箱或一个文件夹。
- 定时报告、适用于 Linux 与 macOS 的后台服务，以及 Telegram 回复。
- 会话同步到你的 Tauric 账号（默认开启），以及你自己编写的 `SKILL.md` 工作流。
