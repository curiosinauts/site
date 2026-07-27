# Lesson 3 homework

Three triangles. Every one of them is the star triangle from the lesson with **different numbers** — the pseudocode barely changes; only the math does.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Make a have/want table: what does the loop give you, what does the row need?
3. Find the math that turns have into want
4. Translate to Python

* Make as many mistakes as you like
* Don't give up

## Problem 1 — upside down

Flip the lesson's triangle: the widest row comes first.

Output

```
**********
*********
********
*******
******
*****
****
***
**
*
```

Code

* Start from the star triangle program — the pseudocode is the same, one number changes
* Have/want table: `row_num` goes 1, 2, 3, ... — but row 1 needs **10** stars, row 2 needs **9**, row 3 needs **8**...
* What math turns 1 into 10, 2 into 9, and 3 into 8?

## Problem 2 — slope on the left

Same triangle as the lesson, but leaning the other way: the slope runs from top-left down to bottom-right, and the straight edge is on the right.

Output

```
         *
        **
       ***
      ****
     *****
    ******
   *******
  ********
 *********
**********
```

Code

* Look carefully at row 1: the star is pushed to the right by **spaces**. A space is a real character, and you can print it: `print(" ", end="")`
* Each row now has **two parts**: first the spaces, then the stars. Two parts means two inner loops, one after the other, inside the outer loop
* Write the pseudocode for the two parts first, then make **two** have/want tables — one for spaces, one for stars
* Count from the output: row 1 has 9 spaces + 1 star, row 2 has 8 spaces + 2 stars... row 10 has 0 spaces + 10 stars

## Problem 3 — upside down, slope on the left

Now flip problem 2: widest row first, straight edge still on the right.

Output

```
**********
 *********
  ********
   *******
    ******
     *****
      ****
       ***
        **
         *
```

Code

* Same two-part rows as problem 2 — only the math changes
* Count the spaces and stars in the first few rows and build the have/want tables
* If your problem 1 and problem 2 tables were right, this one is just combining them

When all three run, look at your four programs side by side — the lesson's triangle and these three. Same pseudocode, same skeleton, four different pictures. That is what the have/want math controls.
