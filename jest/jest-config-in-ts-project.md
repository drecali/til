# Jest config in Typescript project

## Problem

Jest requires additional configuration to work with Typescript projects.

## Solution

1. Install the required dependencies:

```bash
$ npm install --save-dev jest babel-jest @babel/core @babel/preset-env ts-jest @types/jest
```

2. Create the `babel.config.js` file in project root with the following content:

```js
module.exports = {
  presets: [["@babel/preset-env", { targets: { node: "current" } }]],
};
```

3. If `jest.config.js` doesn't already exist in the project root, create it with the following content:

```js
module.exports = {
  preset: "ts-jest",
  transform: {
    "^.+\\.(ts|tsx)?$": "ts-jest",
    "^.+\\.(js|jsx)$": "babel-jest",
  },
};
```

4. (Optional) Add the following to the `scripts` section of the `package.json` file:

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch"
  }
}
```

While actively developing/testing certain features it's best to run the tests in watch mode, which causes them to re-run whenever a file changes.

To run tests in watch mode, use the following command:

```bash
$ npm run test:watch
```

To run tests once, use the following command:

```bash
$ npm test
```

## References:

- [Jest docs](https://jestjs.io/docs/getting-started#using-babel)
- [StackOverflow answer](https://stackoverflow.com/a/64223627/10117759)
