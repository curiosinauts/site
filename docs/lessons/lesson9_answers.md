# Lesson 9 — answer key

Read this *after* you've run the code, not instead of it.

Every answer here comes with the *why*, because the why is the part that transfers. Read the explanations for the questions you got right as well — sometimes a right answer comes from a slightly wrong reason, and that's worth catching now.

---

## Round 1 — Calling a function

**Q1.** Two lines: `hi` and `hi`.

Defining a function doesn't run it. `def greet():` just writes the recipe down. Each `greet()` runs it once, so two calls make two lines.

**Q2.** `7`, then `-7`.

The inputs go in by **position**. First call: `a` is 10, `b` is 3, so `10 - 3`. Second call: `a` is 3, `b` is 10, so `3 - 10`. Same function, same order of parameters — you changed which value landed in which one.

**Q3.**

```
TypeError: rectangle() missing 1 required positional argument: 'pixels'
```

`rectangle` promised it needs one input, and got none. Read that message closely — it names the function, says how many are missing, and tells you the missing one is called `pixels`. Error messages are hints.

---

## Round 2 — The name and the call

**Q4.** Something like:

```
<function greet at 0x1074473d0>
hi
None
```

Three lines, in fact — and if you predicted two, that's the lesson.

* `print(greet)` prints **the function itself**, as an object. The long number is just where it sits in memory; it'll differ on your machine.
* `print(greet())` has to run `greet()` first to find out what to print. Running it prints `hi`. Then `greet` hands back nothing — remember `return` from Lesson 7? A function with no `return` gives you `None` — so `print` prints `None`.

**`greet` is the recipe. `greet()` is cooking it.**

**Q5.** Because `onkey` needs the recipe, not the meal.

You're saying *"here's a function — hold onto it, and run it later, every time the Up arrow is pressed."* To hold onto it, `onkey` needs the function itself.

If you wrote `go_up()`, Python would run it **immediately**, right there on that line, once — before the window is even listening. Then it would hand `onkey` whatever `go_up` returned, which is `None`. So the turtle would twitch once at startup and the arrow key would do nothing forever after.

**Q6.**

```
registering: <function handler at 0x1074fdd20>
handler ran!
registering: None
```

The surprise is the middle line. In `register(handler())`, Python must work out what's *inside* the parentheses before it can call `register` — so `handler()` runs first and prints `handler ran!`, and only then does `register` get called with the `None` it returned.

**Inside-out.** Python always finishes the inner call before starting the outer one. That's the same rule that makes Q17 and Q23 behave the way they do.

---

## Round 3 — Making an object

**Q7.** Once.

`Tree(100, "green")` is instantiation — it builds a new object and runs `__init__`. `a = Tree` doesn't build anything.

**Q8.** `a` is the **class itself** — the blueprint. It prints as `<class '__main__.Tree'>`.

It is not a tree, the way a cookie cutter is not a cookie. `a` and `Tree` are now two names for the same blueprint. You'd still have to call `a(100, "green")` to get an actual tree.

Notice this is Q4's lesson again, in a new costume: `Tree` is the name, `Tree()` does the work.

**Q9.** Python did.

That's what the double underscores mean — `__init__` is a name Python knows about and calls *for* you at the moment you instantiate. You never write `b.__init__(...)` yourself. Lesson 6 put it this way: *it* calls this one, not you.

**Q10.** Python supplies it. The third one is `self`, and it's the new object being built.

When you write `Tree(100, "green")`, Python creates a blank object, then calls `__init__` with that object as the first input, followed by yours. So `self` is `100`'s neighbour, not something you pass.

**Q11.** `self.` is missing. It should be `self.width = width`.

The line `width = width` takes the parameter and assigns it right back to the same local variable — a no-op. Nothing is ever attached to the object, so later `bar.width` raises:

```
AttributeError: 'Bar' object has no attribute 'width'
```

This is the local-versus-attribute trap, and it's Lesson 6's scope lesson in a new place: **a parameter is scratch paper that disappears when the constructor ends. `self.something` is what the object keeps.**

---

## Round 4 — Functions and methods

**Q12.** `t.goto(...)` is called **on** something.

`to_screen_x(50)` is a plain function — it stands alone. `t.goto(50, 50)` is a **method**: it belongs to `t`, and it acts on `t`. The dot means "this function lives inside that object."

Practical consequence: `to_screen_x` works anywhere, but `goto` is meaningless without a turtle to do the going.

**Q13.** `self` is `bar`, and Python put it there.

`bar.move_left()` is Python's shorthand for *"run `move_left`, and pass `bar` in as the first input."* The dot before the name is what becomes `self` inside. That's why every method's parameter list starts with `self` even though you never pass it.

**Q14.** `bar` is the object; `Bar` is the blueprint.

`bar.move_left` is a *bound* method — it already knows which bar it belongs to, so calling it moves that specific bar. `Bar.move_left` doesn't know which bar you mean, so calling it with no arguments gives:

```
TypeError: Bar.move_left() missing 1 required positional argument: 'self'
```

