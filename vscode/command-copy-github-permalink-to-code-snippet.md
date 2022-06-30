# `[Command]` - Copy GitHub permalink to code snippet

[TL;DR - I want to skip to the magical part](#code-snippet-permalinks-ftw)

> Note: this article covers a `command` for a VS Code `extension`. It's not the main function of the extension so it feels more appropriate to classify this as a `[Command]` article.

## What are permalinks and why should I use them?

Permalinks are magical because they never break and the content at their destination never change. A GitHub permalink is tied to a specific commit so even if those lines in that file change after the permalink is generated, it won't affect the permalink content. The permalink is frozen in time, which is great when you want to refer to a specific line of code in a deeply-nested file in a repo.

```md
# DON'T send a message like this

Hey, on the `dev` branch of <repoName>, look at `line 38` of `src/app/components/menu/submenu/options/BestOption.tsx`.  
Can we refactor that?

# DO send a message like this

Can we refactor this?  
https://github.com/<userName>||<OrgName>/<repoName>/blob/<commitSha>/src/app/components/menu/submenu/options/BestOption.tsx#L38
```

## Code snippet permalinks FTW

https://github.com/drecali/til/blob/c202b18c7d76857d61d179b8634e509170601ce2/css/combining-multiple-selectors.md#L45-L48

```yaml
# The actual code for this code snippet permalink
https://github.com/drecali/til/blob/c202b18c7d76857d61d179b8634e509170601ce2/css/combining-multiple-selectors.md#L45-L48
```

## The best part: create permalinks from VS Code!

Most people know how to generate permalinks on the GitHub website. It used to be a painstaking process of clicking to navigate to the correct file on the website. If it's nested several levels deep, it's too annoying.

The VS Code extension [GitHub Pull Requests and Issues](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) can generate GitHub permalinks! Just highlight the lines of code you're interested in, right click, and choose `Copy as > Copy GitHub Permalink`.

<img width="1171" alt="image" src="https://user-images.githubusercontent.com/24983797/176687078-110c4582-dabc-4720-a8c5-6cbb3328e0ab.png">

I also assigned a custom keyboard shortcut to this feature to make it even easier.

## But wait, there's more!

You can also generate permalinks for an entire file. They won't render magically, but they're still really useful. Just right-click a file in the `Explorer` panel and choose `Copy as GitHub Permalink`.

## Caveats

- You can only create permalinks for code that has been committed on a `remote branch`. So it needs to be on GitHub for you to permalink to it.
- GitHub only renders code snippet permalinks magically within the same repo. So a code snippet permalink from repo A won't render magically on a page in repo B. As GitHub says:
  > This type of permanent link will render as a code snippet only in the repository it originated in. In other repositories, the permalink code snippet will render as a URL.

## Resources

- GitHub docs for [code snippet permalink](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-a-permanent-link-to-a-code-snippet)
- GitHub docs for [file permalink](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files)
