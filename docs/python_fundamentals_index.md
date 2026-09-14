# Python fundamentals index

Six lessons in, you know more Python than you probably realize. This page is the proof.

Use it two ways:

- **Look something up.** Half-remember a tool — *"what was the thing that picks a random number?"* — and find it in [the A–Z index](#part-2-the-index-az), which tells you which page to go back to.
- **See how far you've come.** Read [the spine](#part-1-the-spine-lesson-by-lesson) top to bottom.

## How to read the locators

| Locator | Means |
|---------|-------|
| **4** | Introduced on the Lesson 4 page |
| **4R** | Introduced in the Lesson 4 reading |
| **4H** | Introduced in the Lesson 4 homework |
| 4 | Used again in Lesson 4, but not taught there |
| 7 *(planned)* | Coming in a lesson that isn't written yet |

Bold means *this is where it first showed up*. Plain means *you met it again here*.

---

## Part 1 — The spine, lesson by lesson

One big new idea per lesson. Everything else is either a callback to something older or a small tool that serves the big idea.

### Lesson 1 — Numbers, text, and a place to put them

> **Big idea:** a program is input → calculation → output.

**From the lesson**

- **The shape of a program** — input, calculation, output
- **Output** — `print()`
- **Variables** — memory in the computer, and `=` to put something in it
- **Types** — string, integer, float, boolean
- **`+` does two different jobs** — addition on numbers, gluing on strings
- **Input** — `input()`, which always hands back a string
- **Type conversion** — `int()`, also called casting

**From the reading**

- **The math operators** — `+` `-` `*` `/` `//` `%` `**`
- **Division has a catch** — `/` always gives a float, even when it divides evenly
- **`//` and `%` are a team** — how many times it fits, and what is left over

**From the homework**

- Store a sentence once, print it many times
- The two-number calculator
- Days into full weeks plus leftover days
- Square, cube, divide — and predicting whether the answer prints `2` or `2.0`

### Lesson 2 — True, false, and the first decision

> **Big idea:** a comparison is a value, and `if` spends it.

**From the lesson**

- **The REPL** — `python3` and the `>>>` prompt
- **Asking Python about types** — `type()`
- **Booleans** — `True` and `False`, and storing them in variables
- **Errors are hints, not punishments** — reading a `NameError`
- **Comparisons produce booleans** — `==` `!=` `<` `>` `<=` `>=`
- **`==` compares value *and* type** — `"10" == 10` is `False`; `str()` bridges the gap
- **Spotting a pattern** — `number % 2 == 0` is the whole even/odd question
- **The `if` / `else` statement** — and indentation as the thing that marks a block
- **`=` vs `==`** — the most common typo in programming, and the `SyntaxError` it makes

**From the reading**

- **The `for` loop** — `range(n)` and the loop variable
- **Counting from zero** — and stopping one short of the number you wrote
- **Computing with `i`** — the loop variable is a real number
- **An `if` inside a loop** — and what double indentation means

**From the homework**

- The primes from 0 to 15, by trial division
- The boolean flag variable — `is_prime = True`, flipped to `False`
- Two-argument `range(2, number)`
- Twelve copy-pasted blocks, on purpose, until it aches

### Lesson 3 — Thinking in English first

> **Big idea:** plan in English, then translate line by line.

**From the lesson**

- **Pseudocode** — write the plan in English, run it in your head, *then* translate
- **Comments** — `#`, ignored by Python, written for humans
- **Nested loops** — an outer loop that chooses, an inner loop that works
- **The invisible newline** — `print("*", end="")`, and a bare `print()` as pressing Enter
- **The range end is one short** — again
- **Watch the numbers change** — when a loop confuses you, print its variables and look

**From the reading**

- **`print` with several values** — commas, and the space you get for free
- **`TypeError`** — `"I am " + age` refuses; a comma or `str(age)` fixes it
- **`sep=` and `end=`** — what goes *between* the values, and what goes *after*
- **f-strings** — `f"I am {age}"`, and any expression inside the braces

**From the homework**

- Three triangles, one skeleton
- The have/want table — what the loop gives you, what the row needs
- A space is a real character you can print
- Two inner loops, one after the other, inside one row

### Lesson 4 — Many things in one name

> **Big idea:** one variable can hold a whole collection.

**From the lesson**

- **Lists** — many values in one variable, in square brackets
- **The index** — `names[i]`, counting from zero
- **The hand-cranked counter** — `i = i + 1`
- **Growing and shrinking** — `append()` and `remove()`
- **A list of lists** — a table, indexed twice: `people[1][0]`
- **`len()`** — and why the last index is one *less* than the length
- **The guard clause** — an `if` in front of a risky reach
- **`IndexError`** — another error that tells you exactly what you did

**From the reading**

- **`in`** — asking a list a yes/no question, and getting a boolean
- **`ValueError`** — what happens when you remove something that isn't there
- **Negative index** — `names[-1]` is always the last one, no arithmetic needed
- **Changing an item in place** — `names[0] = "scotty"`
- **Mutable vs immutable** — lists can be edited, strings cannot
- **`insert()` and `pop()`** — the by-position twins, and `pop` hands the item back to you

**From the homework**

- The roster manager, grown four times
- Numbering the roster with `range(len(names))`
- Guarded add and guarded remove
- Swapping a player by index
- The jersey-number table, printed with an f-string

### Lesson 5 — Your own words, and pictures that move

> **Big idea:** `def` — teach Python a new word. *(As taught 2026-08-17.)*

**From the lesson**

- **Toolboxes** — `import turtle`, `from turtle import *`, `import time`
- **Objects, and what the dot means** — `turtle.Turtle()`, and why `names.append` looked the same
- **You have been calling functions since Lesson 1** — `print`, `input`, `int`, `len`, `range`
- **Drawing** — `forward()`, `left()`, and pixels
- **`def` — a word Python didn't know before** — define once, call whenever
- **Parameters** — `rectangle(pixels)`, and the value arriving at call time
- **How movies move** — still frames, about sixty a second
- **The frame toolkit** — `tracer(0)`, `update()`, `hideturtle()`, `penup()` / `pendown()`, `goto()`, `clear()`, `time.sleep(0.016)`
- **The game loop** — and the discovery that the loop variable *is* the animation

**From the reading**

- **Looks** — `shape()`, `pensize()`, `pencolor()`, `screen.bgcolor()`, `screen.title()`
- **`speed()`** — and why `0` is special
- **The map of the window** — (0, 0) at the centre, x to the right, y up
- **Teleporting** — penup, goto, pendown
- **`circle()` and `dot()`**

**From the homework**

- One function, three sizes
- `polygon(sides, size)` — two parameters, and the 360 ÷ sides pattern
- The spiral — thirty-six squares, ten degrees apart
- The bounce — position and direction as two variables, flipping the sign of `dx`, which is **collision detection**

### Lesson 6 — Keys, scope, blueprints

> **Big idea:** writing a class of your own. *(As taught 2026-08-31.)*

**From the lesson**

- **Borrowing code** — what `import` really is
- **Two objects out of the box** — `turtle.Screen()` and `turtle.Turtle()`; *instantiate* means create
- **Constants** — `UP = 90`, the ALL-CAPS promise, and getting rid of magic numbers
- **Driving** — `setheading()`, `onkey()` with **no parentheses**, `listen()`, `mainloop()`
- **Scope** — global vs local, proved with the `age` / `local_test` experiment
- **Names colliding** — the innermost one wins
- **Classes** — an object has attributes and behavior
- **`__init__`, `self`, and methods** — and instantiating from a blueprint you wrote

**From the reading**

- **`random.randint()`** — both ends included, unlike `range`
- **`random.choice()`** — random meets your Lesson 4 lists
- **`distance()`** — to another turtle, or to a plain point
- **`write()`** — words on the window instead of in the terminal, with a font
- **Costumes** — `shape()`, `turtlesize()`, `color()`
- **Difficulty knobs** — numbers someone sat there and tuned

**From the homework**

- The Breakout bar, drawn with `turtlesize(1, 5)`
- A `Bar` class taking a color and a width
- **Composition** — the bar owns its own turtle
- `move_left()` and `move_right()` wired to the arrow keys, with a `STEP` constant

### Lesson 7 — Something to chase *(planned)*

> **Big idea:** a `while` loop that asks a question every single frame.

- **`while True`** — a loop that doesn't count to anything
- **Why `mainloop()` steps aside** — `screen.update()` inside a loop of your own
- **The `global` statement** — taught through a real `UnboundLocalError`
- **Catching the food** — `distance()` for the catch, `randint()` for the respawn
- **The score** — written on the window with `write()`

---

## Part 2 — The index, A–Z

### A – C

| Term | Where |
|------|-------|
| `append()` | **4**, 4H |
| arguments | **5**, 5H, 6 |
| assignment `=` | **1**, 2 |
| attributes | **6**, 6H |
| blocks and indentation | **2**, 2R |
| booleans | **2** |
| booleans — as a flag variable | **2H** |
| bounce, off a wall | **5H** |
| casting | *see* type conversion |
| `circle()`, `dot()` | 5R |
| `class` | **6**, 6H |
| `clear()` | **5** |
| collision detection | **5H**, 7 *(planned)* |
| comments `#` | **3** |
| comparison operators | **2** |
| composition | **6H** |
| constants, ALL CAPS | **6**, 6H |
| constructor `__init__` | **6**, 6H |
| coordinate plane | **5**, 5R |
| copy-paste itch | 2H, **3**, 5 |
| counter, hand-cranked | **4**, 5H |

### D – G

| Term | Where |
|------|-------|
| data types | **1**, 2 |
| `def` | **5**, 5H, 6 |
| difficulty knobs | **6R**, 6H |
| `distance()` | **6R**, 7 *(planned)* |
| dot notation | 4, **5**, 6 |
| `end=` | **3**, 3R |
| equality `==` | **2** |
| equality — `=` vs `==` | **2** |
| errors as hints | **2**, 3R, 4, 4R |
| even / odd test | **2**, 2R, 4 |
| f-strings | **3R**, 4H |
| float | **1**, 1R |
| floor division `//` | **1R**, 1H |
| `for` loop | **2R**, 3, 4, 5 |
| `forward()`, `left()` | **5** |
| frames and animation | **5** |
| function call, the shape of | 1, **5** |
| functions, your own | **5**, 5H |
| game, the anatomy of | **5**, 6 |
| game loop | **5**, 7 *(planned)* |
| `goto()` | **5**, 5R |
| guard clause | **4**, 4R, 4H |

### H – L

| Term | Where |
|------|-------|
| have / want table | **3H** |
| `hideturtle()` | **5** |
| `if` / `else` | **2**, 2R |
| immutable | **4R** |
| `import` | **5**, 6 |
| `in` (membership) | **4R**, 4H |
| index, list position | **4**, 4H |
| index — negative | **4R** |
| `IndexError` | **4** |
| `input()` | **1**, 2, 4 |
| `insert()` | 4R |
| instantiation | **6**, 6H |
| `int()` | **1**, 2, 4 |
| integer | **1** |
| `len()` | **4**, 4H |
| `listen()` | **6**, 6H |
| lists | **4**, 4R |
| lists — of lists (tables) | **4**, 4H |
| loop variable | **2R**, 3, 5 |

### M – R

| Term | Where |
|------|-------|
| magic numbers | **6**, 6H |
| `mainloop()` | **6**, 7 *(planned)* |
| methods | **6**, 6H |
| modules | **5**, 6 |
| modulo `%` | **1R**, 2, 4 |
| mutable | **4R** |
| `NameError` | **2** |
| nested loops | **3**, 3H |
| newline character | **3** |
| objects | 4, **5**, **6** |
| `onkey()` | **6**, 6H |
| operators, math | **1R** |
| parameters | **5**, 5H, 6 |
| `penup()` / `pendown()` | **5**, 5R |
| `pop()` | 4R |
| `print()` | **1**, **3R** |
| `print()` — several values at once | **3R** |
| pseudocode | **3**, and every homework since |
| `random.choice()` | 6R |
| `random.randint()` | **6R**, 7 *(planned)* |
| `range()` | **2R**, 3, 4 |
| `range()` — two-argument form | **2H**, 3 |
| `remove()` | **4**, 4H |
| REPL | **2** |
| reusability | **5**, 5H, 6H |

### S – Z

| Term | Where |
|------|-------|
| scope, global and local | **6**, 7 *(planned)* |
| `screen` object | 5R, **6** |
| `self` | **6**, 6H |
| `sep=` | 3R |
| `setheading()` | **6**, 6H |
| shadowing (names colliding) | 6 |
| `shape()` | 5R, 6R, 6H |
| `speed()` | 5R, 5H |
| `str()` | **2**, 3R |
| strings | **1**, 2 |
| `SyntaxError` | **2** |
| `time.sleep()` | **5** |
| `tracer(0)` / `update()` | **5**, 7 *(planned)* |
| tracing variables | **3**, 4, 5, 5R |
| `turtlesize()` | 6R, **6H** |
| `type()` | **2** |
| type conversion | **1**, 2 |
| `TypeError` | **3R**, 4R |
| `ValueError` | **4R** |
| variables | **1** |
| `write()`, text on the window | **6R**, 7 *(planned)* |

---

## Part 3 — The road ahead

Everything above is a tool you already own. Here is what is still in the box.

### Next — Lesson 7

- **`while`** — every loop so far counts to a number. A game loop doesn't; it just keeps going.
- **`global`** — Lesson 6 already promised this one by name: a score has to survive between key presses.
- **`and`, `or`, `not`** — asking two questions at once. `if x > left and x < right` is how a ball knows it is still on the screen.
- **`+=`** — the short way to write `i = i + 1`, which you have been hand-cranking since Lesson 4.

### Then — Lesson 8

- **`return`** — your functions can *do* things. Next they will be able to *hand an answer back*, the way `pop()` and `distance()` already do.
- **`elif`** — every decision so far has had two branches. Game states — playing, won, lost — need three.
- **Default parameter values** — functions that work whether or not you pass in every input.
- **`None`** — the value a function gives back when it doesn't give anything back.

### Names for things you have already used

- **Keyword arguments** — you have used three of them: `sep=`, `end=`, `font=`.
- **Tuples** — that `("Arial", 24, "bold")` in the Lesson 6 reading is a kind of value with a name you have not met.

### Later

- **`range(a, b, step)`** — counting by twos, or counting backwards.
- **Dictionaries** — looking something up by name instead of by position. A high-score table wants one.
- **Reading and writing files** — everything your programs remember currently vanishes when the window closes.
- **`try` / `except`** — catching a crash instead of guarding against it with an `if`.
- **String methods** — `.upper()`, `.split()`, and pulling a string apart piece by piece.
- **Inheritance** — once two classes genuinely share behavior, one can be built from the other.
- **Your own modules** — every program so far is a single file. Splitting one in two is the moment `import` stops being magic.
