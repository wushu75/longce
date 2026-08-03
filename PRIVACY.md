# 隐私政策 · Privacy Policy

**龙侧 LongCe** — Every Chinese LLM, one sidebar.

最后更新 · Last updated: 2026-08-03

---

## 🇨🇳 中文版

### 一句话概括

龙侧不收集、不上传、不存储你的任何个人数据。它没有服务器。你的 API 密钥和对话记录**只保存在你自己设备的浏览器里**。

### 我们收集什么

**什么都不收集。** 龙侧没有后端服务器，也没有分析、埋点或遥测代码。我们（开发者）无法看到你的密钥、对话内容、浏览记录或任何使用数据。

### 数据存在哪里

- **API 密钥**：你在设置里填入的各厂商密钥，保存在浏览器本地的 `chrome.storage.local` 中，仅供本扩展在你的设备上使用。
- **对话历史**：每个「厂商 + 模型」的聊天记录同样存于 `chrome.storage.local`，只留在本机。
- **偏好设置**：语言、温度、路由规则、Lite 模式等配置，同样仅存于本地。

以上数据**不会离开你的设备**，也不会同步到任何服务器（包括我们的）。你可以随时在设置页的「数据」区域一键清除。

### 数据发往哪里

当你发送一条消息时，请求会**从你的浏览器直接发往你所选择的大模型厂商的官方 API**（例如 DeepSeek、通义千问、Kimi、智谱、零一、百川、MiniMax）。龙侧不作为中间人，请求不经过我们的任何服务器。

这些第三方厂商如何处理你发送的内容，受**它们各自的隐私政策**约束，与龙侧无关。请在使用前查阅你所选厂商的条款。你的 API 密钥仅用于向对应厂商进行身份认证，通过标准的 `Authorization` 请求头发送。

### 权限说明

龙侧只申请完成功能所必需的最小权限：

- `storage` — 在本地保存你的密钥、历史与设置。
- `sidePanel` — 提供浏览器侧边栏界面。
- `activeTab` + `scripting` — **仅当你主动点击「总结此页」等页面操作时**，读取当前标签页的可见文本，用于该次请求。不会在后台读取或持续监控网页。
- `contextMenus` — 提供右键菜单快捷操作。
- `host_permissions`（各厂商 API 域名）— 允许浏览器直接调用你所配置的大模型接口。

### 儿童隐私

龙侧不面向 13 岁以下儿童，也不会有意收集儿童的任何信息。

### 政策变更

若本政策有更新，我们会修改本文件顶部的「最后更新」日期，并在代码仓库中公开记录变更。

### 联系方式

有任何隐私相关问题，请在 GitHub 仓库提交 issue：
**https://github.com/wushu75/longce/issues**

---

## 🇬🇧 English

### In one sentence

LongCe does not collect, upload, or store any of your personal data. It has no server. Your API keys and conversations **stay in your own browser, on your own device**.

### What we collect

**Nothing.** LongCe has no backend server and contains no analytics, tracking, or telemetry. We (the developers) cannot see your keys, your conversations, your browsing, or any usage data.

### Where your data lives

- **API keys** — the provider keys you enter in Settings are saved in your browser's local `chrome.storage.local` and used only on your device by this extension.
- **Chat history** — conversations, kept per `provider + model`, are also stored in `chrome.storage.local` and never leave your machine.
- **Preferences** — language, temperature, routing rules, Lite mode, and similar settings are stored locally as well.

None of this data **leaves your device** or syncs to any server (including ours). You can wipe it all at any time from the **Data** section of the Settings page.

### Where your data is sent

When you send a message, the request goes **directly from your browser to the official API of the LLM provider you chose** (e.g. DeepSeek, Qwen, Kimi, GLM, Yi, Baichuan, MiniMax). LongCe is not a middleman — no request passes through any server of ours.

How those third-party providers handle the content you send is governed by **their own privacy policies**, not this one. Please review the terms of whichever provider you use. Your API key is used solely to authenticate to that provider, sent via the standard `Authorization` header.

### Permissions

LongCe requests only the minimum permissions its features need:

- `storage` — to save your keys, history, and settings locally.
- `sidePanel` — to provide the browser side-panel interface.
- `activeTab` + `scripting` — to read the current tab's visible text **only when you explicitly trigger a page action** (e.g. "Summarize this page"), for that single request. It does not read or monitor pages in the background.
- `contextMenus` — to offer right-click shortcuts.
- `host_permissions` (the provider API domains) — to let your browser call the LLM endpoints you've configured.

### Children's privacy

LongCe is not directed at children under 13 and does not knowingly collect any information from them.

### Changes to this policy

If this policy changes, we'll update the "Last updated" date at the top of this file and record the change publicly in the repository.

### Contact

For any privacy question, please open an issue on GitHub:
**https://github.com/wushu75/longce/issues**
