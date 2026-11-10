# 统计学试卷 LaTeX 电子稿

主文件是 `exam.tex`，使用 UTF-8 编码和 XeLaTeX 编译。源码只包含照片中的印刷内容，不包含手写答案或批注。

## 迁移到 WSL

Windows 中的当前目录是：

```text
D:\Code\exam
```

WSL 会把它映射为：

```text
/mnt/d/Code/exam
```

目标目录使用 `xjn` 的 Linux 主目录。下面的命令会复制项目、确认题目和 7 页 PDF 均存在，并逐文件比较两边内容：

```bash
set -e
test -d /mnt/d/Code/exam
test ! -e /home/xjn/exam
cp -a -- /mnt/d/Code/exam /home/xjn/exam
test -f /home/xjn/exam/exam.tex
grep -q '一、单项选择题' /home/xjn/exam/exam.tex
pdfinfo /home/xjn/exam/output/pdf/exam.pdf | grep -q '^Pages:.*7$'
diff -qr /mnt/d/Code/exam /home/xjn/exam
cd /home/xjn/exam
```

`/mnt/d/Code/exam` 就是 Windows 的 `D:\Code\exam`，这里只作为复制来源，不会删除。前面的任何校验失败都会因 `set -e` 而停止。

如果 `/home/xjn/exam` 已存在，命令会在复制前停止，防止覆盖旧文件。

## 安装 LaTeX

以下命令适用于 Ubuntu/Debian WSL：

```bash
sudo apt update
sudo apt install -y texlive-xetex texlive-lang-chinese texlive-latex-extra latexmk poppler-utils
```

这里使用 TeX Live 自带的 Fandol 中文字体，不依赖 Windows 字体。

## 编译

```bash
cd /home/xjn/exam
mkdir -p output/pdf
latexmk -xelatex -interaction=nonstopmode -halt-on-error -outdir=output/pdf exam.tex
```

生成的 PDF 位于：

```text
/home/xjn/exam/output/pdf/exam.pdf
```

若要从 Windows 资源管理器打开该目录，可在 WSL 中运行：

```bash
explorer.exe "$(wslpath -w /home/xjn/exam/output/pdf)"
```

清理编译产生的辅助文件：

```bash
latexmk -C -outdir=output/pdf exam.tex
```

需要在 WSL 中初始化 Git 时，再运行：

```bash
cd /home/xjn/exam
git init
```
