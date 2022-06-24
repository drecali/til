# Combine conditions using array

ES7 brought an elegant way to check if at least one of multiple conditions are true. It's much cleaner in my opinion. 🤩

Both cases are functionally identical. They'd work with `number` data types as well.

❗️ There might be a performance cost with large arrays, especially if `myVar` is not in the array. This doesn't seem relevant to most uses cases of this pattern, but it's still worth noting.

## Code

```js
// 🙂 The old way
if (myVar === "A" || myVar === "B" || myVar === "C") {
}

// 🤩 The new way
if (["A", "B", "C"].includes(myVar)) {
}
```

# Resources

- MDN docs for [`Array.prototype.includes()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
- Another [example](https://dev.to/gabrielrufino/more-readable-conditional-with-array-includes-2m3j) on dev.to
