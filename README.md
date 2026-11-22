# LaTeX 试卷

本仓库用于存放和编译 LaTeX 试卷。所有试卷源文件统一放在 `exams/`，生成的 PDF 统一放在 `output/pdf/`。

## 环境准备

试卷使用 UTF-8 编码，并通过 XeLaTeX 编译。在 Debian 或 Ubuntu 上可以安装以下依赖：

```bash
sudo apt update
sudo apt install -y texlive-xetex texlive-lang-chinese texlive-latex-extra latexmk
```

## 编译试卷

编译单份试卷时，将 `<试卷文件名>` 替换为 `exams/` 中对应的文件名（不含 `.tex`）：

```bash
mkdir -p output/pdf
latexmk -xelatex -interaction=nonstopmode -halt-on-error \
  -outdir=output/pdf exams/<试卷文件名>.tex
```

生成的文件位于 `output/pdf/<试卷文件名>.pdf`。

编译全部试卷：

```bash
mkdir -p output/pdf
for source in exams/*.tex; do
  latexmk -xelatex -interaction=nonstopmode -halt-on-error \
    -outdir=output/pdf "$source"
done
```

清理编译产生的辅助文件：

```bash
for source in exams/*.tex; do
  latexmk -c -outdir=output/pdf "$source"
done
```
