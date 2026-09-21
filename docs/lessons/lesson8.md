# Lesson 8

Last week you built an arena and locked the turtle inside it. It worked — but think about what you actually did. You took a world the size of a window and put walls around it, because the window *was* the world.

Now think about a game you've actually played. Mario. Zelda. Minecraft. Pokémon. Is the world the size of the screen?

Not even close. The world is enormous, and the screen is a little window sliding around on top of it.

That's today's big idea, and it's the one that turns a program into a game:

> **The world is bigger than the window. The window is a camera looking at part of it.**

There is no turtle function called `camera()`. You're going to build one — out of two variables, subtraction, and the `return` you learned last week.

## Two different kinds of coordinates

Here's the thing that trips up everyone the first time, so let's say it slowly.

A tree in your game has a position. But *which* position?

* **Where the tree is in the world.** The world is 4000 pixels across. The tree stands at world position (1500, 200), and it stands there forever. It never moves.
* **Where the tree is on the screen.** That depends entirely on where the camera is looking. Sometimes the tree is on the left of the window. Sometimes it's on the right. Sometimes it's not on the screen *at all*.

Two different numbers for the same tree. They need two different names, and mixing them up is the single most common bug in this kind of code:

* **world coordinates** — where a thing *is*. Permanent.
* **screen coordinates** — where it *appears right now*. Temporary.

The turtle only understands one of them. `t.goto(x, y)` is always **screen** coordinates — the window, with (0, 0) at the center, exactly the map from Lesson 5. The turtle has never heard of your world and never will.

So you need a translator.

## The camera is two variables

Here's the whole trick, and it's smaller than you'd expect.

The camera is a *position in the world* — the spot the window is centered on:

```python
cam_x = 0
cam_y = 0
```

That's it. That's the camera. Two numbers.

Now: if the camera is looking at world position `cam_x`, and a tree is at world position `tree_x`, where does the tree appear on screen?

Think about it before reading on. Try the easy case: what if the tree is standing *exactly* where the camera is looking? Then it appears dead center — screen position 0.

And if the tree is 100 pixels further right in the world than the camera? Then it appears 100 pixels right of center.

So:

```python
screen_x = tree_x - cam_x
```

**Subtraction.** That's the camera. That's the whole thing.

Let's make it a pair of functions — and here is where last week's `return` stops being an exercise and starts being load-bearing:

```python
def to_screen_x(world_x):
    return world_x - cam_x

def to_screen_y(world_y):
    return world_y - cam_y
```

Two functions that **answer**. Give them a world coordinate, they hand back a screen coordinate. Now drawing anything in the world is one line:

```python
t.goto(to_screen_x(1500), to_screen_y(200))
```

Run the numbers in your head with `cam_x = 0`: the tree is at screen 1500, far off the right edge of a 600-wide window. Invisible. Now set `cam_x = 1500`: the tree lands at screen 0, dead center. The tree never moved. **The camera moved.**

That sentence is the lesson. Read it twice.

## Watch the numbers change

Don't take my word for any of it. Here's the whole idea with no turtle at all — just numbers:

```python
cam_x = 0

def to_screen_x(world_x):
    return world_x - cam_x

print(to_screen_x(0))
print(to_screen_x(500))
print(to_screen_x(-900))

cam_x = 500

print(to_screen_x(0))
print(to_screen_x(500))
print(to_screen_x(-900))
```

Predict all six numbers before you run it. Then run it and check.

Look at what happened when the camera moved right by 500: **every screen number went down by 500.** Everything in the world slid left. That's what it looks like out of a car window when you drive forward — the world streams past you backwards. Your `to_screen_x` just did that with one subtraction.

## Moving the camera needs a new word

Now let's drive it. Arrow keys move the camera, Lesson 6 style:

```python
def look_right():
    cam_x = cam_x + 50
    redraw()
```

Run it and Python stops you cold:

```
UnboundLocalError: cannot access local variable 'cam_x' where it is not associated with a value
```

Read the error — it's a hint, not a punishment. It says **local**. And you know exactly what that means, because you ran the experiment in Lesson 6: `age = 15` inside a function doesn't touch the global `age`, it makes a brand-new local one. Scratch paper, not the whiteboard.

That's fine when you're just *reading* a global — `to_screen_x` reads `cam_x` happily. But the moment a function tries to **assign** to a name, Python decides that name is local, for the whole function. So `cam_x + 50` is reading a local variable that doesn't exist yet. Hence the error.

You need to tell Python: *no, I mean the one on the whiteboard.*

