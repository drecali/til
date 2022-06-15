# Collapsible Sections + Free bonus bookmarklet! 💥

Collapsible sections are great! They're really useful and I think they're underutilized because people don't know about them or forgot how to use them properly. For a long time, I didn't know Markdown has this feature.

Collapsible sections are especially great to segment a huge amount of information and let the reader decide if a particular section is relevant to them. If some information is extremely important to 20% of readers, why force all readers to scan through it and decide how far to skip?

## Requirements

More detailed 👇

```xml
<details>
    <summary>Always visible. Can **ONLY** be plaintext</summary> <!-- Good place for a CTA (Call to Action) -->
 <!-- empty line *️⃣  -->
    Markdown for
    collapsible content
    goes here.
</details>
<!-- empty line *️⃣  -->
```

Minimalist 👇

```xml
<details>
    <summary> Always visible. Can **ONLY** be plaintext </summary>
<!-- empty line -->
    Collapsible content (Markdown-stylable)
</details>
<!-- empty line -->
```

## Bonus! Free Bookmarklet! 💥

<details>
    <summary> 👉 Click to see the bookmarklet in action 🎬 </summary>

https://user-images.githubusercontent.com/24983797/173832754-3331ee59-7b7c-4c82-add4-9083a3f22885.mov

</details>

<hr>

- Copy this code:
  - `javascript: (() => { const ele = document.activeElement; ele.setRangeText('<details>\n <summary> Always visible. Can **ONLY** be plaintext </summary>\n<!-- empty line -->\n Collapsible content (Markdown-stylable)\n</details>\n<!-- empty line -->', ele.selectionStart, ele.selectionEnd, 'select'); })();`
- Create a bookmark in your browser (Chrome 102 tested)
- Paste the code as the bookmark's `URL`.

To use it:

- Click on an editable text field so you can see the text cursor.
- Click the bookmarklet to insert a minimalist snippet for a collapsible section at your current cursor position.
- Profit (unless you tried to use it in an `iframe` element 😢)

<details>
    <summary>*️⃣</summary>

The `empty lines` are not required in **all** situations, but they're harmless and essential for **some** situations, so it's easier to remember to always include them.

</details>

<hr>

## Full disclosure

All the content below comes directly from a very helpful and thorough [Gist](https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab) with 814 stars, 109 forks, 107 comments, and 4 revisions. Some comments pointed out edge cases and improvements that led to the excellent Gist we have today. I wanted to keep my summary short and sweet, but I also wanted others to marvel at the beauty of more complex collapsible sections without having to click on a link. Enjoy!

<hr>

## Gist content

## A collapsible section containing markdown

<details>
  <summary>Click to expand!</summary>
  
  ### Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details>

## A collapsible section containing code

<hr>

<details>
  <summary>Click to expand!</summary>
  
  ```javascript
    function logSometing(something) {
      console.log(`Logging: ${something}`);
    }
  ```
</details>

## How to structure

<hr>

```
# A collapsible section with markdown
<details>
  <summary>Click to expand!</summary>

## Heading

1. A numbered
2. list
_ With some
_ Sub bullets
</details>

```

**Two important rules:**

1. Make sure you have an **empty line** after the closing `</summary>` tag, otherwise the markdown/code blocks won't show correctly.
2. Make sure you have an **empty line** after the closing `</details>` tag if you have multiple collapsible sections.

## Resources

- Original [Gist]() about collapsible sections.
  - [Comment](https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab?permalink_comment_id=4169582#gistcomment-4169582) that inspired the bookmarklet.
- StackOverflow [answer](https://stackoverflow.com/a/34278578/10117759) that showed how to insert text at the current cursor.
- FreeCodeCamp article about [bookmarklets](https://www.freecodecamp.org/news/what-are-bookmarklets/)
