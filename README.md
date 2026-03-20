# 我的学术主页

基于 [Hugo](https://gohugo.io/) + [hugo-theme-reimu](https://github.com/D-Sketon/hugo-theme-reimu) 搭建的个人学术网站。

## 本地预览

```bash
hugo server -D
```

访问 http://localhost:1313

## 部署

推送到 `main` 分支后，GitHub Actions 自动构建并部署到 GitHub Pages。

## 配置说明

| 文件 | 说明 |
|------|------|
| `hugo.toml` | 站点基础配置（标题、baseURL 等） |
| `config/_default/params.yml` | 主题参数配置（作者、社交链接等） |
| `data/covers.yml` | 文章封面图列表 |
| `data/friends.yml` | 友链数据 |
| `content/about.md` | 关于页面 |
| `content/post/` | 博客文章目录 |

## 修改步骤

1. 将 `hugo.toml` 中 `YOUR_USERNAME` 替换为你的 GitHub 用户名
2. 将 `config/_default/params.yml` 中 `YOUR_NAME`、`YOUR_USERNAME` 替换为你的信息
3. 编辑 `content/about.md` 填写个人简介
4. 在 `content/post/` 下新建 `.md` 文件发布文章

## 发布新文章

```bash
hugo new post/my-article.md
```
