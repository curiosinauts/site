# Lesson 7 homework

Your Lesson 6 driver works — but the world it drives in has no edges. This week you're going to build the edges: an **arena** the turtle can't escape, made entirely of questions your program asks about itself.

Start from your Lesson 6 program, exactly as you left it. One program, grown four times. Each problem is the last one plus one idea.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line

* Make as many mistakes as you like
* Don't give up

Before you touch anything, add one line so the window is the same size every time you run it:

```python
screen = turtle.Screen()
screen.setup(600, 600)
```

## Problem 1 — where am I?

Before you can catch the turtle leaving, you have to *see* it leave. Make each mover print the turtle's position after it moves.

What you should see: drive around with the arrow keys and watch numbers pour into the terminal — x going up as you drive right, y going down as you drive down. Keep driving right past the edge of the window and the numbers **keep going**: 300, 320, 340... The turtle is gone but the program never noticed.

Code

* Add one line to the bottom of each of your four movers: `print(t.xcor(), t.ycor())`
* Also print the window size once, up near the top: `print(screen.window_width(), screen.window_height())`
* Now the measuring job. Drive slowly to the right until the turtle is *just* touching the edge and read the last x it printed. Compare it to half the window width. Write the two numbers down — that's your wall, and you found it by experiment, exactly like Lesson 2

## Problem 2 — one wall

Time to stop the escape, on one side first. When the turtle would go past the right edge, don't let it.

What you should see: drive right and the turtle slides to the right edge and **stops dead**, no matter how many times you press the key. Every other direction still works.

Code

* Name the wall at the top of the file, with your Problem 1 measurement: `RIGHT = 280` — ALL CAPS, because it's a promise, like `STEP` in the last homework
* Inside `go_right`, after the `forward`, ask the question: `if t.xcor() > RIGHT:` — and if it's true, put the turtle back: `t.setx(RIGHT)`
* `t.setx(280)` sets only the x and leaves y alone, so the turtle stays at the same height. (`setx` is `goto`'s one-axis cousin — try `t.sety()` too)
* Add `t.penup()` near the top if you haven't; the wall is easier to see without scribble everywhere
* Check the direction of your `<` and `>` carefully. If the turtle freezes the instant you press right, you've got the sign backwards — errors are hints

## Problem 3 — a function that answers

Four walls, four `go_` functions, four `if` statements? Feel that copy-paste itch. There's a better question to ask, and it's **one** question: *"am I outside the arena at all?"*

Write a function that **answers** it — no `if` inside, just a `return`:

```python
def is_out_of_bounds():
    return ...
```

What you should see: drive off any edge and the word **OUT!** appears on the window where the turtle is. The alarm fires for all four directions, and the function that decides it is written once.

Code

* Four constants at the top, the four walls: `RIGHT`, `LEFT`, `TOP`, `BOTTOM` — remember left and bottom are **negative**
* The English first:

    ```python
    # hand back True if:
    #    my x is past the right wall
    #    or my x is past the left wall
    #    or my y is past the top wall
    #    or my y is past the bottom wall
    ```

* Translate it into **one** `return` with three `or`s — that pseudocode is almost Python already. No `if` belongs in this function; the comparisons are already `True` or `False`
* Then a second function that reacts to the answer:

    ```python
    def check_bounds():
        if is_out_of_bounds():
            t.write("OUT!", font=("Arial", 24, "bold"))
    ```

    Say that `if` out loud. It reads like the sentence you'd say to a friend — that's what naming a question buys you
* Call `check_bounds()` at the bottom of all four movers. Written once, called four times: Lesson 5's whole point, now with Lesson 7's twist
* Take Problem 2's `if` out first. You're replacing four guards-that-might-have-been with one question
* Predict before you run: what does `is_out_of_bounds()` hand back when the turtle sits peacefully in the middle? Print it and check — `print(is_out_of_bounds())` right inside a mover will show you `True` and `False` flickering as you drive
* Bonus, one word long: also print `"safe"` when the turtle is inside, using `not` — `if not is_out_of_bounds():`. No new comparisons, no second function. That's the opposite question, for free

## Problem 4 — fence the whole arena (stretch)

Now turn the alarm into a real fence: don't just announce the escape, **prevent** it, on all four sides.

What you should see: the turtle can drive anywhere it likes, and slides along every wall like it's in a box. It cannot get out, in any direction, ever.

Code

* This is Problem 2's trick, four times — but now you know which side you're on, so each one is its own `if`:

    ```python
    if t.xcor() > RIGHT:
        t.setx(RIGHT)
    if t.xcor() < LEFT:
        t.setx(LEFT)
    ```

    and the two `sety` twins for top and bottom
* Put all four inside `check_bounds()`, under the `OUT!` alarm — one function, called from all four movers, still. Keep `is_out_of_bounds()` exactly as it is; it answers a question, and that job hasn't changed
* Why four `if`s here, when Problem 3 needed none? Because Problem 3 asked **one** question — "out?" — and one question needs one boolean. This asks **four** questions that each need a *different fix*. Matching the shape of the code to the shape of the question is a real skill, and you just did it both ways
* Draw the arena so the player can see it: before `listen()`, take a second turtle with `penup`, `goto(LEFT, BOTTOM)`, `pendown`, and a `for` loop of four `forward`/`left(90)` pairs. A square you compute from your own constants — change `RIGHT` and the fence moves with it

**Bonus — count the bumps.** Every time the turtle hits a wall, add one to a counter and write the total in the corner. You'll need `bumps += 1` from the reading, and you'll need the `global` keyword from this lesson so `check_bounds` can change a variable that lives outside it — same reason the score needed it.

When all four run, look at what you've built. The turtle now *knows where it is* and the program *reacts to it* — and that's the same machinery, exactly, as the bounce in Lesson 5's homework and the ball-hits-paddle you'll need for Breakout. Walls, paddles, floors, goals: every one of them is a number, a comparison, and an `if`.
