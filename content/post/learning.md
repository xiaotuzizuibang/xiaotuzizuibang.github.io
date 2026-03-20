---
title: " 小bug教你 Hugo建个人网站"
date: 2026-03-20T23:11:08+08:00
lastmod: 2026-03-20T23:11:08+08:00
categories:
  - 教程
tags:
  - Hugo
  - 建站
  - GitHub Pages
description: "从零开始，用 Hugo 搭建并部署个人学术网站的完整教程。"
cover: /images/learning.jpg
draft: true
---

小bug老师开课了，借助 [Hugo](https://gohugo.io/) 静态站点生成器搭建学术网页，整个流程其实非常简洁。本文记录了完整的搭建过程。

<!--more-->

## 1. 准备工作

### 安装 Hugo Extended

**Windows：**

```powershell
winget install Hugo.Hugo.Extended
```

验证安装：

```bash
hugo version
# 输出应包含 "+extended"
# hugo v0.144.2+extended ...
```

### 安装 Git

```bash
git --version  # 验证是否已安装
```

---

## 2. 创建新站点

```bash
hugo new site mysite
cd mysite
git init
```

---

## 3. 安装主题

这里使用 [hugo-theme-reimu](https://github.com/D-Sketon/hugo-theme-reimu)，以 Git Submodule 方式安装：

```bash
git submodule add https://github.com/D-Sketon/hugo-theme-reimu.git themes/reimu
```

然后在 `hugo.toml` 中启用主题：

```toml
baseURL = 'https://你的用户名.github.io/'
languageCode = 'zh-CN'
defaultContentLanguage = 'zh-CN'
title = '我的学术主页'
theme = 'reimu'

[markup.highlight]
  guessSyntax = true
  noClasses = false
```

---

## 4. 必要的内容目录结构

```bash
# 创建归档页（必须）
mkdir -p content/archives
# 创建 archives/_index.md（主题归档页需要）

# 新建一篇文章
hugo new post/hello-world.md
```

`content/post/_index.md` 必须存在且设为草稿（主题要求）：

```yaml
---
date: 2026-01-01T00:00:00+08:00
draft: true
---
```

---

## 5. 本地预览

```bash
hugo server -D
```

打开浏览器访问 `http://localhost:1313`，实时预览效果，修改文件后页面自动刷新。

> `-D` 参数让草稿文章也显示出来，方便写作时预览。

---

## 6. 写文章

在 `content/post/` 下新建 Markdown 文件，Front Matter 示例：

```yaml
---
title: "文章标题"
date: 2026-03-20T10:00:00+08:00
categories:
  - 研究
tags:
  - 机器学习
description: "文章摘要，显示在首页卡片上。"
cover: https://example.com/image.jpg  # 封面图 URL
draft: false  # false = 正式发布，true = 草稿
---
```

---

## 7. 封面图放在哪里？

有两种方式：

### 方式一：使用网络图片 URL

直接在 Front Matter 中填写图片链接：

```yaml
cover: https://images.unsplash.com/photo-xxx?w=800
```

### 方式二：放到本地 static 目录

将图片放到 `static/images/covers/` 下：

```
mysite/
└── static/
    └── images/
        └── covers/
            └── my-cover.jpg
```

然后在 Front Matter 引用（路径从 `/` 开始）：

```yaml
cover: /images/covers/my-cover.jpg
```

### 全局随机封面

编辑 `data/covers.yml`，添加多张图片 URL，文章未指定封面时自动随机选取：

```yaml
- https://images.unsplash.com/photo-xxx?w=800
- https://images.unsplash.com/photo-yyy?w=800
```

---

## 8. 部署到 GitHub Pages

### 第一次推送

```bash
# 提交所有文件
git add -A
git commit -m "feat: initial site"

# 关联 GitHub 仓库（仓库名必须是 用户名.github.io）
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
git branch -M main
git push -u origin main
```

### 开启 GitHub Pages

前往仓库 → **Settings → Pages → Source** → 选择 **GitHub Actions**。

之后每次推送代码，GitHub Actions 自动构建并发布，约 1-2 分钟生效。

### 日常发布文章

```bash
git add -A
git commit -m "post: 新文章标题"
git push
```

推送后等待约 1 分钟，网站自动更新 ✅

---

## 9. 常用命令速查

| 命令 | 作用 |
|------|------|
| `hugo new post/文章名.md` | 新建文章 |
| `hugo server -D` | 启动本地预览（含草稿） |
| `hugo` | 生成静态文件到 `public/` |
| `git push` | 推送并触发自动部署 |
