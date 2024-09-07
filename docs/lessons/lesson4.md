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
    a = 5
    s = 0

    for i in range(5):
        a = 5 - i
        s = i
        print(f"a = {a}, s = {s}")

    ```

## for-loop continued 2

Pseudo code
``` py
# We need to work out spacing vs asterisk

# We need to iterate at least 5 times

# Let's use variable s for spacing, variable a for asterisk

# iteration 1: a = 1, s = 4
# iteration 2: a = 2, s = 3
# iteration 3: a = 3, s = 2
# iteration 4: a = 4, s = 1
# iteration 5: a = 5, s = 0


```

=== "expected output 1"
    ```
        *
       **
      ***
     ****
    *****
    ```

=== "code 1"
    ``` py
    a = 5
    s = 0

    for i in range(5):
        print(f"a = {a}, s = {s}")

    ```