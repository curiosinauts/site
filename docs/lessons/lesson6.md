# Lesson 6

Lesson 5 ended with a confession: the loop decided where the square went. You watched. Today that flips — **the keyboard calls your functions**, and by the end you'll have an actual game with an actual objective: drive your turtle around the screen and catch food that jumps to a new spot every time you eat it.

Count the new ideas as we go. Almost everything today is a callback — the one genuinely new idea is small, sneaky, and sits inside a single pair of parentheses.

## Why games needed `def` first

Every program you wrote before Lesson 5 ran top to bottom and ended. A game is different: it **waits**, and when the player presses a key, some code has to run. "A named block of code, ready to run when called" — that's exactly what a function is. This is why `def` had to come before the game could start.

The waiting itself is handled by the window. Grab it — the window is an object too, stored in a variable like everything else:

```python
screen = turtle.Screen()
```

Now the three-step recipe for a key:

```python
def go_up():
    t.setheading(90)
    t.forward(20)

screen.onkey(go_up, "Up")
screen.listen()
screen.mainloop()
```

- **`t.setheading(90)`** points the turtle in an exact compass direction: 0 is right, 90 is up, 180 is left, 270 is down. Then `forward(20)` takes one step that way.
- **`screen.onkey(go_up, "Up")`** connects the up arrow key to your function.
- **`screen.listen()`** tells the window to pay attention to the keyboard.
- **`screen.mainloop()`** replaces `turtle.done()`: a loop that runs forever, waiting for keys and calling your functions.

Run it, **click the window once** so it hears the keyboard, and tap the up arrow. The turtle steps. You're in.

## The experiment: parentheses or no parentheses?

Look again at the strangest thing on that page: `screen.onkey(go_up, "Up")` — `go_up` with **no parentheses**. Every function call you've ever made had them. Time for the Lesson 2 skill: run the experiment. Change the line to this and rerun:

```python
screen.onkey(go_up(), "Up")
```

Watch closely. The turtle moves **once, by itself, the instant the program starts** — and then the up arrow does *nothing*. No error. No traceback. Just a dead key.

Here's what happened. Parentheses mean **call it now**. So `go_up()` ran immediately — that's the one ghost step — and what got handed to `onkey` was the *result* of the call, which is nothing at all. The key got connected to nothing.

Without parentheses, `go_up` is the function *itself* — and it turns out a function is a **value**, just like `100` or `"scott"` or a list, and you can hand it to someone. `onkey(go_up, "Up")` hands the screen the recipe so *it* can cook, once per key press. Parentheses cook the meal now; no parentheses hand over the recipe.

One more thing this experiment taught you, and it's bigger than turtle: the bug made **no noise**. Since Lesson 2 we've said error messages are hints — but the nastiest bugs never print one. The only way to catch those is what you just did: predict what should happen, run it, and notice the difference.

## Drive

Fix the line back, then finish all four directions:

```python
import turtle
from turtle import *

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

Drive around. The pen is down, so driving draws — you've built an Etch A Sketch. (Homework adds keys to lift the pen and wipe the screen.)

And yes — those four functions are almost identical. Feel the itch? Same itch as the four forward-left pairs in Lesson 5. Hold that thought; it's homework Problem 2.

## A second turtle

A game needs something to chase. Watch this:

```python
food = turtle.Turtle()
food.shape("circle")
food.color("green")
food.penup()
food.goto(100, 100)
```

Read the first line carefully — it's the same `turtle.Turtle()` from Lesson 5, called a *second time*. `Turtle()` is a cookie cutter: every call stamps out a brand-new turtle, with its own position, its own pen, its own everything. `t` and `food` are two separate objects, and the dot says whose function you're calling: `t.forward(20)` moves the player; `food.goto(100, 100)` moves the food. (You've seen this since Lesson 4 — every list has its *own* `append`.)

`food.penup()` matters: the food is going to teleport around the screen, and we don't want it drawing lines on the way.

## Rolling dice — the `random` toolbox

A game where the food always sits at (100, 100) is boring after one catch. We want the computer to *surprise us* — and there's a toolbox for that. Try it in the REPL:

```pycon
>>> import random
>>> random.randint(-200, 200)
37
>>> random.randint(-200, 200)
-144
>>> random.randint(-200, 200)
12
```

Same call, three times, three different answers. `random.randint(-200, 200)` hands back a whole number between −200 and 200 — a different one each time, like rolling a 401-sided die. Notice it *hands back* a value: you've been using functions like that all along (`input` hands back a string, `len` hands back a count). `randint`'s specialty is that the value is a surprise.

Two of them make a surprise *location*:

```python
food.goto(random.randint(-200, 200), random.randint(-200, 200))
```

The x is one roll, the y is another — the food lands somewhere new every time. (Add `import random` at the top with the other imports.)

## The catch

Now the game rule. English first, as always:

```python
# after every move the player makes:
#     if the player is close to the food:
#         move the food to a new random spot
```

"Close to" — how does a program measure that? The turtle can tell you:

```pycon
>>> t.distance(food)
141.42135623731
```

`t.distance(food)` hands back the number of pixels between the two turtles. A number — and you know exactly what to do with a number: compare it. `t.distance(food) < 20` is a boolean, and a boolean feeds an `if`. It's the Lesson 2 pipeline, beat for beat: function → number → comparison → boolean → `if`.

Translate the pseudocode:

```python
def check_food():
    if t.distance(food) < 20:
        food.goto(random.randint(-200, 200), random.randint(-200, 200))
```

All four movers need this check. And here's the flagship idea from Lesson 5 doing its job: imagine pasting that `if` into `go_up`, `go_down`, `go_left`, and `go_right` — four copies, and the day you decide 20 is too strict, you fix it in four places. Instead: **define once, call four times.** One new line at the bottom of each mover:

```python
def go_up():
    t.setheading(90)
    t.forward(20)
    check_food()
```

A function calling a function — your words are building on your words now, exactly like `print` and `range` build on words some other programmer defined.

## The whole game

```python
import turtle
from turtle import *
import random

t = turtle.Turtle()
screen = turtle.Screen()

food = turtle.Turtle()
food.shape("circle")
food.color("green")
food.penup()
food.goto(random.randint(-200, 200), random.randint(-200, 200))

def check_food():
    if t.distance(food) < 20:
        food.goto(random.randint(-200, 200), random.randint(-200, 200))

def go_up():
    t.setheading(90)
    t.forward(20)
    check_food()

def go_down():
    t.setheading(270)
    t.forward(20)
    check_food()

def go_left():
    t.setheading(180)
    t.forward(20)
    check_food()

def go_right():
    t.setheading(0)
    t.forward(20)
    check_food()

screen.onkey(go_up, "Up")
screen.onkey(go_down, "Down")
screen.onkey(go_left, "Left")
screen.onkey(go_right, "Right")

screen.listen()
screen.mainloop()
```

Run it. Click the window. Chase the dot. Every time you touch it, it jumps somewhere new. That's a game — one you can hand to a friend with no instructions, and they'll just *play* it.

## The anatomy, updated

| game part  | you built it with                                   |
|------------|-----------------------------------------------------|
| window     | `turtle.Screen()`                                   |
| player     | a `Turtle()` object                                 |
| controls   | keys handing your functions to `onkey`              |
| objective  | `random` + `distance` + `if`                        |
| score      | **missing**                                         |

That last row is next lesson — and it's harder than it looks. A score is a number that has to *survive between key presses*: `check_food` must add 1 to it and then remember the total after the function ends. That job belongs to variables, and it's the biggest job we've ever asked of them. Bring your homework game; the score goes into *yours*.