```python
def look_right():
    global cam_x
    cam_x = cam_x + 50
    redraw()
```

`global cam_x` says **"when I write `cam_x` in here, I mean the one outside."** One line, at the top of the function, and now the key handler can actually move the camera.

This is the word Lesson 6 set you up for without naming. And note what it's good for: `cam_x` is *game state* — it belongs to the whole program, not to one function, and several different functions need to change it. That's what globals are for.

A caution worth taking seriously: `global` is powerful and easy to overuse. If every variable in your program is global, then any function can break any other function and you'll never find out where the bug came from. Use it for genuine game state — the camera, the score, whether the game is over — and use parameters and `return` for everything else.

## Redraw: the world is a list

One more piece. If the camera can move, the picture has to be redrawn — and to redraw the world, the program has to *remember* the world.

Lesson 4 gave you lists. Lesson 6 gave you classes. Put them together and you get a world:

```python
class Tree:

    def __init__(self, x, y, color):
        self.x = x
        self.y = y
        self.color = color

trees = [
    Tree(0, 0, "green"),
    Tree(500, 0, "green"),
    Tree(-900, 200, "brown"),
    Tree(250, -250, "green"),
]
```

A **list of objects**. Those `x` and `y` attributes are world coordinates — permanent, written down once, never touched again.

And now redrawing is a `for` loop over the world, running every object through the translator:

```python
def redraw():
    t.clear()
    for tree in trees:
        t.color(tree.color)
        t.goto(to_screen_x(tree.x), to_screen_y(tree.y))
        t.stamp()
    screen.update()
```

Read those six lines and notice how much of your own history is in them. `clear` and `stamp` from Lesson 6. A `for` loop over a list from Lessons 3 and 4. Attributes from Lesson 6's classes. `goto` from Lesson 5. `update` from Lesson 5's animation. Two functions you wrote yourself, using Lesson 7's `return`.

Nothing in that function is new. The only new thing today is the **idea**: the world is stored in world coordinates, and gets translated to screen coordinates at the last possible moment, every time you draw.

## The whole thing

```python
import turtle

WIDTH = 600
HEIGHT = 600
STEP = 50

screen = turtle.Screen()
screen.setup(WIDTH, HEIGHT)
screen.tracer(0)

t = turtle.Turtle()
t.hideturtle()
t.penup()
t.shape("circle")

cam_x = 0
cam_y = 0


class Tree:

    def __init__(self, x, y, color):
        self.x = x
        self.y = y
        self.color = color


trees = [
    Tree(0, 0, "green"),
    Tree(500, 0, "green"),
    Tree(-900, 200, "brown"),
    Tree(250, -250, "green"),
]


def to_screen_x(world_x):
    return world_x - cam_x


def to_screen_y(world_y):
    return world_y - cam_y


def redraw():
    t.clear()
    t.clearstamps()
    for tree in trees:
        t.color(tree.color)
        t.goto(to_screen_x(tree.x), to_screen_y(tree.y))
        t.stamp()
    screen.update()


def look_right():
    global cam_x
    cam_x = cam_x + STEP
    redraw()


def look_left():
    global cam_x
    cam_x = cam_x - STEP
    redraw()


def look_up():
    global cam_y
    cam_y = cam_y + STEP
    redraw()


def look_down():
    global cam_y
    cam_y = cam_y - STEP
    redraw()


screen.onkey(look_right, "Right")
screen.onkey(look_left, "Left")
screen.onkey(look_up, "Up")
screen.onkey(look_down, "Down")

redraw()
screen.listen()
screen.mainloop()
```

Click the window, hold an arrow key, and watch the trees slide past. Four trees in a world far wider than the window, and you can go look at any of them.

That is a scrolling game world. You built it out of subtraction.

## What you just learned

| Idea | What it is |
|------|-----------|
| world coordinates | where a thing *is*, permanently |
| screen coordinates | where it *appears*, right now |
| the camera | two variables: which world spot the window is centered on |
| the transform | `screen = world − camera`, wrapped in a function that returns |
| `global` | "the variable outside, not a new local one" |
| redraw | clear, loop the world, translate, stamp |

Every 2D game with a map bigger than its screen works this way. Mario works this way. The names change, the subtraction doesn't.

And here's the part that matters for your own project: nothing above is really about turtle. If you ever move to a different graphics library, `screen = world − camera` moves with you unchanged. You didn't learn a turtle trick today. You learned how games work.

Next week: making the camera **follow a player** instead of being driven directly — which is one subtraction away from what you already have.
