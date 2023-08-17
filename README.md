# SOLID Principles and Top Design Patterns

- [SOLID Principles and Top Design Patterns](#solid-principles-and-top-design-patterns)
  - [Introduction](#introduction)
    - [What are Design Patterns and why do we need them?](#what-are-design-patterns-and-why-do-we-need-them)
      - [What are they?](#what-are-they)
      - [Why use them?](#why-use-them)
      - [Summary](#summary)
    - [The WHY of Software Architecture](#the-why-of-software-architecture)
  - [S.O.L.I.D Design Principles](#solid-design-principles)

## Introduction

### What are Design Patterns and why do we need them?

#### What are they?

- Desing patterns are well tested, reusable solution.
- They are like a <u>solution template</u> for how to solve common software engineer ploblems.
- They are flexible and adaptable.
- They save time because they are optimal.

#### Why use them?

- You know that you are using something that has been utilized successfully in countless projects before.
- They are like a common meta-language for developers. If you and I both know what a **Singleton Pattern** is then we already have a common understanding of everything about how it would be used or how it should be implemented. You can think of a pattern as a common vocabulory for architects.
- In other words we are on the same page. And this is powerful.
- If you understand a pattern in a general manner, then you know that regardless of the language implementation, it will effectively offer the same useful solution.

#### Summary

- Design Patterns are associated with good, well organized Software Design.
- As developers, we are prone to mistakes and sometimes inexperienced decisions.
- Think of design patterns as a bag of reusable experience from many generation of coders and Software Engineers.

*Here are the patterns that we will are going to learn:*

1. Creational
   - Singleton Pattern
   - Factory Method Pattern
   - Builder Pattern

**Creational Design Patterns** are design patterns that manage **object creation** mechanisms. They are desinged to create **objects** in flexible and highly adaptable ways. These patterns offer the most reusable and flexible ways of creating object instances.

2. Structural
   - Adapter Pattern

**Structural Design Patterns** are design patterns that <u>improves</u> and <u>simplify</u> your designs by identifying the most <u>most efficient</u> and <u>reusable</u> way to composing relationships among entities. <u>This allows for the best and most efficient ways of creating complex hierarchies of objects.</u>

3. Behavioral
   - Strategy Pattern
   - Observer Pattern
   - State Pattern

**Behavioral Design Patterns** are design patterns that <u>imporves interation</u> and <u>communication</u> between objects. These patterns offer **<u>loosely coupled</u>** ways of allowing objects to talk to each other and exchange messages.

Once you master these patterns you will immediately see the world of coding differently. <u>You will start seeing those patterns everywhere.</u>

*Just remember these pattern families:*

**Creational:** Deals with wasy of creating objects or families of objects.

**Structural:** Deals with wasy of managing complex objects hierarchies.

**Behavioral:** Deals with wasy of identifying and improving object messaging.

### The WHY of Software Architecture

Complex software systems are plagued with many issues:

   1. **Timelines are streched** as requirements changes.
   2. Mulitple developers have **hard time coordinating** their efforts.
   3. Often there is **Code redundancy** and poor documentation.

This in turn creates issues with **maintenance** and overall flexibility for **adding new features**.

In general, this means poorly desined systems that are hard to maintain, and **are not adaptable**.

One answer to all the cited problems is having a proper
***design and architecture***.

**Let's look at an example**

Think of a large building being built.

There is always a **high-level blueprint**.

This blueprint is used to show everbody involved (from architects, to supply chain, to construction workers, to machinery scheduling etc...) what is being worked on.

We want that kind of predictability and coherence in our **Software Projects**.

## S.O.L.I.D Design Principles

**SOLID** Principles of object-oriented programming.

 1. **<u>S</u>ingle-responsibility principle**: *There should never be more than one reason for a class to change.* Each class should have only one central responsibility.
 2. **<u>O</u>pen-closed principle**: *Software entities...should be open for extension, but closed for modification.*
 3. **<u>L</u>iskov substitution principle**: *Functions that use pointers, or references to base classes, must be able to use objects of derived classes without knowing it.*
 4. **<u>I</u>nterface segregation principle**: *Clients should not be forced to depend upon interfaces that they do not use.*
 5. **<u>D</u>ependency inversion principle**: *Depend upon abstractions, [not] concretions.*
