# asblog

基于 [Astro](https://astro.build) + [Fuwari](https://github.com/saicaca/fuwari) 主题搭建的个人博客，通过 GitHub Actions 自动部署到 GitHub Pages。

- 在线地址：https://ashizcq.github.io/asblog/
- 主题：Fuwari
- 包管理器：pnpm 9（通过 corepack 管理）

## 本地开发

```bash
# 启用 pnpm（Node 18+ 自带 corepack）
corepack enable pnpm

# 安装依赖
pnpm install

# 启动开发服务器（http://localhost:4321/asblog/）
pnpm dev

# 生产构建（astro build + pagefind 搜索索引）
pnpm build

# 预览构建产物
pnpm preview
```

## 新建文章

```bash
pnpm new-post <filename>
```

文章生成在 `src/content/posts/` 目录下，frontmatter 字段示例：

```markdown
---
title: 文章标题
published: 2026-07-21
description: 文章描述
tags: [标签1, 标签2]
category: 分类
draft: false
---
```

## 站点配置

- `src/config.ts`：站点标题、副标题、语言、作者资料、导航栏、社交链接等。
- `astro.config.mjs`：`site` 与 `base` 已针对 GitHub Pages 项目站点配置：
  - `site: "https://ashizcq.github.io"`
  - `base: "/asblog"`

> 如果将仓库改名为 `<用户名>.github.io`（用户主站点），需把 `base` 改回 `"/"`。

## 部署（GitHub Pages）

部署由 `.github/workflows/deploy.yml` 自动完成，遵循 [Astro 官方 GitHub Pages 指南](https://docs.astro.build/zh-cn/guides/deploy/github/)：

1. 在 GitHub 仓库 **Settings → Pages → Build and deployment** 中，将 **Source** 设置为 **GitHub Actions**。
2. 向 `main` 分支推送代码后，工作流会自动执行 `pnpm install`、`pnpm build` 并发布 `dist/` 到 GitHub Pages。
3. 构建完成后访问 https://ashizcq.github.io/asblog/ 查看博客。
