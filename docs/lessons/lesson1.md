# Lesson 1

## What is programming?

Programming means we **compute**. To compute means to **calculate**.

Computing always has three parts:

1. Input
2. Calculation
3. Output

```
1 + 1 = 2
```

## Your first program

`print` outputs whatever you give it. Here the input is the text `"hello world"`:

```python
print("hello world")
```

## Variables

A variable is **memory in the computer**. The `=` sign assigns a value to a variable. Here `"I will not talk in class"` is the value:

```python
phrase = "I will not talk in class"
```

The simple way to print the same sentence many times:

```python
print("I will not talk in class")
```

The smart way — store it once, use it many times:

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

## Data types

In the human world we have text and numbers. Computers have their own names for them:

| Human      | Computer data type |
|------------|--------------------|
| text       | string             |
| number     | integer, float     |
| true/false | boolean            |

Watch what `+` does with different types:

```python
print(1 + 1)               # prints 2
print("hello" + " world")  # prints hello world
print("2" + "2")           # prints 22
```

Numbers come in two kinds:

```python
age = 13       # whole number   =>  integer
height = 1.75  # decimal number =>  float
```

## Getting input

`input` always gives you a **string**, even when the user types a number. We have to convert the string to an integer before we can do math:

```python
first_number = input("first number?")
second_number = input("second number?")

# we have to convert string to integer
print(int(first_number) + int(second_number))
```
