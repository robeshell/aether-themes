# Aether 主题包验收测试提示词

这份提示词只给 Aether 主题包的维护者或贡献者使用，用来验证 npm 包、主题生成器和语义契约。

普通用户要创建自己的正式网站，请使用 [`STARTER_PROMPT.md`](./STARTER_PROMPT.md)。正式建站不会创建 `aether-ai-smoke-test`。

## 复制下面的提示词

```text
请你作为 Aether 主题包的验收助手，在当前 Aether 仓库中创建一个隔离的临时测试站点。

重要规则：

- 先执行 pwd 和 git status，确认当前目录是 Aether 主题仓库。
- 如果当前目录不是 Aether 仓库，请停止并告诉我，不要自行猜测路径。
- 不要修改、删除或覆盖仓库源码和已有未提交修改。
- 所有测试文件只能放在当前仓库的隔离子目录中。
- 不要访问或修改当前目录之外的文件。
- 不要提交 GitHub，不要发布 npm，也不要部署线上网站。
- 每一步先用一句简单中文说明要做什么，再执行命令。

一、创建隔离测试项目

请在当前目录创建：

./aether-ai-smoke-test

如果这个目录已经存在，不要删除它，改用：

./aether-ai-smoke-test-2

然后在该目录中创建：

./site

之后只在这个 site 目录中创建和修改测试网站。

二、安装并配置

在 ./site 中从零创建 Astro 网站：

- 使用 npm 安装 aether-themes
- 根据仓库中的 aether.config.example.mjs 创建配置
- 只启用 minimal 和 persona
- defaultTheme 设置为 minimal
- 使用 aether-themes 命令生成 src/styles/aether-themes.css
- 主题切换器读取 aether.config.mjs 中的 themes 数组
- 不要复制 W.Site 的代码或内容

三、创建测试页面

请创建首页、文章列表页、文章详情页、关于页和主题切换器，并用明确标注的示例内容测试：

- 普通长文
- 图片、视频、音频播放器
- 代码块和数学公式
- 图片影集
- 引用、列表和表格

没有真实媒体文件时，不要下载或使用有版权风险的素材。

四、验证

分别检查 minimal 和 persona：

- 主题切换和主题列表是否正常
- 富媒体排版是否正常
- 桌面端和 390px 手机端是否横向溢出
- 浏览器控制台是否有错误
- 减少动画设置是否生效
- npm run build 是否成功

构建成功后，在 ./site 执行 npm run dev -- --host 0.0.0.0，并报告本地访问地址。

最后报告创建的相对路径、aether-themes 版本、执行过的命令、验证结果和剩余问题。
```

## 通过标准

- 测试站点位于 `aether-ai-smoke-test/site` 或递增的隔离目录中
- Aether 仓库源码和原有修改没有变化
- npm 包可以安装，主题可以切换
- 富媒体内容可以显示
- 桌面端和手机端没有横向溢出
- `npm run build` 成功
