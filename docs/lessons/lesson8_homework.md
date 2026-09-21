# Lesson 8 homework

This week you build a world you can explore — a map far bigger than the window, a player who walks around it, and a camera that follows.

By Problem 4 you'll have something that is, honestly, the skeleton of a real game. It's the piece your own project has been waiting for.

One program, grown four times. Each problem is the last one plus one idea.

Work like a programmer on each one:

1. Write the pseudocode in English first
2. Run it in your head before you run it in Python
3. Translate line by line

* Make as many mistakes as you like
* Don't give up

Start from the lesson's program, exactly as you left it.

## Problem 1 — build a world worth exploring

Four trees isn't a world. Make a real one, and make the computer place it for you.

What you should see: drive the camera around with the arrow keys and discover trees scattered far beyond the edges of the window — in every direction, well past where you can see at the start.

Code

* A named world, at the top with your other constants:

    ```python
    WORLD_SIZE = 2000
    HALF_WORLD = WORLD_SIZE // 2
    ```

    Note the `//` — floor division, from the Lesson 1 reading. You'll see why in a moment

* Build the list with a `for` loop instead of typing it out — Lesson 3's loop, Lesson 4's list, Lesson 6's reading's `random`, all at once:

    ```python
    trees = []

    for i in range(60):
        x = random.randint(-HALF_WORLD, HALF_WORLD)
        y = random.randint(-HALF_WORLD, HALF_WORLD)
        trees.append(Tree(x, y, random.choice(COLORS)))
    ```

* **Expect an error here, and read it.** If you wrote `WORLD_SIZE / 2` with a single slash, `randint` refuses:

    ```
    TypeError: 'float' object cannot be interpreted as an integer
    ```

    Lesson 1's reading told you why: `/` **always** hands back a float, so `2000 / 2` is `1000.0`, not `1000`. And `randint` counts in whole numbers — you can't ask for a random tree at position 4.7. Use `//`, which throws the decimal away, or wrap it in `int()`. A real error, from a real rule you learned in Lesson 1, biting you seven lessons later
* `COLORS` is a list of your choosing — `["green", "darkgreen", "olive", "brown"]` makes a believable forest
* Don't forget `import random` at the top
* Now the test that proves the camera is real: the window is 600 across and the world is 2000. Drive right, and keep driving. Do trees keep coming? Can you get to a place where there's nothing but background? Both answers should be yes

## Problem 2 — a player in the world

Right now you're a floating eye. Time to put someone in the world.

The player is a thing with a **world position**, just like a tree — and the camera has to translate it like everything else. That's the part worth getting right.

What you should see: a red turtle standing in the middle of the window. Drive the camera with the arrow keys and the player stays put **in the world** — so it slides across the window and off the edge as the camera moves away, exactly as the trees do.

Code

* Two more globals, next to the camera: `player_x = 0` and `player_y = 0` — world coordinates, same as a tree's
* A second turtle for the player, so it can be drawn separately from the stamped forest: `player = turtle.Turtle()`, `player.shape("turtle")`, `player.color("red")`, `player.penup()`
* At the end of `redraw()`, put the player where the camera says it goes:

    ```python
    player.goto(to_screen_x(player_x), to_screen_y(player_y))
    ```

* Predict before you run: when `cam_x` and `player_x` are both `0`, where on the window does the player appear? Check that your prediction is right before moving on — this is the idea the rest of the homework stands on
* If the player sits frozen at the center of the window no matter where you drive, you've drawn it at `(player_x, player_y)` without translating. That's the classic bug, and now you know its face

## Problem 3 — move the player, and let the camera follow

Swap it around. The arrow keys should move the **player** through the world. The camera's job is to follow.

What you should see: the player stays dead center in the window, always. The forest streams past underneath as you walk. Walk in any direction as long as you like and the world keeps coming.

Code

* Rename the four movers to say what they now do — `walk_right`, `walk_left`, `walk_up`, `walk_down` — and have them change `player_x` / `player_y` instead of the camera. Each one still needs its `global` line, now naming the player
* Then the follow, one line, and it's the whole idea of a camera in a game:

    ```python
    def update_camera():
        global cam_x, cam_y
        cam_x = player_x
        cam_y = player_y
    ```

    (One `global` statement can name several variables, separated by commas)
* Call `update_camera()` inside each mover, **before** `redraw()`. Order matters: move the player, then point the camera, then draw
* Now run the numbers in your head and predict what you'll see. If `cam_x` always equals `player_x`, then `to_screen_x(player_x)` is `player_x - cam_x`, which is... what? So where does the player always appear? Confirm your prediction on screen — and notice you've just explained why Mario is always in the middle of the screen
* Bonus, one word each: swap the four `onkey` calls for `onkeypress` (from the reading) so you can hold a key down and keep walking

## Problem 4 — fence the world, and skip what you can't see (stretch)

Two finishing touches, and they're both callbacks.

**First, the edge of the world.** The player can currently walk forever into empty blackness. Fence the world in — Lesson 7's arena, except now the walls are at the edges of a 2000-pixel world instead of the edges of the window.

**Second, culling.** Stop drawing trees that aren't on screen.

What you should see: for the fence — walk to the edge of the forest and stop dead, in all four directions, with trees still visible around you. For culling — no visible change at all. That's the point.

Code

* The fence is Homework 7, Problem 4, moved into world coordinates. Your `is_out_of_bounds` becomes a question about the *player's* world position against `HALF_WORLD`, and the fix is to clamp `player_x` / `player_y` back
* Write it as its own function — `keep_player_in_world()` — and call it from each mover, before `update_camera()`. Move, fence, aim the camera, draw: four steps, in that order, every time
* Culling is the reading's `is_on_screen(thing)` — a function returning one boolean built from two `and`ed range checks — plus one `if` inside the redraw loop
* Prove culling works, because "no visible change" is a hard thing to trust. Count what you drew:

    ```python
    drawn = 0
    for tree in trees:
        if is_on_screen(tree):
            ...
            drawn += 1
    print(drawn, "of", len(trees))
    ```

    Walk around and watch that first number rise and fall while the second never moves. (`len(trees)` hands back how many items a list holds — a function that *answers*, just like the ones you've been writing.) Then crank `range(60)` up to `range(2000)` and see whether the program still feels smooth
* Bonus: put the count on the window instead of the terminal, with a third `penup` turtle parked in a corner doing `write` — a heads-up display, which is what a score will be

When all four run, sit back and look at it. A world the computer built, bigger than the screen. A player walking through it. A camera following. Only the visible part being drawn. Walls at the edges of the world.

Strip out the trees and put in a maze — that's a dungeon crawler. Make the camera lag a little behind the player instead of snapping to it — that's every platformer you've played. Make the world a grid of tiles instead of scattered objects — that's Pokémon.

You have the engine now. Your side project just got a lot more interesting.
