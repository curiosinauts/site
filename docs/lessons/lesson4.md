# Lesson 4

## for-loop continued

Pseudo code
``` py
# We need to work out spacing vs asterisk

# We need to iterate at least 5 times

# Let's use variable s for spacing, variable a for asterisk

# iteration 1: a = 5, s = 0
# iteration 2: a = 4, s = 1
# iteration 3: a = 3, s = 2
# iteration 4: a = 2, s = 3
# iteration 5: a = 1, s = 4


```

=== "expected output 1"
    ```
    *****
     ****
      ***
       **
        *
    ```

=== "code 1"
    ``` py
    # Problem solving challenge 1
    a = 5
    s = 0

    for i in range(6):
        a = 5 - i
        s = i
        # print(f"a = {a}, s = {s}")
        print(" " * s, end="")
        print("*" * a)
    
    ```
The followin line of the code from above shows code that has been commented out. That means it doesn't get executed when you click on run.
``` py
# print(f"a = {a}, s = {s}")  #(1)
```

1.  We can use comment to write pseudo code to outline our logic OR disable the code.

## for-loop continued 2

Pseudo code
``` py
# We need to work out spacing vs asterisk

# We need to iterate at least 5 times

# Let's use variable s for spacing, variable a for asterisk

# iteration 1: a = 0, s = 6
# iteration 1: a = 1, s = 5
# iteration 2: a = 2, s = 4
# iteration 3: a = 3, s = 3
# iteration 4: a = 4, s = 2
# iteration 5: a = 5, s = 1


```

=== "expected output 2"
    ```

        *
       **
      ***
     ****
    *****
    ```

=== "code 2"
    ``` py
    a = 5
    s = 0

    for i in range(6):
        a = i
        s = 6 - i
        # print(f"a = {a}, s = {s}") 
        print(" " * s, end="")
        print("*" * a)
    ```

## Coding challenge for next week
Tweak the code from above to print a bazaar looking shape. I don't care what it looks like. Create something.