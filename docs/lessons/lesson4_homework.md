# Lesson 4 homework

One program, grown four times. You'll start from the `names` list in the lesson and turn it into a little **roster manager** — a tool that prints the team, adds players, removes them, and swaps them out. Each problem is the last one plus one new idea.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line — every piece is something from the lesson or the reading

* Make as many mistakes as you like
* Don't give up

Start every problem from this list:

```python
names = ["scott", "rish", "tom", "jerry", "john"]
```

## Problem 1 — number the roster

Print every player with its index in front, so you can see the position numbers you'll need later.

Output

```
0 scott
1 rish
2 tom
3 jerry
4 john
```

Code

* This is the "watch the numbers change" loop from the end of the lesson: `for i in range(len(names))`
* Inside, print two things on one line — the index `i` and `names[i]`. Commas in `print` put a space between them for free

## Problem 2 — add and remove, safely

Ask the user for a name to **add**, then a name to **remove**. Print the whole list after each change.

Output (the user typed `mo`, then `tom`)

```
player to add: mo
['scott', 'rish', 'tom', 'jerry', 'john', 'mo']
player to remove: tom
['scott', 'rish', 'jerry', 'john', 'mo']
```

Code

* `input` gets the name, `append` adds it, `remove` deletes it — all straight from the lesson
* One trap: `remove` **crashes** if the name isn't in the list (you saw the `ValueError` in the reading). Guard it — only remove `if the name in names`, otherwise print something friendly like `no such player`
* Bonus: guard the add the same way, so you don't append a name that's already on the team

## Problem 3 — swap a player

Ask the user for an **index** and a **new name**, then replace the player at that index. Print the list.

Output (the user typed `2`, then `tommy`)

```
which index to swap? 2
new name? tommy
['scott', 'rish', 'tommy', 'jerry', 'john']
```

Code

* Changing an item in place is `names[i] = new_name` — the mutable-list idea from the reading
* Remember `input` gives a string; the index has to be a number, so `int(...)` it — like the calculator in Lesson 1
* Guard the index with `len`, exactly like the lesson: only swap `if the index < len(names)`, otherwise print `no such index`. A careless `9` should print a message, not crash

## Problem 4 — the roster table (stretch)

Give every player a jersey number by turning the roster into a **list of lists**:

```python
players = [
    ["scott", 7],
    ["rish", 10],
    ["tom", 4],
    ["jerry", 23],
    ["john", 15]
]
```

Ask the user for an index and print a sentence about that player.

Output (the user typed `1`)

```
which player? 1
rish wears number 10
```

Code

* Each row is itself a list, so you index **twice**: `players[i][0]` is the name, `players[i][1]` is the number
* Build the sentence with an f-string from the Lesson 3 reading: `f"{players[i][0]} wears number {players[i][1]}"`
* Guard the index with `len` again — same safe habit as Problem 3

When all four run, look at them side by side: one list, and a whole tool built out of the handful of moves from this week — loop, `append`, `remove`, `names[i] = ...`, and a `len` guard on every risky reach. That's a real program.
