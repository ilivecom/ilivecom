# AGENTS.md · hiwd.com 项目说明（给 AI agent 看）

> 这份文件是给 Codex / Claude 等 AI agent 看的操作指南。
> 人类换机器请看 `SETUP.md`（不在仓库里）。

## ⭐ 总指令（最重要，先读这条）

**收到任何「发文章 / 写文章 / 发布」类任务时，默认就按本文件的全部规则执行，无需用户重复说明。**
用户的指令通常很短，你要自动补全所有默认行为：

- **自动选目录**：原创 → `andrew/`；转载/笔记/分享 → `notes/`。用户没说就按主题判断，一般是原创。
- **自动起文件名**：英文小写 + 连字符，能概括主题，例如 `andrew/why-i-quit-notion.html`。
- **自动套模板**：用下方对应模板（原创带 h1，转载从 h2 开始），补全 og 标签、署名、返回首页链接、footer 脚本。
- **自动更新 `sitemap.html`**：在对应分类列表最前面加一行入口，链接文字用文章标题。
- **自动发布**：直接 commit 并 **push 到 `main` 分支，不要创建 PR**。
- **默认篇幅**：约 1000 字，用户另有说明则从其要求。
- **文笔要求**：通顺、易懂、口语化但不啰嗦；把**前因后果讲清楚**（为什么写、发生了什么、结论或感悟）；少堆术语。第一人称（作者是 Andrew）。

> 用户无需说「按 AGENTS.md」「直接推 main 不开 PR」这类话——这些都是默认。只有当用户**明确要求例外**（如「这次开 PR」「放 notes」「不要更新 sitemap」）时才偏离。

## 三种发文模式（按用户给的信息量自动判断）

| 模式 | 用户会给什么 | 你怎么做 |
|---|---|---|
| **A · 自带正文** | 用户把完整正文贴给你 | **原样使用正文**，只负责套模板、排版成 `<p>`、更新 sitemap、发布。不要改写或删减用户的文字。 |
| **B · 给要点扩写** | 用户给主题 + 几个要点/方向 | 按要点**扩写成完整文章**，文笔参照上方要求，覆盖前因后果。 |
| **C · 只给主题** | 用户只给一个主题/标题 | 自行构思、写成完整文章。围绕主题讲清前因后果，观点真诚不空洞。 |

判断规则：贴了大段成文文字 → A；给了要点/提纲 → B；只有一句主题 → C。拿不准时按 B 处理，并在文章里保持作者第一人称口吻。

## 这是什么

- **hiwd.com** 是一个纯静态 HTML 博客，托管在 GitHub Pages。
- 仓库：`ilivecom/ilivecom`，域名由根目录 `CNAME` 指定。
- **没有构建步骤、没有框架、没有依赖**。改完 HTML 文件 `git push`，1–2 分钟后 hiwd.com 自动更新。
- 所有页面都是手写 HTML + 一个全站样式表 `style.css`。

## 目录与分类约定

| 位置 | 用途 | 标题规则 |
|---|---|---|
| `andrew/` | Andrew 的**原创**文章 | 正文用 `<h1>` 开头 |
| `notes/` | **转载 / 读书笔记 / 分享** | 正文用 `<h2>` 开头（**不要 h1**） |
| 根目录 | 长文 / 特殊页面 | 视情况，一般 `<h1>` |

- 文件名用**英文小写 + 连字符**，例如 `andrew/my-new-post.html`。
- `index.html`（各目录都有）、`sitemap.html`、`404.html`、`andrew.html`、`footer.html`、`style.css`、`admin.html` 是**结构性文件**，不是文章，新增文章时不要改它们（`sitemap.html` 除外，见下）。

## 发布一篇新文章的完整步骤

1. **创建文章 HTML 文件**，放进 `andrew/` 或 `notes/`（按上表选分类），用下面的模板。
2. **更新 `sitemap.html`**：在对应分类的 `<ul class="article-list">` 里加一行链接。
   - 原创放「个人观点」那个列表，转载放「个人分享」那个列表。
   - 新文章习惯加在列表**靠前**位置。
3. **直接提交并推送到 `main` 分支**（见下方「发布方式」）。

> ⚠️ 只创建文件却忘了更新 `sitemap.html`，文章就没有入口、读者找不到。两步都要做。

## 发布方式：直接推 main，不要开 PR

这是**一个人维护的个人博客**，没有协作审查需求。所有改动请**直接 commit 并 push 到 `main` 分支**，
**不要创建 Pull Request**。这样 GitHub Pages 会立刻部署，文章马上上线，作者无需再手动合并。

- 默认目标分支：`main`
- 改完执行：`git add` → `git commit` → `git push origin main`
- 除非作者在某次任务里明确要求「开 PR / 不要直接推」，否则一律直推 main。

## 文章模板

### 原创文章（放 `andrew/`，带 h1）

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>文章标题 - hiwd</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" type="text/css" href="../style.css">

    <meta property="og:title" content="文章标题">
    <meta property="og:description" content="一句话摘要">
    <meta property="og:image" content="https://hiwd.com/img/andrew.jpeg">
    <meta property="og:url" content="https://hiwd.com/andrew/文件名.html">
  </head>
  <body>
    <a href="https://hiwd.com/" id="logo"></a>

    <div id="content">
      <h1>文章标题</h1>

      <p>第一段……</p>
      <p>第二段……</p>

      <p>Andrew, June 2026</p>

      <p><a href="../index.html">← 返回首页</a></p>
    </div>

    <script>
    fetch('/footer.html')
      .then(response => response.text())
      .then(data => document.body.insertAdjacentHTML('beforeend', data));
    </script>
  </body>
</html>
```

### 转载 / 笔记（放 `notes/`，从 h2 开始，无 h1）

和上面**几乎一样**，区别只有两点：
- 正文第一个标题用 `<h2>` 而不是 `<h1>`。
- 注明出处（在结尾加一句来源说明）。

其余（`../style.css`、logo、`#content`、footer 脚本、返回首页链接）都保持一致。

## 路径规则（容易错，注意）

- **子目录**（`andrew/`、`notes/`）里的文章：样式表用 `href="../style.css"`，返回首页用 `../index.html`。
- **根目录**的页面：样式表用 `href="style.css"`，返回首页用 `index.html`。
- `og:url` 永远是完整线上地址 `https://hiwd.com/路径/文件名.html`。
- 页脚由每篇文章末尾那段 `fetch('/footer.html')` 脚本动态加载，**不要把页脚内容写死进文章**，照抄那段脚本即可。

## 不要碰 / 不要做的事

- 不要新建任何"管理后台""登录页""加密控制台"类文件——历史上有过，已废弃删除。发布只走 git。
- 不要把 GitHub token、密码等机密写进任何文件。仓库是公开的。
- `admin.html` 是一个**本地用的图形化编辑器**（在浏览器里写文章、调 GitHub API 发布），agent 一般用不到它，直接改文件更高效。不要删它，但也不依赖它。
- 不要引入任何外部 JS/CSS 依赖或构建工具，保持纯静态。

## 验证（可选）

本地预览：
```bash
python3 -m http.server 8000
# 浏览器开 http://localhost:8000/
```
agent 环境下一般不需要预览，确认 HTML 结构正确即可 push。
