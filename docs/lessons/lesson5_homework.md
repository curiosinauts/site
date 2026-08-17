# Lesson 5 homework

One drawing program, grown four times — and by Problem 4 you're back in the driver's seat. Each problem is the last one plus one new idea, and everything you need is in the lesson or the reading.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line

* Make as many mistakes as you like
* Don't give up

Start every problem from this skeleton:

```python
import turtle

t = turtle.Turtle()
t.speed(0)

# your code here

turtle.done()
```

## Problem 1 — three squares, one function

Define `draw_square(size)` exactly like the lesson, then call it three times — `50`, `100`, `150` — so three nested squares share a corner.

What you should see: three squares of different sizes, growing out of the same corner.

Code

* The whole point: the square loop is written **once**, inside the `def` — the three sizes come from the three calls
* If you see nothing, check: did you *call* the function, or only define it?

## Problem 2 — any shape at all

Define `draw_polygon(sides, size)` — a function with **two** inputs, separated by a comma, just like `print` can take two things. Then call it a few times:

```python
draw_polygon(3, 100)
draw_polygon(4, 100)
draw_polygon(6, 80)
draw_polygon(12, 40)
```

What you should see: a triangle, a square, a hexagon, and a 12-sided shape that's nearly a circle, all drawn from the same spot.

Code

* Inside is the `360 / sides` loop from the lesson — the pattern you spotted does all the work
* Bonus: use `penup` / `goto` / `pendown` from the reading to draw each shape in a different part of the window instead of on top of each other

## Problem 3 — the spiral

Here's the wow. Call `draw_square(100)` thirty-six times — but turn a little between calls:

```python
# 36 times:
#     draw a square
#     turn left 10 degrees
```

What you should see: the squares fan out into a flower-like spiral pattern.

Code

* Translate the pseudocode: a `for` loop with `range(36)`, and inside it a call to your function plus one `t.left(10)`
* Why 36 and 10? Same pattern as the lesson: 36 × 10 = 360 — the squares go exactly once around
* `t.speed(0)` is a must, and try it on a black background with a bright pen color
* Bonus: try `draw_polygon(6, 80)` in the spiral instead of a square

## Problem 4 — upgrade the driver (stretch)

Take the arrow-key driving program from the lesson and give the player more controls. Every new key is the same two steps: **define a function, connect it with `onkey`.**

| key   | what it does                                    |
|-------|-------------------------------------------------|
| `"u"` | lift the pen — drive without drawing             |
| `"d"` | pen down — draw again                            |
| `"c"` | erase the drawing (`t.clear()`)                  |
| `"r"` | change pen color to red — add more color keys!   |

Code

* Each row of the table is a `def` with one or two lines inside, plus one `screen.onkey(..., "u")` line — note the key names are lowercase letters in quotes
* Remember the lesson's trap: `screen.onkey(pen_up, "u")` — no parentheses on the function
* Keep `screen.listen()` and `screen.mainloop()` at the bottom; `onkey` connections go above them

When all four run, look at what you've got: functions you defined, taking inputs you chose, called by loops and by *keys* — the same handful of moves behind every drawing program and every game. Next lesson, the game starts pushing back.
