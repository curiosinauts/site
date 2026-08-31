# Lesson 6

Lesson 5 ended with a confession: the loop decided where the square went. You watched. Today that flips — **the keyboard calls your functions**, and you drive the turtle around the screen with the arrow keys. Along the way, three deeper fundamentals sneak in: giving names to numbers, the question of **where a variable lives**, and — biggest of all — building **your own kind of object**.

## Borrowing someone else's code

```python
# borrowing someone else's code
import turtle
```

That's what `import` really is — code some other programmer wrote, tested, and shared, and you get it with one line. Every toolbox from Lesson 5 (`turtle`, `time`) was someone else's code.

Now two objects come out of the toolbox:

```python
# instantiate (meaning create) an object
# screen is a variable that refers to a special object
screen = turtle.Screen()

# scope of variable t is global
t = turtle.Turtle()
```

**Instantiate** means *create* — `turtle.Turtle()` stamps out a brand-new turtle object, and `turtle.Screen()` hands you the window itself as an object, so you can talk to it. Two variables, two objects, and the dot tells you whose function you're calling — the same dot as `names.append` in Lesson 4.

That comment on `t` — "scope of variable t is global" — is the day's deepest idea. Hold it; we come back to it after the driving works.

## Constants — naming your numbers

Which way is `setheading(90)`? You'd have to remember the compass: 0 right, 90 up, 180 left, 270 down. A number that means something — but doesn't *say* it — is called a **magic number**, and programmers get rid of them the same way we get rid of everything repetitive: name it.

```python
# constants
UP = 90
DOWN = 270
```

Now `t.setheading(UP)` reads like English. `UP` is just a variable — same `=` as always — but the ALL CAPS is a **promise to whoever reads the code**: this value is set once and never changes. A never-changing variable is called a **constant**. Python doesn't enforce the promise; the capitals are programmers talking to programmers, like the comments from Lesson 3.

## Drive

The four movers, and the wiring that connects them to keys:

```python
def go_up():
    t.setheading(UP)
    t.forward(20)

def go_down():
    t.setheading(DOWN)
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

- **`screen.onkey(go_up, "Up")`** connects the up arrow key to your function. Look closely: `go_up`, **no parentheses**. Parentheses would mean *call it now, once*; without them, the function itself is handed over — a function is a value, like `100` or a list — so the screen can call it every time the key is pressed. Hand over the recipe, don't cook the meal.
- **`screen.listen()`** tells the window to pay attention to the keyboard.
- **`screen.mainloop()`** replaces `turtle.done()`: a loop that runs forever, waiting for keys and calling your functions.

Run it, **click the window once** so it hears the keyboard, and drive. The pen is down, so driving draws — you've built an Etch A Sketch. (Homework adds keys to lift the pen and wipe the screen.)

Two itches to notice before moving on. `go_left` and `go_right` still use magic numbers — the constants job is half-finished. And the four movers are nearly identical — the Lesson 5 copy-paste itch again. Both are homework.

## Scope — where a variable lives

Now the big one. Every mover uses `t` — but none of them *created* `t`. It was created at the top of the file, outside every function, and somehow the functions can see it. Why?

Because every variable has a **scope**: the region of the program where it exists. A variable created at the top level of the file, outside all functions, is **global** — visible everywhere, including inside your functions. That's the comment from the start of the lesson: the scope of `t` is global, and that is exactly why `go_up` can use it.

A variable created *inside* a function is different. Run the experiment:

```python
age = 0

def local_test():
    # scope of age here is local
    age = 15
    print(age)

print(age)
local_test()
```

Predict first, then run. The output:

```
0
15
```

The first `print(age)` sees the global `age` — `0`. Then `local_test` runs, and `age = 15` inside it does **not** touch the global — it creates a brand-new, separate variable that is **local**: it exists only inside `local_test`, only while it runs. Same name, two different variables, two different scopes.

Don't take my word for it — add one more probe after the call:

```python
print(age)
local_test()
print(age)
```

```
0
15
0
```

The global `age` is still `0`. The local one lived, printed, and vanished when the function ended. Think of it this way: globals are written on the classroom whiteboard — everyone can see them. Locals are scratch paper inside one function — private, and thrown away when the function returns.

This is why your game can work at all: `t`, `screen`, `UP`, `DOWN` are on the whiteboard, so every key-press function shares the same turtle. And it's also a warning you'll meet again very soon — a *score* has to survive between key presses, and now you know the vocabulary to say what that means: the score must live in **global** scope, not local.

## Blueprints — making your own kind of object

One mystery is left over from the top of the lesson. `turtle.Turtle()` *instantiates* an object — but where did the idea of a "turtle" come from in the first place? Someone wrote a **blueprint** for it. Today you write your own.

First, what an object even is:

```python
# an object has attributes and behavior

