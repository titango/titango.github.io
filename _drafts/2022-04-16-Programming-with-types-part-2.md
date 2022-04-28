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

1. Enumerations

    We can present a number of day in a week using enum type such as 
    ```javascript
    enum DayOfWeek {
      Sunday,
      Monday,
      Tuesday,
      Wednesday,
      Thursday,
      Friday,
      Saturday
    }
    ```
    This has the advantage as Countries such as the United States, Canada, and Japan consider Sunday to be the
    first day of the week, whereas the ISO 8601 standard and most European countries
    consider Monday to be the first day of the week. With this approach, there is no ambiguity about what is Monday and what is Sunday,
    as they are spelled out in the code.

2. Optional Types

    An **optional type**, also known as a maybe type, represents an
    optional value of another type T. An instance of the optional type can hold a
    value (any value) of type T or a special value indicating the absence of a value
    of type T.

3. Variants

    **Variant types**, also known as tagged union types, contain a value
    of any number of underlying types. Tagged comes from the fact that even if
    the underlying types have overlapping values, we are still able to tell exactly
    which type the value comes from.

    Let's take a look at an example. Here we have 3 classes preresent 3 shapes: **Point**, **Circle**, and **Rectangle**.
    These classes have a readonly `kind` string to represent their types.

    ```javascript
    class Point {
      readonly kind: string = "Point";
      x: number = 0;
      y: number = 0;
    }
    
    class Circle {
      readonly kind: string = "Circle";
      x: number = 0;
      y: number = 0;
      radius: number = 0;
    }

    class Rectangle {
      readonly kind: string = "Rectangle";
      x: number = 0;
      y: number = 0;
      width: number = 0;
      height: number = 0;
    }
    ```

    If we want to group into an array called `Shape` including all these classes object. We can do the followings:

    ```javascript
    type Shape = Point | Circle | Rectangle;
    let shapes: Shape[] = [new Circle(), new Rectangle()];
    ```
    
    And then we iterate over the shapes and check the kind property of each. 
    Let’s implement a simple variant that can store a value of up to three types and
    keep track of the actual type stored based on a type index.

    ```javascript
    class Variant<T1, T2, T3> {
      readonly value: T1 | T2 | T3;
      readonly index: number;
      private constructor(value: T1 | T2 | T3, index: number) {
        this.value = value;
        this.index = index;
      }
      static make1<T1, T2, T3>(value: T1): Variant<T1, T2, T3> {
        return new Variant<T1, T2, T3>(value, 0);
      }
      static make2<T1, T2, T3>(value: T2): Variant<T1, T2, T3> {
        return new Variant<T1, T2, T3>(value, 1);
      }
      static make3<T1, T2, T3>(value: T3): Variant<T1, T2, T3> {
        return new Variant<T1, T2, T3>(value, 2);
      }
    }
    ```

    We can safely remove the `kind` readonly attribute, and we can take a look at the following code to how declare an array of shapes

    ```javascript
    type Shape = Variant<Point, Circle, Rectangle>;
    let shapes: Shape[] = [
      Variant.make2(new Circle()),
      Variant.make3(new Rectangle())
    ];
    for (let shape of shapes) {
      switch (shape.index) {
        case 0:
          let point: Point = <Point>shape.value;
          console.log(`Point ${JSON.stringify(point)}`);
          break;
        case 1:
          let circle: Circle = <Circle>shape.value;
          console.log(`Circle ${JSON.stringify(circle)}`);
          break;
        case 2:
          let rectangle: Rectangle = <Rectangle>shape.value;
          console.log(`Rectangle ${JSON.stringify(rectangle)}`);
          break;
        default:
          throw new Error();
      }
    }
    ```

    This implementation might not look as though it adds a lot of benefit; we ended up
    using numeric tags and arbitrarily decided that 0 is a Point and 1 is a Circle. We
    might also wonder why the book didn’t use a class hierarchy for our shapes, where we have a
    base method that each type implements instead of switching on tags.
  
    For that task, we need to take a look at the visitor design pattern and the ways in
    which it can be implemented.

### The visitor pattern

### Algebraic data types

