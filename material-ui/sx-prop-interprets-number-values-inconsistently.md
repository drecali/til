# `sx` prop interprets `number` values inconsistently

Starting with MUI v5, the `sx` prop has [different behavior](https://mui.com/system/the-sx-prop/#sizing) for `sizing` vs `spacing` CSS properties. This behavior is only inconsistent if the CSS properties have a `number` value. An MUI v5+ user must know this behavior and keep it in mind all the time. Or just use values that are a pixel string (`'number px'`). If every member on the team isn't constantly aware of this MUI v5 quirk, it can easily cause errors as shown below. IMO, this is a poor DX.

| Property | `value <= 1` | `value > 1` |
|--|--|--|
| Sizing (`width`, `height`, `minHeight`, `maxHeight`, `minWidth` and `maxWidth`) |  `(value * 100) + '%'` | `value + 'px'` |
| Spacing (`margin`, `padding`) | `theme.spacing(value)` | `theme.spacing(value)` |

Note: `theme.spacing`'s default logic is `(value * 8) + 'px'`. `8px` is the default but can be changed.

<img width="784" alt="image" src="https://user-images.githubusercontent.com/24983797/162678413-70309574-aa58-4c51-9bc3-dea721e5f909.png">

Source: [MUI Docs](https://mui.com/system/the-sx-prop/#sizing)

Here is a real world example. Imagine a team has been using MUI v4 for a long time with a large codebase. They've mostly enjoyed using it and haven't had any large problems. After an MUI v5 migration, they read about the possibilities of the `sx` prop and are eager to start using it. The app is quite large so there aren't visual tests to detect a bug this strange. Who would imagine that MUI's default behavior could be so counter-intuitive?

In this example, when the drawer/sidebar is open, it should occupy the first 240px on the left side of the screen. When it's closed, it should disappear by starting at -240px and ending at 0px. The rest of the app should size appropriately to fill the remaining space. Material UI decided that the same input to 2 different CSS properties in the `sx` prop should behave totally differently. Well done, MUI! Thankfully it was an easy fix, but it could have easily prevented if the default behavior was consistent and predictable.

```ts
const DRAWER_WIDTH = 240 //' 'number data type
    <MuiDrawer
      sx={{
        // correct
        width: DRAWER_WIDTH, // 240px
        flexShrink: 0,
        ...(open ? {} : {
            
          // ❌ bug
          marginLeft: -DRAWER_WIDTH, // -1920px (-240*8px) 🤬 MUI

          // ✅ Correct!
          // marginLeft: `-${DRAWER_WIDTH}px`,  // -240px
        }),
      }}
    />
```

## TL;DR

Never use `number` values for any styling with MUI. Always use `pixel strings`. Yes, that makes syntax highlighting less appealing and semantically it makes sense for `px` values to be considered `numbers`, but MUI v5+ `sx` prop's behavior is confusing enough to cause bugs for casual users. Using `pixel strings` avoids all possibilities of `sx` prop bugs unless MUI decides to change its behavior again somehow 🤣
