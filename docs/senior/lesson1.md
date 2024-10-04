# Lesson 1

## Numbering system

### Binary numbers
Origin of binary numbers. That meant zeros and ones. 10101010....

As of today, computers run on electricity. It only knows on and off. Computers have millions of tidy little switches. 1 for on, 0 for off.

So to express numbers like 4 it needs to be written like `00000100`

#### Examples of binary numbers
```
Decimal | Binary
1       = 00000001
2       = 00000010
3       = 00000011
4       = 00000100
5       = 00000101
6       = 00000110
```

### Octal
Octagon, prefix `oct` means 8. That means octal numbers start from 0 to 7. Counting 0 and all together it's 8 numbers.

```
Decimal | Octal
0       = 0
1       = 1
2       = 2
3       = 3
4       = 4
5       = 5
6       = 6
7       = 7
----------> here is how octal representation differs
8       = 10
9       = 11
10      = 12
```

### Hexidecimal
FF A0 ....... boring boring boring but hecidecimal and binary numbers are like the most boring and yet exciting couple you will ever meet. We will come back to this later. I promise!


## REPL - whaa...?

When you open a terminal and type `python` you are getting into REPL mode.
```
> python
1 + 1
2
```

REPL mode allows you to test out simple python code. It can come in handy.

I encourage to have fun by writing code to break your computer. Learning to code is all about making silly mistakes. If you make enough silly mistakes then you end up with awesome code.


## Hello World

```
print("hello world")
```

### Variables
Just like we say that person's name is mo and his age is 25. Computers can do something similar.

```
name = "mo"
age  = 25

```

`name` and `age` are called `variables` in computer programming.

`name` is a variable that stores `string` data type, meaning it stores text.
`age`  is a variable that stores `int` data type, meaning it store numbers.


Run the following code
```
print(f"{name} is {age} years old")
```
It will output something like
```
mo is 25 years old
```
