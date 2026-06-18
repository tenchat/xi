---
name: generate-unit-review-site
description: Generate a Chinese unit-based web review site from source materials such as Markdown notes, PDFs, LaTeX files, teaching objectives, syllabus files, or mixed course documents. Use when Codex needs to analyze course/reference files, split content into chapters or units, create or update `md/*.md`, generate self-contained `unit/*.html` review pages, and update the static `index.html` navigation for a browsable study-material website. 当前项目（f:\学习资料网站\st）已实现 5 章统计学 + 1 速查页结构，可作为模板。
---

# 分单元网页复习资料生成指南（统计学实例）

本 skill 用于把课程文件、教材摘要、讲义、教学目标、PDF、LaTeX 或 Markdown 资料整理成当前项目风格的分单元网页复习资料。产物应能直接作为静态网页打开，不依赖构建工具。

**当前项目实例**：f:\学习资料网站\st —— 统计学（5 章 + 1 速查页）

- 第一章 绪论
- 第二章 统计学原理
- 第三章 概率论与数理统计
- 第四章 统计分析
- 第五章 统计预测与决策
- 考试重点与公式速查

## 项目结构

当前项目是静态复习资料站：

- `index.html`：总入口。包含顶部标题、侧边栏导航、欢迎页、iframe 容器，以及 `units` 数组。新增或调整单元时必须同步这里的导航配置。
- `md/`：章节源稿。每个单元一个 Markdown 文件，命名形如 `第1章 财务管理概述.md`。优先把资料清洗、归纳到这里，再生成网页。
- `unit/`：最终单元网页。每个单元一个独立 HTML 文件，命名形如 `1.html`、`2.html`；总表或速查页可使用语义名，如 `FINANCIAL_REFERENCE.html`。
- 根目录资料：可能包含 `教学目标.md`、`.pdf`、`.tex`、`.docx`、`.xlsx` 等输入文件。它们是内容来源，不一定都要发布到网页。

## 工作流程

1. 盘点输入资料：用 `rg --files` 查看项目文件，识别课程名、章节数、已有 `md/` 和 `unit/` 是否可复用。
2. 建立单元清单：按章节、周次、教学目标或用户指定结构拆分单元。每个单元至少要有编号、标题、源文件、输出 HTML 路径。
3. 整理 Markdown 源稿：把每个单元归纳为稳定的学习稿，保留公式、例题、选择题、判断题和参考答案；修复乱码、重复标题、断裂列表。
4. 生成单元网页：每个 `unit/*.html` 必须是完整 HTML 文档，内含 CSS 和少量切换脚本，可被 `index.html` iframe 加载。
5. 更新总入口：修改 `index.html` 中的 `units` 数组，确保 `id`、`title`、`file`、`icon` 与生成文件一致。
6. 验收：检查链接、标签切换、中文显示、移动端布局、公式显示和题目答案，不留下空白 iframe 或失效路径。

## 内容组织

每个单元网页优先使用这些标签页；可按学科增减，但不要少于学习、概念、练习、重难点四类：

- `知识框架`：学习目标、知识地图、本章结构、考试/复习抓手。
- `核心概念`：用概念卡片列出术语、定义、辨析和常见误区。
- `专题内容`：按本章主题设置 1-3 个专门标签，例如 `计算模型`、`财务效率`、`金融市场`、`债券估值`。
- `重点问答`：用问答形式覆盖简答题、论述题、易混点。
- `练习题`：包含单选、多选、判断、计算题或案例题；题干和选项要清晰分段。
- `重难点`：列出高频考点、难点辨析、公式使用条件、答题提示。

如果资料中有大量公式或缩写，额外生成一个速查页放入 `unit/`，并在 `index.html` 的 `units` 数组中注册。

## 单元网页结构

沿用现有页面模式：

- 使用 `<!DOCTYPE html>`、`<html lang="zh-CN">`、`<meta charset="UTF-8">`。
- 保持温和纸面感视觉：`--ink`、`--red`、`--gold`、`--blue`、`--green`、`--border`、`--bg`、`--paper` 这组 CSS 变量。
- 顶部 `.header` 展示章号、标题和副标题。
- `.nav` 中放 `.nav-tab`，点击后调用 `switchTab(id)`。
- `.main` 中每个标签对应 `<div class="section" id="section-...">`，默认第一个加 `active`。
- 常用组件包括 `.card`、`.concept-grid`、`.concept-item`、`.keypoint`、`.formula-box`、表格、题目块和答案块。
- 页面底部放极简 `switchTab` 脚本，只负责切换 active 状态和滚动回顶。

保持每个单元 HTML 自包含。允许通过 CDN 加载 KaTeX 渲染数学公式；如果网络不可用，公式文本仍应可读。

## 内容写作规则

- 先忠实提取，再压缩整理。不要凭空添加教材没有支持的结论、公式或答案。
- 中文用词应面向复习：短句、分点、强结构、少废话。
- 保留原始题目的选项顺序和答案；若答案无法确定，标注“待核对”，不要猜。
- 公式用普通文本或 KaTeX 友好的写法，补充变量含义和适用条件。
- 概念卡片要“术语 + 定义 + 易混点/用途”，避免只堆名词。
- 问答题要给出可背诵的分层答案，优先使用“是什么、为什么、怎么用、注意什么”的结构。
- 重难点页要服务考前复盘，突出高频、易错、公式条件、典型题型。

## 从不同资料生成

- Markdown：优先使用标题层级切分。清理重复空行、断裂编号、错误嵌套列表。
- PDF：先抽取目录和章节标题；必要时按页码拆分。抽取后核对公式、表格、题目选项是否错位。
- LaTeX：保留章节结构、公式和枚举环境；把 `\section`、`\subsection` 转为网页标签和卡片结构。
- 教学目标/大纲：用于补全每章学习目标、重点难点和章节顺序，不要替代正文知识。
- 多文件混合：以课程大纲确定单元边界，以讲义/教材提供正文，以题库提供练习。

## 更新 `index.html`

新增或重排单元时，找到类似下面的数组并保持路径准确：

```js
const units = [
  { id: 1, title: '第一章 财务管理概述', file: 'unit/1.html', icon: '1' },
  { id: 2, title: '第二章 财务报表分析', file: 'unit/2.html', icon: '2' }
];
```

规则：

- `id` 用数字或稳定标识，不要重复。
- `file` 使用相对路径 `unit/...html`。
- `icon` 对章节用数字；速查、附录可用短符号或 1-2 个字符。
- 生成文件后检查侧边栏点击是否能加载对应 iframe。

## 质量检查

完成后至少检查：

- `rg --files` 能看到新增或更新的 `md/`、`unit/`、`index.html`。
- 每个 `unit/*.html` 都有 `<meta charset="UTF-8">`、标题、`.nav-tab`、`.section`、`switchTab`。
- `index.html` 的 `units` 数组没有指向不存在的文件。
- 中文没有乱码；尤其检查从 PDF/LaTeX/旧终端输出复制来的文本。
- 移动端下概念网格变为单列，导航横向滚动不遮挡内容。
- 题目答案与题干对应，公式和表格没有被截断。

## 输出说明

向用户汇报时说明：

- 识别到的项目结构和输入来源。
- 新增或更新了哪些 `md/` 源稿、`unit/` 页面和 `index.html` 导航。
- 哪些内容需要用户后续人工核对，例如来源不清的答案、PDF 抽取失败的公式或缺失章节。
