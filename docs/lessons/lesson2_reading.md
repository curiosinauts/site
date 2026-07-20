# Lesson 2 reading

## The for loop

Remember the "smart way" from Lesson 1?

```python
print(phrase)
print(phrase)
print(phrase)
print(phrase)
print(phrase)
print(phrase)
print(phrase)
print(phrase)
```

Eight copies of the same line is still not very smart. Computers exist to repeat things — we just need a way to say "do this 8 times":

```python
phrase = "I will not talk in class"

for i in range(8):
    print(phrase)
```

`range(8)` produces the numbers 0 through 7, and the loop runs the indented code once for each of them. The indentation rule is the same one you learned with `if`: the indented lines *belong to* the loop.

## The loop variable

That `i` is a variable, and it changes on every trip through the loop. Print it and watch:

```python
for i in range(5):
    print(i)
```

```
0
1
2
3
4
```

Two things to notice: it starts at `0`, not 1, and it stops *before* 5. Programmers count from zero — you still get exactly 5 numbers, just shifted.

Since `i` is a real number, you can compute with it:

```python
for i in range(5):
    print(i ** 2)
```

That prints the first five square numbers: 0, 1, 4, 9, 16.

## Loops + if

The loop body can contain anything — including an `if` statement. This checks every number from 0 to 9, using the even/odd expression from the lesson:

```python
for i in range(10):
    if i % 2 == 0:
        print(i, "even")
    else:
        print(i, "odd")
```

Note the double indentation: the `if` belongs to the loop, and each `print` belongs to its branch of the `if`.

## Try it

Before running each one, predict the exact output. Then run it and check yourself:

```python
for i in range(3):
    print("ha")
```

```python
for i in range(4):
    print(i * 10)
```

```python
for i in range(6):
    if i % 2 == 0:
        print(i)
```
