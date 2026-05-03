# 个人博客设计方案

## 概述

将 `zzzzzy2k.github.io` 从默认的 Jekyll Architect 主题改造为基于 Hugo + Stack 主题的个人综合博客，定位为温暖文艺风格，中文为主，涵盖文章、项目展示、个人介绍和社交联系。

## 技术选型

- **静态站点生成器**：Hugo Extended（支持 SCSS）
- **主题**：[hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack)
- **部署**：GitHub Actions → GitHub Pages
- **主题管理**：git submodule

## 目录结构

```
zzzzzy2k.github.io/
├── .github/workflows/hugo.yml   # GitHub Actions 自动部署
├── config/                       # Hugo 多文件配置
│   └── _default/
│       ├── hugo.toml             # 主配置（站点标题、URL、主题等）
│       ├── params.toml           # 主题参数（布局、颜色、社交链接等）
│       ├── menus.toml            # 导航菜单
│       └── languages.toml        # 语言设置（中文）
├── content/
│   ├── posts/                    # 博客文章
│   ├── projects/                 # 项目作品集
│   └── about.md                  # 关于我页面
├── assets/css/custom.css         # 自定义样式覆盖
├── static/                       # 静态资源（头像、封面图等）
└── themes/stack/                 # Stack 主题（git submodule）
```

## 功能模块

### 1. 文章列表 + 分类/标签

- Stack 主题原生支持，无需额外开发
- 文章使用 Hugo 前置元数据：
  ```yaml
  ---
  title: "文章标题"
  date: 2026-05-03
  categories: [技术]
  tags: [Python, Web]
  summary: "文章摘要"
  ---
  ```
- 首页展示文章卡片列表，侧栏展示分类树、标签云、归档时间线

### 2. 关于我页面

- `content/about.md`，使用 Stack 的 profile 布局
- 展示头像、个人简介、技能/经历
- Profile sidebar 组件展示社交链接

### 3. 项目作品集

- `content/projects/` 目录下每篇文章即一个项目
- 使用文章卡片布局，带封面图展示
- 可通过 `weight` 字段置顶重点项目

### 4. 联系/社交

- 在 `params.toml` 中配置社交图标链接
- 支持 GitHub、邮箱、微信等 20+ 种图标
- 配置即生效，无需写代码

## 视觉设计

### 配色

- 亮色模式：暖白背景 `#faf8f5`，深棕文字 `#2c2c2c`，橙棕 accent 色
- 暗色模式：深灰背景，保留温暖感，不使用纯黑
- 通过自定义 CSS 变量覆盖主题默认配色

### 字体

- 正文：思源宋体（Noto Serif SC）或霞鹜文楷，适合中文长文阅读
- 标题：思源黑体（Noto Sans SC）
- 代码：JetBrains Mono
- 通过 Google Fonts 或 CDN 加载

### 排版

- 两栏布局：左侧个人资料侧栏 + 右侧主内容区
- 文章卡片带封面图，杂志排版感
- 充足留白，优化中文阅读体验

## 部署方案

### GitHub Actions 工作流

```yaml
name: Deploy Hugo site to GitHub Pages
on:
  push:
    branches: [master]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: true
          fetch-depth: 0
      - uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
          extended: true
      - run: hugo --minify
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

### 本地开发工作流

1. `hugo server` 启动本地预览（热重载）
2. `hugo new posts/my-post.md` 创建新文章
3. 编写 Markdown 内容
4. `git push` → GitHub Actions 自动构建部署

## 后续可扩展

- **评论系统**：Giscus（基于 GitHub Discussions，中文友好）
- **访问统计**：Umami（自托管）或 Google Analytics
- **搜索**：Stack 主题自带搜索功能，无需额外配置
- **RSS**：Hugo 自动生成 RSS feed
- **SEO**：Hugo 内置 sitemap、Open Graph、Twitter Cards 支持
