# 个人博客实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将 `zzzzzy2k.github.io` 从空白 Jekyll 页面改造为 Hugo + Stack 主题的个人博客

**Architecture:** Hugo Extended 静态站点 + Stack 主题（git submodule）+ GitHub Actions 自动部署

**Tech Stack:** Hugo Extended, Hugo Stack Theme, GitHub Actions, GitHub Pages

---

### Task 1: 安装 Hugo 并初始化站点

**Files:**
- Create: `config/_default/hugo.toml`
- Delete: `_config.yml`（Jekyll 配置）
- Delete: `index.md`（Jekyll 占位页）

- [ ] **Step 1: 安装 Hugo Extended**

在 Windows 上使用 winget 安装：

```bash
winget install Hugo.Hugo.Extended
```

安装完成后验证：

```bash
hugo version
```

预期输出应包含 `hugo v0.xxx` 且带 `+extended` 字样。

- [ ] **Step 2: 删除旧的 Jekyll 文件**

```bash
rm _config.yml index.md
```

- [ ] **Step 3: 初始化 Hugo 站点结构**

```bash
hugo new site . --force
```

这会生成 `hugo.toml`、`archetypes/`、`content/`、`layouts/`、`static/` 等目录。

- [ ] **Step 4: 创建 Hugo 多文件配置目录**

Stack 主题推荐使用 `config/_default/` 多文件配置。移动并拆分配置：

```bash
mkdir -p config/_default
mv hugo.toml config/_default/hugo.toml
```

编辑 `config/_default/hugo.toml`，内容如下：

```toml
baseURL = "https://zzzzzy2k.github.io/"
languageCode = "zh-cn"
defaultContentLanguage = "zh"
title = "zzzzzy2k 的博客"
theme = "hugo-theme-stack"
paginate = 5
enableRobotsTXT = true
buildDrafts = false
buildFuture = false
buildExpired = false

[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNos = false
    style = "monokai"
```

- [ ] **Step 5: 提交**

```bash
git add -A
git commit -m "chore: initialize Hugo site structure, remove Jekyll files"
```

---

### Task 2: 添加 Stack 主题

**Files:**
- Modify: `config/_default/hugo.toml`
- Create: `config/_default/params.toml`
- Create: `config/_default/menus.toml`
- Create: `config/_default/languages.toml`

- [ ] **Step 1: 添加 Stack 主题作为 git submodule**

```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack themes/stack
```

- [ ] **Step 2: 创建 params.toml（主题参数）**

创建 `config/_default/params.toml`：

```toml
mainSections = ["posts"]
defaultTheme = "auto"
robots = true

[sidebar]
  emoji = "📖"
  subtitle = "记录技术与生活"
  [sidebar.avatar]
    enabled = true
    local = true
    src = "images/avatar.png"

[article]
  toc = true
  readingTime = true
  license = { enabled = false }

[sidebar]
  [sidebar.posts]
    limit = 5

[widget]
  [widget.social]
    enabled = true

[footer]
  since = 2026

[comments]
  enabled = false

[readingTime]
  enabled = true

[seo]
  [seo.title]
    separator = " - "
```

- [ ] **Step 3: 创建 menus.toml（导航菜单）**

创建 `config/_default/menus.toml`：

```toml
[[main]]
  name = "首页"
  url = "/"
  weight = 1

[[main]]
  name = "归档"
  url = "/archives/"
  weight = 2

[[main]]
  name = "标签"
  url = "/tags/"
  weight = 3

[[main]]
  name = "关于"
  url = "/about/"
  weight = 4

[[main]]
  name = "项目"
  url = "/projects/"
  weight = 5

[[main]]
  identifier = "github"
  pre = "<svg>...</svg>"
  url = "https://github.com/zzzzzy2k"
  weight = 6
```

- [ ] **Step 4: 创建 languages.toml（语言配置）**

创建 `config/_default/languages.toml`：

```toml
[zh]
  languageName = "中文"
  weight = 1
  [zh.params]
    [zh.params.title]
      normal = "zzzzzy2k"
      subscript = "的博客"
```

- [ ] **Step 5: 提交**

```bash
git add -A
git commit -m "feat: add Stack theme with base configuration"
```

---

### Task 3: 创建内容目录结构和示例内容

**Files:**
- Create: `content/posts/_index.md`
- Create: `content/projects/_index.md`
- Create: `content/about.md`
- Create: `content/posts/hello-world.md`
- Create: `content/projects/my-first-project.md`

- [ ] **Step 1: 创建文章目录索引**

创建 `content/posts/_index.md`：

```yaml
---
title: "文章"
description: "我的博客文章"
---
```

- [ ] **Step 2: 创建项目目录索引**

创建 `content/projects/_index.md`：

```yaml
---
title: "项目"
description: "我的项目作品集"
---
```

- [ ] **Step 3: 创建关于我页面**

创建 `content/about.md`：

```yaml
---
title: "关于我"
description: "关于 zzzzzy2k"
layout: "about"
social:
  - icon: github
    url: "https://github.com/zzzzzy2k"
  - icon: email
    url: "mailto:your-email@example.com"
---

## 你好 👋

这里是 zzzzzy2k 的个人博客。

我是一名开发者，热爱技术与创造。这里记录我的学习笔记、项目经验和生活随想。

### 技能

- 编程语言：待补充
- 技术栈：待补充
- 兴趣：待补充
```

- [ ] **Step 4: 创建第一篇示例文章**

创建 `content/posts/hello-world.md`：

