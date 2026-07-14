# 论文写作 Skills 整理与推荐

本文整理本机已经安装、与论文工作直接相关，并且适合复制到其他电脑使用的 Skills。整理日期为 2026 年 7 月 14 日。

## 1. 筛选标准

收录项目必须同时满足：

1. 能直接服务于论文检索、阅读、写作、实验分析、文献管理或语言修改。
2. 目录中没有写死当前电脑的用户名、工作区盘符或个人缓存路径。
3. 复制前未发现真实 API Key、Token、Cookie、私钥或认证缓存。
4. `SKILL.md` 以及它引用的脚本、参考资料一并保留。

GitHub 来源不是强制条件。能确认公开仓库的项目会列出链接，无法确认的项目标记为“来源未确认”，不会猜测或伪造仓库地址。

本目录是分享副本，不是 Codex 当前加载 Skill 的安装目录。删除或修改这里的文件不会自动更新本机已经安装的 Skill。

## 2. 分享包结构与安装

所有可分享 Skill 都放在 [`skills`](./skills/) 目录中。接收者不要只复制这份说明文档，应保留每个 Skill 的完整目录。

Windows 上可以把需要的 Skill 文件夹复制到下面任一目录：

```text
%USERPROFILE%/.agents/skills/
%USERPROFILE%/.codex/skills/
```

例如，要安装 `academic-translation-guide`，应复制整个文件夹：

```text
skills/academic-translation-guide/
```

复制后重新启动 Codex 或新建任务。部分 Skill 还依赖浏览器插件、MCP、Zotero、MinerU、Office、LaTeX 或 Python；复制 Skill 只会安装工作流程，不会自动安装这些外部软件。

## 3. 星级说明

星级评价的是“对完整论文工作流的推荐程度”，不是 GitHub Star 数量。

| 星级 | 含义 |
| --- | --- |
| ★★★★★ | 论文工作流中的核心能力，适用范围广，建议优先保留 |
| ★★★★☆ | 很实用，但依赖特定软件、服务或使用阶段 |
| ★★★☆☆ | 有明确用途，适合作为补充工具 |
| ★★☆☆☆ | 使用场景较窄，或需要较多人工检查 |
| ★☆☆☆☆ | 与论文只有间接关系，不建议作为主要工具 |

## 4. 总览

### 4.1 写作、翻译和投稿检查

