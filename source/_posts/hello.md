---
title: 第一篇文章
tags:
  - 随笔
categories:
  - 生活
abbrlink: 5c2fafc7
date: 2026-10-12 21:30:00
---

这是占位文章，删掉它完全没问题（Hexo 在文章数为 0 时不会生成首页，所以建议等你自己的第一篇文章写好之后再删）。

## 写新文章

```bash
npx hexo new "文章标题"
```

文件会生成在 `source/_posts/`，用 Markdown 写完然后：

```bash
git add .
git commit -m "post: 新文章"
git push
```

推送后 GitHub Actions 会自动构建发布，一两分钟后见 <https://zeroct0.github.io>。

## 本地预览

```bash
npx hexo server
```

打开 <http://localhost:4000>，存盘自动刷新。
