# Markdown Tables Basics

There are some distinctions between Markdown and GitHub [Flavored](https://www.markdownguide.org/getting-started/#flavors-of-markdown) Markdown, but I only use Markdown on GitHub since it't what I'm most familiar with and what I need to remember. It's probably where most people use Markdown the most.

Markdown tables are pretty awesome, quick, and most of the syntax is intuitive. Cells can contain Markdown with some exceptions, like block elements:

- Fenced code blocks (\`\`\``\n`\`\`\`)
- Blockquotes (`>`)
- Collapsible sections (`<details><summary></summary></details>`)

Markdown tables, like Markdown in general, can contain images and `HTML`.

This is what I normally do:

```
| Column A | Column B |
|--|--|
| A1 | B1 |
```

| Column A | Column B |
| -------- | -------- |
| A1       | B1       |

## Colons (`:`) align columns

```md
| Default = Left-align |   Centered    | Right-aligned |
| -------------------- | :-----------: | ------------: |
| col 2 is             |   centered    |         $1600 |
| col 3 is             | right-aligned |           $12 |
```

| Default = Left-align |   Centered    | Right-aligned |
| -------------------- | :-----------: | ------------: |
| col 2 is             |   centered    |         $1600 |
| col 3 is             | right-aligned |           $12 |

The outer pipes (`|`) are optional, and you don't need to make the raw Markdown line up prettily. You can also use inline Markdown.

```
Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
```

| Markdown | Less      | Pretty     |
| -------- | --------- | ---------- |
| _Still_  | `renders` | **nicely** |
| 1        | 2         | 3          |

## Resources

- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).
- [Markdown Explained](https://www.markdownguide.org/getting-started/).
- Free online Markdown [editor](https://dillinger.io/) with live preview. It can even convert HTML files to Markdown!
- The original Markdown [spec](https://daringfireball.net/projects/markdown/) and [syntax](https://daringfireball.net/projects/markdown/syntax).
- Interactive Markdown [tutorial](https://www.markdowntutorial.com/) that unfortunately does not cover `tables` but is otherwise nicely done.
