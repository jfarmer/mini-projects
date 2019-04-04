# Complex Numbers

The [complex numbers](https://en.wikipedia.org/wiki/Complex_number) play an important role in mathematics, physics, and engineering.  The math behind anything involving waves or periodic functions uses complex numbers.

For example, the algorithms involved in creating MP3s from raw audio use complex numbers.  The entire mathematical basis of quantum mechanics requires complex numbers, so in some ways complex numbers do a better job representing reality than real numbers do!

If you remember, complex numbers are numbers of the form

```
a + bi
```

where `a` and `b` are real numbers and `i` is a special number that satisfies the following property:

```
i**2 = i*i = -1
```

## Complex Number Type

In the same way that a rational number `p/q` can be thought of as a pair of integers `(p, q)` with special rules for addition and multiplication, a complex number `a + bi` can be thought of as a pair of real numbers `(a, b)` with special rules for addition and multiplication.

Create a `Complex` type or class that works as follows:

```javascript
x = new Complex(a, b);
y = new Complex(c, d);

x.add(y);
x.mul(y);
x.sub(y);
x.div(y);
x.eq(y);
```

## Further Iterations

If you have time and this interests you, extend your complex number type with other operations like exponentials and square roots.
