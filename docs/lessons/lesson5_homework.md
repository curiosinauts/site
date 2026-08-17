# Lesson 5 homework

One drawing program, grown four times — and by Problem 4 the drawing fights back off the edge of the screen. Each problem is the last one plus one new idea, and everything you need is in the lesson or the reading.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line

* Make as many mistakes as you like
* Don't give up

Start every problem from this skeleton:

```python
import turtle
from turtle import *

t = turtle.Turtle()
t.speed(0)

# your code here

turtle.done()
```

## Problem 1 — three squares, one function

Use the `rectangle(pixels)` function from the lesson, and call it three times — `50`, `100`, `150` — so three squares grow out of the same corner.

What you should see: three nested squares of different sizes, sharing a corner.

Code

* The whole point: the square code is written **once**, inside the `def` — the three sizes come from the three calls
* If you see nothing, check: did you *call* the function, or only define it?
* Bonus from the lesson: replace the four repeated forward-left pairs inside the `def` with a `for` loop — Lesson 3 style

## Problem 2 — any shape at all

Time for the Lesson 2 skill: run the experiment, spot the pattern. A square is 4 sides with `left(90)`. A triangle is 3 sides — try it, and you'll find the turn that works is `120`:

| shape    | sides | turn | sides × turn |
|----------|-------|------|--------------|
| triangle | 3     | 120  | ?            |
| square   | 4     | 90   | ?            |

Fill in the last column. See it? By the time the turtle finishes any shape, it has spun **all the way around** exactly once — and all the way around is 360 degrees. So the turn is always `360 / sides`.

Now capture the pattern: define `polygon(sides, size)` — a function with **two** inputs, separated by a comma — and call it a few times:

```python
polygon(3, 100)
polygon(4, 100)
polygon(6, 80)
polygon(12, 40)
```

What you should see: a triangle, a square, a hexagon, and a 12-sided shape that's nearly a circle.

Code

* Inside the `def`: a `for` loop over `range(sides)`, with `t.forward(size)` and `t.left(360 / sides)`
* Bonus: use `penup` / `goto` / `pendown` from the reading to draw each shape in a different part of the window instead of on top of each other

## Problem 3 — the spiral

Here's the wow. Call `rectangle(100)` thirty-six times — but turn a little between calls:

```python
# 36 times:
#     draw a square
#     turn left 10 degrees
```

What you should see: the squares fan out into a flower-like spiral pattern.

Code

* Translate the pseudocode: a `for` loop with `range(36)`, and inside it a call to your function plus one `t.left(10)`
* Why 36 and 10? The same pattern as Problem 2: 36 × 10 = 360 — the squares go exactly once around
* `t.speed(0)` is a must, and try it on a black background (`screen.bgcolor("black")` from the reading) with a bright pen color
* Bonus: spiral with `polygon(6, 80)` instead of a square

## Problem 4 — the bounce (stretch)

The lesson's animation has a flaw: the square glides right and just... leaves. Make it **bounce** — when it reaches the right edge, it comes back; when it reaches the left edge, it turns around again. Forever-ish.

The English plan first:

```python
# start at some x position, moving right
# repeat many times:
#     draw the square at the current x, show the frame, wait, erase
#     move x by the direction
#     if x has gone past the right edge, make the direction negative
#     if x has gone past the left edge, make the direction positive
```

Code

* Start from the lesson's animation, but the motion needs **two variables** instead of `200 + i`: the position and the direction —

    ```python
    x = -150
    dx = 2
    ```

* Each frame: `t.goto(x, 0)`, and after the frame, `x = x + dx` — the hand-cranked counter from Lesson 4, except now it can count *down* too, because `dx` can be `-2`
* The bounce is two `if` statements straight out of Lesson 2: `if x > 150:` set `dx = -2`, and `if x < -150:` set `dx = 2`
* Use a big loop like `for i in range(600)` so it bounces a few times before the program ends
* Watch it break first: comment out the two `if`s, run it, and watch the square sail off the edge. Then put the guards back. Errors and escapes are hints, not punishments

When all four run, look at what you've got: functions you defined, taking inputs you chose, called by loops — and a thing on screen that *reacts* to where it is. That `if`-inside-the-game-loop in Problem 4? That's collision detection. Every wall in every game works exactly like that.
