# latex-math

[English](README.md) | **中文**

给 AI agent 的常驻规则：公式一律写成 LaTeX，并放进数学分隔符。

纯文本公式是缺陷。读者得先解码这一行：

```
∫e^(−2t)dt = −(1/2)e^(−2t) + C
```

加上分隔符，同一行就是真正的数学：

$$
\int e^{-2t}\,dt = -\frac{1}{2}e^{-2t} + C
$$

这个 skill 让 agent 每次都写第二种形式：聊天回复、文档、PR 描述、幻灯片。

## 规则

- 行内：`$x^{2}$`。块级：`$$` 单独一行，公式，`$$` 单独一行。
- 整条等式或推导进块级。句中符号用行内。
- 推导用一个 `\begin{aligned}` 块，按 `=` 对齐，每步在数学外写一行理由。
- 一个 `$` 就开数学，货币写作 `\$5`。
- `^` 和 `_` 放进数学里。多字母名用 `\mathrm{max}`，不要 `$max$`。
- 只用 KaTeX：`$$`、`aligned`、`cases`、`matrix`。不写 `\usepackage`、`\begin{equation}`、`\label`。
- 不渲染的面直接给 LaTeX 源码，比如提交信息和终端日志。

## 为什么不靠渲染器

渲染 KaTeX 的宿主能读懂 `$...$`。不渲染的宿主只会显示源码。这个 skill 为每种面挑对的写法，不转 Unicode，也不生成图片。

## 安装

把文件夹复制到技能目录：

```
cp -r latex-math ~/.agents/skills/
```

- DSH 读 `~/.agents/skills/<name>/SKILL.md`。
- Codex 读同一路径。
- Claude Code 读 `~/.claude/skills/`。

## 让它常驻

skill 在写数学时触发。要它永远不掉，就在 `AGENTS.md` 或 `CLAUDE.md` 加一行：

```
写数学前加载 `latex-math`。行内用 `$...$`，块级用 `$$`。
```

## 文件

- `SKILL.md` —— 规则、示例、KaTeX 边界。

## 范围

规则只管人读的文字。代码、标识符、路径、命令、日志输出不在范围内。

## License

MIT