| Skill | 主要用途 | 推荐 | 来源状态 |
| --- | --- | --- | --- |
| `research-writing-skill` | 选题、综述、写作、实验、统计、制图、审稿和验证 | ★★★★★ | [GitHub](https://github.com/Norman-bury/research-writing-skill) |
| `latex-paper-en` | 英文 LaTeX 论文编译、检查、润色和投稿前审计 | ★★★★★ | 来源未确认 |
| `office-academic-skill` | 中文学术 Word、PPT、阅读报告和模板匹配 | ★★★★☆ | 来源未确认 |
| `academic-translation-guide` | 学术翻译、译后编辑和中式英语修正 | ★★★★☆ | 来源未确认 |
| `writing-humanizer-zh` | 清理模板化、宣传式和明显的 AI 写作模式 | ★★★★☆ | [GitHub](https://github.com/op7418/Humanizer-zh) |
| `docx-red-yellow-revision` | 用红色旧文、黄色新文制作可见修订版 DOCX | ★★★★☆ | 来源未确认 |

### 4.2 论文解析、文献库和可视化

| Skill | 主要用途 | 推荐 | 来源状态 |
| --- | --- | --- | --- |
| `mineru` | PDF、Word、PPT、图片转 Markdown，提取公式和表格 | ★★★★☆ | [GitHub](https://github.com/Nebutra/MinerU-Skill) |
| `pdf-md-review-zotero` | PDF 转 Markdown、阅读总结并整理 Zotero 附件 | ★★★★☆ | 来源未确认 |
| `zotero` | DOI 导入、集合管理、BibTeX/RIS 和附件管理 | ★★★★☆ | [GitHub](https://github.com/shoei05/claude-code-zotero-skill) |
| `read-arxiv-paper` | 根据 arXiv 链接读取论文 | ★★★★☆ | 来源未确认 |
| `drawio-technical-diagrams` | 创建可编辑的 draw.io 技术路线图和系统图 | ★★★★☆ | 来源未确认 |
| `scientific-figure-text-translation` | 翻译科研图中的文字并保持术语和布局准确 | ★★★★☆ | 来源未确认 |
| `research-to-diagram` | 调研主题并生成知识关系图 | ★★★☆☆ | 来源未确认 |

### 4.3 Google Scholar

| Skill | 主要用途 | 推荐 |
| --- | --- | --- |
| `gs-search` | 按关键词搜索 Google Scholar | ★★★★☆ |
| `gs-advanced-search` | 按作者、期刊、年份和标题字段高级检索 | ★★★★☆ |
| `gs-cited-by` | 查找引用某篇论文的后续研究 | ★★★★☆ |
| `gs-fulltext` | 查找 PDF、DOI 和出版社全文入口 | ★★★★☆ |
| `gs-navigate-pages` | 翻页和继续浏览搜索结果 | ★★★☆☆ |

以上 Skill 来源未确认，使用时需要可访问 Google Scholar 的浏览器环境；导出到 Zotero 时还需要 Zotero 正常运行。

### 4.4 中国知网

| Skill | 主要用途 | 推荐 |
| --- | --- | --- |
| `cnki-search` | 按关键词搜索知网论文 | ★★★★☆ |
| `cnki-advanced-search` | 按题名、作者、期刊、时间和收录类别检索 | ★★★★☆ |
| `cnki-parse-results` | 将当前检索结果整理成结构化数据 | ★★★★☆ |
| `cnki-paper-detail` | 提取题名、作者、机构、摘要、关键词和基金信息 | ★★★★☆ |
| `cnki-download` | 下载指定论文的 PDF 或 CAJ | ★★★★☆ |
| `cnki-journal-search` | 按名称、ISSN、CN 或主办方查找期刊 | ★★★☆☆ |
| `cnki-journal-index` | 查询北大核心、CSSCI、CSCD、SCI、EI 等收录状态 | ★★★★☆ |
| `cnki-journal-toc` | 浏览期次目录和原始目录页 | ★★★☆☆ |
| `cnki-navigate-pages` | 翻页、跳页和切换排序 | ★★★☆☆ |

以上 Skill 来源未确认，需要浏览器和可用的知网访问环境。下载全文、导出或访问机构资源时，接收者还需要自己的合法账号和权限。

## 5. research-writing-skill

本地副本：[research-writing-skill](./skills/research-writing-skill/)

推荐星级：★★★★★

这是四个项目中覆盖范围最广的论文写作 Skill。它不是单一提示词，而是一套由多个子 Skill 组成的工作流，适合从论文启动一直用到投稿前检查。

### 适合做什么

- 明确论文类型、研究问题、方法和章节结构。
- 搜索、整理并综合文献证据。
- 编写引言、相关工作、方法和实验章节。
- 设计实验、评价指标和结果表格。
- 选择统计方法并按照学术规范报告结果。
- 生成论文图表、流程图和 LaTeX 内容。
- 投稿前执行自查、同行评审式检查和引用验证。

### 主要子 Skills

| 子 Skill | 用途 | 推荐程度 |
| --- | --- | --- |
| `using-research-writing` | 进入统一论文工作流并选择后续 Skill | ★★★★★ |
| `brainstorming-research` | 明确选题、论文类型、方法和章节结构 | ★★★★☆ |
| `literature-review` | 规划检索、分类和文献综述写作 | ★★★★★ |
| `evidence-driven-writing` | 要求引言、相关工作等内容由证据驱动 | ★★★★★ |
| `paper-orchestration` | 协调跨章节写作和中大型修改 | ★★★★★ |
| `writing-chapters` | 按章节逐步写作并要求阶段确认 | ★★★★☆ |
| `writing-core` | 中文学术写作、润色和质量检查 | ★★★★★ |
| `experiment-results-planning` | 规划实验、结果表和评价协议 | ★★★★☆ |
| `statistical-analysis` | 选择统计检验并规范报告结果 | ★★★★☆ |
| `figures-python` | 使用 Python 生成论文数据图 | ★★★★☆ |
| `figures-diagram` | 规划流程图、架构图和概念图 | ★★★☆☆ |
| `latex-output` | 将内容放入 LaTeX 模板或输出 LaTeX | ★★★★☆ |
| `peer-review` | 投稿前进行同行评审式自查 | ★★★★★ |
| `verification` | 在宣称完成前执行引用和结果验证 | ★★★★★ |
| `prompts-collection` | 提供翻译、润色和降低 AI 痕迹的提示词 | ★★★☆☆ |
| `environment-setup` | 为绘图和统计任务准备 Python 环境 | ★★★☆☆ |

### 为什么给五星

它覆盖了论文写作最容易断开的几个环节：选题、证据、实验、正文和最终验证。尤其值得保留的是 `evidence-driven-writing` 与 `verification`，它们能减少“先写结论、后找引用”和未经核实就宣称完成的问题。

### 使用限制

- 它能规范流程，但不能保证引用本身真实，DOI、页码和原始结论仍需核对。
- 实验规划不能代替真实实验数据。
- 图表和统计结果必须保留代码、原始数据及可复现步骤。

## 6. MinerU

本地副本：[mineru](./skills/mineru/)

推荐星级：★★★★☆

MinerU Skill 用于把 PDF、Word、PPT、图片或公开文档链接解析成结构化 Markdown。处理论文时，它可以提取标题层级、正文、表格、公式和图片，便于后续检索、总结和引用原文。

### 适合做什么

- 将单篇或多篇论文 PDF 转成 Markdown。
- 提取扫描版论文中的文字。
- 保留公式、表格和图片目录。
- 为本地知识库、Obsidian 或 AI 阅读工作流准备材料。
- 在 MinerU 请求超时或 SSL 出错时执行诊断和重试流程。

### 为什么是四星半以下

文档解析是论文阅读的重要前置步骤，但转换结果不是原文。双栏排版、跨页表格、脚注和复杂公式仍可能识别错误，正式引用必须回到 PDF 核对。

### 服务与凭据说明

该 Skill 支持 MinerU MCP、云端 API 和本地输出流程。整理副本中没有 API Key 或 Token。需要云端精确模式时，应由使用者在自己的安全配置中提供凭据，不要把密钥写入 Skill、论文目录或公开仓库。

## 7. Zotero

本地副本：[zotero](./skills/zotero/)

推荐星级：★★★★☆

Zotero Skill 用于管理文献库，而不是直接生成论文正文。它可以处理 DOI 导入、集合管理、条目检索、BibTeX/RIS 导入，以及部分附件和标签操作。

### 适合做什么

- 根据 DOI 批量创建文献条目。
- 搜索已有 Zotero 条目和集合。
- 整理课题、章节或实验对应的文献集合。
- 导入 BibTeX、RIS 和 Crossref 元数据。
- 把 PDF、Markdown 阅读笔记和其他附件关联到同一条目。

### 为什么给四星

引用管理贯穿整个论文周期，Zotero 能显著减少重复录入和文件散落。但条目元数据仍可能缺作者、页码、期号或正确标题大小写，导入后必须抽查。

### 服务与凭据说明

该 Skill 同时支持 Zotero 本地 API 和 Web API。整理副本中没有 Zotero API Key、Library ID 或登录凭据。涉及远程库写入时，应从安全的环境变量或本地配置读取使用者自己的凭据。

## 8. writing-humanizer-zh

本地副本：[writing-humanizer-zh](./skills/writing-humanizer-zh/)

推荐星级：★★★★☆

这个 Skill 用于识别并修改常见的 AI 写作模式，例如空泛强调、宣传式措辞、三段式堆砌、模糊归因、过多连接词和机械结尾。

### 适合做什么

- 修改论文初稿中的模板化中文。
- 清理摘要、引言和结论中的空话。
- 让教程、阅读笔记和研究报告更自然。
- 在不改变技术含义的前提下压缩重复内容。

### 为什么不是五星

它是语言编辑工具，不负责验证论点、数据和引用。过早使用还可能把尚未稳定的术语改乱。建议在事实、结构和引用基本确定后再使用，并明确要求保留专业术语和数值。

## 9. 按论文阶段选择

| 阶段 | 首选 Skill | 配合使用 |
| --- | --- | --- |
| 选题和研究设计 | `research-writing-skill` | `zotero` |
| 文献收集 | `zotero` | `research-writing-skill/literature-review` |
| PDF 阅读与整理 | `mineru` | `zotero` |
| 引言和相关工作 | `evidence-driven-writing` | `literature-review`、`zotero` |
| 实验设计 | `experiment-results-planning` | `statistical-analysis` |
| 图表制作 | `figures-python`、`figures-diagram` | `verification` |
| 章节写作 | `writing-chapters`、`writing-core` | `paper-orchestration` |
| 中文润色 | `writing-humanizer-zh` | `writing-core` |
| 投稿前检查 | `peer-review`、`verification` | `zotero` |

## 10. 推荐组合

### 阅读一篇论文

1. 用 `mineru` 转换 PDF 并保留图片。
2. 回到 PDF 检查公式、表格和关键结论。
3. 用 `zotero` 保存条目、PDF 和阅读笔记。
4. 用 `literature-review` 判断该论文应放入哪一类研究脉络。

### 写文献综述

1. 用 `zotero` 建立主题集合并清理元数据。
2. 用 `literature-review` 设计检索和分类框架。
3. 用 `evidence-driven-writing` 写作，要求每个重要判断都有来源。
4. 用 `verification` 检查引用是否真实支持正文。
5. 最后用 `writing-humanizer-zh` 清理生硬表达。

### 完成整篇论文

1. 用 `using-research-writing` 和 `brainstorming-research` 明确任务。
2. 用 `paper-orchestration` 管理章节和阶段目标。
3. 按章节调用写作、实验、统计和图表 Skills。
4. 用 `peer-review` 找问题，再用 `verification` 检查完成条件。
5. 最后进行语言润色和版式检查。

## 11. 外部依赖

“可以复制”不等于“复制后所有功能都能离线运行”。接收者需要根据任务准备相应环境：

| Skill 类别 | 运行前提 |
| --- | --- |
| `research-writing-skill`、翻译和润色类 | 通常只需要 Codex；绘图和统计子任务可能需要 Python |
| `latex-paper-en` | 需要可用的 LaTeX 环境，例如 TeX Live 或 MiKTeX |
| `office-academic-skill`、`docx-red-yellow-revision` | 需要文档处理运行时；视觉检查通常需要 Microsoft Office 或 LibreOffice |
| `mineru`、`pdf-md-review-zotero` | 需要 MinerU MCP、云端服务或相应解析环境 |
| `zotero` | 需要 Zotero；远程库操作可能需要使用者自己的 Web API 凭据 |
| Google Scholar Skills | 需要浏览器和可访问 Google Scholar 的网络环境 |
| CNKI Skills | 需要浏览器；下载和导出需要使用者自己的合法账号及机构权限 |
| `read-arxiv-paper` | 需要可用的 arXiv 读取工具或 MCP |
| draw.io 和科研图翻译 | 需要 draw.io、Inkscape、PowerPoint、图像工具或相应插件中的至少一种 |

分享包不会替接收者安装这些软件，也不会包含你的账号、浏览器登录状态或 API Key。

## 12. 凭据安全检查

复制前已检查 27 个顶层 Skill 目录中的文件名和文本内容，未发现：

- `.env`、认证缓存或凭据文件。
- OpenAI、Anthropic、GitHub、AgentKey 或 AWS 常见密钥格式。
- JWT、Bearer Token、Cookie 或带用户名密码的 URL。
- RSA、EC 或 OpenSSH 私钥。

说明文档和脚本中可能出现 `API_KEY`、`TOKEN` 等环境变量名称，这是参数说明，不是密钥值。整理目录中没有新增任何 API Key、Zotero 登录信息、知网账号或浏览器认证数据。

## 13. 因个人路径未收录的 Skills

下面这些本地 Skill 与论文工作有关，但文件中出现了当前电脑的固定用户名、工作区盘符或个人过程目录，因此没有放入分享包：

- `pdf-layout-translate`
- `doc`
- `pdf`
- `editable-scientific-figures`
- `isac-fso-research`
- `presentation-skill`
- `zotero-md-collection-export`
- `cnki-export`
- `gs-export`

这些 Skill 并不一定有安全问题，但直接复制后可能在别人的电脑上读取不存在的路径或把文件写到错误位置。`cnki-export` 和 `gs-export` 写死的是原作者电脑上的目录，其他项目写有当前电脑的个人目录。按照本次要求，它们整体排除，没有自动替换路径后再打包。

OpenAI 运行时中的 PDF、Documents 和 LaTeX 插件也没有复制。它们属于应用管理的运行时或插件缓存，不是独立的个人 Skill 包；只复制其中一个 `SKILL.md` 会遗漏脚本和依赖，不能保证在其他电脑上正常工作。接收者应通过 Codex 的插件或 Skill 安装渠道获取对应版本。

## 14. 更新建议

需要更新某个 Skill 时，应先查看对应 GitHub 仓库的发布说明和文件差异，不要直接覆盖正在使用的本地版本。更新后重新执行凭据扫描，并确认新版本的 `SKILL.md`、脚本和依赖文件都在。
