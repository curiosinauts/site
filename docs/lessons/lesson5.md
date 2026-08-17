# Lesson 5

Four lessons, and every program so far has talked to you in plain text. Today your program opens a **window**, draws pictures in it, and — by the end — makes a square glide across the screen, redrawn 60 times every second. That is the same trick behind every movie and every game ever made. And almost everything in this lesson is stuff you already know. There are two genuinely new ideas: teaching Python a new word, and making pictures *move*.

One note before we start: turtle opens a real window on your screen, so it needs Python installed on your computer — it won't work in the web editor. Run these as files with the Run button in VSCode.

## Borrowing a toolbox

Python doesn't come with drawing switched on. Instead it comes with **toolboxes** — pre-written code called **modules** — and you borrow one with `import`:

```python
import turtle
from turtle import *
import time

# t is an object
t = turtle.Turtle()

turtle.done()
```

Run it. A window opens with a little arrow sitting in the middle. That arrow is the turtle.

Two of those imports grab the turtle toolbox, in two different ways. `import turtle` fetches the toolbox and makes you say where things came from: `turtle.Turtle()`, `turtle.done()`. `from turtle import *` dumps the toolbox's contents straight onto the table, so later we can write `tracer(0)` instead of `turtle.tracer(0)`. And `import time` borrows a second toolbox — we'll need it to control *speed* at the end.

`turtle.Turtle()` creates one turtle and stores it in the variable `t`. The comment says `t` is an **object** — a value that carries its own functions with it. You've already met one: lists are objects too, which is why you wrote `names.append(...)` in Lesson 4. The dot means "belongs to": `append` belongs to the list, `forward` belongs to the turtle.

`turtle.done()` at the very end keeps the window open — without it, the program finishes instantly and the window vanishes before you can blink.

## You've been calling functions since Lesson 1

`print("hello")` — a name, parentheses, and an input inside them. That shape is called a **function call**, and you've been making them all along: `print(...)`, `input(...)`, `int(...)`, `len(...)`, `range(...)`. The turtle just brings its own:

```python
# forward is a function
t.forward(100)
t.left(90)
```

`t.forward(100)` walks the turtle 100 steps in the direction it's facing, drawing a line as it goes — the input is a distance in **pixels**, the tiny dots your screen is made of. `t.left(90)` turns it 90 degrees to the left — the same degrees as in math class.

A square is four sides and four turns:

```python
t.forward(100)
t.left(90)
t.forward(100)
t.left(90)
t.forward(100)
t.left(90)
t.forward(100)
t.left(90)
```

It works — but feel that copy-paste itch? It's the same feeling as the prime homework in Lesson 3: *there has to be a smarter way.* And what if we want two squares? Sixteen more lines?

## The big new idea: teach Python a new word

You know how to name a *value*: `size = 100`. Now you'll name a *block of code*. That's what `def` does — it **defines** a function of your own, a brand-new word that Python didn't know before:

```python
# def -> define, rectangle <- name of a function, which means reusable code
def rectangle(pixels):
    t.forward(pixels)
    t.left(90)
    t.forward(pixels)
    t.left(90)
    t.forward(pixels)
    t.left(90)
    t.forward(pixels)
    t.left(90)
```

Run just that and... nothing happens. No square. That's not a bug — `def` only *teaches* Python the word. Nothing runs until you **call** it, exactly the way you call `print`:

```python
rectangle(150)
```

*Now* the square appears. Define once, call whenever — and each call is one line, no matter how big the block inside is.

Look at the parentheses in the `def`. The reason we put `pixels` inside them is that we want to **pass a value in** — `print("hello")` takes an input, and now your function does too. `pixels` is a variable that gets its value **at call time**: call `rectangle(150)` and the block runs with `pixels = 150`; call `rectangle(50)` and it runs again with `pixels = 50`. One definition, any size of square.

`def rectangle(pixels)` — that's you extending the Python language. `print` and `range` were written by programmers; now you're one of them.

