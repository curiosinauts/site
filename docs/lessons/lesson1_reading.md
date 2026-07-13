# Lesson 1 reading

In the lesson we only used `+`. Python has a full set of math operators:

| Operator | What it does      | Example  | Result |
|----------|-------------------|----------|--------|
| `+`      | addition          | `7 + 2`  | `9`    |
| `-`      | subtraction       | `7 - 2`  | `5`    |
| `*`      | multiplication    | `7 * 2`  | `14`   |
| `/`      | division          | `7 / 2`  | `3.5`  |
| `//`     | floor division    | `7 // 2` | `3`    |
| `%`      | remainder (modulo)| `7 % 2`  | `1`    |
| `**`     | power             | `7 ** 2` | `49`   |

## Division and types

Remember integers and floats from the lesson? Division connects to types in a sneaky way: `/` **always** returns a float, even when the numbers divide evenly:

```python
print(10 / 2)   # 5.0  — a float, not 5
print(10 // 3)  # 3    — floor division throws away the decimal part
```

## Remainder

`//` and `%` are a team. `//` tells you how many times something fits, and `%` tells you what is left over:

```python
print(17 // 5)  # 3  — 5 fits into 17 three times
print(17 % 5)   # 2  — with 2 left over
```

This is how you answer questions like "if 17 students split into teams of 5, how many full teams are there, and how many students are left without a team?"

## Try it

Before running each line, predict the answer. Then run it and check yourself:

```python
print(2 ** 10)
print(100 / 8)
print(100 // 8)
print(100 % 8)
```
