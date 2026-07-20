# Lesson 2 homework

This homework combines everything so far: `for` loops, `if`/`else`, and `%`.

A quick math reminder: a **prime number** is a number greater than 1 whose only divisors are 1 and itself. So 7 is prime, but 9 is not (3 divides it). 0 and 1 are not prime.

## Find the primes from 0 to 15

Write a program that prints every prime number from 0 to 15.

The idea: for each number, try dividing it by 2, then 3, then 4, and so on. If any divisor leaves remainder 0, the number is not prime.

Why isn't checking 2 enough? Watch what happens with 9:

```python
9 % 2 == 0   # does 2 divide 9?  False — so far 9 looks prime...
9 % 3 == 0   # does 3 divide 9?  True  — caught! 9 = 3 × 3
```

9 sneaks past the even/odd test, but the very next divisor catches it. That is why we try **every** divisor, not just 2.

Here is a block that checks one number:

```python
number = 9
is_prime = True
for divisor in range(2, number):
    if number % divisor == 0:
        is_prime = False
if is_prime:
    print(number)
```

Read it line by line: start by assuming the number is prime, let the loop try every divisor from 2 up to the number, and flip `is_prime` to `False` if any divisor leaves remainder 0. If `is_prime` survives the loop, the number gets printed.

Your job: make this run for **every** number from 2 to 15. The plain way — copy the block, paste it, change `number = 9` to the next number. Again. And again.

* Make as many mistakes as you like
* Don't give up

Output
```
2
3
5
7
11
13
```

While you are copy-pasting block number twelve, notice the feeling: *there has to be a smarter way.* You felt it once before — in Lesson 1, when we printed `phrase` eight times. Bring that feeling to the next class.