(Those four repeated forward-left pairs inside the `def`? That's a `for` loop waiting to happen — Lesson 3 style. Try tightening it yourself.)

## How movies move

Here's a secret about every screen you've ever watched: **nothing on it actually moves.** A movie is a stack of still pictures — *frames* — shown one after another, each slightly different from the last, so fast your eye is fooled. Games work exactly the same way: draw a frame, erase it, draw the next one a tiny bit different, about 60 times per second.

So to make our square glide, the plan in English is:

```python
# repeat, many times:
#     draw the square
#     show the finished frame
#     wait a tiny moment
#     move one pixel to the right
#     erase everything
```

Every line of that plan needs a tool, and here they are:

- **`tracer(0)`** — normally the turtle draws slowly, line by line, so you can watch. Great for learning, useless for animation. `tracer(0)` turns automatic drawing **off**: nothing appears on screen at all until you say so. (Note it's bare `tracer`, no `t.` — it came from `from turtle import *`.)
- **`update()`** — "show everything now." With tracer off, this is how a finished frame appears, all at once. Draw in secret, then reveal — that's a frame.
- **`hideturtle()`** — hides the arrow itself, so you see only the drawing.
- **`t.penup()` / `t.pendown()`** — lifts the pen so the turtle can move without drawing, and puts it back down to draw again.
- **`t.goto(200, 200)`** — walks the turtle straight to a point. The window is a coordinate plane exactly like math class: **(0, 0) is the center**, x grows right, y grows up. (The reading has the full map.)
- **`t.clear()`** — erases everything the turtle has drawn. This is the "erase the frame" step.
- **`time.sleep(0.016)`** — from the `time` toolbox: pause for 0.016 seconds. Why that strange number? `0.016` is about **1/60 of a second** — pause that long between frames and you get 60 frames per second, the number real games chase.

## The animation

The whole plan, translated:

```python
import turtle
from turtle import *
import time

t = turtle.Turtle()

def rectangle(pixels):
    t.forward(pixels)
    t.left(90)
    t.forward(pixels)
    t.left(90)
    t.forward(pixels)
    t.left(90)
    t.forward(pixels)
    t.left(90)

# turn off automatic drawing -- we will say when to show a frame
tracer(0)

hideturtle()

t.goto(200, 200)

for i in range(150):

    t.pendown()

    # draw the square (invisibly -- tracer is off)
    rectangle(150)

    # show the finished frame
    update()

    t.penup()

    # wait 1/60 of a second
    time.sleep(0.016)

    # move to the next spot: one pixel further right each frame
    t.goto(200 + i, 200)

    # erase, ready for the next frame
    t.clear()

turtle.done()
```

Run it: the square drifts smoothly to the right. Nothing is actually moving — you're watching 150 still pictures.

Trace one lap of the loop, "watch the numbers change" style: pen down, `rectangle(150)` draws the square (invisibly — tracer is off), `update()` reveals the frame, pen up, sleep 1/60 of a second, `goto(200 + i, 200)` walks to the next spot, `clear()` wipes the canvas. Then the loop comes around and draws again.

The motion hides in `200 + i`. First frame, `i` is 0, the square is at x = 200. Next frame, `i` is 1 — x = 201. Then 202, 203... `i` climbs by one each lap, exactly like every loop counter you've traced since Lesson 3, so each frame lands one pixel further right. **The loop variable is the animation.** Change `200 + i` to `200 + i * 2` and it moves twice as fast — because each frame jumps two pixels instead of one.

## The anatomy of every game

Step back and look at what you built: a **window**, a **thing** on the screen, and a **loop** that draws, shows, waits, moves, and erases — 60 times a second. That loop has a name: the **game loop**, and it is the beating heart of every game ever made — Snake, Minecraft, all of them. The rest of a game is just more of what you already do: variables for score, `if` for collisions, lists for enemies.

One piece is missing: **the player**. Right now the loop decides where the square goes. Next lesson, the keyboard does — a key press will call a function *you* defined. Bring your homework shapes; they're going in.
