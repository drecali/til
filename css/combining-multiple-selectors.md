# Combining multiple selectors

What is the difference between these 2 selectors? They're very subtly different, but their effects are not.

```css
#header .callout {
  /* Select .callout elements if they are CHILDREN of #header */
}
#header.callout {
  /* Select elements with BOTH both those selectors */
}
```

## With a space (`#A .B`)

The `space` between selectors signifies a `parent > child` relationship. `B` MUST be the child of `A`.

```swift
// #header .callout
element.PARENT.id === "header" && element.class === "callout"
// Select all elements with the class name callout that are decendents of the element with an ID of header.
```

## Concatenated (`#A.B`)

All concatenated selectors MUST match. `B` MUST be the child of `A`.

```swift
// #header.callout
element.id === "header" && element.class === "callout"
//Select the element which has an ID of header and also a class name of callout.
```

![image](https://user-images.githubusercontent.com/24983797/174083930-0c5c5450-ba09-4384-b34a-531ddd6226dd.png)

## Going overboard

You can combine multiple `class` and `id` selectors. The snippets below are valid, but they're not nice to look at.

> We aren’t limited to only two here, we can combine as many classes and IDs into a single selector as we want.
>
> Although bear in mind that’s getting a little ridiculous =)

```css
.snippet#header.code.red {
  color: red;
}
```

And here's the longest combined selector I've felt the need to use, at least as a proof of concept before refactoring. I'm sorry you had to see this. It's pretty cool that you can combine pseudo-classes too though!

PS. I blame a very ambitious and customized design system that needs to be coded and documented in Storybook 🤷‍♂️.

```css
.storybook-scroll--large:hover.storybook-scroll--horizontal:hover.storybook-scroll--hidden-true:hover {
}
```

## Credits

- CSS Tricks [article](https://css-tricks.com/multiple-class-id-selectors/).
