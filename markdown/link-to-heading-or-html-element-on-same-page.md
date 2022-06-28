# Link to heading or HTML element on same page

Markdown supports hyperlinks with the syntax `[innerText](href)`. You might have already known that, but there's a pretty cool feature many people didn't know about. [Click here](#longH) to skip to the best part ⭐️.

## Basic syntax

Here's is a Markdown example with its HTML equivalent:

```md
[Click here](#linkOrID)

<a href="#linkOrID">Click here</a>
```

> ❗️ Note: I'm using the term `href` to refer to the destination of the Markdown link (`#linkOrID`) because it's functionally equivalent to the `<a>` tag's `href` attribute. Technically, the correct term is [`link reference definition`](https://github.github.com/gfm/#link-reference-definition), but that doesn't roll off the tongue as nicely.

## Link to a heading on the same page

Just like HTML anchor tags can link to an element with a specified `id` attribute on the same page, Markdown can also link to another element on the same page (with some twists and limitations).

This code links to the top heading of this page:

[Click here to link to the main heading](#link-to-heading-or-html-element-on-same-page)

```md
[Click here to link to the main heading](#link-to-heading-or-html-element-on-same-page)
```

## !@#$%^&\*()_+{}[]:";'-_\|\<>.,/~\`What about **special** characters or ...Markdown?

Markdown is pretty flexible. It will ignore any special characters in the heading, which is nice because you don't need to escape the special characters in the hyperlink. To link to the heading above: [Click here](#what-about-special-characters-or-markdown)

```md
[Click here](#what-about-special-characters-or-markdown)
```

## <a id="longH"></a> ⭐️ Linking to hidden HTML `<a>` tags, or 'What if I want to link to this really long heading but don't want my `href` to be ridiculously long or contain any emojis?'

Linking to the monstrous header directly above this sentence is pretty simple. Markdown supports `html` so you can just add a sneaky `<a>` tag with an `id` attribute on the same line as your long heading. The `<a>` tag is sneaky because it doesn't render on the screen if you don't give it any `innerText`. Actually, you can link to any `html` element with an `id` attribute.

[Click here to scroll to the long heading above](#longH)

```md
## <a id="longH"></a> ⭐️ Linking to hidden HTML `<a>` tags, or 'What if I want to link to this really long heading but don't want my `href` to be ridiculously long or contain any emojis?'

[Click here to scroll to the long heading above](#longH)
```

The other benefit of linking to a shorter `id` attribute within the `<a>` tag, you can change the actual heading text and the `link` will still work without updating it to match the new heading text. You just need to make sure the `id` attribute and the Markdown link `href` are identical.

It's amazing how much there is to learn even about a seemingly simple topic as Markdown.

## 💥 Bonus VS Code tip:

If you're writing your Markdown document in VS Code, it will give you suggestions for elements on the same page you can link to. Just type `[](#)` and wait a second. The intelli-sense should pop up and suggest correct `href`s for the headings on the page. It'd be nice if it could also suggest linking to elements with `id` attributes, but 🤷‍♂️.

<img width="616" alt="image" src="https://user-images.githubusercontent.com/24983797/176207255-cf3e0c0a-1675-4855-9fae-c85d9825a4c2.png">

## Resources

- Official GitHub Flavored Markdown spec giving you way more detail about [links](https://github.github.com/gfm/#links) than you wanted.
