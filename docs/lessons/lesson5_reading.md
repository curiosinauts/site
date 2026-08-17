# Lesson 5 reading

The lesson gave you the skeleton: a window, a function of your own, and a square gliding across the screen. This reading is the paint and wheels — the turtle functions that make things *look* good. Every one of them is just another function call, the shape you already know: a name, parentheses, maybe an input.

## Make it look like a turtle

```python
t.shape("turtle")
```

The arrow becomes an actual little turtle. Small thing, instant charm.

## Speed

```python
t.speed(1)   # slowest
t.speed(6)   # normal
t.speed(0)   # FASTEST — zero is special
```

`1` is a crawl and `10` is fast, but `0` is a special value meaning *no animation at all* — the drawing just appears. Use `t.speed(0)` when a drawing has lots of lines (you'll want it for the homework spiral).

## Pen thickness and color

```python
t.pensize(5)
t.pencolor("red")
```

Lines come out thick and red until you change them again. Colors are strings — `"red"`, `"blue"`, `"green"`, `"orange"`, `"purple"`, `"hotpink"` and dozens more all work by name.

The window background belongs to the *screen*, not the turtle — so that function lives on `screen`:

```python
screen = turtle.Screen()
screen.bgcolor("black")
```

Black background, `"cyan"` pen, `t.speed(0)` — instant neon.

## Lifting the pen

The turtle draws because its pen is down. You can lift it, move without drawing, and put it back down:

```python
t.penup()
t.forward(100)   # moves, no line
t.pendown()
t.forward(100)   # draws again
```

This is how you draw two shapes with a *gap* between them — and it's exactly what the animation loop did every frame: pen down to draw the square, pen up to walk to the next spot without leaving a smear.

## Jumping to a spot: `goto` and the map of the window

```python
t.goto(100, 50)
```

The turtle walks straight to the point (100, 50). The window is a coordinate plane, exactly like math class: **(0, 0) is the center** of the window, x grows to the right, y grows upward, negative numbers go the other way.

```
                 (0, 200)
                    |
(-200, 0) ----- (0, 0) ----- (200, 0)
                    |
                (0, -200)
```

`goto` draws a line on the way there like any other move — combine it with `penup` to *teleport*:

```python
t.penup()
t.goto(-100, -100)
t.pendown()
```

That pattern — up, goto, down — is how you place shapes wherever you want. You'll use it constantly.

## Circles and dots

```python
t.circle(50)     # circle with radius 50, drawn from the bottom
t.dot(20)        # filled dot, 20 across, right where the turtle stands
```

A circle for a face, two dots for eyes — you can already see where this goes.

## Title

One for the screen, because every game needs a name in the title bar:

```python
screen.title("Turtle Hero")
```

## Try it

Same rules as always: **predict first, then run.** For each one, say out loud what the window will look like before you press Run — where the turtle starts, what color, what gets drawn.

```python
import turtle

t = turtle.Turtle()
t.shape("turtle")
t.pencolor("blue")
t.pensize(3)

t.circle(50)

turtle.done()
```

```python
import turtle

t = turtle.Turtle()
t.speed(0)

t.penup()
t.goto(-150, 0)
t.pendown()
t.forward(300)

turtle.done()
```

```python
import turtle

t = turtle.Turtle()
screen = turtle.Screen()
screen.bgcolor("black")
t.pencolor("cyan")

for i in range(4):
    t.forward(100)
    t.left(90)

t.penup()
t.goto(50, 50)
t.dot(20)

turtle.done()
```

One habit worth keeping: when a drawing surprises you, it's the turtle's *position* or *heading* you've lost track of. Slow it down — `t.speed(1)` — and watch it move. That's "watch the numbers change" from Lesson 3, in picture form.
