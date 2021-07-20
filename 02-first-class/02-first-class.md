# Chapter 2: First-class citizenship
Apart from [purity](../01-purity/01-purity.md), which as we saw can be optional,
another important aspect of functional programming is the fact that functions
are _first-class citizens_.

A first-class citizen is a citizen that enjoys all the benefits of a society,
without being discriminated or treated differently or poorly. In programming
terms, the meaning is that a function is treated the same as any other type of
data, such as a string or a number, and can be used in the same ways, such as
being assigned to a variable, being used as a function argument, or being
returned by another function.

This haskell function called `incrementer` returns a function that accepts
one numerical value _n_ as its input argument, and returns _n_ + 1.
`decrementer` returns a function that subtracts 1 instead.
```haskell
let incrementer = \n -> n + 1
let decrementer = \n -> n - 1
```
Maybe we have a function that can return a `Result` that can be either `Success`
or `Failure`, and we need to modify a counter depending on the result.
Here's one way we could do it.

```haskell
type Result = Success | Failure

countAction :: Result -> (Int -> Int)
countAction Success = incrementer
countAction Failure = decrementer

handle :: SomeInput -> Int -> Int
handle input counter =
    let result = (doSomething input) in
        count counter
    where
        count = (countAction result)
```
A few things happens here:
* `countAction` returns a function.
* A function is bound to the `count` variable
* The function contained in `count` is invoked with the `counter` argument.

## Next chapter
[Chapter 03: Control flow abstraction](../03-control-flow-abstraction/03-control-flow-abstraction.md)
