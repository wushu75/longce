<div align="center">

# 龙侧 LongCe

**每一个中文大模型，尽在侧边栏。**
**Every Chinese LLM, one sidebar.**

Manifest V3 · Side Panel · BYOK · Privacy-first · MIT · 免费开源

<p>
  <a href="https://github.com/wushu75/longce/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/wushu75/longce?style=for-the-badge&logo=github&color=d7263d&labelColor=17130f"></a>
  <a href="https://github.com/wushu75/longce/blob/main/LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-1f7a5c?style=for-the-badge&labelColor=17130f"></a>
  <img alt="Manifest V3" src="https://img.shields.io/badge/Manifest-V3-b8903f?style=for-the-badge&labelColor=17130f">
  <img alt="Chrome 116+" src="https://img.shields.io/badge/Chrome-116%2B-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white&labelColor=17130f">
</p>

### ⭐ 喜欢就点个 Star！ · If it's useful, give it a star!

觉得龙侧有用？点右上角的 **⭐ Star** 支持一下 —— 这是对开源最好的鼓励，也能帮更多中文用户发现它。
Enjoying LongCe? A **⭐ Star** is the best encouragement for open source and helps more people find it.

**👉🏿 [github.com/wushu75/longce](https://github.com/wushu75/longce)**

</div>

---

> 🇨🇳 中文在前，English below. Scroll down for the English version.

## 品牌故事 · 龙侧 LongCe

**龙侧（LongCe）** 取意“龙之侧” —— 中文大模型如龙腾起，而你需要的，是一个随时伴其左右、触手可及的**侧边栏**。

浏览器右侧一拉开，DeepSeek、通义千问、Kimi、GLM、Yi、百川、MiniMax 尽在其中：一处输入，随意切换，甚至并排对比。密钥是你自己的（BYOK），数据只留在本机，没有服务器、没有中间商、没有埋点。

龙侧只做一件事：**让中文用户用最顺手的方式，调用最合适的中文大模型。**

## ✨ 功能

- **中文大模型枢纽**：在一个统一的侧边栏里对话，内置 7 家中文 LLM
  - DeepSeek 深度求索 · 通义千问 Qwen（阿里）· 月之暗面 Kimi · 智谱 GLM · 零一万物 Yi · 百川 Baichuan · MiniMax
- **模型切换 & 独立历史**：每个「厂商 + 模型」拥有独立对话记录，存于 `chrome.storage.local`
- **对比模式**：勾选 2–3 个模型，同一问题并排作答
- **中文优先 UI**：默认简体中文，一键切换 English（结构上便于扩展繁体）
- **页面助手**（读取当前网页）：
  - 用中文总结此页 · 提取要点 · 生成邮件回复 · 写小红书文案
- **提示词模板**：润色中文 / 写 PRD / 小红书文案 / 中英互译 / 微博文案，一键填入
- **模型路由**：按任务类型（总结 / 写作 / 代码 / 翻译 / 润色）自动选用你指定的厂商
- **Lite 省钱模式**：长文本先用小模型压缩，再交给主模型，节省 Token
- **隐私优先**：BYOK，无服务器、无埋点，一切留在本机

## 🚀 本地安装（加载已解压的扩展）

1. 克隆或下载本仓库。
2. 打开 Chrome，访问 `chrome://extensions`。
3. 打开右上角 **开发者模式**。
4. 点击 **加载已解压的扩展程序**，选择本项目根目录（含 `manifest.json` 的那一层）。
5. 点击工具栏中的 **龙** 图标即可打开侧边栏。首次使用请先到 **设置** 填入至少一个厂商的 API Key。

> 需要 Chrome 116+（side panel API）。

## 🎨 生成图标

仓库已内置生成好的 `icons/icon16/48/128.png`，通常无需重新生成。若要自定义：

```bash
cd icons
npm i canvas        # node-canvas，用于绘制 龙 字
node generate-icons.js
```

脚本会在 `icons/` 下重新生成三个尺寸的 PNG。

## 🔑 配置 API 密钥

1. 打开侧边栏，点击右上角 **⚙ 设置**（或在 `chrome://extensions` 中点“扩展选项”）。
2. 在 **API 密钥** 区，为你要用的厂商粘贴 Key（点右侧“获取密钥”前往对应控制台）。
3. 点击底部 **保存**。

密钥只保存在本机 `chrome.storage.local`，**绝不上传**。

## 🧩 如何新增一个模型厂商

绝大多数中文大模型都提供 **OpenAI 兼容** 的 `/chat/completions` 接口，因此新增厂商通常只需在 `src/core/providers.js` 的 `PROVIDERS` 里加一个对象，并把它加入 `PROVIDER_ORDER`：

```js
// src/core/providers.js
myprovider: {
  id: 'myprovider',
  name: { zh: '我的厂商', en: 'My Provider' },
  site: 'https://console.example.com',
  endpoint: 'https://api.example.com/v1/chat/completions',
  models: [
    { id: 'my-fast', label: 'My-Fast（快·省）', small: true },
    { id: 'my-pro', label: 'My-Pro' },
  ],
  defaultModel: 'my-fast',
  adapter: 'openai',                 // 复用通用适配器
  tags: ['write', 'summarize'],
  keyHint: { zh: '在控制台创建 API Key', en: 'Create an API key in the console' },
},
```

别忘了把域名加进 `manifest.json` 的 `host_permissions`，例如 `https://api.example.com/*`。

**非 OpenAI 兼容的厂商**：在 `providers.js` 底部的 `ADAPTERS` 里注册一个同签名的适配器函数，并把 provider 的 `adapter` 指向它。适配器签名：

```js
async function myAdapter({ provider, apiKey, model, messages, temperature, onToken, signal }) { /* ... */ }
```

## 🔒 隐私与安全

- **BYOK（自带密钥）**：你使用自己的 API Key，直接从浏览器请求各厂商官方接口。
- **无服务器**：龙侧没有后端，不经过任何第三方中转。
- **全部本地**：密钥、设置、对话历史都存在 `chrome.storage.local`。
- **无埋点**：默认不收集任何数据；如未来加入统计，将**默认关闭、需你手动开启**，并在此说明。
- **最小权限**：`storage`、`sidePanel`、`activeTab`、`scripting`、`contextMenus`；`host_permissions` 仅限各厂商 API 域名。
- **无远程代码**：无 inline 脚本、无 `eval`、无远程加载，符合 MV3 CSP。

## 🗺️ 路线图 Roadmap

- [ ] 繁体中文 / 更多界面语言
- [ ] 更多厂商（讯飞星火、腾讯混元、字节豆包、商汤等）
- [ ] 提示词模板市场（导入 / 分享）
- [ ] 流式对比模式的差异高亮
- [ ] 会话导出（Markdown / JSON）
- [ ] 快捷键与更多右键菜单动作
- [ ] 可选的本地向量检索 / 网页问答

## 🏗️ 项目结构

```
longce/
├── manifest.json                 # MV3 清单
├── LICENSE                       # MIT
├── README.md
├── _locales/                     # 商店元数据本地化（zh_CN / en）
│   ├── zh_CN/messages.json
│   └── en/messages.json
├── icons/
│   ├── generate-icons.js         # 用 canvas 生成 龙 字图标
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
└── src/
    ├── background/
    │   └── service-worker.js      # 侧边栏行为、右键菜单、页面上下文桥接
    ├── sidepanel/
    │   ├── index.html
    │   ├── sidepanel.css
    │   └── sidepanel.js           # 聊天 / 流式 / 页面助手 / 对比 / 路由
    ├── options/
    │   ├── index.html
    │   ├── options.css
    │   └── options.js             # BYOK 密钥、通用设置、路由、Lite 模式
    ├── content/
    │   └── content.js             # 提取页面标题 / URL / 选区 / 正文
    └── core/
        ├── providers.js           # 厂商配置 + OpenAI 兼容适配器
        ├── router.js              # 任务路由 + Lite 压缩 + ask() 编排
        ├── storage.js             # chrome.storage.local 封装
        └── i18n.js                # 中英文案 + DOM 翻译
```

---

# LongCe 龙侧 (English)

**Every Chinese LLM, one sidebar.**

**LongCe (龙侧, “the dragon’s side”)** puts China’s major LLMs into one Chrome **side panel**. Open it and DeepSeek, Qwen, Kimi, GLM, Yi, Baichuan and MiniMax are all one click away — switch between them, or ask two or three the same question side by side. You bring your own API keys (**BYOK**); nothing leaves your machine. No server, no middleman, no telemetry.

## Features

- **Chinese-LLM hub** — unified side-panel chat across 7 providers (DeepSeek, Qwen, Kimi/Moonshot, GLM/Zhipu, Yi/01.AI, Baichuan, MiniMax).
- **Model switcher + per-model history** in `chrome.storage.local`.
- **Compare mode** — send one prompt to 2–3 models, responses side by side.
- **Chinese-first UI** with a one-tap English toggle (structured for Traditional Chinese later).
- **Page-aware actions** — summarize this page, extract key points, draft an email reply, write social copy — powered by a content script that reads the current page.
- **Prompt templates** for common Chinese workflows.
- **Model router** — auto-pick a provider per task type (summarize / write / code / translate / polish).
- **Lite mode** — condense long text with a small model first to save tokens.
- **Privacy-first** — BYOK, no server, no analytics, all local.

## Install locally (load unpacked)

1. Clone or download this repo.
2. Go to `chrome://extensions`, enable **Developer mode**.
3. Click **Load unpacked** and select the project root (the folder with `manifest.json`).
4. Click the **龙** toolbar icon to open the side panel, then open **Settings** and add at least one provider API key. Requires Chrome 116+.

## Generate icons

Pre-built PNGs are committed. To customize:

```bash
cd icons && npm i canvas && node generate-icons.js
```

## Configure API keys

Open the side panel → **⚙ Settings** → paste a key for each provider you want (the “Get a key” link opens each console) → **Save**. Keys live only in local storage and are never uploaded.

## Add a new provider

Most Chinese LLMs are OpenAI-compatible, so adding one is a single object in `src/core/providers.js` (`PROVIDERS` + `PROVIDER_ORDER`) plus its API domain in `manifest.json` → `host_permissions`. For a non-compatible API, register a same-signature function in the `ADAPTERS` map and point the provider’s `adapter` at it. See the Chinese section above for a full snippet.

## Privacy & security

BYOK, no backend, everything in `chrome.storage.local`, no analytics by default (any future analytics will be opt-in and documented here), minimal permissions, and no remote code (MV3 CSP compliant).

## Roadmap

Traditional Chinese & more locales · more providers · a prompt-template marketplace · diff highlighting in compare mode · conversation export · keyboard shortcuts · optional local retrieval / page Q&A.

## License

[MIT](./LICENSE) — free and open source. Contributions welcome.
