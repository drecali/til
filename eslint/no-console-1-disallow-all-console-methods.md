# `no-console` - 1 - Disallow all `console` methods

One popular ESLint rule is `no-console`. The official ESLint [docs](https://eslint.org/docs/latest/rules/no-console) say that console methods should not be used in production for code that runs in the browser.

> In JavaScript that is designed to be executed in the browser, it’s considered a best practice to avoid using methods on console. Such messages are considered to be for debugging purposes and therefore not suitable to ship to the client. In general, **calls using console should be stripped before being pushed to production**.

You may not want to use the console in production code because:

1. It's generally not advisable to expose inner logic in production. This is to prevent competitors from copying or reverse-engineering your tools for malicious purposes.
1. It makes the software feel less professional. The console is supposed to be used to troubleshoot during development, not all the time.
1. If the console is opened accidentally, it can look a bit sketchy to output certain code periodically or when certain actions occur.

AirBnB has a popular ESLint [config](https://github.com/airbnb/javascript/tree/1677ba6c6a285366e38998e292d42a7eab64d18e/packages/eslint-config-airbnb-base) that includes [this rule](https://github.com/airbnb/javascript/blob/1677ba6c6a285366e38998e292d42a7eab64d18e/packages/eslint-config-airbnb-base/rules/errors.js#L26-L27).

Treating `no-console` infractions as warnings seems reasonable because they may be necessary sometimes during development.

<img width="342" alt="image" src="https://user-images.githubusercontent.com/24983797/188299556-c94ae3ea-ca07-4165-abd4-36699053bfca.png">

```js
// in .eslintrc.js
module.exports = {
  //...
  rules: {
    // ...
    "no-console": "warn",
  },
};
```

<img width="625" alt="image" src="https://user-images.githubusercontent.com/24983797/188299821-06a8a0be-a19c-4474-b56c-1f1fde196b67.png">

They can also be designated as an `error`, which changes the underline color and icon.

```js
// in .eslintrc.js
module.exports = {
  //...
  rules: {
    // ...
    "no-console": "error",
  },
};
```

<img width="625" alt="image" src="https://user-images.githubusercontent.com/24983797/188299794-059153cd-1362-43b4-a8f6-705d479decaa.png">

But what if you need to output some information to the console and want to avoid triggering ESLint errors or warnings? Read [Part 2](./no-console-2-allow-some-console-methods.md) to find out.
