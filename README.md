# SOLID Principles Using Dart and Top Design Patterns

## 1. Introduction

### What are Design Patterns and why do we need them?

#### What are they?

- Desing patterns are well tested, reusable solution.
- They are like a **solution template** for how to solve common software engineer ploblems.
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

*Here are the patterns that we are going to learn:*

1. Creational
   - Singleton Pattern
   - Factory Method Pattern
   - Builder Pattern

**Creational Design Patterns** are design patterns that manage **object creation** mechanisms. They are desinged to create **objects** in flexible and highly adaptable ways. These patterns offer the most reusable and flexible ways of creating object instances.

2. Structural
   - Adapter Pattern

**Structural Design Patterns** are design patterns that **improves** and **simplify** your designs by identifying the most **most efficient** and **reusable** way to composing relationships among entities. **This allows for the best and most efficient ways of creating complex hierarchies of objects**.

3. Behavioral
   - Strategy Pattern
   - Observer Pattern
   - State Pattern

**Behavioral Design Patterns** are design patterns that **imporves interation** and **communication** between objects. These patterns offer **loosely coupled** ways of allowing objects to talk to each other and exchange messages.

Once you master these patterns you will immediately see the world of coding differently. **You will start seeing those patterns everywhere**.

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

## 2. S.O.L.I.D Design Principles

**SOLID** Principles of object-oriented programming.

 1. **Single-responsibility principle**: *There should never be more than one reason for a class to change.* Each class should have only one central responsibility.
 2. **Open-closed principle**: *Software entities...should be open for extension, but closed for modification.*
 3. **Liskov substitution principle**: *Functions that use pointers, or references to base classes, must be able to use objects of derived classes without knowing it.*
 4. **Interface segregation principle**: *Clients should not be forced to depend upon interfaces that they do not use.*
 5. **Dependency inversion principle**: *Depend upon abstractions, [not] concretions.*

     ### 1. Single Responsibility Principle (SRP)

     Let's look at a class that violates the SRP.

     ```dart
     class User {
       String name;
       String email;

       User(this.name, this.email);

       void saveUserToDatabase() {
          // save user to the database
       }

       void showWelcomeMessage() {
          print('Welcome, $name!');
       }
     }
      ```

      We have a single class that has some data and it has two functions or two methods.

      Take some time and think about how does this class violate the **Single Responsibility Principle**?

      Ok... Here's the hints as follows to identify different responsibilities in the given code.

      **Hints:**
      
      1. Identify **different responsibilities** in the given code. 
      2. **Create separate classes** for each responsibility.
      3. Ensure that each class **has only one** reason to change.
   
      Hope you got it. Ok fine let's look at the solution.

      ```dart
      class User {
        String name;
        String email;

        User(this.name, this.email);
      }

      class UserRepository {
        void saveUserToDatabase(User user) {
           // save user to the database
        }
      }

      class UserView {
        void showWelcomeMessage(User user) {
           print('Welcome, ${user.name}!');
         }
      }
       ```
      Let's have a look at what we did here.

      4. The original code violate the **Single Responsibility Principle** because the `User` class had more than one responsibility: **holding user data**, **saving user data** to the database, and **displaying** a welcome message to the user. This makes the class harder to maintain and modify in the future.
      5. In the refactored solution, we have separated the responsibilities into three different classes: `User`, `UserRepository` and `UserView`.
      6. `User` class is responsible for holding user data, `UserRepository` class is responsible for saving user data to the database, and `UserView` class is responsible for displaying a welcome message to the user.
      
      That's basically it. The **S** and the solid, which is the Single Responsibility Priciple.

      ### 2. Open/Closed Principle (OCP)

      Let's have a look at this piece of code.

      ```dart
      class Shape {
        String type;

        Shape(this.type);
      }

      class AreaCalculator {
        double calculateArea(Shape shape) {
          if (shape.type == 'circle') {
             // calculate area of circle
          } else if (shape.type == 'square') {
            // calculate area of square
          }
            // ...
        }
      } 
       ```
      This code is Pretty Bad, it violates **Open/Closed Principle**

      Take some time and think about how does this class violate the **Open/Closed Principle**?

      Did you get it? Ok fine let's look at the hints and try again.

      **Hints:**

      7. Identify the parts of the code **that changes** when a new type of object is introduced.
      8. Create an **abstraction** (interface or abstract class) for these objects and define the behaviour that varies in this abstraction.
      9. **Implement this abstraction** in each of the object classes, providing their own implementation of the behaviour.
      10. Use the **abstraction instead of the concrete classes** where the behavior is needed.
      
      Did you succeed? Ok fine let's look at the solution.

      ```dart
      abstract class Shape {
        double calculateArea();
      }

      class Circle extends Shape {
        double radius;

        Circle(this.radius);

        @override
        double calculateArea() {
          return 3.14 * radius * radius;
        }
      }
      class Square extends Shape {
        double side;

        Square(this.side);

        @override
        double calculateArea() {
          return side * side;
        }
      }

      class AreaCalculator {
        double calculate(Shape shape) {
          return shape.calculateArea();
        }
      }   
       ```

      So what have we learned from the refactoring?

      11. In the refactores solution, we have an abstract `Shape` class with **an abstract** calculateArea method.

      ```dart
      abstract class Shape {
        double calculateArea();
      }
      ```
      12. Then we have the `Circle` and `Square` classes, which are **concrete** implementation of the `Shape` class.
      13. Each of these classes overrides the `calculateArea()` method to provide it's own implementation.

      ```dart
      class Circle extends Shape {
        double radius;

        Circle(this.radius);

        @override
        double calculateArea() {
          return 3.14 * radius * radius;
        }
      }

      class Square extends Shape {
        double side;

        Square(this.side);

        @override
        double calculateArea() {
          return side * side;
        }
      }
      ```
      4. 