# 回归分析期中考试试卷

主文件为 `regression_analysis.tex`，使用 UTF-8 编码，通过 XeLaTeX 编译。

```bash
sudo apt update && sudo apt install -y texlive-xetex texlive-lang-chinese texlive-latex-extra latexmk
mkdir -p output/pdf && latexmk -xelatex -interaction=nonstopmode -halt-on-error -outdir=output/pdf regression_analysis.tex
```

生成文件为 `output/pdf/regression_analysis.pdf`；清理辅助文件可运行 `latexmk -C -outdir=output/pdf regression_analysis.tex`。
