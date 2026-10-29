# latex-math

**English** | [中文](README.zh.md)

A standing rule for AI agents. Every formula is LaTeX between math delimiters.

Plain text math is a defect. A reader must decode this:

```
∫e^(−2t)dt = −(1/2)e^(−2t) + C
```

The same formula between delimiters renders as real math:

$$
\int e^{-2t}\,dt = -\frac{1}{2}e^{-2t} + C
$$

This skill makes an agent write the second form every time: in chat replies, docs, PR text, and slides.

## The rule

- Inline math: `$x^{2}$`. Display math: `$$` alone on a line, the formula, `$$` alone on a line.
- A standalone equation or a derivation goes in a display block. A symbol inside a sentence goes inline.
- A derivation is one `\begin{aligned}` block, aligned on `=`, with one line of reason per step in prose.
- One `$` opens math, so write currency as `\$5`.
- Keep `^` and `_` inside math. A multi-letter name takes `\mathrm{max}`, not `$max$`.
- KaTeX only: `$$`, `aligned`, `cases`, `matrix`. No `\usepackage`, no `\begin{equation}`, no `\label`.
- A surface that cannot render math gets the LaTeX source. A commit message and a terminal log are examples.

## Why a rule and not a renderer

A host that renders KaTeX reads `$...$` correctly. A host that does not render shows the raw source. The skill picks the right form for each surface. It does not convert math to Unicode, and it does not render images.

## Install

Copy the folder into a skill directory:

```
cp -r latex-math ~/.agents/skills/
```

- DSH reads `~/.agents/skills/<name>/SKILL.md`.
- Codex reads the same path.
- Claude Code reads `~/.claude/skills/`.

## Make it stick

The skill loads when the model writes math. For a rule that never falls off, add one line to `AGENTS.md` or `CLAUDE.md`:

```
Load the `latex-math` skill before you write math. Inline math uses `$...$`, display math uses `$$`.
```

## Files

- `SKILL.md` — the rule set, the display example, and the KaTeX limits.

## Scope

The rule applies to text that a person reads. It does not apply to code, identifiers, paths, command syntax, or log output.

## License

MIT
