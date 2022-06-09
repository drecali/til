# Sort array of strings or object array alphabetically

The ES6 method `String.prototype.localeCompare()` is very easy to remember. There are some caveats compared to other methods of sorting arrays:

* It only works on `strings` (obviously).
* It can be slow with larger data sets.

Still, it can be very useful for debugging, prototyping, and light automation. Here is a typical use case:

```js
const arr = [
    {
        "name": "Alice",
        "otherKey": null
    },
    {
        "name": "Bob",
        "otherKey": []
    },
    {
        "name": "Cindy",
        "otherKey": true
    },
    {
        "name": "Jim",
        "otherKey": 1
    }
]

arr.sort((a,b) => a.name.localeCompare(b.name))

/*
[
    {
        "name": "Alice",
        "otherKey": null
    },
    {
        "name": "Bob",
        "otherKey": []
    },
    {
        "name": "Cindy",
        "otherKey": true
    },
    {
        "name": "Jim",
        "otherKey": 1
    }
]
*/

```

## Source

StackOverflow [answer](https://stackoverflow.com/a/45544166/10117759).
