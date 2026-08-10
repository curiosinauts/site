# Lesson 4

Last week the computer handed you numbers — `range(1, 11)` gave you 1, 2, 3, and your loops turned them into triangles. Today the computer hands you something you actually care about: **a list of things**. Names of players. And by the end, the program will let you *add* and *remove* them while it runs. But first, the homework.

## One name, or many

You know how to store a name — it's a string, one value in memory:

```python
name = "scott"
```

But a team isn't one name, it's several. A **list** holds many values, wrapped in square brackets and separated by commas:

```python
names = ["scott", "rish", "tom", "jerry"]
```

One variable, `names`, now remembers all four. Lists are special — they're the first value we've met that holds *other* values inside it.

## Looping with a counter

We want to print every *other* name — the ones at position 0, 2, 4... Here's the loop:

```python
names = ["scott", "rish", "tom", "jerry"]

i = 0
for name in names:
    if i % 2 == 0:
        print(names[i])
    i = i + 1
```

```
scott
tom
```

Three things are happening, and you already know all three:

- **`names[i]`** reaches into the list and pulls out the item at position `i`. Like `range`, positions start at **0**, so `names[0]` is `"scott"`, `names[1]` is `"rish"`. That position number is called the **index**.
- **`i % 2 == 0`** is the even test from Lesson 2, back again — this time asking about the *index* instead of a number the user typed.
- **`i = i + 1`** is new-looking but simple. Read the right side first (just like `=` always works): take the current `i`, add one, and store it back into `i`. So `i` climbs 0, 1, 2, 3 as the loop runs — a hand-cranked counter that keeps pace with the loop.

So the loop walks the list, and `i` walks the positions alongside it. When `i` is even (0, then 2), we print — `scott`, then `tom`.

## Growing the list from the keyboard

A list isn't frozen. We can add to it with **`append`** — and we can ask the user *what* to add using `input`, exactly like Lesson 1:

```python
new_player = input("your name: ")
print(new_player)

names.append(new_player)
print(names)
```

```
your name: john
john
['scott', 'rish', 'tom', 'jerry', 'john']
```

`names.append(new_player)` sticks the new name onto the **end** of the list. Notice the last `print(names)` shows the whole list, brackets and all — that's Python showing you a list as a value. The team grew from four to five, and *we* didn't type the fifth name — the user did, while the program was running.

## Removing from the list

If a list can grow, it can shrink. **`remove`** takes out a name by its value:

```python
player_to_remove = input("player to remove: ")

names.remove(player_to_remove)
print(names)
```

```
player to remove: tom
['scott', 'rish', 'jerry', 'john']
```

`append` adds to the end; `remove` deletes whichever item *equals* what you gave it. Together they're how a program keeps a list up to date instead of being stuck with whatever you typed in the code.

## A list of lists

Here's where "a list holds other values" gets powerful. Those values can themselves be lists — and suddenly you have a **table**:

```python
people = [
    ["name", "address"],
    ["scott", "1 apple ave"],
    ["rishi", "2 google drive"]
]
```

Read it as rows. `people[0]` is the whole first row, `["name", "address"]` — the headings. `people[1]` is `["scott", "10 alabama ave"]`. And because each row is itself a list, you can index *twice*: `people[1][0]` is `"scott"` (row 1, column 0), and `people[1][1]` is `"10 alabama ave"`. The first bracket picks the row, the second picks the column — just like a spreadsheet.

## Reaching in safely

Let the user pick which name to see, by index:

```python
names = ["scott", "rish", "tom", "jerry", "john"]

name_index = int(input("give me the index of the person's name "))
names_length = len(names)

if name_index < names_length:
    print(names[name_index])
```

Two familiar tools do the work. `int(input(...))` reads a number from the keyboard — `input` always gives a string, so we convert, exactly like Lesson 1's calculator. And **`len(names)`** tells us how many items are in the list: here, 5.

Why the `if`? Because the list has 5 items, the valid indexes are 0, 1, 2, 3, 4 — the last index is **one less** than the length. Ask for `names[5]` and Python stops you:

```pycon
>>> names[5]
IndexError: list index out of range
```

The error is a hint, not a punishment: you reached past the end. The line `if name_index < names_length` is a **guard** — it only prints when the index is in range, so a careless `9` produces nothing instead of a crash. Same `<` you've used since Lesson 2, now protecting your program.

## Watch the numbers change

Same skill as always: when a list confuses you, print the index next to the item it unlocks.

```python
names = ["scott", "rish", "tom", "jerry", "john"]

for i in range(len(names)):
    print(i, names[i])
```

```
0 scott
1 rish
2 tom
3 jerry
4 john
```

There they are — every index and the name it points to. `range(len(names))` gives `0, 1, 2, 3, 4`, one short of the length, exactly as `range` has behaved all along. Master this little table and lists hold no more mystery.
