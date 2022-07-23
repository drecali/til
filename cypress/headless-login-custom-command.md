# Headless login custom command

End-to-end tests tend to take longer than any other type of test, because they have to wait for the UI to load. That's why Cypress says:

> When you're writing tests for a very specific feature, you should use your UI to test it.
>
> But when you're testing another area of the system that relies on a state from a previous feature: **do not use your UI to set up this state**. ([Cypress docs](https://docs.cypress.io/guides/end-to-end-testing/testing-your-app#Bypassing-your-UI))

Here's a [custom command](https://docs.cypress.io/api/cypress-api/custom-commands) to log in quickly with a direct request to the API, then store the `access_token` as a cookie. It's using [Typescript](https://docs.cypress.io/guides/tooling/typescript-support#Types-for-Custom-Commands), but the TS parts can be omitted if just working with JS. The default user credentials are Cypress `env` variables, but custom credentials can be passed in too. It makes sure the `access_token` is preserved across multiple tests. By default, Cypress doesn't save it between tests.

## Setup

```ts
// in cypress/support/commands.ts

interface Login {
  email: string;
  password: string;
}

// type definition
declare global {
  namespace Cypress {
    interface Chainable {
      headlessLogin({ email, password }?: Login): void;
    }
  }
}

//...
Cypress.Commands.add("headlessLogin", (login?: Login) => {
  cy.request("POST", `${Cypress.env("API_URL")}/auth/login/`, {
    id: login?.email ?? Cypress.env("email"),
    password: login?.password ?? Cypress.env("password"),
  }).then((response) => {
    cy.setCookie("TOKEN", response.body.access_token, {
      sameSite: "strict",
    });
    Cypress.Cookies.defaults({
      preserve: "TOKEN",
    });
  });
});
```

## Use cases

The basic use case with the default user credentials:

```ts
cy.headlessLogin();
```

With custom credentials:

```ts
cy.headlessLogin({
  email: "user@email.com",
  password: "testpw",
});
```

It's useful to put call this command in the `before()` hook so it will log in before all tests in the suite are run.

```ts
describe("Demo Page", () => {
  before(() => {
    cy.headlessLogin();
  });
});
```
