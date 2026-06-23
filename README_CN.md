# 学术项目网站快速搭建指南（中文）

这是一个学术项目网页模板，适用于展示论文、项目、代码、演示视频和海报等内容。你已经通过 `git clone` 下载了本仓库，下面说明如何基于该模板快速制作自己的学术网站。

---

## 1. 目录结构

- `index.html`：网站主页，所有文本、链接、图片、视频、海报内容都在此文件中编辑。
- `static/css/`：页面样式文件。主要包括 `bulma.min.css` 和 `index.css`。
- `static/js/`：页面交互脚本。包含复制 BibTeX、下拉菜单、滚动按钮等功能。
- `static/images/`：图片资源，放置展示图、流程图、示意图、favicon 等。
- `static/videos/`：演示视频文件。
- `static/pdfs/`：论文 PDF、补充材料 PDF、海报 PDF 等。

---

## 2. 先决条件

你不需要编写复杂前端代码，修改现有模板即可。推荐工具：

- VS Code 或其他文本编辑器
- 浏览器（Chrome、Firefox、Safari 等）
- 本地静态服务器（可选，用于本地预览）

本模板适合直接部署到 GitHub Pages、Netlify、Vercel 等静态网站托管服务。

---

## 3. 修改步骤

### 3.1 修改页面元信息

打开 `index.html`，定位到 `<head>` 部分，替换以下内容：

- `meta[name="title"]`：论文标题 + 作者。
- `meta[name="description"]`：研究摘要，建议 150-160 个字符。
- `meta[name="keywords"]`：关键词，用逗号分隔。
- `meta[name="author"]`：作者列表。
- `og:title` / `og:description` / `og:image`：社交媒体分享用预览信息。
- `twitter:*`：Twitter 分享信息。
- `citation_title` / `citation_author` / `citation_publication_date` / `citation_conference_title` / `citation_pdf_url`：学术引用信息。
- `title`：浏览器标签上的标题。
- `link rel="icon"`：替换为你自己的 `favicon.ico`。

这些元信息不仅影响 SEO，还能提升页面在社交媒体和 Google Scholar 中的展示效果。

### 3.2 修改首页内容

在页面主体中，替换以下部分：

- 论文标题、作者、单位、日期。
- `publication-links` 区域中的 `Paper`、`Supplementary`、`Code`、`arXiv` 按钮链接。
- `video` 部分中的 `source src="static/videos/....mp4"`，替换为你的演示视频文件。
- 视频下方的说明文字。
- `Abstract` 区域中的论文摘要。
- 图片和文本区域中的图像路径与解释文字。
- `BibTeX` 代码块中的引用格式。

### 3.3 替换文件资源

- `static/images/`：把你的展示图、流程图、结果图、封面图等放到该目录。
- `static/videos/`：把你的演示视频或实验视频复制到该目录。
- `static/pdfs/`：把论文 PDF、补充材料、海报等放到该目录。
- `static/images/favicon.ico`：更换为你的站点图标。

建议：

- 图片压缩后再上传，减少页面加载时间。
- 视频文件较大时优先使用第三方视频平台如 YouTube，再通过 iframe 嵌入。

### 3.4 可选模块

该模板包含多个可选内容块，可根据需要打开或注释：

- 图像轮播（carousel）
- YouTube 视频嵌入
- 视频轮播
- PDF 海报预览
- `More Works` 相关工作下拉菜单

如果不需要某个区块，可以直接删除对应的 HTML 代码，或者保留并将 `style="display: none;"` 改为 `display: block;`。

---

## 4. 本地预览

建议先在本地打开页面预览：

方法一：直接打开 `index.html`。
方法二：使用本地服务器，例如：

```bash
python3 -m http.server 8000
```

然后访问 `http://localhost:8000`。

---

## 5. 部署网站

### 5.1 GitHub Pages

1. 将仓库推送到 GitHub。
2. 在仓库设置中启用 GitHub Pages，选择 `main` 或 `master` 分支的 `root`。
3. 等待页面发布即可。

### 5.2 其他静态托管

- Netlify：直接连接 GitHub 仓库并部署。
- Vercel：选择静态站点部署即可。

---

## 6. 进一步优化建议

- 生成 1200x630 的社交分享图像并替换 `og:image`。
- 将论文 PDF、补充材料、海报等资源放入 `static/pdfs/`。
- 检查 `index.js` 是否包含你需要的脚本行为，如果不需要可删除冗余内容。
- 确保 `static/css/index.css` 与页面内容配合良好。

---

## 7. 常见问题

- 如果页面加载不出图像，确认 `src` 路径是否正确。
- 如果视频无法播放，检查文件格式是否为 MP4，并确认浏览器支持。
- 如果 `BibTeX` 复制按钮无效，检查 `static/js/index.js` 是否被正确加载。

---

## 8. 总结

本仓库是一个学术项目网页模板，主要通过修改 `index.html` 和替换 `static/` 下的资源来完成内容定制。

步骤总结：

1. 编辑 `index.html` 中的元信息和页面内容。
2. 替换图片、视频、PDF 资源。
3. 本地预览并确认效果。
4. 部署到 GitHub Pages 或其他静态托管服务。

祝你的网站制作顺利！
