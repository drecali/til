# Search + RegEx = SuperSearch 🚀

VS Code's search feature is useful, but it's even more powerful when combined with RegEx. I'm a big fan of RegEx and wrote a bit about dev-friendly ways to prototype RegEx online [here](../javascript/regex-is-awesome-online-regex-playgrounds-cheatsheets.md).

RegEx is especially useful when refactoring a certain pattern in a large codebase because there will be lots of occurrences of it and you want to focus only the ones that need refactoring.

Use the VS Code Search option with RegEx to search more precisely.

1. Open the Search panel. The keyboard shortcut is <kbd>⌘</kbd> + <kbd>Shift</kbd> + <kbd>F</kbd>.
2. To enable the RegEx option press the <kbd>.\*</kbd> button.

<img width="361" alt="image" src="https://user-images.githubusercontent.com/24983797/179531487-7c926f8b-d1a3-4e25-aaa2-77983422fe40.png">

## Real world example

When using Redux it's best to access state with [Selectors](https://redux.js.org/usage/deriving-data-selectors) and the [`useSelector`](https://react-redux.js.org/api/hooks#useselector) hook whenever possible. My team's preference is to assign the selector's value to a variable near the top of the React functional component, then use that variable as needed.

We followed that code since we joined the team but in the legacy code there were some different Redux selector patterns. There were some instances where this wasn't done. Here are some examples. These changes may seem small, but they improve readability by abstracting away implementation details.

```jsx
// ❌ DON'T
<Component data-ms={useSelector(timeSpentSelector)} />;

// ✅ DO
const time = useSelector(timeSpentSelector);
//...
<Component data-ms={time} />;
```

```jsx
// ❌ DON'T
const backdropAlpha = (100 - useSelector(getBackdropBrightnessSelector)) / 100;

// ✅ DO
const backdropBrightness = useSelector(getBackdropBrightnessSelector);
//...
const backdropAlpha = (100 - backdropBrightness) / 100;
```

We also prefer creating a selector instead of accessing Redux `RootState` directly. It's a small investment to make a dedicated selector, but the reward is better readability in the files that use it.

```jsx
// ❌ DON'T
const isSidebarOpen = useSelector((state: RootState) => state.ui.sidebarOpen);

// ✅ DO (create the isSidebarOpenSelector in the proper file, then import it here)
const isSidebarOpen = useSelector(isSidebarOpenSelector);
```

## 🥇 Real world solution

There were a **lot** of matches for `useSelector`. Even `/useSelector\(` had a ton of matches.

![image](https://user-images.githubusercontent.com/24983797/179450027-3629b77e-6881-4302-86c0-94050969930f.png)

I specifically wanted to find `useSelector(` if it doesn't follow a normal assignment pattern which includes an `=` sign and an empty space.

This RegEx does exactly that 🎉

```js
/(?<!=\s)useSelector\(/;
```

![image](https://user-images.githubusercontent.com/24983797/179458247-15b4f6ed-fdf2-482d-b590-e27511b42732.png)
