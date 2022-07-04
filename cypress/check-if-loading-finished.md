# Check if loading is finished

If certain behaviors or assertions need to be used multiple times in multiple test spec files, it's best to turn it into a [Cypress command](https://docs.cypress.io/api/cypress-api/custom-commands).

> A great place to define or overwrite commands is in your `cypress/support/commands.js|ts` file, since it is loaded before any test files are evaluated via an import statement in the `supportFile`.

## User Story

Several of my tests in several spec files need to wait until loading is complete, which is indicated by the Material UI loading animations disappearing.

## Solution

In this case, I know that Material UI has 2 types of `loading` components and we use them both in our app: `MuiCircularProgress` and `MuiLinearProgress` ([MUI Docs](https://mui.com/material-ui/react-progress/)). These components are only mounted in the DOM while they are needed to indicate `loading` status. When `loading` has finished, they are unmounted from the DOM. This makes it easy to detect their presence with the built-in `.should()` command and the `exist` or `not.exist` assertions.

This command could be modified to fit your unique non-MUI loading situations.

To create the command:

```ts
// in cypress/support/commands.ts

Cypress.Commands.add("isLoadingFinished", (finished: boolean) => {
  cy.get(".MuiCircularProgress-root")
    .should(`${finished ? "not.exist" : "exist"}`)
    // This is optional but looks nice in the logs
    .as(`CircularLoading${finished ? "Finished" : "NotFinished"}`);

  cy.get(".MuiLinearProgress-root")
    .should(`${finished ? "not.exist" : "exist"}`)
    // This is optional but looks nice in the logs
    .as(`LinearLoading${finished ? "Finished" : "NotFinished"}`);
});
```

To use the command:

```js
// inside an actual test

cy.isLoadingFinished(true);
// other behavior that can only happen after loading is finished.
```

Since this command is needed in multiple spec files, it's much cleaner to write a custom command and easily use it where it's needed.
