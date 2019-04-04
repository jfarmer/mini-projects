# Symbolic Calculator

Most calculators are "numerical calculators" — you type in some numbers and operations like addition/subtraction/etc., hit enter, and the calculator spits out the result.  A _symbolic_ calculator is able to evaluate not just numerical expressions but also algebraic expressions.  For example, a symbolic calculator might let a user do following:

```text
calc> (x * 1) + 0
 => x
calc> x * 0
 => 0
calc> 5 + (x * 0)
 => 5
calc> x * 3 * 4
 => x * 12
calc> (x + x) - x
 => x
calc> ((x / 2) + (y / 2)) * 2
 => x + y
```

If you have ever used them, the [TI-89](http://en.wikipedia.org/wiki/TI-89_series) or [TI-92](http://en.wikipedia.org/wiki/TI-92_series) calculators by Texas Instruments were capable of doing this.

We will implement a calculator that can do this, too. Because it's easier to parse, we'll be using [reverse Polish notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation) for our expressions instead of [infix notation](http://en.wikipedia.org/wiki/Infix_notation).

## Symbolic Expressions

With a basic numerical calculator, our expressions look like

```
5 4 + 7 *
```

which corresponds to `(5 + 4) * 7` in our usual infix notation.  There are only two types of tokens: numbers and operators.  In a symbolic calculator, we add a _third_ type of token: variables.  Our expressions can now look like

```text
5 x + 7 *
```

There are two things we might want to do with expressions like this:

1. Simplify them so that, e.g., `x 0 +` becomes just `x`
2. Replace variables with specific values

## Iterations

### [v1.0] Variable Binding

For v1.0, we will build a version that allows us to bind values to variables.  When we try to evaluate an expression that references undefined variables, we should raise an error.  The `Expression#evaluate` method is where the bulk of the work happens.

It should behave like this

```javascript
expr = new Expression('x 5 +');
expr.evaluate({ x: 10 }); // => 15

expr = Expression('x y *');
expr.evaluate({ x: 10, y: 2 }); // => 20

expr = new Expression('7 2 + 2 *')
expr.evaluate() // => 18

expr = new Expression('x z +')
expr.evaluate({ x: 5 }) // => UndefinedVariableError
```

### [v2.0] Simplification

Even if we don't know the _particular_ value of a variable we can still say many things about an expression containing that variable.  For example, the expressions

```text
x 0 *
0 x *
```

will be `0` no matter what the value of `x` is.  That means we can replace any expression that looks like either of these with `0`.

In this version, we'll no longer need to raise an error when we have an expression containing an undefined variable. This is called "simplification" and the process involves encoding these rules in our program and applying them as we evaluate an expression.

It will probably make most sense for the `Expression#valuate` in this version to _always_ return an `Expression`, although it might be a single, numerical expression like `Expression.new(0)`.  It makes it difficult to reason about the behavior of `evaluate` if it returns a number sometimes and an `Expression` other times.

## Binary Expression Trees

When you get to implementing simplification, consider constructing a [binary expression tree](http://en.wikipedia.org/wiki/Binary_expression_tree).  Briefly, a binary expression tree is a way of organizing basic algebraic expressions.  An expression like this

```text
x 5 + 0 *
```

would be represented as a binary expression tree as

```text
    *
   / \
  +   0
 / \
x   5
```

Seeing the "tree" structure of an algebraic expression makes it easier to express the simplification rules for `evaluate`.  The internal nodes of a binary expression tree are all operators and the leaves are all either variables or numbers.

Consider the tree-centric expression of `evaluate`, below:

```text
<number>   :: 0-9
<variable> :: a-z
<operator> :: + | *
<expr>     :: <number> | <variable> | <expr> <expr> <operator>

evaluate(<number>)   = <number>
evaluate(<variable>) = <variable>

# Here, "e" is any arbitrary expression and
# "n1" and "n2" are arbitrary numbers.

         (   +   )
evaluate (  / \  ) = n1 + n2
         ( n1 n2 )

         (   *   )
evaluate (  / \  ) = n1 * n2
         ( n1 n2 )

         (   +   )
evaluate (  / \  ) = evaluate(e)
         ( e   0 )

         (   +   )
evaluate (  / \  ) = evaluate(e)
         ( 0   e )

         (   *   )
evaluate (  / \  ) = 0
         ( e   0 )

         (   *   )
evaluate (  / \  ) = 0
         ( 0   e )

         (   *   )
evaluate (  / \  ) = evaluate(e)
         ( e   1 )

         (   *   )
evaluate (  / \  ) = evaluate(e)
         ( 1   e )
```

Thus, "simplification" boils down to replacing certain expressions in the binary expression tree with ever-smaller expressions, until we've done all the replacing we can.  If every variable has an associated value, we will wind up with a single-node tree consisting of one number.  If some variables don't have associated values, we can still "partially" evaluate the expression by simplifying it.
