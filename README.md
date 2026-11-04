# pdf-unicode-math

This package allows for the use of unicode characters for the input of mathematical symbols in pdflatex and other 8-bit formats (assuming the use of utf-8 input as has been the default since 2018).

The main idea is to take the existing [symbol table](https://texdoc.org/serve/unimath-symbols/0) defined by [unicode-math](https://ctan.org/pkg/unicode-math) and turn it on its head: In unicode-math, the table defines control sequences to expand to a unicode character; here, we instead use it to define unicode characters that expand to control sequences. This approach is based on a [TeX.SE post](https://tex.stackexchange.com/questions/601579/unicode-maths-in-pdflatex#601583) by David Carlisle, but with some more QOL features to make it semi-usable.

## Features
- Iterates through all 2,448 unicode symbols defined in `unicode-math-table.tex`(see [unimath-symbols.pdf](https://texdoc.org/serve/unimath-symbols/0) for a typeset list). In most cases, defines the unicode character shown on the left to expand to the control sequence shown on the right.
- Will not declare any unicode character for which the associated control sequence is not already defined.
 - The package works best if loaded after any other packages defining math symbols.
 - If a package defines a symbol with a different control sequence, you must alias the control sequence in [unimath-symbols](https://texdoc.org/serve/unimath-symbols/0) if you want it to work.
- In the case of special alphabets like blackboard bold, almost no package will have defined, e.g., `\BbbR` to expand to `\mathbb{R}`. Therefore this package defines all such alphabetical control sequences approproately.
 - This package attempts to make sane defaults for the setup to avoid defining broken macros; see the next section for customization.
- In many cases LaTeX pre-defines unicode characters as text symbols, e.g. `U+00D7 × MULTIPLICATION SIGN` is already defined as `\texttimes` whereas this package attempts to define it as `\times`. The package can either attempt to keep the existing definition in text mode and change the meaning in math mode (default), or leave the existing definition alone, or override it entirely; see package options below.

## Package Options
All options are in key=value format.
