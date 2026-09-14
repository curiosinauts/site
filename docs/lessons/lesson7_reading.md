# Lesson 7 reading

Your Lesson 6 driver has a hole in it. Hold the right arrow down long enough and the turtle walks straight off the edge of the window — still there, still listening, still moving, just somewhere you can't see. The program has no idea it left.

That's not a turtle problem. It's a *question* problem: nothing in your code ever asks **"where am I?"** This reading hands you that question, and the word that lets you ask two questions at once.

## Ask the turtle where it is

Two functions, and they are the plainest ones you've met all year:

```pycon
>>> t.goto(100, 50)
>>> t.xcor()
100.0
>>> t.ycor()
50.0
```

`t.xcor()` hands back the turtle's x coordinate. `t.ycor()` hands back its y. That's the whole story.

Two things worth noticing. First, the answers came back as `100.0` and `50.0` — **floats**, not integers, exactly like `10 / 2` gave you `5.0` back in the Lesson 1 reading. The turtle keeps its position in decimals so it can move smoothly.

Second, and this is the bigger one: these functions **hand a value back to you**. `print` doesn't do that — it puts something on the screen and gives you nothing to hold. `t.xcor()` is different. It *becomes* a number, right there in your code, and you can do anything with a number:

```python
print(t.xcor())          # print it
far = t.xcor() + 50      # do math with it
t.xcor() > 280           # compare it -- and now you have a boolean
```

Look at that last line and follow the pipeline, the same one from the Lesson 6 reading: **function → number → comparison → boolean → `if`**. You already own every link in that chain.

```python
if t.xcor() > 280:
    print("too far right!")
```

`pop()` did this in Lesson 4. `distance()` did it in the last reading. There's a name for what these functions do, and by the end of this reading you'll be writing your own.

## How big is the window, anyway?

To know where the edge *is*, you have to know how big the window is. And the honest answer is: it depends on the computer, unless you say.

So say:

```python
screen = turtle.Screen()
screen.setup(600, 600)
```

`setup` pins the window to exactly 600 by 600 pixels, every time, on every machine. Now you can ask it about itself:

```python
print(screen.window_width())    # 600
print(screen.window_height())   # 600
```

Here's the part that catches everyone. The window is 600 wide — so is the right edge at 600?

No. Remember the map from Lesson 5: **(0, 0) is the centre**. The window runs from −300 on the left to +300 on the right. The edge is at **half** the width:

```python
right_edge = screen.window_width() / 2     # 300.0
```

One practical wrinkle. The turtle is a shape with actual size, so at exactly `x = 300` it's already half off the screen. Back off a little and use a number like `280` for the wall. A number like that, sitting in your program meaning "the right wall" — you know what to do with it by now:

```python
RIGHT = 280
LEFT = -280
TOP = 280
BOTTOM = -280
```

Four constants, four ALL-CAPS promises, and not a magic number in sight.

## Two questions at once

Now the new idea, and it's a real one.

You know how to ask **one** question: `if t.xcor() > RIGHT:`. But an arena has four sides. Four separate `if` statements? You've felt that itch before — and sometimes it isn't even four questions. Sometimes it's genuinely *one* question that happens to have two parts: *"did I leave the arena sideways?"* means off the right **or** off the left.

Python has three words for gluing booleans together:

| Word | What it asks | Gives `True` when |
|------|--------------|-------------------|
| `and` | both? | both sides are `True` |
| `or` | either? | at least one side is `True` |
| `not` | the opposite | the thing after it is `False` |

Take them to the REPL, where every new idea belongs:

```pycon
>>> True and True
True
>>> True and False
False
>>> True or False
True
>>> False or False
False
>>> not True
False
>>> not False
True
```

One warning about `or`, because English lies to you here. When someone says "you can have cake or ice cream," they mean *one of them*. Python's `or` means **at least one, and both is fine**:

```pycon
>>> True or True
True
```

Now the real thing. Off the side, in either direction, as **one** question:

```python
if t.xcor() > RIGHT or t.xcor() < LEFT:
    print("off the side!")
```

Read it out loud — *"if my x is past the right wall, or my x is past the left wall"* — and it says exactly what it does. That's one `if`, two ways to be true.

And `and` asks the opposite kind of question — *"am I safely inside?"* — where **everything** has to be true at once:

```python
if t.xcor() < RIGHT and t.ycor() < TOP:
    print("still in the arena")
```

A small gift for the algebra you already know. You'd write "x is between −280 and 280" in math class as `-280 < x < 280`. Python lets you write it exactly that way, and it means the same thing as the `and` version:

