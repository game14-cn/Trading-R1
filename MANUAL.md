# Trading-R1 使用手册

简体中文 | [English](docs/en/MANUAL.md)

每条命令都支持 `--help`，其中还会列出较少使用的命令与选项。

## 命令

| 命令 | 作用 |
|---|---|
| `trading-r1 [QUESTION]` | 打开终端。`--profile NAME`、`--mode MODE` |
| `trading-r1 serve` | 只运行后端，并保持在前台 |
| `trading-r1 export ID` | 导出一份报告。`--format pdf\|md\|html`、`-o FILE`、`--send CHANNELS` |
| `trading-r1 sessions list`、`delete ID` | 你的会话；在这里删除会同时删除你账号中的副本 |
| `trading-r1 channels add KIND`、`list`、`test NAME`、`remove NAME` | 你的推送渠道 |
| `trading-r1 jobs add`、`list`、`run ID`、`runs ID`、`remove ID` | 你的定时报告，以及每次运行的情况 |
| `trading-r1 secrets set NAME`、`list`、`delete NAME` | 已保存的 Key、密码与 token |
| `trading-r1 daemon install`、`status`、`logs`、`uninstall` | 后台服务 |
| `trading-r1 sync status`、`on`、`off`、`pull [ID]` | 会话同步；`pull` 可以从账号找回某个会话 |

`sessions`、`jobs` 以及大部分 `sync` 子命令需要一个正在运行的后端：终端自带的那个、后台服务，
或者 `trading-r1 serve`。

## 设置

在命令面板中打开 **Settings**。

| 设置项 | 作用 | 默认值 |
|---|---|---|
| Verification（校验） | 对照数据记录核对报告中的数字，并重新演算推算出的结果。耗时和 token 大约翻倍。 | 关闭 |
| Source review（来源复核） | 对照引用来源核查报告内容。开启 Verification 时本项被忽略。 | 关闭 |
| Default mode（默认模式） | 应用启动时进入的模式。 | auto |
| Auto-compact（自动压缩） | 在上下文占满模型窗口之前先压缩上下文。 | 开启 |
| Show reasoning（显示推理） | 在对话记录中显示模型的思考过程。 | 开启 |
| Tool details（工具详情） | `brief` 显示工具调用的取值；`full` 按参数名显示全部入参。 | brief |
| Side panel（侧边面板） | 对话记录旁边的计划、数据记录与来源。 | 开启 |
| Also save as Markdown, HTML page（另存为 Markdown、HTML 页面） | 随报告 PDF 一并保存在旁边的文件。 | Markdown 开启，页面关闭 |
| Session sync（会话同步） | 把你的会话副本同步到 Tauric 账号。 | 开启 |
| Remembered notes…（记忆笔记） | 查看或删除智能体记录下的关于你的内容。 | |

## 报告与任务

`TR1_REPORTS_DIR` 用于更改报告目录。当 PDF 无法正确呈现报告文字时，报告会改存为一个 HTML 页面。

```bash
trading-r1 channels add telegram
trading-r1 channels add email --preset gmail --to me@example.com   # 会询问应用专用密码
trading-r1 channels add folder --path briefs
trading-r1 channels test telegram
trading-r1 export SESSION_ID --format pdf -o report.pdf            # 也可 md、html；--turn N
trading-r1 export SESSION_ID --send telegram,email
```

使用 Gmail 时，请开启两步验证并在 Google 账号中生成一个应用专用密码。其他服务商可以用
`--host`、`--port` 和 `--username`。

```bash
trading-r1 jobs add --name "Morning brief" --every weekdays --time 08:00 --tz America/New_York \
    --prompt "What moved my watchlist overnight? NVDA, AAPL, MSFT." --deliver email,telegram
trading-r1 jobs add --name "Weekly review" --every week --weekday fri --time 17:00 \
    --prompt "Review my portfolio's week." --deliver email
trading-r1 jobs list
```

`--cron` 接受任意五字段表达式，`--at 2027-01-04T08:00:00-05:00` 只运行一次。`--profile` 和
`--mode` 用于固定模型与模式。任务是无人值守运行的，因此不会向你提问。

## 会话同步

只要配置了 Tauric Key，无论你使用哪个模型，同步都默认开启：你的会话（包含问题、模型请求与响应
以及工具结果）会复制一份到 `api.tauric.ai` 上的账号。可在 *Settings > Session sync* 中关闭，
或运行 `trading-r1 sync off`。

## 你的数据与 Key

- `trading-r1 secrets set` 和各类 Key 输入框把 Key 存放在 `~/.trading-r1/credentials.json`，
  `trading-r1 daemon install` 会把它们复制到 `~/.trading-r1/daemon.env`。这些文件只有你可读，
  但你自己启动的进程，以及复制该目录的任何备份工具同样能读到。
- 会话、笔记和设置都是 `~/.trading-r1/` 下的普通文件。
- 后端默认监听 `127.0.0.1`，除存活检查外的每条路由都需要 bearer token，该 token 保存在只有
  你能读取的文件里。不要把它暴露在你不信任的网络上。
- 智能体可以代你读取网页、调用数据 API，并把它读到的内容发送给你所选用的模型。
- 报告经由这些服务（你的邮箱服务商、Telegram）推送到你的渠道。开启 `reply` 后，与你的 Telegram
  bot 配对的私聊可以向智能体提问。

## 配置

Key 先是从环境变量读取，再从 `~/.trading-r1/credentials.json` 读取。设置、渠道和模型 profile
都在同一个目录（用 `TR1_HOME` 可以更改位置）。

| 变量 | 作用 |
|---|---|
| `TR1_PROFILE` | 启动时使用的模型 |
| `TR1_REPORTS_DIR` | 报告目录 |
| `TR1_SKILLS_DIR` | 额外一个技能目录 |
| `TR1_PORT` | 后端的端口 |
| `TR1_VLLM_BASE_URL` | 你的 vLLM 服务地址，例如 `http://gpu-box:8000/v1` |
| `TR1_<NAME>_BASE_URL`、`TR1_<NAME>_MODEL`、`TR1_<NAME>_API_KEY` | 某个模型的地址、模型名与 Key |

要新增模型，在 `~/.trading-r1/providers.json` 里给它一个 profile：

```json
{"profiles": {"my-qwen": {"extends": "vllm", "base_url": "http://gpu-box:9000/v1",
                          "reader_profile": "my-qwen"}}}
```

自带地址的 profile 不会发送任何 Key，除非它指定了（`"api_key_env": "MY_KEY"`）。继承自托管
profile 的则会保留原来的 Key，因此要写明它们应当发送哪个 Key。

## 新增技能

技能是 `SKILL.md` 文件，用来告诉智能体如何用现有工具完成某一类工作。把文件放到启动目录下的
`./skills/my-recipe/SKILL.md`，或者放到 `TR1_SKILLS_DIR`。与内置技能同名的技能会覆盖内置技能。
