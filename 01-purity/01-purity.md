# Chapter 1: Purity
When describing what functional programming is, the topic of _purity_ often
comes up. The meaning of functional purity can be summarized like this:

```
f(x) = f(y) if x = y
```

In other words, when a function is called, assuming the input is the same,
the output is also the same. The implications of this are:

* The output of the function `f` cannot depend on state.
* The function `f` cannot modify any state.

## A stateless program
If a program doesn't have a state and cannot modify a state, that means it's not
possible to:

* Read or write a file
* Open a socket
* Write to the terminal
* Read user input
* Generate a random number
* Change the value of a "reference"

This trips many people up. The idea of functional purity and that you are not
even allowed to make a program that reads files or accesses databases makes many
dismiss functional programming entirely as something that's "purely academical,
and not at all useful in real-life practical applications".

## Representing state
There are many programs written in functional languages that obviously do
real and practical tasks such as accessing databases, so something is missing
from the above understanding of purity. There are ways to represent state in
a functional program.

### Monads
Haskell is a pure functional programming language. Haskell solves several
impurity problems with the use of _monads_. A monad is a way to represent a
computation, and it is very prevalent everywhere in Haskell. Instead of having a
program do an impure action, the program can instead return the _promise_ of an
impure computation. This keeps the language itself pure, but allows for impure
actions to happen anyway.

#### The `IO` monad
The I/O impurity problem is solved with the `IO` monad.

The `IO` module does _not_ perform I/O. It returns I/O actions, that _describe_
an I/O operation that needs to be performed. The `IO` type is completely pure,
it has no side effects, and thus the I/O operations have been separated from
the language itself. These `IO` types can be bound and chained in ways that
handle all the IO of a single program, and redirects the output to the `main`
function of the program, which always has the return type `IO ()`.

#### The `State` monad
...

### _Impurity_
Not that many functional programming languages actually aspire to be pure.
In that case, impure functionality such as writing a file is just as simple
in functional programming as in any other paradigm. It is up to the programmer
to ensure that functions that should be pure are pure. It is desirable to have
a function be either pure, or _only_ used for its side-effects, not both.

* Several dialects of `ML` (meta language) are impure. `OCaml` is a dialect
  that has a special data type called a reference, which is a reference to any
  other "pure" type in the language. The value within this reference can
  be accessed and updated from anywhere. `F#` is a dialect made by Microsoft,
  that is completely based on the `.NET` framework, inherently object-oriented.
* `Erlang` (and its derivatives `LFE`, `Gleam`, `Elixir`) is a functional
  programming language invented for telecom applications, with a huge focus on
  scalability, concurrence and reliability. It simply has no guarantee that any
  function call is pure, as it allows the reading or writing of files, opening
  of sockets and anything else you might need to have your program communicate
  with the outside world.
* `Lisp` and its derivatives (`Clojure`, `Common Lisp`, `LFE`, `Elisp`) have
  a wide range of origins and usages. `Closure` runs on the Java virtual machine
  which is inherently object-oriented. `Elisp` runs in the emacs editor, and is
  used by the emacs interpreter as a way to extend or configure the editor.

### Loops
```erlang
loop(ListeningSocket, State) ->
    {ok, Socket} = gen_tcp:listen(ListeningSocket),
    UpdatedState = handle_connection(Socket),
    loop(ListeningSocket, UpdatedState).
```
