# Lesson 6 homework

One game, grown four times. Start every problem from **the whole game** at the end of the lesson — by Problem 4 it has more controls, cleaner insides, random style, and a hazard that bites.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line

* Make as many mistakes as you like
* Don't give up

## Problem 1 — more keys

Give the player four more controls. Every new key is the same two steps: **define a function, hand it to `onkey`.**

| key   | what it does                          |
|-------|----------------------------------------|
| `"u"` | lift the pen — drive without drawing   |
| `"d"` | pen down — draw again                  |
| `"c"` | erase the scribbles (`t.clear()`)      |
| `"r"` | turn the player's pen red              |

What you should see: driving works as before, and the four letter keys each do their job.

Code

* Each row of the table is a `def` with one line inside, plus one `screen.onkey(..., "u")` line — letter keys are lowercase, in quotes
* The lesson's trap is waiting for you: `screen.onkey(pen_up, "u")` — hand over the recipe, no parentheses
* Keep every `onkey` above `screen.listen()` and `screen.mainloop()`

## Problem 2 — four movers become one

Look at `go_up`, `go_down`, `go_left`, `go_right`: identical except for one number. That's the copy-paste itch, and you know the cure — **one function, with the difference passed in**:

```python
# define move(angle):
#     point the turtle at angle
#     step forward
#     check the food
```

Then each direction becomes a one-liner:

```python
def go_up():
    move(90)
```

What you should see: the game plays *exactly* the same as before. That's the point — same behavior, better insides.

Code

* `move(angle)` holds the `setheading` / `forward` / `check_food` lines — `angle` gets its value at call time, just like `pixels` did in Lesson 5
* `go_up` calling `move` calling `check_food` — your functions are three layers deep now
* The payoff test: make the player faster by changing `forward(20)` to `forward(40)`. How many places did you have to edit? Before this problem, it was four

## Problem 3 — random flair

Every time the food is eaten, it should respawn wearing a **random color**.

What you should see: the dot jumps *and* changes color with every catch — green, then maybe purple, then maybe green again (random is allowed to repeat!).

Code

* Make a list near the top: `colors = ["red", "orange", "yellow", "green", "blue", "purple"]` — Lesson 4's tool
* Inside `check_food`, next to the `goto`, one new line: `food.color(random.choice(colors))` — `choice` is in the reading
* Bonus: also give it a random size with `food.turtlesize(random.randint(1, 3))` — now some food is big and easy, some small and tricky

## Problem 4 — the hazard (stretch)

Add a **third turtle**: a red square, sitting at a random spot. Touch it and the player gets thrown back to the center. You built the food from parts; now build its evil twin *unaided* — it's the exact same pattern.

The English plan:

```python
# make a poison turtle: red, square, pen up, random spot
# define check_poison:
#     if the player is close to the poison:
#         send the player back to (0, 0)
# after every move, check the poison too
```

What you should see: chase the green dot, and if you clip the red square on the way, you're back at the center.

Code

* The poison setup is the food setup with different clothes: `turtle.Turtle()`, `shape("square")`, `color("red")`, `penup()`, a random `goto`
* `check_poison` is `check_food` with a different `if`-body: `t.goto(0, 0)`
* Call it from `move` (Problem 2 pays off — one place, not four)
* Bonus: make the poison *taunt you* — after teleporting the player, move the poison to a new random spot too
* Bonus: announce the hit with `t.write("ouch!", font=("Arial", 16, "bold"))` from the reading — where will the word appear, and when does it disappear?

When all four run, count the turtles on your screen: a player, a food, a poison — three objects from one cookie cutter, steered by functions calling functions you defined. The only thing your game doesn't do is *count*. Next lesson it learns to keep score.
