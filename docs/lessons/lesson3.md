# Lesson 3

Remember the feeling from the homework — copy-pasting the prime-check block for the twelfth time, thinking *there has to be a smarter way*? Today we learn it. And we learn something bigger: how programmers **think before they type**.

## Answer to lesson 2 homework

The homework gave you a block that checks **one** number, and the plain way to check every number from 2 to 15 was to paste it fourteen times, editing `number = ...` each time. Here is the smarter way:

```python
for number in range(2, 16):
    is_prime = True
    for divisor in range(2, number):
        if number % divisor == 0:
            is_prime = False
    if is_prime:
        print(number)
```

Output

```
2
3
5
7
11
13
```

Look closely — the inside of that loop **is your homework block**, unchanged except for one thing: the line `number = 9` is gone, because the outer loop now sets `number` for us. First it runs the whole block with `number = 2`, then with `number = 3`, and so on up to 15. The copy-pasting still happens — the computer just does it for us.

A loop with another loop inside it is called a **nested loop**. The outer loop picks which number we are on; the inner loop does the divisor-checking work for that number.

(Small detail: `range(2, 16)` stops at 15, not 16 — just like `range(10)` stops at 9. The end is always one short.)

## Think in English first

You speak English. Python is a foreign language — like French. When you want to say something in French, you don't *think* in French; you think in English and then translate. Programmers work the same way: **plan in English first, then translate to Python.**

The English plan is called **pseudocode**, and it lives in comments — lines starting with `#`, which Python ignores completely. They are for humans only.

Today's goal: print this triangle.

```
*
**
***
****
*****
******
*******
********
*********
**********
```

Before any Python, describe it in English. Look at the picture: row 1 has one star, row 2 has two stars... row 10 has ten. The row number *is* the star count. So the plan:

```python
# for each row number from 1 to 10
#     print a row of stars: as many stars as the row number, all on one line
#     go to the next line
```

Python cannot run this — but **you** can. Run it in your head: row 1, print one star, next line; row 2, print two stars, next line... Yes, that draws the triangle. We checked the plan was right *before* writing a single line of Python. That is the whole point of pseudocode.

## Translating — and one missing word

Now translate line by line. Line 1 we know from the prime program:

```python
# for each row number from 1 to 10
for row_num in range(1, 11):
```

Line 2 says "as many stars as the row number" — repeating something `row_num` times is a loop:

```python
    # print a row of stars: as many stars as the row number, all on one line
    for j in range(row_num):
        print("*")
```

But "all on one line" — there we are stuck. Watch what `print` does:

```python
print("*")
print("*")
print("*")
```

```
*
*
*
```

Three lines. `print` secretly adds an invisible character after every call: the **newline**, which pushes the cursor down. It is like a word we don't know how to say in French yet. Here is the word — the ending character is called `end`, and we can change it:

```python
print("*", end="")
print("*", end="")
print("*", end="")
```

```
***
```

With `end=""` the newline is replaced by nothing, so the stars land side by side. And the last pseudocode line, "go to the next line"? A `print()` with nothing inside prints no characters — but still adds the newline. It is how a program presses the **Enter** key.

## The star triangle

The full translation, with the English plan kept as comments above each piece:

```python
max = 11

# for each row number from 1 to 10
for row_num in range(1, max):
    # print a row of stars: as many stars as the row number, all on one line
    for j in range(row_num):
        print("*", end="")
    # go to the next line
    print()
```

Output

```
*
**
***
****
*****
******
*******
********
*********
**********
```

English first, Python second — and the comments stay in the file, so anyone reading the code later (including future you) gets the English version for free.

## Watch the numbers change

The program runs too fast to see, but inside it, `row_num` and `j` are changing constantly. Being able to **work out those numbers by hand** is the skill that makes the next lab easy. Trace it on paper:

| `row_num` | `j` goes through          | stars printed |
|-----------|---------------------------|---------------|
| 1         | 0                         | `*`           |
| 2         | 0, 1                      | `**`          |
| 3         | 0, 1, 2                   | `***`         |
| 4         | 0, 1, 2, 3                | `****`        |

See the pattern? `j` always starts at 0 and stops one short of `row_num` — that is `range` behaving exactly as it did in the prime program.

Don't take the table's word for it. Make the program *show* you its numbers — print `j` instead of a star:

```python
max = 11

for row_num in range(1, max):
    for j in range(row_num):
        print(j, end=" ")
    print()
```

```
0
0 1
0 1 2
0 1 2 3
0 1 2 3 4
0 1 2 3 4 5
0 1 2 3 4 5 6
0 1 2 3 4 5 6 7
0 1 2 3 4 5 6 7 8
0 1 2 3 4 5 6 7 8 9
```

There they are — the invisible numbers, made visible. This trick works on any program: when you can't tell what a loop is doing, print its variables and look.
