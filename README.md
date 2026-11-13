<p align="center">
  <a href="https://tauric.ai/">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="assets/Trading-R1-dark.svg">
      <img src="assets/Trading-R1.svg" alt="Trading-R1" width="60%">
    </picture>
  </a>
</p>

<p align="center">
  <a href="https://arxiv.org/abs/2509.11420"><img alt="arXiv" src="https://img.shields.io/badge/arXiv-2509.11420-B31B1B?logo=arxiv"/></a>
  <a href="https://discord.com/invite/hk9PGKShPK"><img alt="Discord" src="https://img.shields.io/badge/Discord-TauricResearch-7289da?logo=discord&amp;logoColor=white"/></a>
  <a href="https://x.com/TauricResearch"><img alt="X" src="https://img.shields.io/badge/X-TauricResearch-white?logo=x&amp;logoColor=white"/></a>
  <a href="https://github.com/TauricResearch/"><img alt="GitHub" src="https://img.shields.io/badge/GitHub-TauricResearch-14C290?logo=github&amp;logoColor=white"/></a>
  <a href="https://tauric.ai/"><img alt="Website" src="https://img.shields.io/badge/Website-tauric.ai-14C290?logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZmZmIiBzdHJva2Utd2lkdGg9IjIiPjxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjEwIi8+PHBhdGggZD0iTTIgMTJoMjBNMTIgMmExNSAxNSAwIDAgMSAwIDIwTTEyIDJhMTUgMTUgMCAwIDAgMCAyMCIvPjwvc3ZnPg=="/></a>
</p>

<p align="center">
  <a href="docs/en/README.md">English</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=de">Deutsch</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=es">Español</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=fr">français</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=ja">日本語</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=ko">한국어</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=pt">Português</a> |
  <a href="https://www.readme-i18n.com/TauricResearch/Trading-R1?lang=ru">Русский</a>
</p>

<h2 align="center">Trading-R1：面向金融研究与分析的终端工具</h2>

<p align="center">
  <img src="assets/trading-r1.gif" alt="Trading-R1 在终端中回答一个研究问题" width="100%">
</p>

## 快速开始

**1. 注册 Tauric 账号并获取 API Key。** [注册](https://tauric.ai/signup)，然后
[创建 Key](https://tauric.ai/settings/api-keys)。

**2. 安装。**

```bash
curl -fsSL https://raw.githubusercontent.com/TauricResearch/Trading-R1/main/install.sh | sh
```

或者，在已具备 Python 3.12 及以上版本和 `bun` 的环境下：`pip install trading-r1`。

**3. 填入 Key 并启动。**

```bash
export TAURIC_API_KEY=your-key
trading-r1
```

如果希望持久保存 Key，运行 `trading-r1 secrets set TAURIC_API_KEY`，或在应用里按 `/`
并选择 *API keys…*。

卸载时，若安装过后台服务，先运行 `trading-r1 daemon uninstall`，再执行
`uv tool uninstall trading-r1` 或 `pip uninstall trading-r1`。你的数据保留在 `~/.trading-r1`
和报告目录中。

## 选择模型

| 名称 | 模型 | 所需条件 |
|---|---|---|
| `tauric` | `tauric` | `TAURIC_API_KEY` |
| `gpt` | `gpt-6.1-sol` | `OPENAI_API_KEY` |
| `anthropic` | `claude-sonnet-5-5` | `ANTHROPIC_API_KEY` |
| `gemini` | `gemini-3.8-flash` | `GEMINI_API_KEY` |
| `vllm` | `Qwen3.8-27B` | 由你自己运行的 vLLM 服务 |

应用会按 OpenAI、Anthropic、Gemini、Tauric、vLLM 的顺序，启动第一个你已配置好的模型。
可在命令面板中用 *Model…* 切换，或用 `trading-r1 --profile gpt` 指定启动模型。要把
`vllm` 指向你自己的服务，见[配置](MANUAL.md#配置)。

## 使用方式

```bash
trading-r1                                          # 打开终端
trading-r1 "What's NVDA's last quarterly revenue?"  # 并抛出第一个问题
trading-r1 --mode analytical                        # 以某个模式启动
```

| 按键 | 作用 |
|---|---|
| `/` 或 `^K` | 打开命令面板 |
| `shift+tab` | 循环切换模式 |
| `^N` | 开始新的研究 |
| `esc` | 取消正在执行的回合，或关闭对话框 |
| `^C` | 退出 |

| 模式 | 侧重点 |
|---|---|
| `auto` | 可用全部工具，由智能体自行决策 |
| `research` | 以网络检索为主，适合深度研究 |
| `analytical` | 以数字为主：优先使用数据与估值工具，网络用于补充背景 |

命令面板列出全部操作：会话、模型与模式、报告、推送渠道、定时报告、工具与技能、API keys、
后台服务、Settings 和 Help。

## 架构

<p align="center">
  <img src="assets/taxonomy.svg" alt="Trading-R1 的工具：始终加载的工具、按学科与领域划分的金融工具，以及工作流技能" width="100%">
</p>

## 报告与推送

*Export report…* 会把最近一次回答保存为 PDF，并默认同时保存 Markdown，位置在
`~/Documents/Trading-R1` 或 `~/Trading-R1`。

*Send report…* 会把报告推送到你的渠道；如果还没有配置任何渠道，会先引导你完成配置。

| 渠道 | 你需要提供 | 会收到 |
|---|---|---|
| `telegram` | 从 @BotFather 获取的 bot token，然后给该 bot 发一条消息并确认会话 | 文本与 PDF |
| `email` | 你的邮箱地址和一个应用专用密码（预设：`gmail`、`icloud`、`yahoo`、`fastmail`） | 文本与 PDF |
| `folder` | 一个本地路径 | 报告文件 |

想在手机上提问，把 Telegram 渠道的 `reply` 设为 `on`。只要后端服务在运行，你的 bot 就会用一次
简短的研究来回复你发来的消息，`/new` 可重新开始。

## 定时报告

任务会按计划定时提出问题，并把报告推送到你的渠道。使用命令面板里的 *Scheduled reports…*，或：

```bash
trading-r1 jobs add --name "Morning brief" --every weekdays --time 08:00 --tz America/New_York \
    --prompt "What moved my watchlist overnight? NVDA, AAPL, MSFT." --deliver email,telegram
```

报告、渠道和任务的完整命令与选项见[使用手册](MANUAL.md#报告与任务)。

## 后台服务

定时任务和 Telegram 自动回复都需要后端持续运行，而终端进程在你关闭窗口后就会停止。要保持后端
常驻，可安装一个用户级服务（Linux 使用 systemd，macOS 使用 launchd），入口是命令面板中的
*Background service…*，或：

```bash
trading-r1 daemon install      # 另有：status、logs、start、stop、restart、uninstall
```

升级之后，或在 shell 配置里改动过 Key 之后，请重新运行 `trading-r1 daemon install`。

## 使用手册

命令、设置、会话同步、你的数据与 Key、配置以及新增技能的说明都在
[用户手册](MANUAL.md) 中。若要参与代码开发，见 [参与贡献](CONTRIBUTING.md)。

## 引用

```bibtex
@article{xiao2025trading,
  title={Trading-r1: Financial trading with llm reasoning via reinforcement learning},
  author={Xiao, Yijia and Sun, Edward and Chen, Tong and Wu, Fang and Luo, Di and Wang, Wei},
  journal={arXiv preprint arXiv:2509.11420},
  year={2025}
}
```

## 免责声明

仅供研究与教育使用，不构成投资建议。

## 许可证

Apache-2.0，详见 [LICENSE](LICENSE)。
