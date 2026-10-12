# zeroct's blog

个人博客：[Hexo](https://hexo.io/) + [Butterfly](https://butterfly.js.org/) 主题，托管在 GitHub Pages。

**线上地址** → <https://zeroct0.github.io>

| 组件 | 版本 |
| --- | --- |
| Hexo | 8.1.2 |
| Butterfly | 5.7.0 |
| Node.js | ≥ 20.19（CI 用 24） |
| Markdown 渲染 | hexo-renderer-markdown-it |

---

## 一、日常使用

### 写一篇新文章

```bash
npx hexo new "文章标题"
```

生成的文件在 `source/_posts/文章标题.md`，用 Markdown 写正文。文件顶部是 front-matter：

```yaml
---
title: 文章标题
date: 2026-10-12 21:30:00
tags:
  - 标签一
  - 标签二
categories:
  - 分类名
description: 列表页和搜索结果里显示的摘要
---
```

`tags` 和 `categories` 都可以写多个，会自动出现在「标签」「分类」页面和首页筛选里。

### 本地预览

```bash
npx hexo server
```

打开 <http://localhost:4000>。改 Markdown 存盘会**自动刷新**，不用重启。

> 改了 `_config.yml` 或 `_config.butterfly.yml` 需要**重启** server 才生效。

### 发布

```bash
git add .
git commit -m "post: 文章标题"
git push
```

推送到 `main` 后 GitHub Actions 自动构建部署，约 1 分钟上线。

### 清掉本地构建缓存

```bash
npx hexo clean
```

页面内容诡异、样式错乱时先试这个。

---

## 二、目录结构

```
博客/
├── _config.yml              # 站点配置（标题/作者/URL/插件）
├── _config.butterfly.yml    # 主题配置（菜单/头像/banner/侧边栏…）
├── package.json             # 依赖清单
├── .github/workflows/
│   └── deploy.yml           # 自动部署工作流
├── scaffolds/               # 新文件的模板
│   ├── post.md              # npx hexo new 用的模板
│   ├── page.md              # npx hexo new page 用的模板
│   └── draft.md
└── source/
    ├── _posts/              # ★ 文章都放这里
    ├── about/index.md       # 关于页
    ├── link/index.md        # 友链页
    ├── tags/index.md        # 标签页（type: tags，勿改）
    ├── categories/index.md  # 分类页（type: categories，勿改）
    └── img/                 # 头像、banner、favicon
```

`public/` 和 `node_modules/` 是构建产物，已被 `.gitignore` 忽略，**不要提交**。

---

## 三、常用配置改哪里

### 站点级 → `_config.yml`

| 想改什么 | 键 |
| --- | --- |
| 站点标题（浏览器标签、导航栏） | `title` |
| 站点描述 / 关键词 | `description` / `keywords` |
| 作者署名（页脚版权） | `author` |
| 语言 | `language`（当前 `zh-CN`） |
| 时区 | `timezone`（当前 `Asia/Shanghai`） |
| 域名 | `url` |
| 文章 URL 格式 | `permalink` |
| 首页每页文章数 | `index_generator.per_page` |

> ⚠️ `title` 里含英文单引号，YAML 里必须用双引号包住：`title: "zeroct's blog"`。

### 外观级 → `_config.butterfly.yml`

| 想改什么 | 位置 |
| --- | --- |
| 导航栏菜单项 | `menu:` |
| 导航栏 Logo / 是否固定 | `nav.logo` / `nav.fixed` |
| 社交图标（GitHub、邮箱…） | `social:` |
| 头像 | `avatar.img` |
| 首页全屏大图 | `index_img` |
| 其他页面默认大图 | `default_top_img` |
| 网站图标 | `favicon` |
| 首页副标题打字机 | `subtitle.enable` / `subtitle.effect` / `subtitle.sub` |
| 首页文章排版（1–7 种） | `index_layout` |
| 首页摘要长度 | `index_post_content.length` |
| 首页显示分类还是标签 | `post_meta.page.categories` / `post_meta.page.tags` |
| 侧边栏卡片开关 | `aside.card_*` |
| 侧边栏公告文字 | `aside.card_announcement.content` |
| 侧边栏 Follow 按钮链接 | `aside.card_author.button.link` |
| 页脚起始年份 | `footer.owner.since` |
| 主题署名（版权栏第二行） | `footer.copyright.enable` |
| 深色模式 | `darkmode.enable` |
| 代码块配色 / Mac 风格 | `code_blocks.theme` / `code_blocks.macStyle` |
| 正文目录 | `toc.post` |
| 字数统计 | `wordcount.enable` |
| 访问量统计 | `busuanzi` |

### 想换主题色

`theme_color` 在配置里默认是**注释掉**的。取消注释后每一项都要照抄，**颜色值必须加双引号**，否则 Hexo 会报错：

```yaml
theme_color:
  enable: true
  main: "#49B1F5"        # 主色
  paginator: "#00c4b6"
  link_color: "#99a9bf"
```

---

## 四、友链怎么加

编辑 `source/link/index.md`，把 `link_list: []` 展开成列表：

```yaml
{% flink %}
- class_name: 友情链接
  class_desc: 欢迎交换友链
  link_list:
    - name: 某某的博客
      link: https://example.com
      avatar: https://example.com/avatar.png
      descr: 一句话简介
    - name: 另一个站
      link: https://another.com
      avatar: https://another.com/avatar.png
      descr: 也写点东西
{% endflink %}
```

字段说明：

| 字段 | 含义 |
| --- | --- |
| `name` | 站点名称 |
| `link` | 站点地址 |
| `avatar` | 头像图片直链 |
| `descr` | 一句话简介 |

分多个组就写多个 `- class_name:` 开头的条目。想分组但暂时没链接，`link_list: []` 保持空数组不会报错。

> Butterfly 5 的友链**写在页面 markdown 里**，`_config.butterfly.yml` 里没有 `flink:` 段（那是 Butterfly 4 的写法）。

---

## 五、部署原理

```
本地写文章 → git push main
      ↓
GitHub Actions（.github/workflows/deploy.yml）
      ↓
npm ci → npx hexo generate → 产出 public/
      ↓
actions/deploy-pages 发布到 GitHub Pages
      ↓
https://zeroct0.github.io
```

仓库的 Pages 设置必须保持 **Settings → Pages → Source = `GitHub Actions`**。
如果被改回 `Deploy from a branch`，GitHub 会拿 Jekyll 去构建 `main` 根目录的**源码**，发布出来的是乱七八糟的源文件而不是站点。

`_config.yml` 里的 `deploy:` 是空的，**本地不需要执行 `hexo deploy`**，部署完全交给 Actions。

---

## 六、常见问题

### 首页 404 / 站点根目录打不开

Hexo 在**文章数为 0 时不会生成 `public/index.html`**，根目录直接 404。

所以 `source/_posts/hello.md` 是刻意保留的占位文章——**等你写好自己第一篇文章之后再删它**。

如果你确实想要「零文章也能开首页」，把 `_config.yml` 里的 `index_generator.per_page` 改成 `0`：

```yaml
index_generator:
  per_page: 0
```

代价是所有文章堆在一页，失去分页，文章多了首页会很长。

### 图标不显示 / 首页副标题打字机不动

说明第三方资源没加载到。本站已经把它们**自托管**了（`third_party_provider: local` + `hexo-butterfly-extjs` 依赖），正常情况下从 `github.io` 直接取，不依赖任何外部 CDN。

如果还是丢了，按顺序查：

1. `npx hexo clean && npx hexo server` 重来一遍
2. `node_modules` 是否完整：`npm ci`
3. 浏览器控制台看是哪个请求失败

> 之前本来用的是 jsDelivr CDN，但实测国内访问**失败率约 50%**，会导致图标全丢、副标题不动。改成自托管后解决。代价是构建产物 `public/` 涨到 11MB，其中约 9MB 是 mermaid、twikoo、mathjax 等**未启用**功能的库——它们不会被加载，只是占体积。首页实际只加载约 210KB CSS + 50KB JS。

### 文章 URL 是怎么定的

格式是 `/post/<8位十六进制>.html`，由 `hexo-abbrlink` 按**文章标题**的 crc32 算出，并**写回 front-matter**：

```yaml
---
title: 第一篇文章
abbrlink: 5c2fafc7        # 首次生成时自动写入
---
```

因为值已经存下来了，**之后再改标题，URL 不会变**，不用担心旧链接失效。

想强制重算，把 `_config.yml` 的 `abbrlink.force` 改成 `true` 构建一次——但那样旧链接会全部失效，慎用。

### 图片放哪、怎么引用

放进 `source/img/`，Markdown 里用绝对路径引用：

```markdown
![说明](/img/图片名.png)
```

引用其他网站的图直接用完整 URL。

### Actions 报了 Node.js 20 弃用警告

```
Node.js 20 is deprecated. The following actions target Node.js 20 but are being
forced to run on Node.js 24: actions/checkout@v4, ...
```

只是提示，**不影响构建**。等这些 action 发布 v5 再升级 `deploy.yml` 里的版本号即可。

### 我改了配置但页面没变化

两种情况：

1. **改了 `_config*.yml`**：server 不会热重载，需要 `Ctrl+C` 重启 `npx hexo server`
2. **浏览器缓存**：`Ctrl+Shift+R` 强制刷新

---

## 七、换回自己的素材

当前仓库里的图片是我生成的蓝色星空渐变占位图，建议尽快替换：

| 文件 | 用途 | 建议尺寸 |
| --- | --- | --- |
| `source/img/avatar.png` | 导航栏 Logo + 侧边栏头像 | 400×400 |
| `source/img/top.png` | 首页全屏 banner | 1920×1080 |
| `source/img/favicon.png` | 浏览器标签图标 | 128×128 |

替换后文件名保持一致就不用改配置；想换文件名则同步修改 `_config.butterfly.yml` 里的 `avatar.img`、`index_img`、`default_top_img`、`favicon`。

另外 `source/about/index.md` 里的自我介绍、`_config.butterfly.yml` 里 `aside.card_announcement.content` 的公告文案，都还是占位内容，记得改成你自己的。
