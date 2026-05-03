# zzzzzy2k.github.io

我的个人博客，使用 [Hugo](https://gohugo.io/) + [Stack 主题](https://github.com/CaiJimmy/hugo-theme-stack) 搭建，托管在 GitHub Pages。

## 本地开发

### 环境要求

- [Hugo Extended](https://gohugo.io/installation/) v0.157.0+

### 启动本地预览

```bash
hugo server
```

访问 http://localhost:1313 查看效果。

### 创建新文章

```bash
hugo new posts/my-new-post.md
```

### 构建

```bash
hugo --minify
```

## 部署

推送到 `master` 分支后，GitHub Actions 会自动构建并部署到 GitHub Pages。

## 目录结构

```
├── config/_default/     # Hugo 配置文件
├── content/
│   ├── posts/           # 博客文章
│   ├── projects/        # 项目作品集
│   ├── about.md         # 关于我
│   └── archives.md      # 归档页面
├── assets/css/          # 自定义样式
├── static/              # 静态资源
└── themes/stack/        # Stack 主题
```
