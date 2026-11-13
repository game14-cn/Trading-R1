# 参与贡献

简体中文 | [English](docs/en/CONTRIBUTING.md)

欢迎提交 issue 和 pull request。安全问题请[私下报告](https://github.com/TauricResearch/Trading-R1/security/advisories/new)，不要发在 issue 里。

## Issues

请使用 issue 表单。提供 `trading-r1 --version` 的输出、所用模型、你做了什么、期望得到什么以及
实际发生了什么。提交前请先移除 Key 以及任何隐私内容。

## Pull requests

- 一个 pull request 只改一件事，并说明它做了什么以及为什么。
- 较大的改动或新增依赖，请先开一个 issue。
- 运行 `make lint` 和 `make smoke`，两者都必须通过。

## 代码规范

- Python 3.12 及以上，由 `ruff` 负责格式化与静态检查。TypeScript 由 Biome 格式化。
- 每个源文件都以版权行和 SPDX 行开头。
- 各层只向下导入：先是 `contract`、`state` 和 `providers`，然后是 `runtime`，再是 `tools` 和
  `service`。`runtime` 不导入 `tools`。
- 工具用 `ToolError` 报告可预期的失败，不抛出其他异常。每个价格类工具都要经过
  `tools/data/pricing.py`。
- 注释说明代码做什么，或读者必须知道的约束，不写它的历史。
- 面向用户的文案简短平实。不使用长破折号、短破折号或间隔号。
- `tui/src/lib/events.gen.ts` 和 `assets/taxonomy.svg` 是生成文件，交给维护者处理。
- 不要提交凭据，也不要提交与具体机器相关的路径和主机名。
