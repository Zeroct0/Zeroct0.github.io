---
title: 你好，世界
tags:
  - 随笔
categories:
  - 生活
description: 博客搭好了，这是第一篇文章。
abbrlink: acf5da54
date: 2026-10-12 21:30:00
---

博客终于搭起来了。以后技术笔记和生活碎片就都存在这儿。

## 怎么发一篇新文章

在项目根目录执行：

```bash
npx hexo new "文章标题"
```

生成的文件在 `source/_posts/` 下，用 Markdown 写完，然后：

```bash
git add .
git commit -m "post: 新文章"
git push
```

推送后 GitHub Actions 会自动构建并发布，一两分钟后就能在 <https://zeroct0.github.io> 看到。

## 文章开头要写什么

文件顶部那段 `---` 包裹的是 front-matter，用来告诉 Hexo 这篇文章的元信息：

```yaml
---
title: 你好，世界
date: 2026-10-12 21:30:00
tags:
  - 随笔
categories:
  - 生活
description: 列表页显示的摘要
---
```

`tags` 和 `categories` 都可以写多个，会自动归类到「标签」和「分类」页面里。

## 本地预览

推到线上之前，可以先在本地看看效果：

```bash
npx hexo server
```

然后浏览器打开 <http://localhost:4000>。改完 Markdown 存盘会自动刷新，不用重启。

## 代码块

写技术文章少不了代码，语法高亮是现成的：

```python
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

print(list(fib(10)))
```

行内的 `inline code` 也支持。

---

接下来就交给你了，把上面那篇当成模板，开始写吧。
