# 哈尔滨理工大学 电子信息硕士学位论文 LaTeX 模版

一套非官方的哈尔滨理工大学硕士学位论文 XeLaTeX 模版，按学校 Word 格式要求调校了
字体、页边距、页眉页脚、章节标题、目录、图表标题与参考文献样式（GB/T 7714-2015）。
仓库自带一份**完整的示例论文**，方便你直接看到排版效果后，逐文件替换为自己的内容。

> ⚠️ **示例内容仅作排版演示**：仓库里的示例论文是《基于卷积神经网络的手写数字识别方法研究》，
> 属于经典教学题材，**与任何人的真实研究无关**，请务必全部替换为你自己的论文内容。
> 图片均为占位图，请替换为你自己的图片。

---

## 一、环境要求

- **TeX 发行版**：TeX Live 2021 及以上（或 MacTeX）。也可直接用 [Overleaf](https://www.overleaf.com)（编译器选 XeLaTeX）。
- **编译引擎**：XeLaTeX（务必使用 XeLaTeX，不能用 pdfLaTeX）。
- **参考文献**：biber + `biblatex` + `biblatex-gb7714-2015`（TeX Live 完整安装已包含）。
- **字体**：宋体、黑体需自备，详见下文「字体」一节。

## 二、如何编译

依次执行（共 4 步，确保目录与参考文献正确生成）：

```bash
xelatex  main
biber    main
xelatex  main
xelatex  main
```

或一条命令搞定（推荐）：

```bash
latexmk -xelatex main.tex
```

Overleaf 用户：菜单 **Menu → Compiler 选 XeLaTeX**，主文件设为 `main.tex`，直接点 Recompile 即可。

**prism.openai.com 用户（推荐）**：用 [prism.openai.com](https://prism.openai.com) 在线编译本模版。导入时**不要上传含 `.git` 的本地文件夹**，而是在本仓库点 **Code → Download ZIP** 下载干净压缩包再上传。注意：该 ZIP 不含宋体/黑体字体文件（版权原因未入库，见第五节），编译前请在 `main.tex` 启用「Fandol 兜底方案」，或自行将字体上传到 `fonts/` 目录。

## 三、目录结构

```
.
├── main.tex                 # 主文件：字体/页面/样式/章节装配，从这里开始读
├── paper.bib                # 参考文献库（示例为 CNN 方向，请替换）
├── frontmatter/             # 前置部分
│   ├── abstract_zh.tex      #   中文标题 + 摘要 + 关键词
│   └── abstract_en.tex      #   英文标题 + 摘要 + 关键词
├── chapters/                # 正文各章
│   ├── ch1_intro.tex        #   第一章 绪论
│   ├── ch2_related.tex      #   第二章 相关理论与技术基础
│   ├── ch3_model.tex        #   第三章 网络结构设计
│   ├── ch4_training.tex     #   第四章 训练与优化
│   └── ch5_experiment.tex   #   第五章 实验与结果分析
├── backmatter/              # 后置部分
│   ├── conclusion.tex       #   结论
│   ├── references.tex       #   参考文献（仅一条打印命令，一般不用动）
│   ├── results.tex          #   攻读学位期间成果（请替换为自己的）
│   └── acknowledgements.tex #   致谢（请替换为自己的）
├── figures/                 # 图片目录（当前全是占位图，请替换）
└── fonts/                   # 字体目录（宋体/黑体需自备，见 fonts/README.md）
```

## 四、替换成你自己的论文

按这个顺序改最省心：

1. **标题 / 摘要**：改 `frontmatter/abstract_zh.tex` 和 `abstract_en.tex`
   （注意中文标题在 `abstract_zh.tex` 第一行的 `\section*{...}`，太长时用 `\\` 手动换行）。
2. **正文**：逐章改 `chapters/*.tex`。每章开头形如
   ```latex
   \section{章标题}
   \setchapternum{2}   % ← 关键：把本章号告诉计数器，图/表/公式会自动按「2-1」编号
   ```
   改章节就改 `\section / \subsection / \subsubsection` 的标题与正文。
3. **图片**：把你的图片放进 `figures/`，改正文里的 `\includegraphics{figures/你的图.png}`。
4. **表格**：模版用 `booktabs` 三线表，复制现成 `table` 环境改数据即可。
5. **公式**：用 `equation` 环境，编号自动为「章号-序号」。
6. **参考文献**：把你的文献写进 `paper.bib`，正文用 `\cite{条目key}` 引用。
7. **个人成果 / 致谢**：改 `backmatter/results.tex`、`backmatter/acknowledgements.tex`。
8. **学校 / 学位（可选）**：页眉文字在 `main.tex` 的
   `\fancyhead[C]{...哈尔滨理工大学电子信息硕士学位论文}`，换学校或学位时改这里。

### 图 / 表 / 公式 的引用

用 `\label` + `\ref`，编号会自动更新（**别手写「图 3-2」**）：

```latex
\begin{figure}[htb]
  \centering
  \includegraphics[width=0.9\linewidth]{figures/your-figure.png}
  \caption{中文图题\\Fig.~\thefigure\ English Caption}
  \label{fig:your-label}
\end{figure}
% 正文引用：如图\ref{fig:your-label}所示……
```

## 五、字体

正文用**宋体**、标题用**黑体**。它们是 Windows 版权字体，未随仓库分发，需你自行放入
`fonts/` 目录（`simsun-win.ttc`、`SimHei.ttf`，详见 [`fonts/README.md`](fonts/README.md)）。
仿宋、楷体用 TeX Live 自带的开源 Fandol，无需另装。

**没有宋体/黑体也能先编译**：在 `main.tex` 里注释掉「中文字体」一段，启用紧随其后的
**Fandol 兜底方案**（已写好，去掉注释即可），即可在 Overleaf / 任意 TeX Live 上直接出 PDF。
正式提交前建议换回宋体/黑体以符合学校排版要求。

## 六、许可

代码与排版配置以 [MIT License](LICENSE) 开源。注意：
- **字体文件**不在本仓库内，其版权归各自权利人所有；
- 示例文字与占位图仅供演示，请勿用于真实学术署名。

## 七、致谢与免责声明

本模版为社区自发整理的非官方模版，与学校官方无关；能否用于最终答辩/提交，请以学院/研究生院的
最新格式要求为准。欢迎提 Issue / PR 一起完善。
