# OpenClaw 🦞 — 你的助手，跑在你自己的设备上，就在你常用的聊天里

<p align="center">
  <a href="README.md">English</a> ·
  <b>简体中文</b>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-banner-light.png">
    <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-banner-dark.png" alt="OpenClaw — EXFOLIATE! EXFOLIATE! 你的 AI 助手，运行在你自己的设备上。">
  </picture>
</p>

<p align="center">
  <a href="https://github.com/openclaw/openclaw/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/openclaw/openclaw/ci.yml?branch=main&style=flat-square&label=ci" alt="CI 状态"></a>
  <a href="https://www.npmjs.com/package/openclaw"><img src="https://img.shields.io/npm/v/openclaw?style=flat-square&label=npm" alt="npm 版本"></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/node/v/openclaw?style=flat-square" alt="Node.js 版本"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" alt="许可证：MIT"></a>
  <a href="https://discord.gg/clawd"><img src="https://img.shields.io/discord/1456350064065904867?label=discord&logo=discord&logoColor=white&color=5865F2&style=flat-square" alt="Discord"></a>
</p>

OpenClaw 是一个开源 AI 助手，运行在你自己的电脑上，并在你已经在用的渠道里与你见面：Discord、iMessage、Slack、Teams、Telegram、WhatsApp，以及另外 20 多种渠道，此外还提供 macOS、iOS、Android、Windows 和 Linux 的原生应用。同一个 Gateway 既可以作为笔记本上的个人助手运行，也可以作为共享的[团队部署](https://docs.openclaw.ai/start/teams)，两者唯一的差别就是配置。

**完全属于你，没有任何附加条件。** 状态、记忆和凭据都存放在你自己的硬件上。模型和 agent 框架（Claude、Codex、本地模型）都是可以随时替换的插件，换掉它们不会影响其他任何部分。你的提示词只会发送给你自己配置的模型提供商和聊天平台，以及你主动启用的诊断数据导出；默认情况下，OpenClaw 自身对外发起的请求仅仅是每天一次的版本检查，匿名功能统计需要你主动选择加入，而 `update.checkOnStart: false` 可以同时关掉这两者（[OpenClaw 会发送什么](https://docs.openclaw.ai/gateway/telemetry)）。OpenClaw 由[OpenClaw 基金会](https://openclaw.org)（一家独立的 501(c)(3) 非营利组织）负责治理，没有付费档位、托管服务或代币。其架构主张——可信网关、不可信执行、由代码强制的策略——写在 [Why OpenClaw](https://docs.openclaw.ai/start/why-openclaw) 里。

[官网](https://openclaw.ai) · [文档](https://docs.openclaw.ai) · [入门指南](https://docs.openclaw.ai/start/getting-started) · [为什么选择 OpenClaw](https://docs.openclaw.ai/start/why-openclaw) · [常见问题](https://docs.openclaw.ai/help/faq) · [愿景](VISION.md) · [DeepWiki](https://deepwiki.com/openclaw/openclaw)

## 安装

安装程序支持 macOS、Linux 和 Windows，并在需要时自动准备好受支持的 Node.js 运行时。

```bash
# macOS / Linux / WSL2
curl -fsSL https://openclaw.ai/install.sh | bash
```

```powershell
# Windows PowerShell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

已经在自己管理 Node.js？那就直接安装已发布的包（需要 Node 24.16+ 或 26.1+，推荐 Node 26）：

```bash
npm install -g openclaw@latest --allow-scripts=openclaw
```

上面这条命令适用于 npm 12 或 npm 11.16+。如果你用的是 npm 11.15 及更早版本，请去掉 `--allow-scripts=openclaw`。关于生命周期脚本约定、Docker、Nix 以及其他部署方式，请参阅[安装指南](https://docs.openclaw.ai/install)。

## 快速开始

全新安装时，安装脚本会自动启动引导流程，完成它打开的向导即可。如果你是直接用 npm、pnpm 或 Bun 安装的包，请运行：

```bash
openclaw onboard --install-daemon
```

引导完成之后：

```bash
openclaw gateway status
openclaw dashboard
```

引导流程会校验模型访问权限、创建工作区并配置 Gateway。最后一条命令会打开 Control UI，在那里发一条消息即可确认助手是否正常工作。渠道配置和故障排查见[入门指南](https://docs.openclaw.ai/start/getting-started)。

## 整体架构

- [Gateway](https://docs.openclaw.ai/gateway) 是会话、工具、事件和渠道连接的本地控制平面。
- [Control UI](https://docs.openclaw.ai/web/control-ui)、CLI 和 [TUI](https://docs.openclaw.ai/web/tui) 都连接到 Gateway。
- [渠道（Channels）](https://docs.openclaw.ai/channels) 把助手带到 WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage 等消息服务中。
- [配套应用与节点](https://docs.openclaw.ai/platforms) 在受支持的平台上提供语音、Canvas、摄像头、屏幕以及设备本地操作能力。

OpenClaw 同时支持托管型和本地[模型提供商](https://docs.openclaw.ai/concepts/model-providers)。它的[工具](https://docs.openclaw.ai/tools)、[技能](https://docs.openclaw.ai/tools/skills)和[插件](https://docs.openclaw.ai/plugins)可以扩展助手能做的事。

## 安全

请把收到的消息当作不可信输入。支持私信的渠道默认对未知发送者进行配对；你可以用 `openclaw pairing approve <channel> <code>` 批准某个配对请求。

除非你另行配置了沙箱，否则工具会在主会话所在的主机上运行。在让其他用户接入、或把 Gateway 暴露到远程之前，请先阅读[安全指南](https://docs.openclaw.ai/gateway/security)、[暴露应对手册](https://docs.openclaw.ai/gateway/security/exposure-runbook)和[沙箱指南](https://docs.openclaw.ai/gateway/sandboxing)。

## 文档

| 目标 | 从这里开始 |
| ---- | ---------- |
| 配置模型与认证 | [Models（模型）](https://docs.openclaw.ai/concepts/models) · [Model providers（模型提供商）](https://docs.openclaw.ai/concepts/model-providers) |
| 接入消息服务 | [Channels（渠道）](https://docs.openclaw.ai/channels) |
| 添加工具、技能和插件 | [Tools（工具）](https://docs.openclaw.ai/tools) · [Skills（技能）](https://docs.openclaw.ai/tools/skills) · [Plugins（插件）](https://docs.openclaw.ai/plugins) · [ClawHub](https://clawhub.ai) |
| 运行应用与设备节点 | [Platforms（平台）](https://docs.openclaw.ai/platforms) · [Nodes（节点）](https://docs.openclaw.ai/nodes) |
| 使用 CLI 与聊天命令 | [CLI reference（CLI 参考）](https://docs.openclaw.ai/cli) · [Slash commands（斜杠命令）](https://docs.openclaw.ai/tools/slash-commands) |
| 配置或运维 Gateway | [Configuration（配置）](https://docs.openclaw.ai/gateway/configuration) · [Architecture（架构）](https://docs.openclaw.ai/concepts/architecture) · [Updating（更新）](https://docs.openclaw.ai/install/updating) · [Release channels（发布渠道）](https://docs.openclaw.ai/install/development-channels) |

## 开发

本仓库是一个 pnpm workspace。不支持在仓库根目录直接执行 `npm install`。

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
pnpm install
pnpm build
pnpm ui:build
```

贡献流程参见 [CONTRIBUTING.md](CONTRIBUTING.md)，开发迭代流程参见[源码搭建指南](https://docs.openclaw.ai/start/setup)。

## 治理

OpenClaw 由[OpenClaw 基金会](https://openclaw.org)（一家独立的 501(c)(3) 非营利组织）以完全公开的方式开发。基金会雇用核心团队并签署发布。捐赠者和基础设施赞助方为基金会提供支持，但他们都不拥有也不主导这个项目。OpenAI 是捐赠者，不是所有者。

## 社区

维护者名单与贡献指南见 [CONTRIBUTING.md](CONTRIBUTING.md)；欢迎 AI 辅助产出的 PR。

用 [issue 选择器](https://github.com/openclaw/openclaw/issues/new/choose)提交 bug 和功能请求，配置类问题到 [Discord](https://discord.gg/clawd) 提问，安全漏洞请通过 [SECURITY.md](SECURITY.md) 报告。新的能力通常应该做成基于[插件 SDK](https://docs.openclaw.ai/plugins/building-plugins) 的插件，并通过 [ClawHub](https://clawhub.ai) 分享。

OpenClaw 由 Peter Steinberger 和社区为 **Molty**（一只太空龙虾 AI 助手）而打造。去看看[项目背景故事](https://docs.openclaw.ai/start/lore)、[soul.md](https://soul.md)、[Peter 的主页](https://steipete.me)、[Star History](https://www.star-history.com/#openclaw/openclaw&type=date&legend=top-left) 和 [@openclaw](https://x.com/openclaw)。

特别感谢 [Mario Zechner](https://mariozechner.at/) 的支持以及他的 [pi](https://github.com/earendil-works/pi)，也感谢 Adam Doppelt 提供的 lobster.bot 域名。

## 捐赠者与赞助方

基金会的资金来自捐赠者，包括 Amazon、Lobster Computer Company、Offline Holdings、OpenAI、Red Hat 和 University of Michigan；基础设施支持来自 Blacksmith、Convex、GitHub、NVIDIA 和 Vercel。

<table>
  <tr>
    <td align="center"><a href="https://blacksmith.sh/"><picture><source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/blacksmith-light.svg"><img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/blacksmith.svg" alt="Blacksmith" height="28"></picture></a></td>
    <td align="center"><a href="https://www.convex.dev/"><picture><source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/convex-light.svg"><img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/convex.svg" alt="Convex" height="24"></picture></a></td>
    <td align="center"><a href="https://github.com/"><picture><source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/github-light.svg"><img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/github.svg" alt="GitHub" height="28"></picture></a></td>
    <td align="center"><a href="https://www.nvidia.com/"><picture><source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/nvidia.svg"><img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/nvidia-dark.svg" alt="NVIDIA" height="28"></picture></a></td>
    <td align="center"><a href="https://github.com/openai"><picture><source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/openai-light.svg"><img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/openai.svg" alt="OpenAI" height="28"></picture></a></td>
    <td align="center"><a href="https://www.redhat.com/"><picture><source media="(prefers-color-scheme: light)" srcset="docs/assets/sponsors/redhat-light.svg"><img src="docs/assets/sponsors/redhat.svg" alt="Red Hat" height="28"></picture></a></td>
    <td align="center"><a href="https://vercel.com/"><picture><source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/vercel-light.svg"><img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/sponsors/vercel.svg" alt="Vercel" height="24"></picture></a></td>
  </tr>
</table>

## 贡献者

感谢所有 clawtributors！贡献者名单由机器人自动生成并持续更新，请以 [英文版 README](README.md) 中的 Clawtributors 区块为准。

本文件是 [README.md](README.md) 的简体中文翻译，内容以英文版为准。


## 许可证

[MIT](LICENSE) © OpenClaw Foundation。已合并或改编的代码详见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
