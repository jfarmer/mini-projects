# Fibonacci (Low-level)

Node supports modules written in C using the [N-API](https://nodejs.org/api/n-api.html).  Let's write our first N-API module and compare its performance agaist equivalent code written in JavaScript.

We'll do this by implementing a function to calculate the [Fibonacci numbers](https://en.wikipedia.org/wiki/Fibonacci_number).

Here's the plan of attack:

1. If you've never written a C program before, start by writing and compiling a C program that calculates the Fibonacci function.
1. Read this tutorial: *[N-API and getting started with writing C addons for Node.js](https://hackernoon.com/n-api-and-getting-started-with-writing-c-addons-for-node-js-cf061b3eae75)
1. Write a Fibonacci implementation in C and in JavaScript
1. Verify you can access your C implementation in Node
1. Use [Benchmark.js](https://benchmarkjs.com/) to compare the two implementations

The emphasis of this project is to write your first C-based Node module, not play around with different Fibonacci implementations.  Here's a straightforward implementation in JavaScript that can be used for as baseline comparison:

```javascript
function fibonacci(n) {
  let a = 0, b = 1;

  if (n === 0) {
    return a;
  }

  for (let i = 2; i <= n; i++) {
    let temp = a + b;
    a = b;
    b = temp;
  }

  return b;
}
```