Which is a surprisingly clear message once you know that `self` normally arrives via the dot.

The convention holds everywhere: **Capitalized names are blueprints, lowercase names are things.**

---

## Round 5 — Assignment and order

**Q15.** `5`.

Line by line: `x = 5` puts 5 in `x`. `y = x` looks at what `x` *is right now* (5) and puts that in `y`. `x = 10` changes `x` only.

`y = x` does not tie the two names together. It copies the value across once, at that moment, and then they're strangers. This is the single most useful thing to understand about `=`.

**Q16.** `2`. And the **right** side first, always.

Python works out `count + 1` completely, using the current value of `count`, and *then* stores the result back in `count`. It's not an equation — it's an instruction with two steps, in that order.

That's also why `count = count + 1` isn't nonsense the way it would be in algebra, and why `count += 1` from the Lesson 7 reading means exactly the same thing.

**Q17.** It prints `2 2`, and one of your values is gone forever.

Follow it with Q16's rule. `a = b` makes `a` into 2 — and the old 1 is now stored nowhere. Then `b = a` reads `a`, which is 2, and puts 2 into `b`. You didn't swap them; you overwrote one with the other and then copied it back.

A real swap needs somewhere to stash the first value:

```python
temp = a
a = b
b = temp
```

**Q18.** `50`.

`cam_x = cam_x + STEP` is worked out immediately, using `STEP`'s value *at that moment*, which is 50. Changing `STEP` afterwards doesn't reach back and update `cam_x` — the addition already happened.

Same lesson as Q15: assignment copies a value at a moment in time. Nothing stays connected.

---

## Round 6 — f-strings

**Q19.**

```
I am 12
I am {age}
```

The `f` is the whole difference. With it, Python looks inside the braces, finds the variable, and swaps in its value. Without it, the string is just characters — braces included — and nothing is swapped.

Forgetting the `f` doesn't crash, it just prints the braces. If you ever see `{something}` in your output, that's the bug.

**Q20.** `next year I will be 13`.

So the braces don't only take variable names — they take an **expression**, something Python can work out. `age + 1` is computed first, then dropped into the text. Function calls work too: `f"{t.xcor()}"`.

**Q21.** Everything outside the braces is literal text — including the `cam_x = ` part, the comma, and the spaces. Only the two `{cam_x}` and `{cam_y}` get replaced.

So with the camera at 50, 0, the line reads `cam_x = 50, cam_y = 0`. The words happen to match the variable names because you wrote them to match — Python doesn't know or care that they're the same word.

---

## Round 7 — `global`

**Q22.** It works, and prints `0`.

**Reading** a global from inside a function is always fine. `show` doesn't have its own `score`, so Python looks outside and finds the one on the whiteboard. This is how `to_screen_x` reads `cam_x` without any ceremony.

**Q23.**

```
UnboundLocalError: cannot access local variable 'score' where it is not associated with a value
```

Here's the rule that explains both questions: **if a function assigns to a name anywhere in its body, Python treats that name as local for the whole function** — decided before the function even runs.

So in `add_point`, `score` is local. The line `score = score + 1` then tries to read that local before anything's been put in it. Hence the error.

Q22 had no assignment, so no local was created, so Python looked outside. One assignment changes everything.

**Q24.** It works. `items` becomes `['sword']`.

And this is the subtle one. `items.append("sword")` is **not an assignment** — there's no `=`. You're not changing which list `items` points at; you're reaching into the list that's already there and modifying it. No assignment means no local is created, so Python finds the global list and appends to it.

Compare: `items = ["sword"]` inside a function *would* be an assignment, would make a local, and the global list would be untouched.

**Changing what's inside an object needs no `global`. Pointing a name at something new does.**

**Q25.** *"When I write `cam_x` in this function, I mean the one outside — don't make me a local one."*

That's all it does. It doesn't create the variable and it doesn't make it visible — Q22 shows it was always visible. It only affects **assignment**.

---

## What your misses mean

| If you missed | The gap is | Go back to |
|---|---|---|
| Q3, Q10, Q13 | how inputs get matched to parameters | Lesson 5 |
| Q4, Q5, Q6, Q8 | the name versus the call — parentheses *do* something | Lesson 6 |
| Q7, Q9, Q11, Q14 | what instantiation actually does, and what `self` is | Lesson 6 |
| Q15, Q17, Q18 | `=` copies a value once; it doesn't link two names | Lesson 3 |
| Q16 | the right side is worked out first | Lesson 4 |
| Q19, Q20, Q21 | f-strings | Lesson 3 reading |
| Q22, Q23, Q24, Q25 | local versus global, and that only assignment matters | Lesson 6, Lesson 8 |

Two ideas underneath all of it:

1. **Parentheses mean "do it now."** No parentheses means you're talking about the thing itself — the recipe, the blueprint, the function you want run later.
2. **A name lives somewhere, and `=` is what decides where.** Reading looks outward; assigning makes it local unless you say `global`.

Get those two solid and most of the confusing moments in your own game stop being confusing.