```yaml
---
title: "你好，世界"
date: 2026-05-03
draft: false
categories: [随笔]
tags: [博客, 开始]
summary: "我的第一篇博客文章"
---

欢迎来到我的博客！这是第一篇文章，用于测试博客的基本功能。

## 关于这个博客

这个博客使用 Hugo + Stack 主题搭建，托管在 GitHub Pages 上。

## 未来计划

- 分享技术学习笔记
- 记录项目开发经验
- 写一些生活随笔
```

- [ ] **Step 5: 创建第一个示例项目**

创建 `content/projects/my-first-project.md`：

```yaml
---
title: "个人博客"
date: 2026-05-03
draft: false
summary: "基于 Hugo + Stack 主题的个人博客"
tags: [Hugo, Web]
weight: 1
---

使用 Hugo 静态站点生成器和 Stack 主题搭建的个人博客，部署在 GitHub Pages 上。

## 技术栈

- Hugo Extended
- Stack Theme
- GitHub Actions
- GitHub Pages

## 链接

- [GitHub 仓库](https://github.com/zzzzzy2k/zzzzzy2k.github.io)
```

- [ ] **Step 6: 提交**

```bash
git add -A
git commit -m "feat: add content structure and sample content"
```

---

### Task 4: 视觉定制（配色与字体）

**Files:**
- Create: `assets/css/custom.css`
- Create: `static/images/avatar.png`

- [ ] **Step 1: 创建自定义样式文件**

创建 `assets/css/custom.css`：

```css
:root {
  --body-background: #faf8f5;
  --card-background: #ffffff;
  --text-primary: #2c2c2c;
  --text-secondary: #666666;
  --accent-color: #c0785c;
  --accent-color-light: #e8c4b0;
  --border-color: #e8e0d8;
  --shadow-color: rgba(0, 0, 0, 0.06);
  --font-body: "Noto Serif SC", "Source Han Serif SC", Georgia, serif;
  --font-heading: "Noto Sans SC", "Source Han Sans SC", sans-serif;
  --font-code: "JetBrains Mono", "Fira Code", monospace;
}

body {
  font-family: var(--font-body);
  background: var(--body-background);
  color: var(--text-primary);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-heading);
}

code, pre {
  font-family: var(--font-code);
}

a {
  color: var(--accent-color);
}

a:hover {
  color: var(--accent-color-light);
}

/* 侧栏样式 */
#sidebar {
  background: var(--card-background);
}

/* 文章卡片 */
.article-card {
  background: var(--card-background);
  border-radius: 12px;
  border: 1px solid var(--border-color);
  box-shadow: 0 2px 8px var(--shadow-color);
}

/* 暗色模式 */
[data-theme="dark"] {
  --body-background: #1a1a2e;
  --card-background: #22223b;
  --text-primary: #e0d8ce;
  --text-secondary: #a09888;
  --accent-color: #e8a87c;
  --accent-color-light: #f0c8a0;
  --border-color: #333355;
  --shadow-color: rgba(0, 0, 0, 0.2);
}
```

- [ ] **Step 2: 放置头像占位图**

将你的头像图片放到 `static/images/avatar.png`。如果没有现成的，先放一个占位图：

```bash
mkdir -p static/images
# 将你的头像文件复制到 static/images/avatar.png
# 或者先跳过此步，后续再添加
```

- [ ] **Step 3: 提交**

```bash
git add -A
git commit -m "feat: add custom warm-tone styling and fonts"
```

---

### Task 5: 配置 GitHub Actions 自动部署

**Files:**
- Create: `.github/workflows/hugo.yml`

- [ ] **Step 1: 创建 GitHub Actions 工作流**

```bash
mkdir -p .github/workflows
```

创建 `.github/workflows/hugo.yml`：

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - master

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.147.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb

      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5

      - name: Build with Hugo
        env:
          HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
          HUGO_ENVIRONMENT: production
          TZ: Asia/Shanghai
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

- [ ] **Step 2: 提交**

```bash
git add -A
git commit -m "ci: add GitHub Actions workflow for Hugo deployment"
```

---

### Task 6: 本地预览与验证

- [ ] **Step 1: 启动本地预览**

```bash
hugo server -D
```

访问 `http://localhost:1313`，检查以下内容：

- [ ] 首页能正常加载，显示文章卡片
- [ ] 点击文章能进入详情页
- [ ] 侧栏显示个人资料和分类
- [ ] 导航菜单（首页、归档、标签、关于、项目）可点击
- [ ] 关于页面正常显示
- [ ] 项目页面正常显示
- [ ] 暗色/亮色主题切换正常
- [ ] 中文显示正常，无乱码

- [ ] **Step 2: 构建验证**

```bash
hugo --minify
```

检查无报错，`public/` 目录生成了完整的静态文件。

- [ ] **Step 3: 推送到 GitHub**

```bash
git add -A
git commit -m "chore: final blog setup verification"
git push origin master
```

推送后到 GitHub 仓库 Settings → Pages，确认 Source 选择的是 "GitHub Actions"。

等待 Actions 完成，访问 `https://zzzzzy2k.github.io` 查看线上效果。

---

## 完成检查清单

- [ ] Hugo 本地预览正常
- [ ] 首页展示文章卡片
- [ ] 分类/标签/归档功能正常
- [ ] 关于我页面正常
- [ ] 项目作品集页面正常
- [ ] 社交链接图标显示
- [ ] 暗色/亮色切换正常
- [ ] 中文字体显示正确
- [ ] GitHub Actions 部署成功
- [ ] 线上站点可访问
