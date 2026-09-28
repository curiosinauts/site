# Lesson 9 — checkpoint quiz

Eight lessons in, you've built a drawing program, an arena, and a scrolling game world with a camera. That's a lot of machinery.

This week, no new machinery. Instead: a checkpoint.

**This is not a test and there is no grade.** The point is to find the soft spots — the things you can *use* but couldn't quite *explain*. Those are normal, everyone has them, and they're exactly what's worth twenty minutes.

## How to take it

Almost every question asks the same thing: **what does this print?**

That's on purpose. It's the same "predict first, then run" you've been doing since Lesson 1, and it means you can check every single answer yourself:

1. **Write down your prediction.** Actually write it. Saying "yeah I know that one" in your head is how a soft spot stays hidden.
2. **Then type the code in and run it.**
3. Where you were wrong, stop and work out *why* — that's the whole lesson.

Some questions have no output and just ask "what's wrong with this?" Say your answer out loud before checking.

There's an answer key with explanations, but use it after you've run the code, not instead of running it.

---

## Round 1 — Calling a function

```python
def greet():
    print("hi")

greet()
greet()
```

**Q1.** What does this print?

```python
def add(a, b):
    print(a - b)

add(10, 3)
add(3, 10)
```

**Q2.** What are the two lines it prints, in order?

```python
def rectangle(pixels):
    print("drawing a square of", pixels)

rectangle()
```

**Q3.** This one crashes. What is Python going to complain about?

---

## Round 2 — The name and the call

This round is about one character: the parentheses.

```python
def greet():
    print("hi")

print(greet)
print(greet())
```

**Q4.** Two lines come out and they look nothing alike. Describe what each one is.

**Q5.** In your Lesson 6 game you wrote this:

```python
screen.onkey(go_up, "Up")
```

Why is there no `()` after `go_up`? What would happen if you wrote `screen.onkey(go_up(), "Up")` instead — and *when* would it happen?

```python
def handler():
    print("handler ran!")

def register(fn):
    print("registering:", fn)

register(handler)
register(handler())
```

**Q6.** Four lines print. What order do they come out in? (Careful — this one surprises almost everybody.)

---

## Round 3 — Making an object

```python
class Tree:

    def __init__(self, x, color):
        print("making a tree")
        self.x = x
        self.color = color


a = Tree
b = Tree(100, "green")
```

**Q7.** How many times does `making a tree` print, and why?

**Q8.** What is `a`? Is it a tree?

**Q9.** Nobody ever calls `__init__` in that code. So what ran it?

**Q10.** In `Tree(100, "green")` there are two things in the parentheses, but `__init__` has three things in its parentheses. Where does the third one come from?

```python
class Bar:

    def __init__(self, width):
        width = width
```

**Q11.** This runs without any error, but the bar is broken. What's missing, and what happens later when you ask for `bar.width`?

---

## Round 4 — Functions and methods

```python
def to_screen_x(world_x):
    return world_x - cam_x

t.goto(50, 50)
```

**Q12.** `to_screen_x(...)` and `t.goto(...)` are both calls. What's different about the second one?

**Q13.** In `bar.move_left()`, you defined the method as `def move_left(self):` — which takes one input. But the call has empty parentheses. So what is `self`, and who put it there?

**Q14.** Lesson 6's homework warned you to write `screen.onkey(bar.move_left, "Left")` and **not** `Bar.move_left`. What's the difference between `bar` and `Bar` here?

---

## Round 5 — Assignment and order

```python
x = 5
y = x
x = 10

print(y)
```

**Q15.** What prints? Say *why* in terms of what happens on each line.

```python
count = 0
count = count + 1
count = count + 1

print(count)
```

**Q16.** What prints? And in the line `count = count + 1`, which side of the `=` does Python work out first?

```python
a = 1
b = 2

a = b
b = a

print(a, b)
```

**Q17.** This is trying to swap two variables. What does it actually print, and what went wrong?

```python
cam_x = 0
STEP = 50

cam_x = cam_x + STEP
STEP = 100

print(cam_x)
```

**Q18.** What prints?

---

## Round 6 — f-strings

```python
age = 12

print(f"I am {age}")
print("I am {age}")
```

**Q19.** Two lines. What does each one print?

```python
age = 12

print(f"next year I will be {age + 1}")
```

**Q20.** What prints? What does that tell you about what's allowed inside the `{ }`?

**Q21.** In Lesson 8 you wrote this debug line:

```python
print(f"cam_x = {cam_x}, cam_y = {cam_y}")
```

Which parts of that are plain text, and which parts get replaced?

---

## Round 7 — `global`

```python
score = 0

def show():
    print(score)

show()
```

**Q22.** Does this work, or does it crash? There's no `global` line anywhere.

```python
score = 0

def add_point():
    score = score + 1

add_point()
```

**Q23.** This one *does* crash. What's the error called, and why does it happen when Q22 was fine?

```python
items = []

def add_item():
    items.append("sword")

add_item()
print(items)
```

**Q24.** No `global` here either. Does it work? (Think carefully — compare it to Q23.)

```python
cam_x = 0

def look_right():
    global cam_x
    cam_x = cam_x + 50
```

**Q25.** In one sentence: what does the `global` line actually tell Python?

---

## When you're done

Count how many you had to change after running. That number isn't a score — it's a shopping list.

Anything you missed in **Rounds 1, 2, 3 or 4** is really the same question wearing different clothes: *what do the parentheses do?* Anything you missed in **Rounds 5 or 7** is the other big one: *where does this name live, and when does it change?*

Two ideas. Twenty-five questions. Go check the [answer key](lesson9_answers.md) — and read the explanations for the ones you got right, too.
