---
layout: post
title:  "Programming With Types (Part 1)"
date:   2022-04-06 00:00:00 +0900
image:  '/assets/img/programming_with_types/cover.png'
tags:   [book,typescript,OOP,coding,web programming,tech]
---

One of the book I've read recently is called Programming With Types from Vlad Riscutia published by Manning Publications. <br /> <br />
I happened to purchase a bundle from [Humble Bundle](https://www.humblebundle.com) a while ago and I thought it was a good time to read it to strengthen my knowledge on Javascript Typescript (as used as examples in the books). <br /><br />
On this post, I will summarize the keys content of the book. I recommend you buy the book to read on for more details.

# Chapter 1: Introduction to Typing
This chapter basically defines some terminologies regarding to the Typing system. These can be summarized as the followings:

A **type** is a classification of data that defines the operations that can be
done on that data, the meaning of the data, and the set of allowed values.
Typing is checked by the compiler and/or run time to ensure the integrity of
the data, enforce access restrictions, and interpret the data as meant by the
developer.

A **type system** is a set of rules that assigns and enforces types to
elements of a programming language. These elements can be variables, functions,
and other higher-level constructs. 

The process of **type checking** ensures that the rules of the type
system are respected by the program. This type checking is done by the compiler
when converting the code or by the run time while executing the code.

The component of the compiler that handles enforcement of the typing rules
is called a **type checker**. If type checking fails, meaning that the rules of the type system are not respected by
the program, we end up with a failure to **compile error** or with a **run-time error**.

Benefits of type system:

1. **Correctness**: Correct code means code that behaves according to its specification, producing
expected results without creating run-time errors or crashes. Types help us add more
strictness to the code to ensure that it behaves correctly.

2. **Immutability** is another property closely related to viewing our running system as moving
through its state space. When we are in a known-good state, if we can keep parts of
that state from changing, we reduce the possibility of errors.

3. **Encapsulation** is the ability to hide some of the internals of our code, be it a function, a class, or a module.

4. Having the ability to combine independent components yields a modular system
and less code to maintain. **Composability** becomes important as the size of the code and the number of components increase

5. **Readability**: Instead of having to find the implementation or look up the documentation, just reading this declaration tells us exactly what type of arguments to pass and reduces our cognitive load, as we can treat it as a self-contained, separate entity.

With **static typing**, type checking is performed at compile time, so when compilation
is done, the run-time values are guaranteed to have correct types. **Dynamic typing**,
on the other hand, defers type checking to the run time, so type mismatches
become run-time errors.

**Strong typing** and **weak typing.** JavaScript is weakly typed. JavaScript provides two equality operators: ==, which checks whether two values are equal, and ===, which checks both that the values and the type of the values are equal

**Type inference**: In some cases, the compiler can infer the type of a variable or a function without us having to specify it explicitly.