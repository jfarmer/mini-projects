# Rational Numbers

A rational number is any number that can be written as a ratio of two integers.


Examples of rational numbers:

- <sup>1</sup>&frasl;<sub>10</sub>
- <sup>4</sup>&frasl;<sub>3</sub>
- <sup>72</sup>&frasl;<sub>846</sub>

Computers support floating-point numbers, but the arithmetic isn't exact.  We're going to implement our own `Rational` class that supports exact arithmetic.

To see what we mean when we say floating-point arithmetic isn't exact, look at this:

```console
user@host $ node
> 0.1 + 0.2
0.30000000000000004
> 0.1 + 0.2 - 0.2
0.10000000000000003
> 0.2 - 0.2
0
> 0.1 + (0.2 - 0.2)
0.1
> (0.1 + 0.2) - 0.2
0.10000000000000003
>
```

This behavior is not a bug.  It's part of [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754), the official standard for how floating-point numbers work.

As you can see, floating-point arithmetic isn't even [associative](https://en.wikipedia.org/wiki/Associative_property).  That is,

```javascript
0.1 + (0.2 - 0.2) != (0.1 + 0.2) - 0.2
```

## Exact Arithmetic

In general, we'd write the set of all rational numbers as

````
{ p/q : p,q are integers }
```

How do we add, subtract, multiply, and divide rational numbers?

```
p/q + r/s = (p*s + r*q) / (q * s)
p/q * r/s = (p * r) / (q * s)
```

Note that the operations on the right-hand side deal only with integers.  The fact that we write "p/q" is purely notation — we're really dealing with two integers.  We could write rational numbers as `(p, q)` and then write addtional and multiplication as

```
(p, q) + (r, s) = (p*s + r*q, q*s)
(p, q) * (r, s) = (p*q, q*s)
```

Or, written as functions

```
add((p, q), (r, s)) = (p*s + r*q, q*s)
mul((p, q), (r, s)) = (p*q, q*s)
```

By implementing rational numbers this way, we don't lose any precision.

## The `Rational` Class

Implement a class called `Rational` that supports the following operations:

```javascript
x = new Rational(p, q);
y = new Rational(r, s);

x.add(y) // Addition
x.mul(y) // Multiplication
x.sub(y) // Subtraction
x.div(y) // Division
x.eq(y)  // Equality
```

Equality is a little tricky because <sup>1</sup>&frasl;<sub>3</sub>,  <sup>2</sup>&frasl;<sub>6</sub>, and <sup>3</sup>&frasl;<sub>9</sub> represent the same rational number even though as pairs of numbers we would write them as `(1, 3)`, `(2, 6)`, and `(3, 9)`.

We can test whether two rational numbers are equal in the following way:

```
(p, q) == (r, s) if p*q == r*q
```

## Note on Language

Many languages have a bulit-in rational type or have one in the standard library.  The goal of this project is to implement your own, so don't use the built-in type if it exists!

Examples:

- Ruby — [Rational](https://ruby-doc.org/core-2.6.1/Rational.html)
- Python — [Fraction](https://docs.python.org/3.1/library/fractions.html)
- C++ — [std::ratio](https://en.cppreference.com/w/cpp/numeric/ratio/ratio)
- Haskell — [Rational](https://wiki.haskell.org/Rational)
