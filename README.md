# FoP Project: A Small Swift-Like Interpreter

This is an individual educational Java project exploring how a simple
interpreter works. Its main component reads a small, Swift-inspired language
and executes supported statements. It is a learning project, not a complete
Swift implementation or a compiler, and it does not translate Swift into Java.

## Project structure

```text
src/
  SwiftInterpreter.java    Main Swift-like interpreter and runnable example
  MinimalInterpreter.java  Separate prototype with a different syntax
  Main.java                Console-input demonstration
  Reader.java              Reads console input and splits it into words
  Variables.java           Generic helper that returns a supplied value
Algorithms/
  *.java                   Standalone algorithm demonstrations
Value.java                 Experimental Value, IntValue, and StringValue types
```

The algorithm classes each contain their own `main` method and a separate,
duplicated interpreter implementation. They are independent demonstrations,
not modules called by `SwiftInterpreter`. The value classes in `Value.java`
are also not connected to the current interpreter.

## Requirements

- JDK 17 or later
- IntelliJ IDEA is optional; the project also runs from a terminal.

The project does not use an external library or build tool.

## Run the main interpreter

In IntelliJ IDEA, run the `SwiftInterpreter` class. From PowerShell, run these
commands from the project root:

```powershell
javac -d out src\Main.java src\Reader.java src\Variables.java src\SwiftInterpreter.java src\MinimalInterpreter.java
java -cp out SwiftInterpreter
```

The `SwiftInterpreter` entry point currently executes the sample program in
its `main` method. The sample calculates a Fibonacci value and prints `55`.
To try another program, replace the sample text in that method and run the
class again.

`Main` is a separate console-input demonstration: it reads lines until an
empty line and prints the collected words. It does not pass the input to the
interpreter. The algorithm demonstrations can be run individually from their
own `main` methods in IntelliJ.

## Supported language subset

Programs are processed line by line. Put the closing brace `}` on its own
line. Semicolons are not required.

| Construct | Example |
| --- | --- |
| Integer variable declaration | `let count = 10` or `var count = 10` |
| Assignment | `count = count + 1` |
| Compound assignment | `count += 1`, `count -= 1`, `count *= 2`, `count /= 2`, `count %= 2` |
| Integer arithmetic | `+`, `-`, `*`, `/`, `%` |
| Integer comparison | `<`, `<=`, `>`, `>=`, `==`, `!=` |
| Conditional | `if (count > 0) { ... }` followed by `else { ... }` |
| `while` loop | `while (count < 10) { ... }` |
| Range loop (experimental) | `for i in 1...10 { ... }` |
| Print an integer or variable | `print(count)` or `print(42)` |

The range loop is inclusive: `1...10` includes both endpoints. The following
example uses the supported `while` form to calculate the sum of the integers
from 1 through 10:

```swift
var total = 0
var i = 1

while (i <= 10) {
    total = total + i
    i += 1
}

print(total)
```

Expected output:

```text
55
```

## Limitations

This interpreter is intentionally small and its parser has known limitations:

- Values and arithmetic expressions are limited to integers.
- It does not provide full Swift semantics. For example, `let` is accepted as
  a declaration keyword but is not enforced as immutable.
- Strings, functions, arrays, general comment syntax, and many Swift language
  features are not implemented.
- Parsing is basic; complex expressions and malformed input are not handled
  comprehensively.
- `for` loops are experimental. Their block handling is incomplete, and
  statements inside a loop may not all execute as expected.
- `MinimalInterpreter` is a separate prototype with a different syntax; its
  behavior should not be confused with the main interpreter.

## Other examples

The `Algorithms` directory contains standalone demonstrations for factorial,
greatest common divisor, multiplication tables, Fibonacci numbers, prime
checking, palindrome checking, reversing a number, summing digits, and summing
the integers up to a value. Each is an independent class with its own entry
point; the implementations duplicate much of the interpreter logic and are
not required to run the main `SwiftInterpreter`.
