# 统计学复习资料网站

一个面向统计学课程复习的静态学习资料网站，提供章节讲义、模拟试卷与备考指南。

## 项目结构

```
.
├── index.html        # 首页（章节导览与入口）
├── exam.html         # 模拟试卷下载页
├── unit/             # 各章节讲义（HTML）
│   ├── 1.html
│   ├── 2.html
│   ├── 3.html
│   ├── 4.html
│   ├── 5.html
│   └── STATS_REFERENCE.html
├── exam/             # 试卷 PDF（多个 AI 模型版本）
├── tex/              # 试卷 LaTeX 源文件
├── md/               # 复习提纲与备考指南 Markdown 源
└── doc/              # 复习提纲 Word 文档
```

## 内容组成

- **章节讲义**（unit/）：基于 Markdown 渲染的 HTML 章节页面
- **模拟试卷**（exam/ + tex/）：由多种 LLM 生成的对照版本，便于横向比较
- **复习提纲**（md/ + doc/）：结构化复习要点

## 本地运行

直接用浏览器打开 `index.html` 即可，无需任何构建步骤：

```bash
# Windows
start index.html

# macOS
open index.html

# Linux
xdg-open index.html
```

也可以使用任意静态服务器：

```bash
python -m http.server 8000
# 然后访问 http://localhost:8000
```

## 工具链

- 页面字体：Noto Serif / Noto Sans SC（Google Fonts）
- 试卷源：LaTeX
- 内容协作：Markdown + Word

## 许可

仅供学习使用。
