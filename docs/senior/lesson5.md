# Lesson 5

## REPL again and Modulo operator

``` bash
# Practice using REPL
>>> a = 2

>>> b = 8

>>> a + b
10

>>> c = 1 / 2

>>> 1 / 2
0.5

# modulo operator
>>> 1 % 2
1

>>> 2 % 2
0

>>> c = 2 % 2
>>> c
0

# if statement
>>> c == 0
True

# Pseudo code
# if True:
#     do something
```

## even or odd number

Pseudo code
``` py
# Modify the code from above and make the output look easier to read

# You may utilize f string from lesson 1

# You may utilize 'end' argument in lesson 4 
```

=== "expected output 1"
    ```
    0 even
    1
    2 even
    3
    4 even
    5
    6 even
    7
    8 even
    9
    10 even
    ```
=== "code 1"
    ``` py   
    # We iterate through 0 through 10
    for i in range(11):
        # Print value of i
        print(f"{i} ", end="")

        # Check to see if current iteration value of i is even
        if i % 2 == 0:
            # Print "even" if the current value of i is even 
            print("even")
        else:
            print("") 
    ```