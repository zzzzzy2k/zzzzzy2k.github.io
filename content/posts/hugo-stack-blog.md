---
title: "用 Hugo + Stack 重构我的 GitHub Pages 博客"
date: 2026-05-03
draft: false
categories: [技术]
tags: [Hugo, GitHub Pages, Stack, 博客]
summary: "从零开始，用 Hugo 和 Stack 主题搭建了一个温暖文艺风格的个人博客。"
---

之前我的 GitHub Pages 只有一个默认的 Jekyll Architect 主题和一篇占位页面，基本等于白板。今天花了点时间，用 Hugo + Stack 主题把它重新搭了一遍。

## 为什么选 Hugo + Stack

选型的时候考虑了几个方案：

- **Jekyll**：GitHub Pages 原生支持，但中文主题选择少，Liquid 模板定制麻烦
- **Next.js / VitePress**：功能强大，但对纯博客来说有点重
- **Hugo + Stack**：构建速度快，Stack 主题在中文技术博客圈口碑很好，开箱即用的效果就很舒服

最终选了 Hugo + Stack，主要是因为 Stack 主题的设计语言本身就偏温暖文艺，和我想要的风格很契合，而且分类、标签、归档、搜索这些功能都是原生支持的，不用额外折腾。

## 搭建过程

整体流程其实不复杂：

1. **安装 Hugo Extended**：`winget install Hugo.Hugo.Extended`，一行搞定
2. **初始化站点**：`hugo new site .`，然后通过 git submodule 引入 Stack 主题
3. **配置**：按 Stack v4 starter 的格式拆分配置文件（`config.toml`、`params.toml`、`menu.toml`、`markup.toml` 等）
4. **写内容**：在 `content/posts/` 下写 Markdown
5. **部署**：GitHub Actions 自动构建，push 到 master 就上线

中间踩了几个坑：

- Hugo 的模板查找规则比我想象的复杂，搜索页面的 JSON 输出搞了好一会儿才调通
- Stack 主题的头像路径需要加 `/` 前缀才能正确引用静态文件
- `paginate` 在新版 Hugo 中已经弃用，要改成 `[pagination] pagerSize`

## 最终效果

现在博客具备了：

- 文章列表 + 分类/标签筛选
- 归档页面
- 搜索功能
- 关于我页面
- 项目作品集
- 暗色/亮色主题切换
- 侧栏小部件（搜索、分类、标签云、归档、目录）

整体风格是暖色调的，用了思源宋体做正文字体，阅读体验还不错。

## 后续计划

- 多写点内容，把博客真正用起来
- 加上评论系统（考虑 Giscus）
- 接入访问统计
- 持续调整样式细节

---

用 Hugo 写作的体验确实很好，纯 Markdown，`hugo server` 本地实时预览，`git push` 自动部署，整个流程非常干净。
