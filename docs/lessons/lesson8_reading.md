# Lesson 8 reading

The lesson gave you a camera built from subtraction. This reading is the rest of the window: what the window actually *is*, the three different rectangles hiding behind the word "screen", how to draw a big world without your program crawling, and the built-in camera turtle ships with — plus why you built your own anyway.

This is the toolkit for your own project. Take your time with it.

## Three rectangles, three names

When people say "the screen," they can mean three different things. Turtle has all three, and knowing which is which will save you an evening of confusion.

**1. The window.** The actual box on your desktop, with a title bar you can drag. You set its size:

```python
screen.setup(600, 600)
```

`setup` also takes a position on your desktop, if you want the window to open somewhere specific:

```python
screen.setup(600, 600, 100, 50)     # 600x600, 100 across and 50 down from the top-left
```

And you ask about it with the two functions from last week:

```python
screen.window_width()     # 600
screen.window_height()    # 600
```

**2. The canvas.** The drawing surface *inside* the window — and here's the surprise: it can be **bigger than the window**. If it is, turtle puts scrollbars on:

```python
screen.screensize(2000, 2000)       # canvas 2000x2000, inside a 600x600 window
print(screen.screensize())          # ask: (2000, 2000)
```

The docstring in turtle's own source has a great line about this — it suggests `screensize` as a way "to search for an erroneously escaped turtle." Your Lesson 7 runaway was out there on the canvas the whole time.

Now, scrollbars are not a game camera. A player shouldn't have to drag a scrollbar to see the rest of the level. But `screensize` is genuinely useful for a **map editor** — a tool where *you* want to see the whole world at once while building it.

**3. The world.** Your game's own coordinate space — 4000 pixels across, or 50, or 1,000,000. It's not a turtle thing at all. It's an idea that lives in your variables, and the camera translates it onto the canvas.

Window, canvas, world. Three rectangles, and today's whole lesson is about the gap between the first and the third.

## Backgrounds

A color:

```python
screen.bgcolor("skyblue")
```

Or an actual picture, which is the fastest way to make a project look real:

```python
screen.bgpic("map.gif")
```

Two catches. First, `bgpic` wants a **GIF** file — turtle's picture support is narrow. Second, the background is pinned to the *window*, so it does **not** scroll with your camera. For a scrolling world, a background image is sky or fog, not terrain. Terrain has to be objects in your world list, going through the transform like everything else.

## Drawing a big world without it crawling

If your map has two hundred objects and you redraw all two hundred every time the camera nudges, you will feel it. Three tools fix that.

### `tracer(0)` and `update()` — from Lesson 5, and now you need them

You met these in the animation. Here's the crisp version:

```python
screen.tracer(0)      # stop drawing to the window; work in secret
# ... draw a hundred things ...
screen.update()       # NOW show the finished picture, all at once
```

Without `tracer(0)` the player watches every single object appear one at a time, which looks like a flicker and is slow. With it, they see finished frames. For anything that redraws a whole world, `tracer(0)` is not optional.

The trap, and everybody falls in it once: with `tracer(0)`, **nothing appears until you call `update()`.** If your screen is mysteriously blank, that's the first thing to check.

### `stamp` and `clearstamps` — one turtle, many pictures

You don't need two hundred turtles for two hundred trees. You need **one** turtle that walks around leaving prints:

```python
t.goto(100, 50)
t.stamp()          # leaves a copy of the turtle's shape here
t.goto(-80, 200)
t.stamp()          # and another
```

`stamp` drops a copy of the turtle's current shape, size, and color and moves on. One turtle, a whole forest.

Clearing them:

```python
t.clearstamps()      # all of them
t.clearstamps(3)     # the 3 oldest
t.clearstamps(-3)    # the 3 newest
```

`t.clear()` erases that turtle's *lines and writing*; `t.clearstamps()` erases its *stamps*. Different things — a redraw that leaves ghosts behind usually needs both.

### Don't draw what isn't on screen

Here's the idea professionals call **culling**, and you already have every tool for it.

If the world is 4000 wide and the window is 600, then most of your objects are off-screen at any moment. Drawing them is wasted work — turtle dutifully stamps things nobody can see.

So ask first. And "is this thing visible?" is a yes-or-no question, which means it's a function that returns a boolean — exactly Lesson 7:

```python
HALF_W = WIDTH / 2
HALF_H = HEIGHT / 2

def is_on_screen(thing):
    return (-HALF_W < to_screen_x(thing.x) < HALF_W
            and -HALF_H < to_screen_y(thing.y) < HALF_H)
```

Two `and`ed range checks, using the between-form from last week's reading. (The parentheses let one expression run across two lines — a neat trick for keeping long conditions readable.)

And then the redraw skips the invisible:

```python
for tree in trees:
    if is_on_screen(tree):
        t.goto(to_screen_x(tree.x), to_screen_y(tree.y))
        t.stamp()
```

Two lines of change and a world of a thousand trees costs the same as a world of ten. Every game engine in existence does this.

## Turtle's built-in camera — and why you built your own

