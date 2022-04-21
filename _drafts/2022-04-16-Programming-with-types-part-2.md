---
layout: post
title:  "Programming With Types (Part 2)"
date:   2022-04-16 00:00:00 +0900
image:  '/assets/img/programming_with_types/cover.png'
tags:   [book,typescript,]
---

# Chapter 3: Composition

In previous chapter, we looked at some common primitive types that form the building
blocks of a type system. In this chapter, we’ll look at ways to combine them to
define new types.

The chapter of this book will cover compound types as well as other some common types such as optional types, either types,
and variants, as well as a few applications of these types.

*(This post does not cover everything from the book and will summarize in the easiest way possible. If you are interested in the book, I recommend to purchase them for further reading.)*

### Compound Types

It's obviously to combine types by **grouping** them to form a new types. An example would be a **coordinate** of a plane, which consists of two separated X and Y numbers, combining them into a new type which gives a pair of numbers.
![figure 3.1.png](/assets/img/programming_with_types/figure%203.1.png)

1. **Tuples**

    Tuple types consist of a set of component types, which we can
    access by their position in the tuple. Tuples provide a way to group data in an
    ad hoc way, allowing us to pass around several values of different types as a
    single variable.

    Using tuples, we can pass around pairs of X and Y coordinates together as points. This
    makes the code both easier to read and easier to write.
      
    ```javascript
      type Point = [number, number];
    ```
    <br />
    Most languages offer tuples as built-in syntax or as part of their library, but let’s look at
    how we would implement a tuple if it were unavailable.
    
    ```javascript
      class Pair<T1, T2> {
        m0: T1;
        m1: T2;

        constructor(m0: T1, m1: T2) {
          this.m0 = m0;
          this.m1 = m1;
        }
      }

      type Point = Pair<number, number>;
    ```

2. Assigning meaning

    Defining points as pairs of numbers works, but we lose some meaning: we can interpret
    a pair of numbers as either X and Y coordinates or Y and X coordinates. This is better as we can 
    encode the meaning within the type system and ensure that there is no room to misinterpret
    X as Y or Y as X.

    ```javascript
    class Point {
      x: number;
      y: number;

      constructor(x: number, y: number) {
        this.x = x;
        this.y = y;
      }
    }
    ```

3. Maintaining invariants

    In languages in which record types can have associated methods, there is usually a way
    to define the visibility of their members. A member can be defined as public (accessible
    from anywhere), private (accessible only from within the record), and so on.
    In TypeScript, members are public by default.

    In order to not cause unnecessary errors, we can make members to be **private** and provide methods to access or change them under a specific rule, or we can put **read-only** so those members cannot be modified after initialization.

    ```javascript
      class Currency {
        private dollars: number = 0;
        private cents: number = 0;
        
        constructor(dollars: number, cents: number) {
          this.assignDollars(dollars);
          this.assignCents(cents);
        }
        
        getDollars(): number {
          return this.dollars;
        }
      }
    ```
    
### Expressing either-or with types

Another fundamental way in
which we can combine types is either-or, in which a value is any one of a possible set of
values of one or more underlying types
### The visitor pattern

### Algebraic data types

