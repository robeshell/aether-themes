# Aether

[English](./README.md) · [简体中文](./README.zh-CN.md) · [日本語](./README.ja.md)

[![npm 版本](https://img.shields.io/npm/v/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![npm 下载量](https://img.shields.io/npm/dm/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![检查状态](https://github.com/robeshell/aether-themes/actions/workflows/check.yml/badge.svg)](https://github.com/robeshell/aether-themes/actions/workflows/check.yml)
[![许可证](https://img.shields.io/npm/l/aether-themes)](./LICENSE)

**面向内容型个人网站的小型、框架无关主题层。**

Aether 为博客、笔记、照片日记或音乐档案提供鲜明的视觉氛围，同时不绑定某个人的内容、路由或框架。它是从 [W.Site](https://robeshell.github.io/) 中提取出来的视觉层。

[浏览演示站](https://robeshell.github.io/) · [阅读 AI 正式建站提示词](./STARTER_PROMPT.md) · [查看 npm 包](https://www.npmjs.com/package/aether-themes)

## Aether 是什么，不是什么

Aether 是框架无关的 CSS 主题层，不是完整的博客主题、站点生成器或 CMS。它不提供路由、内容模型、后台，也不会为所有博客平台自动生成现成模板。

引导式建站流程默认使用 Astro，但包本身没有 Astro 运行时依赖。只要一个框架或静态站点生成器能够加载全局 CSS、输出 HTML，并添加 [`THEME_CONTRACT.md`](./THEME_CONTRACT.md) 中记录的语义化钩子，就可以接入 Aether。

| 环境 | 接入程度 |
| --- | --- |
| Astro | 内置正式建站流程 |
| Eleventy 或原生 HTML | 可直接引入 CSS |
| 其他能输出 HTML 的框架或静态站点生成器 | 将模板映射到契约后即可接入 |
| 现有 CMS 或博客标记 | 不是即插即用，需要模板适配器或本地覆盖样式 |

换句话说，Aether 具有可移植性，但不是对所有博客系统都零配置兼容。网站仍然负责自己的标记、内容、路由和交互。

## 为什么选择 Aether

- **七套可切换主题**，共用一份语义化标记契约。
- **按需加载**，网站只打包实际提供的主题。
- **框架无关**，可用于 Astro、Eleventy、原生 HTML 和其他静态站点工具。
- **适合 AI 协作**，提供可被仓库发现的 Skill 和复制即用的建站提示词。
- **无运行时依赖**，不内置任何影视游戏版权图片或抓取素材。

## 主题

| 主题 | 方向 |
| --- | --- |
| `minimal` | 安静留白与编辑秩序 |
| `magazine` | 纸张、栏目与印刷节奏 |
| `terminal` | 荧光绿、网格与命令行线索 |
| `cyber` | 警示黄、青色诊断线与硬朗面板 |
| `island` | 明亮岛屿生活与柔和圆角表面 |
| `wilds` | 大地色、遗迹与开阔空间 |
| `persona` | 红黑剪纸与预告信构图 |

所有主题都使用同一套语义化钩子。修改根元素属性即可切换视觉系统：

```html
<html data-theme="persona">
```

## 快速开始

在你的网站项目中安装：

```sh
npm install aether-themes
```

先引入基础样式，再引入需要的主题：

```css
@import 'aether-themes/foundation.css';
@import 'aether-themes/themes/minimal.css';
@import 'aether-themes/themes/persona.css';
```

如果网站提供所有内置主题，可以使用便捷入口：

```css
@import 'aether-themes/all.css';
```

Aether 只提供视觉层。HTML、内容、路由、主题选择器和交互逻辑由你的网站负责。

## 只加载需要的主题

将 [`aether.config.example.mjs`](./aether.config.example.mjs) 复制到网站中并命名为 `aether.config.mjs`，然后删除不需要的主题：

```js
export default {
  themes: ['minimal', 'persona'],
  defaultTheme: 'minimal',
};
```

根据配置生成主题导入文件：

```sh
npx aether-themes \
  --config aether.config.mjs \
  --output src/styles/aether-themes.css
```

生成器会校验主题名称、重复项和 `defaultTheme`。主题选择器也应读取同一个 `themes` 数组，这样未启用的主题不会出现在界面中。标签和描述由网站自行维护，让 Aether 保持内容无关。

## 使用 AI 创建网站

正式建站时，请先打开一个准备作为网站根目录的空目录，再把本仓库作为参考交给 AI。不要把 Aether 主题仓库本身当作网站工作目录：Aether 是依赖和视觉层，网站才拥有文件、内容、路由和配置。

如果你是第一次使用终端，请复制 [`STARTER_PROMPT.md`](./STARTER_PROMPT.md)。它会先询问站点名称、介绍、署名、栏目、语言和主题，等你确认方案后，直接在当前网站目录创建正式网站。如果发现当前目录是 Aether 主题仓库，它会停止，不会生成任何文件。

最短交接提示词：

```text
请阅读 https://github.com/robeshell/aether-themes/blob/main/STARTER_PROMPT.md，先向我提问建站需求，等我确认方案后，把当前工作目录作为正式网站根目录从零创建并启动网站。不要创建 aether-ai-smoke-test 或其他测试目录；如果当前目录是 aether-themes 仓库，请先停止并提示我换到网站目录。
```

如果你只是维护 Aether 包本身，请使用 [`SMOKE_TEST_PROMPT.md`](./SMOKE_TEST_PROMPT.md)。它会在仓库内创建隔离的 `aether-ai-smoke-test/site`，只用于验收 npm 包和主题生成器，不用于创建用户网站。

已经有 Aether 网站时，请使用 [`UPDATE_PROMPT.md`](./UPDATE_PROMPT.md)。它会保留内容、配置、本地快照和未提交修改，然后更新主题、重新生成 CSS 并检查网站。

## 标记契约

Aether 为语义化钩子提供样式，而不是生成固定路由的页面。必需钩子和富媒体钩子（图片、视频、音频、代码、公式、影集）见 [`THEME_CONTRACT.md`](./THEME_CONTRACT.md)。

网站负责维护：

- 内容集合和 frontmatter；
- 路由和页面结构；
- 主题选择器状态和持久化；
- 网站文案和标签；
- 素材授权及网站专属覆盖样式。

## 可选图片

Aether 不内置抓取或版权相关图片。`cyber`、`terminal` 和 `wilds` 主题提供可选的图片变量：

```css
:root[data-theme="cyber"] {
  --aether-cyber-dots-image: url('/assets/cyber/dots-yellow.png');
}

:root[data-theme="terminal"] {
  --aether-terminal-rain-image: url('/assets/terminal/matrix-rain.svg');
}

:root[data-theme="wilds"] {
  --aether-wilds-header-image: url('/images/wilds-header.png');
}
```

这些变量默认不加载图片，因此主题无需额外素材也能工作。只添加你拥有或获准再分发的素材。

## 开发

这个包没有运行时依赖。可以在本地检查发布内容：

```sh
npm pack --dry-run
```

每次 push 和 pull request 也会在 [GitHub Actions](https://github.com/robeshell/aether-themes/actions/workflows/check.yml) 中执行同样的检查。

## 参与贡献

修改应面向 [`THEME_CONTRACT.md`](./THEME_CONTRACT.md) 中的语义化钩子，保持基础层与内容无关，并保留网站按需加载主题的能力。提交 pull request 前，请运行 `npm pack --dry-run` 并检查包内容。

发布步骤见 [`PUBLISHING.md`](./PUBLISHING.md)。每次发布都需要升级版本号。

## 许可证

MIT，详见 [`LICENSE`](./LICENSE)。
