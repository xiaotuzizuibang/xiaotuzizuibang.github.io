---
title: "布宝宝教你在 Windsurf 中配置 LaTeX"
date: 2026-03-21T23:30:34+08:00
lastmod: 2026-03-21T23:30:34+08:00
categories:
  - 教程
tags:
  - LaTeX
  - Windsurf
  - 配置
description: "在 Windsurf 中配置 LaTeX Workshop + MiKTeX + Perl 实现实时预览的完整教程。"
cover: /images/learning_latex.jpg

---
# 在 Windsurf 中配置 LaTeX 实时预览（LaTeX Workshop + MiKTeX + Perl）

<!--more-->

## 背景

为了在 Windsurf（类似 VSCode 的开发环境）中高效编写 LaTeX，并实现**实时预览 PDF**，我完成了一套基础环境配置，包括：

* 编辑器插件：LaTeX Workshop
* TeX 发行版：MiKTeX
* 依赖工具：Perl（用于 latexmk）

本文记录完整流程，方便后续复现或迁移环境。

---
## 使用
### 每次修改完
打开 paper.tex，按 `Ctrl+Shift+P` 打开命令面板，输入：

```
LaTeX Workshop: Build LaTeX project
```

先触发一次编译
### 编译成功后
在命令面板搜索：

```
LaTeX Workshop: View LaTeX PDF
```



## 1. 安装 LaTeX Workshop 插件

在 Windsurf 扩展市场中搜索：

```
LaTeX Workshop
```

安装后，它会提供：

* 一键编译 LaTeX
* 自动构建（on save）
* PDF 预览
* 日志与错误提示

---

## 2. 安装 MiKTeX（LaTeX 编译环境）

### 下载

前往官网下载安装：

```
https://miktex.org/download
```

### 安装建议配置

安装时注意：

* ✔ 勾选 **Install missing packages on-the-fly（自动安装缺失包）**
* ✔ 建议使用用户级安装（User install）

### 验证安装

打开终端，运行：

```bash
latex --version
```

如果有输出，说明安装成功。

---

## 3. 安装 Perl（用于 latexmk）

### 为什么需要 Perl？

LaTeX Workshop 默认使用：

```
latexmk
```

而 `latexmk` 是一个 Perl 脚本，因此必须安装 Perl。

### 下载

推荐使用 Strawberry Perl：

```
https://strawberryperl.com/
```

### 验证安装

```bash
perl -v
```

---

## 4. 验证 latexmk 是否可用

```bash
latexmk -v
```

如果失败，通常是：

* Perl 未安装
* 或 PATH 未配置

---

## 5. Windsurf 中配置 LaTeX Workshop

一般情况下**无需额外配置**，但推荐加一个 settings.json：

```json
{
  "latex-workshop.latex.autoBuild.run": "onSave",
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.latex.recipes": [
    {
      "name": "latexmk",
      "tools": ["latexmk"]
    }
  ],
  "latex-workshop.latex.tools": [
    {
      "name": "latexmk",
      "command": "latexmk",
      "args": [
        "-pdf",
        "-interaction=nonstopmode",
        "-synctex=1",
        "%DOC%"
      ]
    }
  ]
}
```

---

## 6. 测试最小 LaTeX 示例

创建 `main.tex`：

```latex
\documentclass{article}
\begin{document}
Hello LaTeX!
\end{document}
```

然后：

* 保存文件
* 自动编译
* 在 Windsurf 中打开 PDF 预览

---

## 7. 常见问题

### ❌ latexmk 不工作

原因：

* 没安装 Perl
* 或 PATH 未配置

解决：

```bash
where latexmk
```

检查路径是否存在。

---

### ❌ 没有图形化 PDF 预览

解决：

* 使用命令：`View LaTeX PDF`
* 或快捷键（通常是）：

```
Ctrl + Alt + V
```

---

### ❌ 编译失败但无提示

查看：

```
OUTPUT → LaTeX Workshop
```

---

## 8. 小结（核心依赖关系）

```
LaTeX Workshop（编辑器插件）
        ↓
latexmk（构建工具）
        ↓
Perl（运行环境）
        ↓
MiKTeX（实际编译）
```

---
