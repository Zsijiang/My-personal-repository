# LaTeX 编译技能

使用 XeLaTeX 编译 Beamer 或其他 LaTeX 文档，完成 3 次编译 + bibtex 引用解析。

## 使用场景

当需要编译 LaTeX 幻灯片或论文时使用。输入文件名（不含 .tex 扩展名）。

---

## 编译步骤

### 第 1 步：导航到文件目录并执行 3 次编译

```bash
cd Slides  # 或论文所在目录
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode [文件名].tex
BIBINPUTS=..:$BIBINPUTS bibtex [文件名]
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode [文件名].tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode [文件名].tex
```

**替代方案 (latexmk):**
```bash
TEXINPUTS=../Preambles:$TEXINPUTS BIBINPUTS=..:$BIBINPUTS latexmk -xelatex -interaction=nonstopmode [文件名].tex
```

### 第 2 步：检查警告
- 搜索 `Overfull \\hbox` 警告
- 搜索 `undefined citations` 或 `Label(s) may have changed`
- 报告发现的问题

### 第 3 步：打开 PDF 进行视觉验证
```bash
# macOS
open [文件名].pdf
# Linux
xdg-open [文件名].pdf
```

### 第 4 步：报告结果
- 编译成功/失败
- overfull hbox 警告数量
- 未定义引用数量
- PDF 页数

## 为什么需要 3 次编译？
1. 第 1 次 xelatex：创建 `.aux` 文件（含引用键）
2. bibtex：读取 `.aux`，生成 `.bbl`（格式化引用）
3. 第 2 次 xelatex：整合参考文献
4. 第 3 次 xelatex：解析所有交叉引用和最终页码

## 重要提醒
- **始终使用 XeLaTeX**，不要用 pdflatex（支持 Unicode 和系统字体）
- **TEXINPUTS** 路径必须包含你的 Beamer 主题所在目录
- **BIBINPUTS** 路径必须包含 `.bib` 文件所在目录
