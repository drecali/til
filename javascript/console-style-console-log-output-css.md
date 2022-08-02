# `[Console]` - Style `console.log()` output with CSS

The humble `console.log()` method can do a **LOT** more than just output plain text to the console, even though that's all it's used for most of the time.

You can add CSS to style the text using the `%c` directive. I summarized a bit of the possibilities below but as always, the [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/console#styling_console_output) have a wealth of knowledge.

## But why?

Styled output in the console is much easier to see. It's especially useful if there are other unformatted logs in the console. Stylish output jumps out at you.

Another excellent use case - which I'll try to address soon - is when outputting colors. What would you prefer? Reading color RGB or hex values, or looking at an actual sample of that color right in the console?

## The basics

The syntax for the basic case is simple:

`console.log(` <kbd>"</kbd> <kbd>%c</kbd> `The string you want to format` <kbd>"</kbd> `,` <kbd>"</kbd> `CSS Styles` <kbd>"</kbd> `)`

```js
// instead of
console.log("Hello World");

// be stylish
console.log("%cHello World", "color:red");
```

<img width="334" alt="image" src="https://user-images.githubusercontent.com/24983797/182379081-aaf87726-965c-4012-8b3e-6526d29e8b8b.png">

## Moving `%c` around

As shown, the `%c` directive doesn't need to be at the beginning of the string.

> The `style` argument is applied immediately after the `%c` directive until the end of the string or the next `%c` directive.

```js
console.log("Hello %cWorld", "color:red");
```

<img width="337" alt="image" src="https://user-images.githubusercontent.com/24983797/182383310-27b07475-55ac-41de-a967-00040cbeecaa.png">

## Using `%c` multiple times

There can be multiple `%c` directives in one string. The `style` arguments are applied in order.

- The 1st `style` argument is applied from the 1st `%c` directive until the 2nd `%c`
- The 2nd `style` argument is applied from the 2nd `%c` directive to the 3rd `%c` and so on, until the end of the string.

```js
console.log("Hello %cWorld%c!!", "color:red", "color: green");
```

<img width="502" alt="image" src="https://user-images.githubusercontent.com/24983797/182382350-728918c1-b67e-41cc-9009-51a2360736b1.png">

## Leave parts of the string unstyled

To leave parts of the string unstyled, just add a `%c` with an empty `string` as its `style`.

```js
console.log("Hello %cWorl%cd", "color:red", "");
```

<img width="381" alt="image" src="https://user-images.githubusercontent.com/24983797/182383628-efbd836f-71c1-4942-a6cf-c9b5e59d8889.png">

## Add all of the styles\*

> \* Not really. There are some limitations. See [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/console#styling_console_output:~:text=The%20properties%20usable%20along%20with%20the%20%25c%20syntax%20are%20as%20follows) for a list of supported CSS properties (at least in Firefox).
>
> Better yet, open the console and try it yourself right now!

What I showed is just the tip of the iceberg. I would highly recommend checking out the excellent examples in [this article](https://levelup.gitconnected.com/add-styles-and-formatting-to-your-console-log-messages-in-javascript-5f14819b1c5d).

Another good place to see these stylish console logs is in the console of tech companies like Facebook or Discord. Here's an example from the latter.

<img width="508" alt="image" src="https://user-images.githubusercontent.com/24983797/182386600-963f7c9a-8282-49aa-8a8d-2332de85a151.png">
