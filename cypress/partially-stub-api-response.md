# Partially stub an API response

This is a way to modify parts of an API response.

```js
cy.fixture("fixturePath").then((fixture) => {
  cy.intercept(
    {
      method: "GET", // optional but it's good make your intercepts more specific
      pathname: "pathNameToIntercept", // ideally, make this as specific as possible too
    },
    (req) => {
      req.continue((res) => {
        // res.body is the normal response body but it's easy to replace parts of it or the entire thing
        res.body.propertyToStubWithYourFixture = fixture;
      });
    }
  );
});
```
