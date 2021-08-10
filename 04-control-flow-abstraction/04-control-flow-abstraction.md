# Chapter 04: Control flow abstraction
One of the major things that is possible in functional programming is the
abstraction of behaviours. Since it's possible to pass functions as arguments,
it's possible to write functions that describe _how_ to do something, without
knowing _what_ to do.

## No more `for`
### Map
Consider this example in Java:
```java
public List<Integer> doubles(int[] numbers) {
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < numbers.length; i++) {
        result.add(numbers[i] * 2);
    }
    return result;
}
```
this would probably be considered a tiny method in Java, where nothing can
really be abstracted (at least not without making it _more_ complex). It's just
a control structure (a `for` loop) and some simple arithmetics.

If we were to explain what happens in more general terms, the method is applying
a certain calculation on every element of a list and returning a new list with
the results.

This sort of construct appears all the time, yet it's just widely accepted that
it's OK to duplicate the same `for` loop that does the same kind of iteration,
as well as the (entirely uninteresting) declaration, instantiation, comparison
and incrementation of the `i` variable, as well as the "getter" `numbers[i]`.

This behaviour, of mapping a behaviour to each value of a list and returning
a new list with the results, is called `map` in functional programming. It
defines only the behaviour, and not the calculation (in this case, the doubling
of values). The part that does the calculation is passed as an argument to the
`map` function.

```haskell
double x = x * 2
doubles numbers = map double numbers
```
And thus we have completely abstracted away the entire control flow part that
was there in Java, into the function `map` that can be re-used with any
function, not just `double`.

In reality the `double` function is so easy that we can write it as:
```haskell
doubles numbers = map (\n -> n * 2) numbers
```
Usage example:
```
Prelude> doubles [1, 2, 3]
[2,4,6]
```

### Filter
If the program needs to go through a list and only operate on those elements
that fulfill a certain criterion, a nested `if` inside a `for` would be used
in C-like languages like C++, Java, Go, etc. In functional programming, once
again the control flow has been abstracted and there's no need to write two
levels deep fluff just to say "every element that..."

The `filter` function does exactly this.
```haskell
isEven n = n `mod` 2 == 0
filterEvens numbers = filter isEven numbers
```
Or, just
```haskell
filterEvens numbers = filter (\n -> n `mod` 2 == 0) numbers
```

Usage example
```
Prelude> filterEvens [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[2,4,6,8,10]
```

### Fold
When all elements of a list are used to generate a single result, we are talking
about a `fold`. The most typical example is to calculate the sum of all elements
in a list. Each element of the list contributes to a final _accumulated_ result.
This is typically called _fold_ in functional programming, though some other
names also exist.

In Haskell, there is a left fold and a right fold (the difference being which
side of the list you start from). What would look like this in java:
```java
public int sum(int[] numbers) {
    int res = 0;
    for (int i = 0; i < numbers.length; i++) {
        res = res + numbers[i];
    }
}
```
would look like this in Haskell (using a left fold):
```haskell
sum numbers = foldl (\s x -> s + x) 0 numbers
```
To break it down, the elements of the list `numbers` is being _folded_ into
a single value (often called the accumulator) that changes with every "loop",
by the use of a "combining function" (in this case, it's just `x + y`).
The initial value is 0. The initial value and the accumulator are represented
by the `res` variable in the Java example. In the Haskell example, the 0
represents the initial value, and the `s` represents the accumulator (sum).

The entire `for` loop as well as the value-getting has been replaced by the
`foldl` function, and the logic inside the for loop used to update the result
has been replaced with a combining function, making `foldl`  reusable for any
calculation by just passing different combining functions as arguments.

```
Prelude> sum [1, 10, 100, 1000]
1111
```

## Polling
## Sequencing
## Next chapter
