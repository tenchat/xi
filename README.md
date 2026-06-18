# 统计学复习资料网站

一个面向统计学课程复习的静态学习资料网站，提供章节讲义、模拟试卷与备考指南。

## 项目结构

```
.
├── index.html          # 首页（章节导览与入口）
├── exam.html           # 模拟试卷页面
├── notes.html          # 复习笔记页面
├── md/
│   └── SKILL.md        # 复习提纲与备考指南
├── unit/
│   ├── note1.md ~ note6.md    # 各章节讲义（Markdown）
│   ├── question1.md ~ question2.md  # 练习题
│   └── svg/            # 配图资源（0.svg ~ 17.svg）
└── README.md
```

## 内容组成

- **章节讲义**（unit/note*.md）：各章节知识点与重点内容
- **练习题**（unit/question*.md）：章节配套练习与答案
- **模拟试卷**（exam.html）：综合测试与模拟考试
- **复习笔记**（notes.html）：重点整理与复习要点
- **配图资源**（unit/svg/）：公式、图表等可视化素材

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
- 内容协作：Markdown

## 许可

仅供学习使用。
