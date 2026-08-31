# CLAUDE.md

This repo is the mkdocs-material site for curiosityworks.org — Python lessons written by a tutor for one student. The lessons are the product; treat every edit as something a smart, eager middle-schooler will read.

## Teaching philosophy (the most important rules)

- Balance game-building excitement with Python foundations. Every game feature is a vehicle for a fundamental — name the fundamental in the lesson. The flagship example: code reusability via functions and passing in a variable/parameter.
- One big new idea per lesson. Everything else should be callbacks to prior lessons ("same `<` you've used since Lesson 2").
- English-first pseudocode before Python, always — plan in comments, "run it in your head," then translate line by line.
- Error messages are hints, not punishments. When a lesson shows an error, show the real traceback and read it.
- "Watch the numbers change": when a loop or animation is confusing, print/trace the variables.

## Voice and structure

- Lessons 3–5 are the canonical voice: narrative second person, warm, builds tension ("feel that copy-paste itch?") before revealing the tool. Match it. Lessons 1–2 and older stubs (lesson 6) are the pre-narrative style — rewrite toward the newer voice when touched, don't imitate them.
- Each lesson is three files in `docs/lessons/`: `lessonN.md`, `lessonN_reading.md` (extras + predict-then-run exercises), `lessonN_homework.md` (one program grown ~4 times, each problem = previous + one idea). Add all three to `nav` in `mkdocs.yml` following the lesson 1–5 pattern.
- Homework problems state the expected output/drawing, then hints — never full solutions.

## After a live session

- Lesson pages get revised to match what was **actually taught**, keeping the tutor's exact code, naming, and comments so the student recognizes them — even if a "cleaner" version exists. Gentle improvements go in as asides ("that's a `for` loop waiting to happen — try it").
- Concepts that got skipped move to the next lesson's tease or the homework; fix any reading/homework references to skipped material.

## Technical

- Python turtle requires a local Python install (python.org build ships tkinter); the web editor / Chromebook option cannot run it. Lessons that need a window should say so.
- Verify every code snippet actually runs (or at least compiles) before publishing. This machine's Homebrew Python lacks tkinter — check turtle API names against the stdlib source instead of importing.
- Validate changes with `mkdocs build` before finishing.
