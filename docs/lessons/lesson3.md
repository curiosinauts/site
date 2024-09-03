# Lesson 3 
We will learn for-loop

## Answer to lesson 2 homework
``` py 
repeat = input("how many $ would you like? : ") #(1)

print("$" * int(repeat))                        #(2)
```

1.  python function `input` returns the value you enter on the terminal
2.  keyword `int` converts data type [string](../lesson1#variables) to data type int

Ouput
``` bash
> how many $ would like : 6
$$$$$$

```

## Breakdown of for-loop
Code
``` py
for i in range(10)          # (1)
    print(i)
```

1.  i is a variable of type int. you can name it anyway you like.

Output
``` bash
0
1
2
3
4
5
6
7
8
9
```

## Lab 1 - triagle
Use for loop and int keyword and python expression for printing * symbol six times e.g. `"*" * 6`

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
    for i in range(6)
        print("*" * i)
    ```

## Lab 2 - reversed triagle

=== "expected output 2"
    ```
    *****
    ****
    ***
    **
    *
    ```

=== "code 2"
    ``` py
    j = 5
    for i in range(5)
        x = j - i
        print("*" * x)
    ```