# Higher-Order Functions

Functions like `map` and `reduce` are called [higher-order functions](https://en.wikipedia.org/wiki/Higher-order_function).  Let's implement our own versions of some common higher-order functions so that we can get more comfortable with them.

This means *do not use the built-in functions of the same name*!

## Iterations

Let's call our library `_`, which is commonly used for libraries that implement higher-order functions (see [Underscore.js](https://underscorejs.org/) and [Lodash](https://lodash.com/)).

Here's a pre-built `each` function.  Every other function should be implemented in terms of this.

```javascript
const _ = {
  each(iterable, callback) {
    for (let item of iterable) {
      callback(item);
    }
  }
}

_.each([1,2,3], (item) => {
  console.log(`Item is '${item}'.`);
})
```

### v0.1 - `reduce` and `map`

Add `reduce` and `map` to the `_` object.  While it might not be obvious at first, almost every commonly-used higher-order function can be written as a call to `reduce`.

See the following for how `reduce` and `map` behave:

#### Reduce / Fold
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce
- https://en.wikipedia.org/wiki/Fold_(higher-order_function)

#### Map
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
- https://en.wikipedia.org/wiki/Map_(higher-order_function)


### v0.2 - `filter`

Add `filter`, which takes a list and a callback, returning a list of all elements for which the callback returns true.

For example:

```javascript
_.filter([1, 2, 3, 4, 5, 6], (num) => num % 2 === 0);               // returns [2, 4, 6]
_.filter([1, 2, 3, 4, 5, 6], (num) => num > 3);                     // returns [4, 5, 6]
_.filter(['one', 'two', 'three', 'four'], (str) => str.length > 3); // returns ['three', 'four']
```

### Other Methods

- `_.max(list)` - Returns the largest element in `list`
- `_.min(list)` - Returns the smallest element in `list`
- `_.maxBy(list, fn)` - Returns the `item` in `list` where `fn(item)` is largest
- `_.minBy(list, fn)` - Returns the `item` in `list` where `fn(item)` is smallest
- `_.reject(list, fn)` — The opposite of `filter`, returns collection of `item`s in `list` where `fn(item)` returns `false`.
- `_.all(list, fn)` — Returns `true` if `fn(item)` returns `true` for every `item` in `list`
- `_.any(list, fn)` — Returns `true` if `fn(item)` returns `true` for any `item` in `list`
- `_.sortBy(list, fn)` - Returns a copy of `list` sorted by applying `fn` to each item in list.  For example, = - `_.sortBy(strings, (str) => str.length)` would return a copy of `strings` sorted by string length.