# e.g. person object

# has attributes
#     height
#     eye_color
#     hair_color

# has behavior
#     walk_on_your_feet
#     you can swim with your arms
```

**Attributes** are what an object *has* — a person has a height, an eye color. **Behavior** is what an object *does* — a person can walk, can swim. Check it against the turtle: it *has* a position, a heading, a pen color; it *does* `forward`, `left`, `goto`. Attributes and behavior. Every object you've met fits — even a list *has* its items and *does* `append`.

The blueprint for a kind of object is called a **class**, and here's one of our own:

```python
# this is how you declare an object
class Snake:

    # constructor
    def __init__(self, length, color, type) -> None:
        self.length = length
        self.color = color
        self.type = type

    def print_attributes(self):
        print("length = ", self.length)
        print("color = ", self.color)
        print("type = ", self.type)

    def did_i_eat_a_dot(self):
        # if I had the dot, +1 on length
        ...
```

Read it piece by piece — every part is a familiar tool wearing a new hat:

- **`class Snake:`** starts the blueprint, the way `def` starts a function. Everything indented under it belongs to the class.
- **`def __init__(...)`** is the **constructor** — the function that runs automatically at the moment of instantiation. Its job is to set up the new object's attributes. The weird name (two underscores on each side) is Python's signal that *it* calls this one, not you.
- **`self`** means *this particular snake*. `self.length = length` takes the value passed in and stores it **on the object** — that's how a plain incoming value becomes an attribute the snake carries around forever.
- **`print_attributes`** is behavior — a function that lives inside the class, so every snake knows how to do it. Functions attached to an object have a name: **methods**. `forward` and `append` were methods all along.
- **`did_i_eat_a_dot`** is an empty promise for now — the `...` is a placeholder where code will go. Read that comment again, though: *"if I had the dot, +1 on length."* A snake that grows when it eats a dot... this class knows what game it wants to be.

Now use the blueprint:

```python
s = Snake(5, "red", "python")

s.print_attributes()
```

```
length =  5
color =  red
type =  python
```

`Snake(5, "red", "python")` is instantiation, exactly like `turtle.Turtle()` — and the three values travel into `__init__` as `length`, `color`, `type`, the same way `150` traveled into `rectangle(pixels)` in Lesson 5. Then `s.print_attributes()` is the dot doing what the dot has always done: calling a function that *belongs to the object* — except this time, **you** wrote the blueprint it came from.

The ladder you've climbed: Lesson 5, you defined your own *function*. Today, your own *kind of object*, with attributes and behavior. `Turtle`, `Screen`, even lists and strings — all just classes somebody wrote. You're on the other side of the toolbox now.

(One aside for the curious: the attribute named `type` quietly hides Python's built-in `type()` function from Lesson 2 while you're inside the class — names can collide, and the innermost one wins. Scope, again.)

## The whole program

```python
# borrowing someone else's code
import turtle

# instantiate (meaning create) an object
# screen is a variable that refers to a special object
screen = turtle.Screen()

# scope of variable t is global
t = turtle.Turtle()

# constants
UP = 90
DOWN = 270

def go_up():
    t.setheading(UP)
    t.forward(20)

def go_down():
    t.setheading(DOWN)
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

## The anatomy, updated

| game part  | you built it with                        |
|------------|-------------------------------------------|
| window     | `turtle.Screen()`                         |
| player     | a `Turtle()` object, global scope         |
| controls   | keys handing your functions to `onkey`    |
| objective  | **missing**                               |
| score      | **missing**                               |

Next lesson the game gets its objective: something to *chase* — a second turtle that jumps to a random spot every time you catch it; the reading has the tools (`random`, `distance`) waiting. After that comes score — and thanks to today, you already know the fundamental that makes score possible.

The homework puts the blueprint idea straight to work on a classic: you'll build the player-controlled bar from **Breakout** — an object with a color, a width, and its own `move_left` and `move_right`. And as for `did_i_eat_a_dot` — a snake growing longer with every dot it eats? You've played that game too. Two retro games are now under construction, and both of them are made of blueprints.
