# Chapter 1: Intro
This chapter introduces some very basic Haskell syntax, just to make it easier
to understand the rest of the course. Don't worry -- this is just so that we
have a language to express some ideas in. Most likely you can skip this intro
chapter and still understand what's going on, and just go back here to check if
there's something you do not understand.

## Constants
A constant in Haskell can be defined like this:
```haskell
pi = 3.14159
```
## Functions
A function in Haskell is declared almost exactly like a constant:
```haskell
double x = x * 2
```
The function `double` takes one argument, and multiplies it by two. There is no
`return` statement or anything like that. Whatever is evaluated to the right of
the equal sign is returned - the same for both functions and constants.

## Types
Haskell is strongly typed, and the types are inferred, meaning that you almost
never need to declare the types. Haskell will figure them out. But, it's still
possible to declare them so that they become easier for humans to read.

Types start with a capital letter, like this: `Integer`.
### Constant type spec
 To declare that a constant has a specific type, this syntax is used:
```haskell
pi :: Float
pi = 3.14159

greeting :: String
greeting = "Hello!"
```
### Function type spec
Functions use a `->` syntax to indicate that a value is returned. Otherwise,
they look identical to constants.
```haskell
double :: Integer -> Integer
double x = x * 2
```
If there are several input values, they are chained with more `->`s.
```haskell
add3 :: Integer -> Integer -> Integer -> Integer
add3 x y z = x + y + z
```
The first three `Integer` are the input values `x`, `y` and `z`, and the
last one represents the return value.
### Type variables
Sometimes a function can work with any type. In that case, _type variables_ are
used. They are normally named `a`, `b`, and so on, in lower-case. A function
with this type spec:
```haskell
a -> b -> a
```
would take two arguments of any type, and return a value of the same type as the
first argument.

## GHCi
GHCi is the name of the interactive Haskell shell, or REPL. A REPL
* Reads
* Evaluates
* Prints
* Loops
Meaning that it reads one statement, evaluates it, prints the result, and then
go back to step 1, read. We do not need to compile any code for the purpose of
this functional programming intro, we can use the GHCi.

```
Prelude> 1 + 2
3
```

There are some special cases we need to have in mind to use the examples
in GHCi.

GHCi reads one line, and evaluates it. When we need to define a function
over more than one line, the special GHCi-specific syntax `:{` is used to
start a block. `:}` ends it.
```
Prelude> :{
Prelude| say 1 = "one"
Prelude| say 2 = "two"
Prelude| say _ = "many"
Prelude| :}
Prelude>
```

Not every data type is _printable_, so the third step of the REPL can run
into problems.
```
Prelude> map
<interactive>:20:1: error:
    • No instance for (Show ((a0 -> b0) -> [a0] -> [b0]))
        arising from a use of ‘print’
        (maybe you haven't applied a function to enough arguments?)
    • In a stmt of an interactive GHCi command: print it
```
We can see the type of an unprintable value with `:type`, like this:
```
Prelude> :type filter
filter :: (a -> Bool) -> [a] -> [a]
```
In the future, the form of Haskell code that would be used in a compilable
file of Haskell source code is used, so add your own `:{ ... :}` when needed.
