# latex-math

A standing rule for AI agents. Every formula is LaTeX between math delimiters.

Plain text math is a defect. The reader must decode this:

```
∫e^(−2t)dt = −(1/2)e^(−2t) + C
```

The same formula between delimiters renders as real math:

$$
\int e^{-2t}\,dt = -\frac{1}{2}e^{-2t} + C
$$

This skill makes an agent write the second form every time.

## What it covers

- Chat replies, docs, READMEs, PR text, and slides use `$x$` inline and `$$` for display.
- A commit message or a terminal log gets the LaTeX source without delimiters, because these surfaces cannot render math.
- A derivation goes in one `\begin{aligned}` block. Each step gets one line of reason in prose.
- Every command stays inside the KaTeX subset. No `\usepackage`, no `\begin{equation}`, no `\label`, no `\ref`.

## Install

Copy the skill into an agent skill directory.

```
cp -r latex-math ~/.agents/skills/
```

DSH reads `~/.agents/skills/<name>/SKILL.md`. Claude Code reads `~/.claude/skills/`.

## Load the skill

Add one line to `AGENTS.md` or `CLAUDE.md`:

```
Load the `latex-math` skill before you write math.
```

## Files

- `SKILL.md` — the rule set, the rewrite table, and the self-check list.

## Scope

This rule applies to text that a person reads. It does not apply to code, identifiers, paths, command syntax, or log output.

## License

MIT
