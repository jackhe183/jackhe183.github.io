# Jack He / Lemon

个人网站。Astro 静态构建，Markdown 管理文章，GitHub Actions 自动部署至 GitHub Pages。无数据库或付费服务。

## 本地开发

需要 Node >=22.12.0，推荐 Node 24。

```sh
nvm use
npm ci
npm run dev
```

打开终端输出的本地地址（默认 http://localhost:4321）。

```sh
npm run build
npm run preview
```

## 修改内容

- 头像、定位、首页文案、背景和邮箱：`src/data/profile.json`。头像原图：`public/avatar.jpg`。
- 页面内容职责和逐项操作方法见 [内容维护指南](CONTENT_GUIDE.md)。未填写的可选内容自动隐藏。
- 项目：`src/data/projects.json`。`teaser` 用于首页简短列表，`purpose` 与 `capabilities` 用于 Projects 的用途和功能说明。首页链接到 Projects 中对应项目的锚点。LLMprobe-engine 是 fork，必须保留上游标注。
- 文章：在 `src/content/writing/` 新建 `.md` 文件，使用以下 frontmatter。文件名生成文章 URL。

```yaml
---
title: "文章标题"
description: "一句话摘要"
date: 2026-10-09
draft: false
---
```

正文支持 Markdown。`draft: true` 不生成文章页面，也不显示在列表中。`first-note.md` 是未发布模板。首版不含虚构的已发布文章。当前未安装 MDX 集成，后续有交互内容需求时可添加官方 `@astrojs/mdx`。

- 样式：`src/styles/global.css`。主题默认跟随系统，手动选择保存在浏览器本地。

## 部署

仓库 Settings → Pages → Source 选择 GitHub Actions。合并到 `main` 或手动触发 Deploy to GitHub Pages 后，会自动构建并部署。PR 会进行构建检查。

正式地址：https://jackhe.top/

GitHub Pages 原始地址：https://jackhe183.github.io/（绑定自定义域名后会跳转）。

维护流程：创建内容分支 → 修改 → 本地 build → 提交 PR → 检查通过 → 合并。

已获授权将自定义域名绑定为 `jackhe.top`，`astro.config.mjs` 的 `site` 已设为 `https://jackhe.top`。DNS 迁移与 HTTPS 签发需单独验证。Actions 部署的域名由仓库 Pages 设置管理，无需依赖 CNAME 文件。保留 DNS 完整备份，按确认的清单操作。

参考：[Astro 官方部署指南](https://docs.astro.build/en/guides/deploy/github/)。
