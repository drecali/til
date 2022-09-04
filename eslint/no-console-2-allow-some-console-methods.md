# `no-console` - 2 - Allow some `console` methods

> This is an continuation of a post that introduced the basics of the `no-console` ESLint rule. [Part 1](../eslint/no-console-1-disallow-all-console-methods.md) explains the advantages of the `no-console` ESLint rule.

In some cases, there may be a legitimate need for code to use `console` methods. One example is logging certain debug information in the development environment. In this case, there are a few options:

1. Disable the `no-console` rule for specific lines or the entire file with `// eslint-disable-next-line no-console`.

   - This is usually not considered a best practice and can clutter the code.

1. Tell ESLint to [ignore](https://eslint.org/docs/latest/user-guide/configuring/ignoring-code) certain files and folders.

   - It's also not a good idea because that disables **all** ESLint's protections for the matching files/folders.

1. Modify the rule to allow **certain** console methods that will be used sparingly and with intent.

   > `allow` has an array of strings which are allowed methods of the console object (Source: [ESLint Docs](https://eslint.org/docs/latest/rules/no-console#options))

   ```js
   // in .eslintrc.js
   module.exports = {
     //...
     rules: {
       // ...

       //🙅‍♂️ Disallows ALL console methods
       "no-console": "warn",

       //👍 This allows console.debug, console.warn, and console.error
       "no-console": ["warn", { allow: ["debug", "warn", "error"] }],
     },
   };
   ```

The console methods above format the output differently:

<img width="682" alt="image" src="https://user-images.githubusercontent.com/24983797/188304293-5fb33951-3eae-4120-9e60-280e0a07a660.png">

🚨 Unfortunately, `console.debug` outputs don't appear in the Chrome console by default. Find out why and how to fix that in [this article](../chrome/devtools-show-console-debug-output.md).

<img width="682" alt="image" src="https://user-images.githubusercontent.com/24983797/188303985-5b6a68a1-0a8d-446c-a70d-4638d14b7642.png">
