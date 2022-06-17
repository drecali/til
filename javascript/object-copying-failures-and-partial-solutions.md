# Object copying failures and partial solutions

JavaScript can do a lot! It's the language of the internet and also pays my bills. Still, there are some surprising frustrations about JavaScript. Some of them seem unbelievable. One of these is `deep-copying` Objects. 🤦‍♂️

## tl;dr

JavaScript does not support `deep-copying` Objects. ES6 introduced some useful ways to do `shallow-copying`, like `Object.assign` and the `spread operator`, but it's important to remember these _DO NOT_ `deep-copy`. Nested objects remain a reference to the original object.

## DON'T do this

```js
const obj = {a: 0} // obj.a = 0} 🙂
const clone = obj  // obj.a = 0} 🙂     clone.a = 0} 🙂
obj.a++            // obj.a = 1} 🤬     clone.a = 1} 🤬
clone.a = 5        // obj.a = 5} 🤬     clone.a = 5} 🤬
```

The complete technical explanation can get complex, but the `tl;dr` is that `clone` is linked to `obj`. It's not a proper clone. It's a reference to the original. Changing properties for one of them will change the same property for the other. 🤦‍♂️

## 🤞 ES6 to the rescue?

Kind of. The `Object.assign` method and `spread operator` only do `shallow-copying`. I'll just show the `spread operator` because as far as I know, they work the same in this case.

```js
const obj = {a: 0}      // obj.a = 0 🙂
const clone = {...obj}  // obj.a = 0 🙂     clone.a = 0 🙂
obj.a++                 // obj.a = 1 🙂     clone.a = 0 🙂
clone.a = 5             // obj.a = 1 🙂     clone.a = 5 🙂
```

Great, right?

Unfortunately they don't work on `nested` objects. 🤦‍♂️

```js
const obj = {a: 0, b:{c: 0}}   // obj.b.c = 0 🙂
const clone = {...obj}         // obj.b.c = 0 🙂     clone.b.c = 0 🙂
obj.b.c++                      // obj.b.c = 1 🤬     clone.b.c = 1 🤬
clone.b.c = 5                  // obj.b.c = 5 🤬     clone.b.c = 5 🤬
```

The `nested` objects remain linked to the original object just like the first example. It's important to be aware of this when using the ES6 features mentioned.

## `JSON.stringify??`

Apparently `const clone = JSON.parse(JSON.stringify(obj))` works except for:

- `Dates`
- Functions
- `undefined`
- regExp
- `Infinity`

## Conclusion

It's a shame that JavaScript needs to rely on libraries, custom algorithms, or sketchy `JSON` workarounds. 😞

At least the ES6 goodies did improve the status quo a bit.

## Resources

- Long [StackOverflow](https://stackoverflow.com/questions/728360/how-do-i-correctly-clone-a-javascript-object?rq=1) page with an alarming number of answers suggesting the `JSON.stringify` method.
