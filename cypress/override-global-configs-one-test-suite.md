# Override global configs for one test/suite

Cypress is very flexible and there are many ways to configure its behavior. It's a best practice to set [global configs](https://docs.cypress.io/guides/references/configuration#Configuration-File) in the `cypress.config.js|ts` file.

Sometimes one test or suite needs a slightly different config. Cypress calls this [Test-specific Configuration](https://docs.cypress.io/guides/references/configuration#Test-specific-Configuration).

Cypress tests can start with any of these interfaces:

> The test interface, borrowed from Mocha, provides `describe()`, `context()`, `it()` and `specify()`.
>
> `context()` is identical to `describe()` and `specify()` is identical to `it()`, so choose whatever terminology works best for you.  
> [`Source: Cypres Docs`](https://docs.cypress.io/guides/core-concepts/writing-and-organizing-tests#Test-Structure)

They all take the same arguments:

```js
it(testName, { optionalTestConfig }, anonFunctionWithTestLogic);

describe(testName, { optionalTestConfig }, anonFunctionWithTestLogic);

context(testName, { optionalTestConfig }, anonFunctionWithTestLogic);

specify(testName, { optionalTestConfig }, anonFunctionWithTestLogic);
```

Most tests typically omit the `optionalTestConfig` object if they're OK with the global config. Overriding a global config is as easy as passing in a config object as the middle argument.

## Ideas

Granular control of Cypress configs can be really useful. You can record video of only certain tests of interest, or vary the video compression for different suites. You can also modify timeouts, retires, or change `env` variables. It's very powerful! The [docs](https://docs.cypress.io/guides/references/configuration#Options) for Cypress configs are really long and detailed, so check them out!

## Real world application

For actionable commands such as `click`, Cypress automatically scrolls to the target element even if it's already in view.

> By default, the scrolling algorithm works by scrolling the top, leftmost point of the element we issued the command on to the top, leftmost scrollable point of its scrollable container. [(`Source: Cypress Docs`)](https://docs.cypress.io/guides/core-concepts/interacting-with-elements#Scrolling)

This is not always desirable since it can mask unintended UI changes that push elements off the page.

If you're sure that all your UI elements should always be visible and no scrolling is needed, it makes sense to add `scrollBehavior: false` to Cypress' global configs.

If you're testing a long dropdown list and want to click an item near the bottom of the list, scrolling may be required. If the global config disabled all scrolling, you need to add custom `scrollBehavior` to the config for that specific test, group of tests, or suite that need it. Many commands also take an `options` objects that can include `config` type values. In this case, the `options` argument for the [`click` command](https://docs.cypress.io/api/commands/click#Arguments) accepts `scrollBehavior` as a key.

Another possible solution to this situation is to add the `{force}` option to the `click` command, but `{force}` feels like the nuclear approach because it has a lot more effects as listed below. I prefer to override the `scrollBehavior` config because it's more obvious.

> When you force an event to happen we will:
>
> - Continue to perform all default actions
> - Forcibly fire the event at the element
>
> We will NOT perform these:
>
> - Scroll the element into view
> - Ensure it is visible
> - Ensure it is not disabled
> - Ensure it is not detached
> - Ensure it is not readonly
> - Ensure it is not animating
> - Ensure it is not covered
> - Fire the event at a descendent
>
> [`(Source: Cypress Docs)`](https://docs.cypress.io/guides/core-concepts/interacting-with-elements#Forcing)
