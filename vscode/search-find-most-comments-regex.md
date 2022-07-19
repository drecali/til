# `[Search]` - Find **most** comments with RegEx

> [tl;dr: go directly to the RegEx](#🚀-the-regex)

Especially when dealing with an unfamiliar/legacy codebase, or just cleaning up a larger codebase, you may want to inspect all the comments. Comments tend to get stale and linger much longer than needed. It's a good idea to prune them as you code or do period tidying. That's what the [RegEx](#🚀-the-regex). I wrote more about my [love of RegEx](../javascript/regex-is-awesome-online-regex-playgrounds-cheatsheets.md), online prototyping and learning tools, and another use [practical use case](../vscode/search-plus-regex-equals-supersearch.md) in the VS Code Search panel.

## ✅ Detect the following:

- single-line comments starting with `//`
  - comments can start at the beginning of the line or they can be added after code
- multi-line comments where every line starts with `//` for some reason 🤷‍♂️

```js
// This will be detected

//so will this

alert(""); // this will also be detected

// This
// and this will be detected (as separate comments)
```

## ❌ Ignore the following:

- multi-line comments or JSDoc-style comments using `/* */`
- URL strings in the code (if they include `://` like `https://`) inside code or in a multi-line comment.
- Items marked `TODO`
- Error suppressing comments starting with:
  - `eslint`
  - `@`

```js
//TODO: this will not be detected

// TODO: neither will this

// @ts-ignore - this will not be detected

//@ts-ignore - this will not be detected

// eslint-disable - this will not be detected

//eslint-disable - this will not be detected

/* 
This will not be detected
*/

/*
This sentence will not be detected. Neither will the URL
https://drecali.link/til
*/
```

Even though it's not a best practice to suppress errors, that feature exists for a reason and is handy when you're happy with your strict linting rules 99% of the time but need to intentionally break them in a unique situation that warrants it.

## 🚀 The RegEx

```
(?<!:)\/\/(?!(\s*eslint))(?!(\s*@))(?!(\s*TODO))
```

This RegEx finds patterns only if all the criteria below are met:

- Includes `//`
- Does **not** include a colon (`:`) before the `//`
- Does **not** include `eslint`, `@`, or `TODO` with or without a space before it.

Many senior devs advised me against reinventing the wheel, so I initially tried to use a RegEx suggested by this StackOverflow [answer](https://stackoverflow.com/questions/5989315/regex-for-match-replacing-javascript-comments-both-multiline-and-inline). That one was really good at detecting edge cases in both both single-line and multi-line comments but it was more difficult to exclude the items I wanted to exclude.
