## My vision of Symvy

A cursed mix of Haskell, K, Lisp and symbolic algebra

## Functions

Symvy's basic premise is that everything is a function. `4` is a function that takes some arguments, ignores them, and returns `4`. `x+y` is a function that takes two arguments and returns the first, plus the second. `+` also works in this case.

Function arguments are curried - that is, a function can only take a single argument at a time.

Functions expressions themselves are written in two different ways. They can be written like `({args}code)`, which is an anonymous function. If no args are given or the function is not top-level, it is assumed to be niladic, and take its arguments from a higher scope. If values within a function are not defined in their scope they are assumed to be function arguments.
. The args section is optional - the three default arguments to a function are `x`, `y` and `z`. The `()` surrounding are often unnecessary - `()` are assumed where parsing ambiguity isn't caused. You can even have pure functions like just `+`.

This means that normal expressions like `3(2x+1)` work as normal.

Furthermore, you can have partial functions like `1+`, which assume the remaining argument as `x`.

You can call functions with the `@` operator, although it is sometimes unnecessary. 

You can (at the top level only) bind functions to names with the `=` operator - for example:

```
inc=1+

inc@1
```

Parentheses are used to group expressions.

## Identifiers

Any sequence of lowercase letters is an identifier. This can be a variable name, or an argument, or pretty much anything.

As mentioned before, `x`, `y` and `z` are special variables inside a function, referencing certain arguments, and `o` references the current function.

## Lists

Lists, although not part of the symbolic algebra section, are part of Symvy's Turing-completeness. They are written like `[1,2,3]` and can be nested.

Symvy's lists are lazy linked lists. There are three basic list operations:

- `C` which prepends its left argument to its right
- `H` which gets the first item of a list
- `T` which gets all but the first item of a list 


## Operators

In a sense, all operators take functions as arguments. `+`, for example, takes two functions and returns a new function which calls those two functions and adds their results.

However, the output function's arity depends on the arity of the inputted functions. 
If I define `f` as `3*` and `g` as `2+`, then `f+g` would be a function that called `f`, called `g`, and added them together, quadrupling its argument and adding `2`. However, if I instead go `(3*x)+(2+x)` this would remain a niladic function and take its arguments from the nearest scope.

If I define `f` as `(x+2)` and `g` as `(x*y)`, where some of the functions have an arity greater than 1, the maximal arity is the arity of the result, and `f+g` would produce a dyadic function that takes `x` and `y` and returns `x+2+x*y`.


### Operator definition?
- Maybe (might be hard to implement) you can wrap an operator in backticks to turn it into a pure function, and you can define an operator with similar syntax?

## Purity

Variables are constant and can only be defined at the global scope, and not redefined.
