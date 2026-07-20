# Lesson 2

## The REPL

Today we work in the **REPL** — type `python3` in the terminal and you get a `>>>` prompt. Type an expression, Python evaluates it and answers immediately:

```pycon
>>> 1
1
```

REPL stands for Read, Evaluate, Print, Loop — exactly the input → calculation → output cycle from Lesson 1, one line at a time.

## Asking Python about types

In Lesson 1 *we* had to know the types. The `type()` function lets us ask Python directly:

```pycon
>>> type(1)
<class 'int'>
>>> type("1")
<class 'str'>
>>> type(int("2"))
<class 'int'>
```

Look at the last one carefully: `int("2")` converts the string to an integer first, so by the time `type()` sees it, it is already an `int`. That is type conversion from Lesson 1, confirmed by the computer itself.

## Booleans

The third row of our type table — true/false — finally gets used. `True` and `False` are real values with their own type:

```pycon
>>> type(True)
<class 'bool'>
>>> type(False)
<class 'bool'>
```

Capitalization matters. Python has never heard of lowercase `true`:

```pycon
>>> type(true)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'true' is not defined. Did you mean: 'True'?
```

Read that error message — Python tells you exactly what went wrong and even guesses what you meant. Error messages are hints, not punishments.

And since booleans are values, they can be stored in variables like any other value:

```pycon
>>> am_i_tall = False
>>> type(am_i_tall)
<class 'bool'>
```

One fun aside — even `type` itself has a type:

```pycon
>>> type(type)
<class 'type'>
```

## Comparisons produce booleans

Where do `True` and `False` actually come from? From **comparisons**. You have written inequalities like `70 > 65` in algebra all year — the difference is that Python *evaluates* them down to a boolean:

```pycon
>>> 70 > 65
True
```

And because a comparison produces a value, you can store the result in a variable:

```pycon
>>> scott_height = 65
>>> is_someone_tall = 70 > scott_height
>>> is_someone_tall
True
```

The right side runs first: Python looks up `scott_height`, evaluates `70 > 65` to `True`, and assigns that to `is_someone_tall`. You can add parentheses to make the order visible — same result:

```pycon
>>> is_someone_tall = (70 > scott_height)
>>> is_someone_tall
True
```

## Equality checks value AND type

`==` asks "are these equal?" Here is where types sneak in again:

```pycon
>>> "10" == 10
False
>>> 10 == 10
True
```

The string `"10"` and the integer `10` are *not* equal — they are different types, just like `"2" + "2"` was not math. But convert one side and they can agree:

```pycon
>>> "10" == str(10)
True
>>> int("10") == 10
True
```

## The whole comparison family

```pycon
>>> 10 != 10
False
>>> 10 != 9
True
>>> 9 < 10
True
>>> 10 > 9
True
>>> 10 >= 10
True
>>> 10 >= 9
True
>>> 9 <= 10
True
```

| Operator | Question it asks         |
|----------|--------------------------|
| `==`     | equal?                   |
| `!=`     | not equal?               |
| `<`      | less than?               |
| `>`      | greater than?            |
| `<=`     | less than or equal?      |
| `>=`     | greater than or equal?   |

## Pattern recognition: even vs odd

Scientists and programmers work the same way: run an experiment, look at the results, spot the pattern. Here is the experiment — `%` (remainder, from the Lesson 1 reading) combined with `==` (from today). Watch the answers as the number goes up by one each time:

```pycon
>>> 7 % 2 == 0
False
>>> 8 % 2 == 0
True
>>> 9 % 2 == 0
False
>>> 10 % 2 == 0
True
>>> 11 % 2 == 0
False
>>> 12 % 2 == 0
True
```

False, True, False, True, False, True... alternating perfectly. Which numbers got `True`? 8, 10, 12 — the **even** numbers.

Why does this work? Divide any number by 2: even numbers leave remainder `0`, odd numbers leave remainder `1`. So `number % 2 == 0` is a single expression that asks: **"is this number even?"**

That is the real skill of programming — we turned a human question ("is it even?") into an expression the computer can answer with a boolean. Spot a pattern, capture it as an expression, and the computer can now check *any* number, instantly.

## The `if` statement

So `number % 2 == 0` answers the question — but the program should *do something* with the answer. That is what the `if` statement is for. It takes a boolean and picks which code to run.

Exit the REPL (type `exit()`) and put this in a file. The anatomy first:

```python
# if bool
#    code
#    code
# else:
#    code
#    code
```

If the boolean is `True`, the code under `if` runs. Otherwise, the code under `else` runs. Exactly one of the two branches happens — never both, never neither. Now with our even/odd expression as the boolean:

```python
number = int(input("pick a number? "))

if number % 2 == 0:
    print("even")
else:
    print("odd")
```

Notice the indentation: the indented lines *belong to* their branch. That is how Python knows which code is inside the `if` and which is inside the `else`.

Follow the whole pipeline — every piece is something you already know: `input()` reads a string, `int()` converts it, `%` computes the remainder, `==` turns it into a boolean, and `if` uses the boolean to choose. Five small ideas, one working program that answers a question about *any* number you give it.

One warning before you write your own conditions...

## `=` vs `==`

One equals sign **stores**, two equals signs **ask**. Mix them up and Python complains:

```pycon
>>> 9 = 10
  File "<stdin>", line 1
    9 = 10
    ^
SyntaxError: cannot assign to literal here. Maybe you meant '==' instead of '='?
```

`9 = 10` tries to store the value `10` into... the number `9`, which makes no sense — `9` is not a variable. Once again Python's error message guesses exactly what you meant. This is the single most common typo in all of programming; now you know how to spot it.
