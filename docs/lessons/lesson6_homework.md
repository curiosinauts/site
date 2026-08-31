# Lesson 6 homework

In 1976 Atari released **Breakout**: a bar at the bottom of the screen, a bouncing ball, a wall of bricks. You're going to build it — starting this week with the bar the player controls, and you're going to build it **the way the lesson taught: as an object**, with attributes and behavior, stamped from a blueprint you write.

One program, grown three times. Each problem is the last one plus one idea.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line

* Make as many mistakes as you like
* Don't give up

## Problem 1 — draw the bar

No class yet — first make the picture. One turtle, dressed up as a bar sitting near the bottom of the window.

What you should see: a wide blue bar, low on the screen, and no pen lines anywhere.

Code

* Start with the usual: `import turtle`, a `turtle.Turtle()`, a `turtle.Screen()`, and `screen.mainloop()` at the bottom to keep the window open
* `t.shape("square")` is a 20-by-20 square — and `t.turtlesize(1, 5)` stretches it: 1 tall, **5 wide**. That's the bar. (The reading used one input for overall size; two inputs stretch height and width separately)
* `t.penup()` before `t.goto(0, -200)` — teleport to the bottom, no scribble on the way
* `t.color("blue")` — dealer's choice on the color

## Problem 2 — blueprint the bar

Same picture, better insides. Wrap the bar in a **class**, exactly like `Snake`: the student's job is a `Bar` blueprint whose constructor takes a **color** and a **width**.

```python
class Bar:

    # constructor
    def __init__(self, color, width):
        ...

bar = Bar("blue", 5)
```

What you should see: exactly the same bar as Problem 1. All the setup lines have moved *inside* the blueprint.

Code

* Store the attributes first, Snake-style: `self.color = color`, `self.width = width`
* Then here's the new idea: the bar needs a turtle of its own, so **create one inside the constructor** — `self.t = turtle.Turtle()`. An attribute doesn't have to be a number or a string; the bar *has* a turtle, the way a person has a height
* The rest of Problem 1's dress-up lines follow, aimed at `self.t` — and use the attributes you just stored: `self.t.color(color)`, `self.t.turtlesize(1, width)`
* The payoff test: change `Bar("blue", 5)` to `Bar("red", 8)`. One line edited, whole bar changes — that's the constructor doing its job

## Problem 3 — behavior: `move_left` and `move_right`

An object has attributes *and behavior*. Give the bar its two moves, and wire them to the arrow keys:

```python
def move_left(self):
    ...

def move_right(self):
    ...
```

What you should see: the bar slides left and right with the arrow keys. (Click the window first so it hears the keyboard.)

Code

* Inside the class, under `__init__`, same indentation — these are **methods**, so `self` comes first in the parentheses
* The insides are the lesson's movers aimed at the bar's own turtle: `self.t.setheading(180)` then `self.t.forward(30)` for left; heading `0` for right
* The wiring is the lesson's recipe rule with a twist — you hand over a **method**: `screen.onkey(bar.move_left, "Left")` — no parentheses, and note it's `bar.`, not `Bar.`: the recipe belongs to the object you instantiated
* `screen.listen()` before `screen.mainloop()`, as always
* One magic number snuck in: the `30` the bar moves per press. You know what to do — `STEP = 30` at the top of the file, ALL CAPS promise, and both movers use it. Then tune it: a big `STEP` is a fast, jumpy bar; a small one is slow and smooth. That number is a difficulty knob, and now it has a name

When it runs, look at what's on the screen: an object stamped from a blueprint **you** wrote — attributes chosen at instantiation, behavior wired to keys. Now think about what Breakout still needs — a ball that flies and *bounces*. Flip back to Lesson 5's homework, Problem 4: you have already animated a bouncing square. A bar, a ball... you can see exactly where this is going.
