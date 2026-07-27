# Lesson 3 reading

You have been using `print` since day one, but it has more to say. This reading is a tour of its options — all of them about the same question: *how do I get the output to look exactly the way I want?*

## Printing several things at once

So far we mostly printed one thing per call. But `print` happily takes several values separated by commas — and they can mix text literals and variables freely:

```python
age = 12
print("I am", age, "years old")
```

```
I am 12 years old
```

Notice two gifts you got for free. First, `print` put a **space** between each value — you didn't type those spaces. Second, it printed a string and an `int` side by side without complaint.

That second gift is bigger than it looks. Try gluing them with `+` instead:

```python
age = 12
print("I am " + age)
```

```
Traceback (most recent call last):
  File "print_age.py", line 2, in <module>
    print("I am " + age)
          ~~~~~~~~^~~~~
TypeError: can only concatenate str (not "int") to str
```

The same type rule from Lesson 2: `+` refuses to mix `str` and `int`, exactly like `"2" + 2`. You would have to write `"I am " + str(age)`. The comma skips all that — `print` converts everything to text for you.

You have already seen the comma in action, by the way — the even/odd printer in the Lesson 2 reading used `print(i, "even")`.

## `sep` — choosing the separator

That automatic space between values is just a default, and defaults can be changed. The separator argument is called `sep`:

```python
print("2026", "07", "27", sep="-")
```

```
2026-07-27
```

Or squeeze the values together with nothing at all:

```python
print("ha", "ha", "ha", sep="")
```

```
hahaha
```

## `end` — choosing the ending

You know this one from the lesson: `print` normally ends by pressing **Enter**, and `end=""` cancels that so the next `print` continues on the same line.

`sep` and `end` are answering two different questions: `sep` is what goes **between** the values inside one `print`, and `end` is what goes **after** the whole thing. One call can use both:

```python
print("2026", "07", "27", sep="-", end="!")
```

```
2026-07-27!
```

## f-strings — the precise way

The comma is easy but it controls nothing — you get a space between values whether you want one or not. When you want a sentence to come out *exactly* right, Python has a nicer tool: put the letter `f` in front of the string, and inside it, anything wrapped in curly braces `{}` is treated as Python instead of text:

```python
age = 12
print(f"I am {age} years old")
```

```
I am 12 years old
```

Python replaces `{age}` with the value of `age`. No commas, no `str()` conversion, no surprise spaces — the string looks like the sentence you want, with blanks filled in.

And the braces hold any expression, not just a variable name — math works in there:

```python
age = 12
print(f"Next year I will be {age + 1}")
```

```
Next year I will be 13
```

The `f` matters. Forget it and Python prints the braces literally — `I am {age} years old`. If your output ever shows curly braces you didn't want, that missing `f` is the first thing to check.

Which one should you use? For quick checks and debugging — like printing a loop's variables to watch them change — commas are fastest to type. For output a person is meant to read, f-strings say exactly what you mean.

## Try it

Before running each one, predict the exact output — spaces, dashes and all. Then run it and check yourself:

```python
name = "Scott"
age = 12
print(name, "is", age)
```

```python
print("A", "B", "C", sep="...")
```

```python
for i in range(3):
    print("ha", end="")
print()
print("done")
```

```python
item = "pencil"
price = 2
print(f"One {item} costs ${price}, two cost ${price * 2}")
```
