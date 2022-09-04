## `[DevTools]` - Show `console.debug()` output in console

In Chrome (and likely other browsers), `console.debug` outputs don't appear in the console panel of the developer tools. This is because `console.debug` outputs are treated as "Verbose" logs, which are not shown by default. Thankfully, it's easy to enable them as shown below.

1. Click the <kbd>Default Levels ▾</kbd> dropdown in the DevTools console.
1. Select <kbd>Verbose</kbd>
1. Profit 🎉

https://user-images.githubusercontent.com/24983797/188302944-c9a45ab3-c561-4616-9ba2-ba5c5184d375.mov

<img width="682" alt="image" src="https://user-images.githubusercontent.com/24983797/188303022-e8c3df7b-84d1-4e2a-a7b8-6dc72268688b.png">

<img width="682" alt="image" src="https://user-images.githubusercontent.com/24983797/188303040-fb8ee7ff-6fec-4b5b-a461-9ddfe8cd8dbd.png">

<img width="682" alt="image" src="https://user-images.githubusercontent.com/24983797/188303069-d4c9d28e-5ed5-46f8-a5a2-afbf444a3a8d.png">

You can further customize the level of console outputs shown below. This is useful for debugging if you want to focus on a very specific category of message.

https://user-images.githubusercontent.com/24983797/188304242-942e9647-abf3-400f-87b3-f3cf20fe1e1c.mov

Details from [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/console/debug):

> The `console.debug()` method outputs a message to the web console at the "debug" log level. The message is only displayed to the user if the console is configured to display debug output. In most cases, the log level is configured within the console UI. This log level might correspond to the `Debug` or `Verbose` log level.

## Why use `console.debug()` anyway?

This is the 3rd part in a series about the `no-console` ESLint rule.

- [Part 1](../eslint/no-console-1-disallow-all-console-methods.md) explains the advantages of the `no-console` ESLint rule.

- [Part 2](../eslint/no-console-2-allow-some-console-methods.md) explains why you'd want to customize the `no-console` ESLint rule to allow some console methods (like `console.debug()`).
