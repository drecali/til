# Stop test suite on API error

When doing end-to-end tests with Cypress, the reason for a test failure is important. An informative failure is much quicker to debug.

While running a test suite with Cypress, it's common for multiple tests to use the same API. If there is an issue with this API, it can cause multiple tests to fail. If you're not checking for the API response, these test failures can seem unrelated to the API, making it hard to debug. Some test suites can be quite long, so if they're running in CI, you need to wait for all of them to run, fail, retry (if applicable) before artifacts are uploaded to help diagnose the issue.

## User Story

- A Cypress test suite should stop if there is an AI outage (signified by an HTTP error code).
- The failing test should give useful information to help debugging. Most importantly:
  - API endpoint
  - HTTP status code

## Solution

This code will detect intercept all API calls of interest and fail if any of their HTTP response codes are 400+. If an endpoint changes, it can lead to a 404 error. More sever server errors can lead to 500-level errors. With this code, troubleshooting is simplified and the frontend developer can know they (likely) didn't cause the error.

Since this solution uses Cypress commands, it can easily be reused in multiple test suites.

This solution is not foolproof since misconfigured `.env` variables could also trigger a failure. Still, the developer gets feedback much quicker than otherwise.

**Note**: This code uses an undocumented Cypress feature. Adding `.all` to an intercept alias returns an array of **all** calls to that alias. Source: GitHub issue [comment](https://github.com/cypress-io/cypress/issues/477#:~:text=There%20actually%20is%20an%20undocumented%20way%20to%20check%20the%20number%20of%20times%20an%20XHR%20was%20responsed%20to%20using%20.all%20on%20the%20alias.).

> There actually is an undocumented way to check the number of times an XHR was responsed to using .all on the alias.

In `cypress/support/commands.ts`

```js
// Intercepts all requests made to your API
Cypress.Commands.add("trackMyApiRequests", () => {
  cy.intercept(`${Cypress.env("API_URL")}/**`).as("myApi");
});

// test fails if any intercepted API call has an error code > 399
Cypress.Commands.add("stopTestSuiteIfApiError", () => {
  cy.get("@myApi.all").each((req) => {
    const cutoff = 399;
    const status = req?.response?.statusCode;
    if (status && status > cutoff) {
      expect(req)
        .to.have.nested.property("response.statusCode")
        .below(
          cutoff,
          `URL:${req.request.url}\nMETHOD:${req.request.method}\nAPI ERROR CODE`
        );
    }
  });
});
```

In your test spec file, add `trackMyApiRequests` to the `beforeEach()` hook, and `stopTestSuiteIfApiError` to the `afterEach()` hook.

```js
describe("Test spec", () => {
  beforeEach(() => {
    cy.trackMyApiRequests(); // add here
  });

  afterEach(() => {
    cy.stopTestSuiteIfApiError(); // add here
  });

  it("some test", () => {
    //Cypress test code
  });
});
```

Failing test in the test runner:
![image](https://github.com/drecali/til/blob/main/cypress/tests-runner.png)

Failing test in headless mode (CI):
![image](https://github.com/drecali/til/blob/main/cypress/tests-ci.png)
