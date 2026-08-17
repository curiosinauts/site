# Lesson 5

Four lessons, and every program so far has talked to you in plain text. Today your program opens a **window**, draws pictures in it, and — by the end — lets you drive a turtle around the screen with the arrow keys. That is the first piece of a real game. And here's the secret: almost everything in this lesson is stuff you already know. There is exactly **one** big new idea, and it's the idea every game is built on.

One note before we start: turtle opens a real window on your screen, so it needs Python installed on your computer — it won't work in the web editor. Run these as files with the Run button in VSCode.

## Borrowing a toolbox

Python doesn't come with drawing switched on. Instead it comes with **toolboxes** — pre-written code called **modules** — and you borrow one with `import`:

```python
import turtle

t = turtle.Turtle()

turtle.done()
```

Run it. A window opens with a little arrow sitting in the middle. That arrow is the turtle.

Three lines, three jobs. `import turtle` fetches the toolbox. `turtle.Turtle()` creates one turtle and stores it in the variable `t` — variables have held strings, numbers, booleans, and lists; now one holds a *turtle*. And `turtle.done()` at the very end keeps the window open — without it, the program finishes instantly and the window vanishes before you can blink.

## You've been calling functions since Lesson 1

`print("hello")` — a name, parentheses, and an input inside them. That shape is called a **function call**, and you've been making them all along: `print(...)`, `input(...)`, `int(...)`, `len(...)`, `range(...)`. The turtle just brings its own functions:

```python
t.forward(100)
t.left(90)
```

`t.forward(100)` walks the turtle 100 steps in the direction it's facing, drawing a line as it goes. `t.left(90)` turns it 90 degrees to the left — the same degrees as in math class. Put those two lines between `t = ...` and `turtle.done()` and run it: a line, then a turn.

## The square — the plain way and the smart way

A square is four sides and four turns. The plain way:

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

Feel that copy-paste itch? It's the same feeling as the prime homework in Lesson 3 — *there has to be a smarter way* — and it has the same cure. The same two lines, repeated 4 times, is a loop:

```python
for i in range(4):
    t.forward(100)
    t.left(90)
```

And put the size in a variable, so one number controls the whole shape:

```python
size = 100

for i in range(4):
    t.forward(size)
    t.left(90)
```

Change `size` to `50` and the whole square shrinks. One variable, total control — that's why we bother with variables.

## Spot the pattern

A triangle is 3 sides — but the turn is not 90, it's **120**:

```python
for i in range(3):
    t.forward(100)
    t.left(120)
```

Time for the Lesson 2 skill: run the experiment, look at the results, spot the pattern.

| shape    | sides | turn | sides × turn |
|----------|-------|------|--------------|
| triangle | 3     | 120  | 360          |
| square   | 4     | 90   | 360          |

Always 360 — because by the time the turtle finishes the shape, it has spun **all the way around** exactly once, and all the way around is 360 degrees. So the turn is always `360 / sides`, and suddenly one loop draws *any* shape:

```python
sides = 6

for i in range(sides):
    t.forward(80)
    t.left(360 / sides)
```

Try `sides = 5`, `8`, `12`. At `sides = 36` it's practically a circle. A human question — "how do I draw any shape?" — captured as one expression. That's programming.

## The big new idea: teach Python a new word

Here's today's one genuinely new thing.

You know how to name a *value*: `size = 100`. Now you'll name a *block of code*. That's what `def` does — it **defines** a function of your own, a brand-new word that Python didn't know before:

```python
def draw_square():
    for i in range(4):
        t.forward(100)
        t.left(90)
```

Run just that and... nothing happens. No square. That's not a bug — `def` only *teaches* Python the word. Nothing runs until you **call** it, exactly the way you call `print`:

```python
draw_square()
```

*Now* the square appears. Define once, call whenever — and each call is one line, no matter how big the block inside is.

One more step and it gets powerful. `print("hello")` takes an input. Your function can too — put a variable name inside the parentheses of the `def`:

```python
def draw_square(size):
    for i in range(4):
        t.forward(size)
        t.left(90)

draw_square(50)
draw_square(100)
draw_square(150)
```

Three calls, three nested squares. `size` is a variable that gets its value **at call time**: the first call runs the block with `size = 50`, the second with `size = 100`. It's the same trick the outer loop pulled in Lesson 3 — something else sets the variable, your block just uses it.

`def draw_square(size)` — that's you extending the Python language. `print` and `range` were written by programmers; now you're one of them.

## Drive the turtle — your first game controls

Why did games have to wait until today? Because every program you've written runs top to bottom and ends. A game is different: it **waits for the player**, and when the player presses a key, it runs *a function*. No functions, no games. Now you have functions.

```python
import turtle

t = turtle.Turtle()
screen = turtle.Screen()

def go_up():
    t.setheading(90)
    t.forward(20)

def go_down():
    t.setheading(270)
    t.forward(20)

def go_left():
    t.setheading(180)
    t.forward(20)

def go_right():
    t.setheading(0)
    t.forward(20)

screen.onkey(go_up, "Up")
screen.onkey(go_down, "Down")
screen.onkey(go_left, "Left")
screen.onkey(go_right, "Right")

screen.listen()
screen.mainloop()
```

Run it, click the window once, and drive with the arrow keys.

The new pieces, one at a time:

- **`turtle.Screen()`** grabs the window itself, so we can talk to it — stored in a variable like everything else.
- **`t.setheading(90)`** points the turtle in an exact direction, compass-style: 0 is right, 90 is up, 180 is left, 270 is down. Then `forward(20)` takes one step that way.
- **`screen.onkey(go_up, "Up")`** connects a key to a function. Look closely: it's `go_up`, **not** `go_up()`. With parentheses you'd be *calling* the function right now, once. Without them, you're handing the screen the recipe so *it* can cook every time the key is pressed. This is the one line in today's lesson everyone gets wrong once — parentheses call now, no parentheses hand it over for later.
- **`screen.listen()`** tells the window to pay attention to the keyboard.
- **`screen.mainloop()`** replaces `turtle.done()`: it's a loop that runs forever, waiting for keys and calling your functions. Your program no longer runs top to bottom — it sits in that loop until you close the window.

Notice the pen is down the whole time, so driving draws — you've built an Etch A Sketch. (The reading shows you how to lift the pen, change its color, and more.)

## The anatomy of every game

Step back and look at what you built: a **window**, a **player** on the screen, **controls** that call functions, and a **loop** that waits for input. That is the skeleton of every game ever made — Snake, Minecraft, all of them. The rest of a game is just more of what you already do: variables for score, `if` for collisions, lists for enemies.

Next lessons we add those, one at a time. Bring your homework shapes — they're going in the game.
