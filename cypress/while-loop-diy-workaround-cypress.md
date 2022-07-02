# `while` loop DIY workaround in Cypress

## Simplified Dev Story

- While running end-to-end tests in Cypress, I want to perform an action a varying number of times `until` a certain condition is met.
- Unfortunately, I can't use a `while` loop because Cypress runs its commands asynchronously so loops don't behave as expected.

## Simplified Solution

To perform an action while as many times as necessary `until` a condition is met, most devs would use normally use a `while` loop. Unfortunately, [loops don't work in Cypress](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#Avoid-loops). Still, here's a pseudocode version of this idea:

```js
while (!condition) {
  perform(actionsToRepeat);
}
// This runs only if the condition is met.
perform(finalAction);
```

Here's the convoluted Cypress solution I that worked for me. It required recursion.

```js
const recursiveFunction = () => {
  cy.get("relevantElementsForCondition") //
    .then((relevantElementsArg) => {
      // stop condition
      if (conditionIsMet(relevantElementsArg)) return;
      // run until stop condition (select next month in dropdown)
      cy.actionsToRepeat();
      /*
       */

      /**
       * I know it't best to avoid adding explicit waits, but
       * it seems like it's required here. Even the Cypress
       * docs include an explicit wait. In my case, 100ms
       * worked, but the Cypress documentation included 500ms 🤷‍♂️
       */
      cy.wait(100);
      recursiveFunction();
    });
};
recursiveFunction();

cy.finalAction();
```

## A real user story

Here is an actual use case. There's a `Dropdown` with month names and a table that lists data for the selected month. We're doing visual testing, so we want to capture a screenshot of the table with data rows, to make sure they are rendered correctly.

`<Dropdown with month names (default = current month)>`

| Heading (always visible)      | Heading (always visible) |
| ----------------------------- | ------------------------ |
| Data rows (min = 0, max = 10) |                          |
| Summary row (always visible)  |                          |

- The `Dropdown`'s selects the current month by default.
- The table has 2 rows that are always present (`Heading` at the top and `Summary` at the bottom). The data rows are loaded for the selected month. If the current month has no data, no data rows are loaded. If there are `n` rows of data, they are all loaded.
- Some months may not have any data so the table will have just 2 rows: the `Heading` and `Summary`. It's not possible to know how many data-less months there are, but we need to capture a table with data rows.

## A real world solution

We need to use the `Dropdown` to change the selected month until we reach a month with `n > 0` rows of data, so the table can have `rows > 2`.

```js
const selectFirstMonthWithDataRows = () => {
  cy.get("tr") // table rows
    .as("expect table rows > 2") // this is optional but labels the command in the Cypress test runner.
    .then((tableRows) => {
      // stop condition
      if (tableRows.length > 2) {
        // optional but nice to see in the Cypress runner.
        cy.log(" 👍 Selected month has data rows");
        return;
      }
      // run until stop condition (select next month in dropdown)
      cy.get("#dropdown").click();
      // find the selected month in the dropdown and click the next sibling (next month)
      cy.get("li[aria-selected=true]").next().click();
      cy.wait(100);
      selectFirstMonthWithDataRows();
    });
};
selectFirstMonthWithDataRows();

cy.takeCustomScreenshots("Table with data rows FTW! 🎉");
```

# Resources

The [Cypress](https://cypress.io) docs are seriously awesome! They [explained](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#Avoid-loops) clearly why loops don't work as expected and showed DOs and DONTs when dealing with these unique situations.
