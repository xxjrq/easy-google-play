<div align="center">

<img src="assets/icon-512.png" width="112" height="112" alt="easyGooglePlay 图标">

# easyGooglePlay

## Google Play Console 自动上架 Agent Skill

让 Claude Code、Codex、OpenCode、WorkBuddy 等 AI Agent 读取 Android 项目，完成 AAB 构建、商店资料、政策表单、Production Release、审核提交和驳回处理。

[简体中文](README.md) | [English](README.en.md)

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-20C77A?style=flat-square)](https://agentskills.io/)
[![Easy WebBridge](https://img.shields.io/badge/runtime-Easy%20WebBridge-111827?style=flat-square)](https://github.com/xxjrq/easy-webbridge)
[![GitHub Stars](https://img.shields.io/github/stars/xxjrq/easy-google-play?style=flat-square)](https://github.com/xxjrq/easy-google-play/stargazers)
[![skills.sh](https://skills.sh/b/xxjrq/easy-google-play)](https://skills.sh/xxjrq/easy-google-play)
[![License](https://img.shields.io/badge/license-MIT-16A34A?style=flat-square)](LICENSE)

</div>

## 它能做什么

- 自动识别原生 Android、Flutter、React Native、Unity、Gradle 和 Fastlane 项目。
- 根据项目现状生成 Release 构建命令，得到并上传 AAB。
- 上传 App 图标、Feature Graphic、手机和平板截图及审核视频。
- 填写商店详情、Data Safety、广告、应用访问权限、内容分级和目标受众。
- 按应用能力处理 VPN、前台服务及其他政策声明。
- 创建 Production Release，发送更改审核，并检查真实发布状态。
- 读取驳回信息，判断应修改安装包、商店资料还是政策声明。

## 它与 Easy WebBridge 的关系

```text
Claude Code / Codex / OpenCode / WorkBuddy
                    |
            easyGooglePlay Skill
          项目构建 + 上架业务流程
                    |
          Easy WebBridge 127.0.0.1:17777
                    |
        浏览器扩展 + 已登录 Google Play Console
```

`easyGooglePlay` 是独立业务 Skill，`Easy WebBridge` 是所有浏览器业务 Skill 共用的运行时。业务 Skill 不引用你电脑上的仓库路径，而是通过本机 HTTP API 连接运行时，因此换一台电脑后仍有明确的安装和自检流程。

## 安装

### 1. 安装一次 Easy WebBridge

```bash
git clone https://github.com/xxjrq/easy-webbridge.git
cd easy-webbridge
npm install
node cli/easy-webbridge.mjs start
```

在已登录 Google Play Console 的 Chromium 浏览器中加载 Easy WebBridge 扩展。这个步骤只需为运行环境配置一次，后续其他 Easy WebBridge 业务 Skill 直接共用。

### 2. 安装 easyGooglePlay

跨 Agent 安装器：

```bash
npx skills add xxjrq/easy-google-play
```

通用手动安装位置：

```bash
git clone https://github.com/xxjrq/easy-google-play.git ~/.agents/skills/easy-google-play
```

仓库根目录的标准 [`SKILL.md`](SKILL.md) 是所有 Agent 的公共入口；[`agents/openai.yaml`](agents/openai.yaml) 只是 Codex 的可选展示信息，不参与核心运行。

## 运行自检

```bash
node scripts/easy-webbridge-client.mjs preflight
```

自检成功会列出在线浏览器的名称和 `browserId`；运行时、Token 或浏览器扩展未就绪时，会返回明确的下一步。

## 直接使用

```text
使用 easyGooglePlay，把 /项目绝对路径 的 Android App 上架到 Google Play。
复用已经登录的 Play Console 浏览器，完成 AAB 构建、商店资料、政策表单、Production Release 和发送审核，并告诉我最终状态。
```

也可以只做一个阶段：

```text
使用 easyGooglePlay 检查这个 Android 项目和 Play Console 当前版本，告诉我还缺哪些资料，先不要发送审核。
```

## 运行要求

- Node.js 20+
- 项目需要的 Android 构建工具
- Easy WebBridge 0.3.2+
- 一个已经登录 Google Play Console 的 Chromium 浏览器环境

## 开源协议

[MIT](LICENSE)
