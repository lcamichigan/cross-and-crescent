# cross-and-crescent

[![Build status](https://ci.appveyor.com/api/projects/status/ad0eshengay90ivq?svg=true)](https://ci.appveyor.com/project/lcamichigan/cross-and-crescent)
[![Build Status](https://travis-ci.org/lcamichigan/cross-and-crescent.svg?branch=master)](https://travis-ci.org/lcamichigan/cross-and-crescent)

This is a [LaTeX](https://www.latex-project.org) package for drawing the logo of
[Lambda Chi Alpha Fraternity](https://www.lambdachi.org) using
[Ti*k*Z](https://www.ctan.org/pkg/pgf) or
[Asymptote](http://asymptote.sourceforge.net).

## Installing

To install the cross-and-crescent package, download cross-and-crescent.sty from
the [Releases](https://github.com/lcamichigan/cross-and-crescent/releases), and
then move this file to your TeX local installation directory. If you use
[TeX Live](https://www.tug.org/texlive/) on Windows, this directory is probably
C:\texlive\texmf-local, and you can move cross-and-crescent.sty by entering in
Command Prompt

```batch
set crossAndCrescent=C:\texlive\texmf-local\tex\latex\local\cross-and-crescent
if not exist %crossAndCrescent%\NUL mkdir %crossAndCrescent%
move /y cross-and-crescent.sty %crossAndCrescent%
```

If you use [MacTeX](https://www.tug.org/mactex/) on macOS, your TeX local
installation directory is probably /usr/local/texlive/texmf-local, and you can
move cross-and-crescent.sty by entering in Terminal

```sh
crossAndCrescent=/usr/local/texlive/texmf-local/tex/latex/local/cross-and-crescent
sudo mkdir -p $crossAndCrescent
sudo mv -f cross-and-crescent.sty $crossAndCrescent
```

Regardless of what platform you use, remember to run `mktexlsr` after moving
cross-and-crescent.sty to your TeX local installation directory.

If you’d rather create cross-and-crescent.sty from its
[source](cross-and-crescent.dtx), enter in Command Prompt

```batch
for /l %G in (1, 1, 2) do xetex -fmt=xelatex cross-and-crescent.dtx
```

or in Terminal

```sh
for i in {1..2}; do xetex -fmt=xelatex cross-and-crescent.dtx; done
```

## Usage

You can use the cross-and-crescent package in a TeX document like this:

```tex
\documentclass{article}
\usepackage{cross-and-crescent}
\begin{document}
\begin{tikzpicture}
  \crossAndCrescentSetMacros
  \draw \crossAndCrescentPath
\end{tikzpicture}
\end{document}
```

If you just want to create a PDF file of a cross and crescent, you can enter in
Command Prompt

```batch
latex -jobname logo -output-format pdf "\documentclass{standalone}\usepackage{cross-and-crescent}\begin{document}\crossAndCrescent\end{document}"
```

or in Terminal

```sh
latex -jobname logo -output-format pdf '\documentclass{standalone}\usepackage{cross-and-crescent}\begin{document}\crossAndCrescent\end{document}'
```

You can use the Asymptote script by `include`-ing it. The Asymptote script
contains a single function `crossAndCrescentPath` that returns an array of paths
for a cross and crescent. For example, enter in Terminal

```sh
asy -outformat png -noView -command '
include crossAndCrescent;
real size = 400; size(size);
fill(scale(size) * shift(-0.5, -0.5) * unitsquare, cmyk(1, 0.6, 0, 0.6));
fill(scale(42) * crossAndCrescentPath(), cmyk(0, 0.18, 1, 0) + evenodd);
' picture.png
```

to create the GitHub profile picture for the
[lcamichigan](https://github.com/lcamichigan) organization.
