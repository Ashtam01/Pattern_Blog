---
title: "The Art of Obscurity: A Tour of Esoteric Languages"
date: 2025-12-07
description: "Exploring Shakespeare, Chef, Piet, and building a Brainfuck interpreter in JavaScript."
tags: ["Compilers", "History", "JavaScript", "Engineering"]
math: true
---

Most programming languages are designed to be efficient, readable, and logical. We build systems in Go, Rust, and Python because they help us manage complexity.

But what happens when you design a language specifically to be **difficult, invisible, or artistic**?

Welcome to the world of **Esoteric Languages (Esolangs)**.

These languages serve no practical purpose other than to push the boundaries of language design and prove the concept of **Turing Completeness**: the idea that any system capable of a few basic data manipulations (conditional jumps and memory modification) can technically solve any computational problem in the universe.

## 1. Shakespeare (SPL)
**Creator:** Karl Hasselström and Jon Åslund (2001)

The Shakespeare Programming Language (SPL) is designed to make source code look exactly like a Shakespearean play. 

* **Variables** are characters (Romeo, Juliet, Hamlet).
* **Values** are determined by how "good" or "bad" a noun is. 
* **GOTO** statements are written as `Let us proceed to Scene III`.
* **Input/Output** involves "listening to your heart" or "speaking your mind".

### The "Hello World" Mechanism
Unlike Python's `print("Hello World")`, SPL requires you to define a `Dramatis Personae`, acts, and scenes just to print text.

```text
The Infamous Hello World Program.

Romeo, a young man with a remarkable patience.
Juliet, a likewise young woman of remarkable grace.

Act I: Hamlet's insults and flattery.
Scene I: The insulting of Romeo.

[Enter Hamlet and Romeo]
Hamlet:
 You lying stupid fatherless big smelly half-witted coward!
 You are as stupid as the difference between a handsome rich brave
 hero and thyself! Speak your mind!

[Exit Romeo]
[Enter Juliet]
Hamlet:
 Speak your mind!

 ```


## 2. Whitespace
**Creator:** Edwin Brady and Chris Morris (2003)

Most languages ignore spaces and tabs. **Whitespace** ignores everything *except* spaces and tabs.

The code is effectively invisible. You could hide a Whitespace program inside the source code of a normal C++ or Java program, and the compiler would simply ignore it, but the Whitespace interpreter would run it.

* **Space (S):** Stack Manipulation (Push/Duplicate).
* **Tab (T):** Arithmetic (Add/Subtract).
* **Line Feed (L):** Flow Control (Jumps/Subroutines).

### The Code
If you were to view the "Hello World" code in a standard editor, it would look like a blank page. However, if we replace Space with `S`, Tab with `T`, and LineFeed with `L`, the logic appears:

```text
S S S T	S S T	S S S L
T	L
S S S S S T	T	S S T	S T	L
T	L
S S S S S T	T	S T	T	S S L
T	L

```

## 3. Piet
**Creator:** David Morgan-Mar

Piet is a language where the source code is a **bitmap image**. It is named after the abstract painter Piet Mondrian.

* The pointer moves from one colored "blob" (codel) to another.
* The machine does not care about the color itself, but rather the **difference in hue and brightness** between the current color and the next.
* **Black pixels** trap the program (edges/walls).

A Piet program looks like modern art, but underneath, it is performing complex stack calculations based on color transitions.

## 4. Chef
**Creator:** David Morgan-Mar

Chef is designed to make code look like a cooking recipe. The core design principle is that the code should not only compile but also **produce a valid, edible recipe**.

* **Variables:** Ingredients.
* **Stack:** Mixing Bowls.
* **Operations:** "Mix", "Stir", "Bake".

```text
Hello World Souffle.

Ingredients.
72 g haricot beans
101 eggs
108 g lard
111 cups oil
32 zucchinis
...

Method.
Put potatoes into the mixing bowl.
Put lard into the mixing bowl.
Liquefy contents of the mixing bowl.
Pour contents of the mixing bowl into the baking dish.

```

## 5. Brainfuck (Interactive Interpreter)
**Creator:** Urban Müller (1993)

Brainfuck is the most famous esolang. It was designed to have the smallest possible compiler. It models a raw **Turing Machine**.

1.  A **Tape** of 30,000 zeros.
2.  A **Pointer** that moves left (`<`) or right (`>`).
3.  Operations to increment (`+`) or decrement (`-`) the value at the pointer.
4.  Loops (`[` and `]`).

### Try it Yourself
I have built a JavaScript interpreter below. The code inside is the standard "Hello World". It works by moving the memory pointer, incrementing values to match ASCII codes (e.g., 'H' is 72), and printing them.

{{< brainfuck >}}

### Engineering Breakdown: How the Interpreter Works
The interactive terminal above isn't magic; it's a Virtual Machine (VM) running in your browser's JavaScript engine.

**1. The Memory Tape:** We use a `Uint8Array` for performance, which automatically handles 8-bit wrapping (255 + 1 -> 0).
**2. Optimization:** Before running, I scan the code to map `[` to `]` so loops run in $O(1)$ time.
**3. CPU Cycle:** A simple `while` loop reads one character, executes it, and moves the instruction pointer.



