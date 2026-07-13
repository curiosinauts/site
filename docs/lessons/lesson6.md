# Lesson 6

## List

Pseudo code
``` py
# Print a list of names by using list data structure
```

=== "expected output 1"
    ```
    Scott
    Mo
    Faz
    CJ
    Rachel
    ```
=== "code 1"
    ``` py   
    names = ["Scott", "Mo", "Faz", "CJ", "Rachel"]

    for name in names:
        print(name)
    ```

## Files

Pseudo code
``` py
# Print a list of names by using file system. Store the expected outout in a file called names.txt
```

=== "expected output 2"
    ```
    Kaelin
    Faz
    CJ
    Rachel
    Scott
    Mo
    ```
=== "code 2"
    ``` py   
    f = open("names.txt")

    i = 0

    while True:
        name = f.readline()
        # check to see if we reached the end of the line
        if not name:
            break
        
        # only print the name if i is even number
        if i % 2 == 0:
            print(name, end="")
        
        i = i + 1
    ```
