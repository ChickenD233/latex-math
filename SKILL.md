---
name: latex-math
description: Use whenever an output contains a formula, equation, derivation, integral, derivative, limit, sum, matrix, probability, statistic, or unit, and whenever a draft holds ASCII math such as e^(−2t), 1/2, sqrt(x), x_i, <=, or a bare ∫. It puts every formula in LaTeX between math delimiters, so the Web GUI shows real math instead of hard-to-read plain text. A standing global rule, not an on-request tool. Also use when asked to fix formulas that are hard to read.
license: MIT
metadata:
  version: "1.0"
  verified-against: DSH Web frontend 0.2.1-rc.2 (KaTeX)
---

# latex-math

Every formula is LaTeX between math delimiters. No exception.

Plain text math is a defect. The reader must decode `∫e^(−2t)dt = −(1/2)e^(−2t) + C`. The same formula between delimiters renders as real math:

$$
\int e^{-2t}\,dt = -\frac{1}{2}e^{-2t} + C
$$

## Delimiters

| Surface | Inline | Display |
|---|---|---|
| Chat reply, docs, README, PR text, slides | `$x^{2}$` | `$$` on its own line, formula, `$$` on its own line |
| Same, when `$` is ambiguous | `\(x^{2}\)` | `\[` … `\]` |
| Commit message, terminal, log, plain text | LaTeX source without delimiters | same, on its own line |

The DSH Web GUI renders KaTeX. All four delimiter forms work. Use `$` by default: it is shortest and every model writes it well.

## Choose the form

1. A standalone equation, a derivation, or anything with `=`, `\int`, `\sum`, or `\lim` goes in a display block.
2. A symbol, a variable, or a short expression inside a sentence goes inline, and the sentence keeps its spaces outside the `$`.
3. A surface that cannot render math gets the LaTeX source. Do not fall back to unicode math.

## Rewrite table

| Plain text | LaTeX |
|---|---|
| `e^(−2t)` | `e^{-2t}` |
| `1/2`, `(a+b)/c` | `\frac{1}{2}`, `\frac{a+b}{c}` |
| `sqrt(x)`, `x^(1/2)` | `\sqrt{x}`, `x^{1/2}` |
| `x_i`, `a_(n+1)` | `x_{i}`, `a_{n+1}` |
| `sum from i=1 to n` | `\sum_{i=1}^{n}` |
| `int f(x) dx` | `\int f(x)\,dx` |
| `lim x->0` | `\lim_{x \to 0}` |
| `<=`, `>=`, `!=` | `\le`, `\ge`, `\ne` |
| `~=`, `≈` | `\approx` |
| `+-`, `*` | `\pm`, `\cdot` |
| `inf`, `->`, `=>` | `\infty`, `\to`, `\Rightarrow` |
| `alpha`, `theta` | `\alpha`, `\theta` |
| `d/dt`, `dy/dx` | `\frac{d}{dt}`, `\frac{dy}{dx}` |
| `90°`, `30 degrees` | `90^{\circ}`, `30^{\circ}` |
| `implies`, `because` | `\implies`, `\because` |

## A derivation

Put the whole chain in one display block with `\begin{aligned}`. Align on `=`. Give one line of reason per step, in words outside the math.

$$
\begin{aligned}
\int_0^{\infty} e^{-2t}\,dt
&= \left[-\frac{1}{2}e^{-2t}\right]_0^{\infty} \\
&= 0 - \left(-\frac{1}{2}\right) \\
&= \frac{1}{2}.
\end{aligned}
$$

## Gotchas

- Put every `^` and `_` inside math. Outside math they start Markdown emphasis or stay literal.
- One `$` opens math. Write currency as `\$5` or `US$5`, or the next `$` closes a fake formula.
- Multi-letter names run together in math. Write `$v$` and name it in prose, or write `\mathrm{velocity}`.
- Write words inside math as `\text{...}`.
- KaTeX takes `$$` and `\begin{aligned}`, `cases`, `matrix`, `array`. It rejects `\usepackage`, `\documentclass`, `\begin{equation}`, `\label`, and `\ref`.
- `\\` breaks a line only inside an environment.
- Math inside a code fence or inline code stays literal. That is correct for source code, and wrong for a formula the reader must read.

## Worked fix

Before:

> 因为 ∫e^(−2t)dt = −(1/2)e^(−2t) + C。对 −(1/2)e^(−2t) 求导得到 e^(−2t)。代入上限：t → ∞ 时，e^(−2t) → 0，所以上限项等于 0。代入下限：t = 0 时，e^0 = 1，所以下限项等于 −1/2。上限减下限：0 − (−1/2) = 1/2。

After:

$$
\int e^{-2t}\,dt = -\frac{1}{2}e^{-2t} + C
$$

因为 $-\frac{1}{2}e^{-2t}$ 的导数是 $e^{-2t}$。

代入上限：当 $t \to \infty$ 时，$e^{-2t} \to 0$，所以上限项等于 $0$。
代入下限：当 $t = 0$ 时，$e^{0} = 1$，所以下限项等于 $-\frac{1}{2}$。
上限减下限：$0 - \left(-\frac{1}{2}\right) = \frac{1}{2}$。

## Self-check before you send

1. Every formula sits between one pair of delimiters.
2. No bare `^`, `_`, `sqrt(`, `1/2`, `->`, or `<=` in prose.
3. Each display block starts at the beginning of a line, with a blank line before and after.
4. Every command is in the KaTeX set, with no preamble command.
5. Each derivation step has one line of reason outside the math.
