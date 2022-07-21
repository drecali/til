# Immutable objects or arrays with `as const`

When JavaScript introduced the word `const` declaration, it was an overdue and welcome change. Finally, variables could be designated as read-only, to prevent accidental mutations.

Unless those variables are `objects` or `arrays` because... reasons.

> The value of a constant can't be changed through reassignment (i.e. by using the assignment operator), and it can't be redeclared (i.e. through a variable declaration). However, if a constant is an `object` or `array` its properties or items can be updated or removed. 🤦 ([MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const))

This means `const` is quite the misnomer.

Luckily TypeScript heard our sighs and introduced the [`const assertion`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions) 😎

The `const assertion` turns **any** simple variable read-only.

```js
// JS lets you do this
const arr = ['foo', 'bar']
arr.push('foobar'); // ['foo', 'bar', 'foobar']

const obj = {foo: 'bar'}
obj.foo = 'foo' // {foo: 'foo'}
```
TypeScript is more civilized. Still, the syntax does look a bit odd and somewhat redundant at first. Seeing `const` at the beginning and end of the declaration seems a bit silly. It's worth it though!

```ts
const arr = ['foo', 'bar'] as const
arr.push('foobar'); // Property 'push' does not exist on type 'readonly ["foo", "bar"]'.

const obj = {foo: 'bar'} as const;
obj.foo = 'foo' // Cannot assign to 'foo' because it is a read-only property.
```

Yes, JavaScript has [`Object.freeze()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze), but TS' `const assertion` works better and prevents deep mutations as far as I can tell.

```js
let obj1 = {
  internal: {a: 'b'}
};

Object.freeze(obj1);
obj1.internal.a = 'aValue'; // internal: {a: 'aValue'}
```

```ts
let obj1 = {
  internal: {a: 'b'}
} as const;

obj1.internal.a = 'aValue'; // Cannot assign to 'a' because it is a read-only property.
```

Finally, `const` is no longer a misnomer 🎉