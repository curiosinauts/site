# Lesson 4 reading

The lesson gave you a list and four things to do with it: loop over it, `append`, `remove`, and index into it. But a list is more alive than that. This reading is a tour of the rest — all of it about the same two questions: *how do I ask a list something, and how do I change it?*

## `in` — asking a yes/no question

You can ask a list whether it contains something, and it answers with a boolean — the same `True`/`False` from Lesson 2:

```python
names = ["scott", "rish", "tom", "jerry"]
print("tom" in names)
print("zoe" in names)
```

```
True
False
```

That's not just a party trick — it fixes a real crash. In the lesson, `remove` deleted a name by value. But watch what happens when the name isn't there:

```python
names = ["scott", "rish", "tom", "jerry"]
names.remove("zoe")
```

```
Traceback (most recent call last):
  File "team.py", line 2, in <module>
    names.remove("zoe")
ValueError: list.remove(x): x not in list
```

Same lesson as the `IndexError`: the error is a hint. You asked Python to remove something that wasn't there. And you already know the fix — **guard it** with an `if`, exactly like the index guard from the lesson:

```python
player_to_remove = input("player to remove: ")

if player_to_remove in names:
    names.remove(player_to_remove)
else:
    print("no such player")

print(names)
```

Now a typo prints a friendly message instead of crashing. `in` before `remove` is the safe habit.

## Negative index — reaching from the end

The lesson ended on a sore spot: the last item sits at index `len - 1`, not `len`, and forgetting that earns you an `IndexError`. Here's the relief — Python lets you count *backwards* with a minus sign:

```python
names = ["scott", "rish", "tom", "jerry", "john"]
print(names[-1])
print(names[-2])
```

```
john
jerry
```

`names[-1]` is always the last item, no matter how long the list is — no `len`, no subtraction, no off-by-one. `names[-2]` is the second-to-last. Read the minus as "from the end": `-1` is the end, `-2` one step back from it.

## Changing an item in place

So far a list could **grow** (`append`) and **shrink** (`remove`). Here's the third power: you can **edit** an item that's already there. It looks just like assigning a variable — because it is:

```python
names = ["scott", "rish", "tom", "jerry"]
names[0] = "scotty"
print(names)
```

```
['scotty', 'rish', 'tom', 'jerry']
```

`names[0] = "scotty"` reaches into slot 0 and stores a new value there, right over the old one. This is a genuinely new idea, and it's worth naming: a list can be **changed**. A string cannot — try to edit one letter and Python refuses:

```python
name = "scott"
name[0] = "S"
```

```
TypeError: 'str' object does not support item assignment
```

That difference has a name. Lists are **mutable** (changeable); strings are **immutable** (fixed). You don't need the vocabulary yet — just remember that `names[0] = ...` works and `name[0] = ...` does not.

## `pop` and `insert` — the by-position twins

`append` and `remove` work by *value* — add this name, delete that name. Their twins work by *position*, using an index.

`insert` drops an item in at a chosen spot, sliding everything after it down:

```python
names = ["scott", "rish", "tom", "jerry"]
names.insert(1, "mo")
print(names)
```

```
['scott', 'mo', 'rish', 'tom', 'jerry']
```

`pop` removes the item at an index — and hands it back to you:

```python
names = ["scott", "rish", "tom", "jerry"]
removed = names.pop(0)
print(removed)
print(names)
```

```
scott
['rish', 'tom', 'jerry']
```

So the toolkit has two pairs: `append`/`remove` think in *names*, `insert`/`pop` think in *positions*. Reach for whichever matches how you're thinking about the change.

## Try it

Before running each one, predict the exact output — every name, every bracket. Then run it and check yourself:

```python
names = ["scott", "rish", "tom", "jerry"]
print("rish" in names)
print(names[-1])
```

```python
names = ["scott", "rish", "tom", "jerry"]
names[2] = "tommy"
names.append("john")
print(names)
```

```python
names = ["scott", "rish", "tom"]
first = names.pop(0)
names.insert(0, "captain")
print(first)
print(names)
```
