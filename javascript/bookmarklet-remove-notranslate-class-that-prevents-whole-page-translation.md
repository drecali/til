# \[Bookmarklet\] - remove `notranslate` class that prevents whole page translation

## Background

<details>
    <summary>Click to expand</summary>

Before HTML5, if an HTML element had `class="notranslate"`, machine translation would ignore that element. It was intended to be used for things like names and other elements that are not supposed to be translated. In HTML5 this can be accomplished with the attribute `translate="no"`. Still, most websites use the legacy method of just adding a `notranslate` class to an element.

Unfortunately, some website generators unreasonably apply the `notranslate` class to too many elements. It almost seems like it's the default. I've seen it mostly on sites from Korean companies/providers, but even [Notion](https://www.notion.so/20-4546184ba007496bbd330688afe484c9)\* does it! Chrome has Google Translate integrated, which is meant to translate entire websites at once. It works well but unfortunately, the evil `notranslate` class blocks it 😭.

</details>

## User Story

- I want my browser's built-in translator to translate **all** pages. It should not be foiled by a developer or website generator obsessed with the `notranslate` class.
- I want the solution to be easy to use. Ideally with 1 click.
- I want the solution to be easy to install.
- I want the solution to be easy to add to any browser I use.

## Solution

The code below is for a bookmarklet. [Bookmarklets](https://www.freecodecamp.org/news/what-are-bookmarklets/) are magic. They appear to be an ordinary browser bookmark but then clicked, they run a predefined JavaScript snippet.

With one click, this snippet removes all `notranslate` classes from all elements on a page. It's about as easy to install as it is to add a bookmark, and you can add it to any browser you want. This means it satisfies all the user stories.

<details>
    <summary>❗️Caution! Click to reveal a warning about this bookmarklet❗️</summary>

> Some websites (like Asana) will save elements every time their text changes. If you machine translate the entire page, you just edited all the editable fields on that page and their state got saved. Toggling the translator back to the source language may not work. I suggest using this bookmarklet cautiously for sites with editable elements you may care about.

</details>

```js
// Sorry, the syntax highlighting is strange because bookmarklets have slightly different syntax than normal JavaScript. They require starting with `javascript:`, which throws off JS syntax highlighting 🤷‍♂️
javascript: (() => {
  const rootOfAllEvil = "notranslate";
  document
    .querySelectorAll(`.${rootOfAllEvil}`)
    .forEach((element) => element.classList.remove(rootOfAllEvil));
})();
```

## A normal website without `notranslate` is easily translated by the browser

https://user-images.githubusercontent.com/24983797/173579878-ede8e77b-d975-429d-91e9-e65c0ab408f0.mov

## An evil website with `notranslate` is translated anyway, thanks to this bookmarklet!

https://user-images.githubusercontent.com/24983797/173579281-af37e236-a06f-471f-a9ab-108e543131b1.mov

## Installation in 10 seconds or your money back!

https://user-images.githubusercontent.com/24983797/173589164-1ffbd374-4532-4018-9aa3-d101f8bd0b81.mov

\* The Notion page linked in the [Background](#background) section uses one other dirty trick to prevent translation. I found a way to disable it too. Stay tuned for a future installment of TIL!

## Further Reading

- W3C [documentation](https://www.w3.org/International/questions/qa-translate-flag#:~:text=express%20similar%20ideas.-,Both%20Google%20and%20Microsoft,standards%20such%20as%20XLIFF.,-Microsoft%20apparently%20supports) about the `translate` attribute. It mentions the `notranslate` class as a "legacy approach". 🤣
- Google [documentation](https://cloud.google.com/translate/troubleshooting) about the `notranslate` class and `translate` attribute.
- [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/translate) for the `translate` attribute. Strangely enough, no mention of the `notranslate` class, but links to the W3C docs above, which do mention it.
- [HTML Spec](https://html.spec.whatwg.org/multipage/dom.html#the-translate-attribute) for the `translate` attribute. This is the HTML living standard. It makes no mention of the `notranslate` class.