```python
if LEFT < t.xcor() < RIGHT:
    print("horizontally fine")
```

Most languages won't let you do that. Python reads like the math because somebody decided it should.

## Write a function that answers

Here's the idea this whole reading has been walking toward.

Every function you have written so far **does** something. `rectangle(100)` draws. `go_up()` moves. You call it, it acts, and it hands you back nothing at all.

But `t.xcor()` doesn't act — it **answers**. So does `t.distance(food)`. Those are somebody else's functions, though. Time to write one of yours.

The magic word is `return`:

```python
def double(n):
    return n * 2
```

Read it literally: *work out `n * 2`, then hand that back to whoever called me.* And now the call **is** the answer:

```pycon
>>> double(5)
10
>>> double(5) + 1
11
>>> x = double(7)
>>> x
14
```

Compare it to the version that only prints:

```python
def double_print(n):
    print(n * 2)
```

On screen they look identical. But `double_print(5) + 1` is an error — there's nothing to add one *to*. `print` shows you a number; `return` **gives** you one. That's the whole difference, and it's a big one.

Two things to know about `return`:

* The function **stops** the moment it hits `return`. Anything written below it never runs
* A function with no `return` still hands something back — a special nothing called `None`. That's what `go_up()` has been quietly returning all along

Now the good part. A function can return a **boolean** — and then you're not returning a number, you're returning an *answer to a question*:

```python
def is_out_of_bounds():
    return t.xcor() > RIGHT or t.xcor() < LEFT
```

No `if` in there anywhere. The comparison already *is* `True` or `False`; the `or` glues the two into one boolean; `return` hands it over. And look what you can write now:

```python
if is_out_of_bounds():
    print("escaped!")
```

That reads like English, because the function has a name that says what it asks. That's the point of the whole exercise: a good question, asked once, given a name, used everywhere.

This is also where `not` finally earns its keep:

```python
if not is_out_of_bounds():
    print("safe")
```

*"If not out of bounds."* One word, and you get the opposite question for free — no second function, no rewriting the comparisons backwards. That's why `not` exists.

One naming habit worth stealing from professionals: functions that answer yes-or-no questions get names starting with **`is_`** or **`has_`** — `is_out_of_bounds`, `has_won`, `is_empty`. Then `if is_empty():` reads right out loud. You have already seen this shape, by the way: `is_prime` back in Lesson 2 was a boolean living in a variable. Same idea, now with a function around it.

## `+=` — the short way to crank the counter

Since Lesson 4 you've been cranking counters by hand:

```python
i = i + 1
```

That works and it always will. But you type it so often that Python has a shorthand:

```python
i += 1
```

Both lines do the identical thing: take what's in `i`, add one, put it back. The `+=` version just says it in three characters. It works with any number:

```python
score += 10
x += 5
bumps += 1
```

And it has a mirror twin for going the other way:

```python
lives -= 1
```

Read `+=` as **"add this to what's already there."** When you meet it in someone else's code — and you will, constantly — that's all it means.

## Try it

Same rule as always: **predict first, then run.** Say the answer out loud before you press Enter.

Start in the REPL, with a plain number standing in for the turtle:

```pycon
>>> x = 300
>>> x > 280
>>> x < -280
>>> x > 280 or x < -280
>>> x > 280 and x < -280
```

That last one is a trap worth falling into. Can a single number be past the right wall **and** past the left wall at the same time? Predict it before you run it, then say why.

Now with a real turtle:

```python
import turtle

screen = turtle.Screen()
screen.setup(600, 600)

t = turtle.Turtle()

print(screen.window_width())
print(screen.window_height())

print(t.xcor(), t.ycor())

t.goto(150, -75)
print(t.xcor(), t.ycor())

turtle.done()
```

Now a function that answers instead of acting. Predict all four lines before you run:

```python
def is_big(n):
    return n > 100

print(is_big(5))
print(is_big(500))
print(not is_big(5))

if is_big(200):
    print("that is a big one")
```

Then change `return n > 100` to `print(n > 100)` and run it again. Three of those lines break. Read the errors — they're telling you exactly what `return` was doing for you.

And the counter, with both spellings side by side:

```python
count = 0

for i in range(5):
    count = count + 1

print(count)

count = 0

for i in range(5):
    count += 1

print(count)
```

One habit to carry into the homework: when a guard doesn't fire, **print the number it's testing**. `print(t.xcor())` right above the `if` will tell you in one second whether the turtle is where you think it is. That's "watch the numbers change" from Lesson 3, pointed at a boolean.
