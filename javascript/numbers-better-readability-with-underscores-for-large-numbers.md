# `[Numbers]` - better readability with underscores for large numbers

The human eye is usually not so good at parsing long sequences of the same character.

❗️Quick! How many zeroes in this number? `20000000`

- [ ] 5 zeroes so `200,000`
- [ ] 6 zeroes so `2,000,000`
- [ ] 7 zeroes so `20,000,000`
- [ ] 8 zeroes so `200,000,000`

We're used to large numbers being formatted. In the West, this usually means commas (or periods) every 3 orders of magnitude. At least in the Korean counting system, they tend to separate numbers at 4 orders of magnitude, but larger numbers get a bit more complicated. Thankfully - in the interest of international compatibility - in everyday life, they still use the "international" formatting. But in speech and numbers written as words, they use the Korean way (of course).

❗️Quick! How many zeroes in this number? `20,000,000`

> Obviously 7. All our lives we've trained with this pattern and counting by 3 for low numbers. What if JavaScript could also format numbers but keep them as a `number` data type? It's trivial to format numbers as a `string`, but that would make it more annoying to use them as `numbers`.

That's why formatted numbers are so great. JavaScript uses the `underscore` character (`_`). It's called a [numeric separator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#numeric_separators)

```js
const lessReadable: 20000000
const moreReadable: 20_000_000
const koreanStylez: 2000_0000
const overkill: 2_0_0_0_0_0_0_0
```

Numeric separators can be used in different type of numbering systems.

```js
// separators in decimal numbers
1_000_000_000_000;
1_050.95;

// separators in binary numbers
0b1010_0001_1000_0101;

// separators in octal numbers
0o2_2_5_6;

// separators in hex numbers
0xa0_b0_c0;

// separators in BigInts
1_000_000_000_000_000_000_000n;
```

And there are some limitations:

```js
// More than one underscore in a row is not allowed
100__000; // SyntaxError

// Not allowed at the end of numeric literals
100_; // SyntaxError

// Can not be used after leading 0
0_1; // SyntaxError
```
