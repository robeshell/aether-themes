# Aether 更新提示词

这份提示词用于已经在使用 Aether 的个人网站。用户不需要理解 npm、主题快照或生成器，只要把下面的一句话发给 AI，并把 Aether 仓库链接一起提供即可。

## 一句话版本

```text
请阅读 https://github.com/robeshell/aether-themes 中的 UPDATE_PROMPT.md，并严格按其中说明检查和更新当前网站的 Aether 主题；保留我的文章、路由、配置和未提交修改，更新后重新生成主题 CSS、运行构建并报告结果，在我确认前不要提交、推送或发布。
```

## 完整操作提示词

```text
请作为一个谨慎的新手友好型网站维护助手，帮我把当前个人网站的 Aether 主题更新到最新稳定版本。

参考仓库：
https://github.com/robeshell/aether-themes

开始前请阅读：

- 当前网站仓库的 AGENTS.md（如果存在）
- 当前网站的 README.md（如果存在）
- https://github.com/robeshell/aether-themes/blob/main/skills/aether-blog/SKILL.md
- https://github.com/robeshell/aether-themes/blob/main/UPDATE_PROMPT.md
- https://github.com/robeshell/aether-themes/blob/main/CHANGELOG.md

安全规则：

- 先执行 git status，保留所有未提交的修改，不要覆盖或清理它们。
- 只修改当前网站和它自己的依赖文件，不要修改 Aether 主题仓库源码。
- 不要删除文章、图片、视频、音频、配置或路由。
- 不要更换框架，不要重写页面，不要顺手升级无关依赖。
- 保留当前 aether.config.mjs 中的 themes 和 defaultTheme，除非我明确要求改变。
- 不要下载或加入有版权风险的主题图片、字体或品牌素材。
- 不要提交 GitHub、发布 npm 或部署网站，除非我在最后明确确认。
- 每一步先用简单中文说明目的，再执行命令。
- 如果发现风险、登录要求、冲突或无法确定的文件，先暂停并询问我。

一、检查当前接入方式

请确认当前网站使用的是哪一种方式：

1. 直接依赖 npm 包 `aether-themes`
2. 从 Aether 仓库生成本地 CSS 快照
3. 其他接入方式

先报告：

- 当前 aether-themes 版本（如果有）
- 使用的包管理器
- aether.config.mjs 的 themes 和 defaultTheme
- 生成 CSS 文件的位置
- 是否存在未提交修改

如果当前网站使用本地快照，不要擅自改成 npm 依赖；先说明切换会带来的影响。

二、更新主题

如果当前网站直接依赖 npm 包：

- 使用当前项目已有的包管理器更新 `aether-themes` 到最新稳定版。
- 保留 lockfile，不要删除 node_modules 或整个依赖目录。

如果当前网站使用本地快照：

- 先读取 Aether 仓库的 CHANGELOG.md，说明有哪些主题变化。
- 按当前项目原来的方式重新生成 CSS。
- 不要修改 themes 列表，不要改变默认主题。

三、重新生成和检查

如果项目使用 aether.config.mjs，请使用它重新生成主题 CSS。生成时保持当前输出路径和 source 方式不变。

然后检查：

- 所有启用的主题都能激活
- 主题切换器只显示启用的主题
- 文章、笔记、游记、照片和音乐页面没有内容丢失
- 图片、视频、音频播放器、代码、公式和影集仍然正常
- 桌面端没有横向溢出
- 390px 宽度手机端没有横向溢出
- 浏览器控制台没有新增错误
- 减少动画设置仍然有效

四、构建验证

使用当前网站已有的检查和构建命令。至少运行：

npm run build

如果项目没有 build 脚本，请先告诉我，不要自行更换构建工具。

五、输出报告

请用简单中文报告：

- 更新前后的 Aether 版本
- 使用的更新命令
- 修改了哪些文件
- 是否重新生成了 CSS
- 启用了哪些主题
- 构建是否成功
- 桌面端和手机端检查结果
- 是否有需要我人工确认的视觉变化
- 是否还有未提交修改

在我确认前不要 commit、push、publish 或 deploy。
```

## 更新原则

- 先读变更记录，再决定是否更新。
- 主题配置是消费站点的所有权，不要被包更新覆盖。
- 文章和媒体内容与主题包分离，更新主题不应改动内容。
- 生成文件必须由配置重新生成，不要手动复制一套新 CSS。
- 每次发布版本都应保留可回滚的 lockfile 和 Git 提交。