Turtle *does* have a camera. It's called `setworldcoordinates`, and it redefines what the window's corners mean:

```python
screen.setworldcoordinates(-300, -300, 300, 300)     # llx, lly, urx, ury
```

That says: the lower-left corner of the window is world (−300, −300) and the upper-right is (300, 300). Move that box and the view moves:

```python
screen.setworldcoordinates(cam_x - 300, cam_y - 300, cam_x + 300, cam_y + 300)
```

Now `t.goto()` takes **world** coordinates directly and turtle does the translating. Tempting! So why didn't we use it?

Three honest reasons:

* **It resets.** The first call switches turtle into "world" mode, and switching modes performs a full screen reset — every turtle homed, every drawing wiped. Surprising if you call it halfway through a program.
* **It distorts angles.** Turtle's own docs warn, in capitals: *in this mode angles appear distorted if x/y unit-ratio doesn't equal 1.* Stretch the box unevenly and your headings stop meaning what you think.
* **It doesn't travel.** This is the big one. `setworldcoordinates` is a turtle feature and only a turtle feature. `screen = world − camera` is arithmetic, and it works in pygame, in JavaScript, in a game engine, on paper. You learned a thing you get to keep.

Use it if you want — for a fixed view of a world in units that aren't pixels (a graph, a map in kilometers) it's genuinely handy. But for a scrolling game, do the subtraction yourself.

## Keys that repeat

One quality-of-life fix you'll want the moment you drive a camera around.

`screen.onkey(fn, "Right")` fires when the key is **released**. Tapping works; holding the key down does nothing until you let go. For smooth scrolling that feels wrong.

```python
screen.onkeypress(look_right, "Right")
```

`onkeypress` fires when the key goes **down**, and your operating system's key-repeat takes over if you hold it. Same wiring otherwise — still needs `screen.listen()`.

For real games there's a better pattern still: the key handler doesn't move anything, it just sets a variable saying "right is held," and a frame loop does the moving. That's how you get diagonal movement and steady speed. You have every tool for it except the frame loop — which is coming.

## A frame loop that lives inside `mainloop`

Speaking of. `screen.mainloop()` sits and waits for keys forever, which is why your programs end with it. But a game also needs a heartbeat — something that happens on its own, without the player pressing anything.

```python
def tick():
    # move things, redraw
    screen.ontimer(tick, 16)     # ask to be called again in 16 milliseconds

tick()
screen.mainloop()
```

`screen.ontimer(fn, ms)` says *"run this function once, in this many milliseconds."* Have the function ask for itself at the end, and you've got a loop that runs forever — about 60 frames a second at `16` — while keys still work.

That's a real game loop, and it's the shape your side project will eventually want. Don't worry about it yet; just know the door is there.

## Try it

**Predict first, then run.** Every time.

Start with no turtle at all — the camera is only arithmetic, and arithmetic is easiest to see in the REPL:

```pycon
>>> cam_x = 0
>>> def to_screen_x(world_x):
...     return world_x - cam_x
...
>>> to_screen_x(100)
>>> to_screen_x(-100)
>>> cam_x = 1000
>>> to_screen_x(100)
>>> to_screen_x(1000)
```

Before that last one: where does a thing appear when the camera is looking straight at it?

Now the three rectangles. Watch the scrollbars show up:

```python
import turtle

screen = turtle.Screen()
screen.setup(400, 400)
screen.screensize(1500, 1500)

print(screen.window_width(), screen.window_height())
print(screen.screensize())

t = turtle.Turtle()
t.penup()
t.goto(600, 600)
t.pendown()
t.circle(50)

turtle.done()
```

The circle is drawn way outside the window — scroll over and find it. That's canvas-versus-window in one picture.

Stamps, and the difference between the two clears:

```python
import turtle

t = turtle.Turtle()
t.shape("circle")
t.penup()

for x in range(-200, 201, 100):
    t.goto(x, 0)
    t.stamp()

t.goto(0, 100)
t.write("stamps!", font=("Arial", 16, "bold"))

t.clear()

turtle.done()
```

Predict before running: after `t.clear()`, what's left on the screen — the stamps, the writing, both, or neither? Run it, then swap `t.clear()` for `t.clearstamps()` and predict again.

And the one that shows why `tracer` matters. Run it as-is, then uncomment the two lines and run again:

```python
import turtle
import random

screen = turtle.Screen()
screen.setup(600, 600)
# screen.tracer(0)

t = turtle.Turtle()
t.shape("circle")
t.penup()

for i in range(300):
    t.goto(random.randint(-280, 280), random.randint(-280, 280))
    t.stamp()

# screen.update()

turtle.done()
```

One habit for your own project, and it's the most useful debugging trick in this whole lesson: when something is drawn in the wrong place, **print both coordinates side by side** —

```python
print("world", tree.x, tree.y, "-> screen", to_screen_x(tree.x), to_screen_y(tree.y))
```

Nine times out of ten you'll see instantly that you fed a screen coordinate into something expecting a world one, or forgot the translation entirely. That's "watch the numbers change" from Lesson 3, pointed at a camera.
