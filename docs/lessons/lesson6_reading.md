# Lesson 6 reading

Two new toolboxes joined the team this week: `random`, and the pieces of turtle that measure and decorate. This reading is the rest of both — every one of them a function call, most of them **handing a value back** for you to use.

## `randint` — both ends included

```pycon
>>> random.randint(1, 6)
4
>>> random.randint(1, 6)
6
>>> random.randint(1, 6)
1
```

`random.randint(1, 6)` is a six-sided die: it can hand back 1, 2, 3, 4, 5, **or 6**. Notice that's different from `range(1, 6)`, which stops at 5 — `randint` includes *both* ends. Two functions, two rules; when a random number seems off by one, this is why.

## `choice` — random meets lists

`randint` picks a random *number*. `random.choice` picks a random *item from a list* — your Lesson 4 lists, meeting this week's toolbox:

```pycon
>>> colors = ["red", "orange", "yellow", "green", "blue", "purple"]
>>> random.choice(colors)
'green'
>>> random.choice(colors)
'red'
```

Anything a list can hold, `choice` can pick: colors, names, sizes. You'll use this in the homework to give the food a new color every time it's eaten.

## `distance` — to a turtle, or to a point

The lesson used `t.distance(food)` — the gap between two turtles. But `distance` also takes a plain point:

```pycon
>>> t.distance(0, 0)
223.606797749979
```

That's how far the turtle is from the **center** of the window. Useful question for a game: "has the player wandered too far?" — `if t.distance(0, 0) > 300:` is an invisible circular fence, built from the same pipeline as the food check: function → number → comparison → boolean → `if`.

## `write` — words on the window

Until now, words went to the terminal with `print`. Games put words **on the window**:

```python
t.write("hello!")
```

Tiny, isn't it? Give it a font — the name, the size, and a style, wrapped in parentheses as one input:

```python
t.write("GAME ON", font=("Arial", 24, "bold"))
```

The text appears wherever the turtle is standing, and stays until a `clear()`. Park a `penup` turtle in a corner and let it do the writing — that's exactly how the score will work next lesson.

## Costumes and sizes

The turtle has six built-in shapes:

```python
t.shape("turtle")    # also: "arrow", "circle", "square", "triangle", "classic"
```

And a size dial:

```python
food.turtlesize(2)   # twice as big
food.turtlesize(3)   # three times
```

Here's the game-design secret hiding in that dial: a **bigger food is easier to hit**, and a bigger `< 20` in the food check is easier too. Those two numbers are difficulty knobs. Every game you've ever played has numbers like these inside it, and someone sat there tuning them.

`color` sets a turtle's whole look in one call:

```python
food.color("hotpink")
```

## Try it

Same rules as always: **predict first, then run.** Say out loud what will happen before you press Run.

```pycon
>>> import random
>>> random.randint(10, 10)
```

(How many possible answers does that one have?)

```python
import turtle
import random

t = turtle.Turtle()
t.penup()

colors = ["red", "orange", "yellow", "green", "blue", "purple"]

for i in range(6):
    t.color(random.choice(colors))
    t.goto(random.randint(-200, 200), random.randint(-200, 200))
    t.write("here!", font=("Arial", 16, "bold"))

turtle.done()
```

```python
import turtle

t = turtle.Turtle()
t.shape("turtle")
t.turtlesize(3)

print(t.distance(0, 0))
t.forward(100)
print(t.distance(0, 0))

turtle.done()
```

One habit worth keeping: when a random thing behaves strangely, run it many times before judging — one roll of a die tells you nothing. That's Lesson 2's experiment skill, and with `random` it's the *only* way to see the pattern.
