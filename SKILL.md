---
name: latex-math
description: Every formula is LaTeX between math delimiters. Use it whenever an output holds a formula, equation, derivation, integral, derivative, limit, sum, matrix, or probability, and whenever a draft shows ASCII math such as e^(−2t), 1/2, sqrt(x), or x_i. Also use it when asked to fix formulas that are hard to read. A standing global rule.
license: MIT
metadata:
  version: "2.0"
  verified-against: DSH Web frontend 0.2.1-rc.2 (KaTeX)
---

# latex-math

Every formula is LaTeX between math delimiters. Plain text math is a defect:

`∫e^(−2t)dt = −(1/2)e^(−2t) + C` → $\int e^{-2t}\,dt = -\frac{1}{2}e^{-2t} + C$

- Inline: `$x^{2}$`. Display: `$$` alone on a line, the formula, `$$` alone on a line.
- A standalone equation or a derivation goes in a display block. A symbol inside a sentence goes inline.
- One `$` opens math, so write currency as `\$5`.
- Keep every `^` and `_` inside math.
- Multi-letter names take `\mathrm{max}`, never `$max$`.
- KaTeX only: `$$`, `\begin{aligned}`, `cases`, `matrix`. No `\usepackage`, `\begin{equation}`, `\label`.
- A surface that cannot render (commit message, terminal, log) gets the LaTeX source.

A derivation is one block, aligned on `=`, with one line of reason per step outside the math:

$$
\begin{aligned}
\int_0^{\infty} e^{-2t}\,dt
&= \left[-\frac{1}{2}e^{-2t}\right]_0^{\infty} \\
&= 0 - \left(-\frac{1}{2}\right) = \frac{1}{2}.
\end{aligned}
$$
