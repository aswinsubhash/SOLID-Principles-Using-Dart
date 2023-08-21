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

     *"There should never be more than one reason for a class to change"*

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
      
      - Identify **different responsibilities** in the given code. 
      - **Create separate classes** for each responsibility.
      - Ensure that each class **has only one** reason to change.
   
      Hope you got it. Ok fine let's look at the solution.

      ```dart
      class User {
        String name;
        String email;

        User(this.name, this.email);
      }
       ```
     ```dart
      class UserRepository {
        void saveUserToDatabase(User user) {
           // save user to the database
        }
      }
       ```

     ```dart
      class UserView {
        void showWelcomeMessage(User user) {
           print('Welcome, ${user.name}!');
         }
      }
       ```
      Let's have a look at what we did here.

      1. The original code violate the **Single Responsibility Principle** because the `User` class had more than one responsibility: **holding user data**, **saving user data** to the database, and **displaying** a welcome message to the user. This makes the class harder to maintain and modify in the future.
      2. In the refactored solution, we have separated the responsibilities into three different classes: `User`, `UserRepository` and `UserView`.
      3. `User` class is responsible for holding user data, `UserRepository` class is responsible for saving user data to the database, and `UserView` class is responsible for displaying a welcome message to the user.
      
      That's basically it. The **S** and the solid, which is the Single Responsibility Priciple.

      ### 2. Open/Closed Principle (OCP)

      *"Software entities...should be open for extension, but closed for modification"*

      Let's have a look at this piece of codes.

      ```dart
      class Shape {
        String type;

        Shape(this.type);
      } 
       ```
      ```dart
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

      - Identify the parts of the code **that changes** when a new type of object is introduced.
      - Create an **abstraction** (interface or abstract class) for these objects and define the behaviour that varies in this abstraction.
      - **Implement this abstraction** in each of the object classes, providing their own implementation of the behaviour.
      - Use the **abstraction instead of the concrete classes** where the behavior is needed.
      
      Did you succeed? Ok fine let's look at the solution.

  
     ```dart
      abstract class Shape {
        double calculateArea();
      }
      ```
    ```dart
      class Circle extends Shape {
        double radius;

        Circle(this.radius);

        @override
        double calculateArea() {
          return 3.14 * radius * radius; // πr²
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
    ```dart
      class AreaCalculator {
        double calculate(Shape shape) {
          return shape.calculateArea();
        }
      } 
       ```  


      So what have we learned from the refactoring?

      1. In the refactores solution, we have an abstract `Shape` class with **an abstract** calculateArea method.

         ```dart
         abstract class Shape {
           double calculateArea();
         }
         ```
      2. Then we have the `Circle` and `Square` classes, which are **concrete** implementation of the `Shape` class.
      3. Each of these classes overrides the `calculateArea()` method to provide it's own implementation.

         ```dart
         class Circle extends Shape {
           double radius;

           Circle(this.radius);

           @override
           double calculateArea() {
              return 3.14 * radius * radius; // πr²
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
      4. Finally, we have the `AreaCalculator` class that uses the `Shape` class to calculate the area, so it doesn't need to know the specific type of shape.

          ```dart
          class AreaCalculator {
             double calculate(Shape shape) {
                return shape.calculateArea();
             }
          }
          ```

      So, this is the solution.

      #### But what exactly was wrong with the code?
      #### What was bad with the code?

      - The bad code violated the Open/Closed Priciple because the `AreaCalculator` class was not closed for modification.

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
      - Every time we wanted to add a new shape, we had to modify the `AreaCalculator` class.
      - This made the class difficult to maintain and also increase the risk of introducing bugs.
     
     So as you've seen, the solution itself is actually very nice, very elegant and most importantly, very easy to use. Because it follows the Open/Closed Principle, the `AreaCalculator` itself doesn't have to change in the future.

### 3. Liskov Substitution Principle (LSP)

*"Functions that use pointers, or references to base classes, must be able to use objects of derived classes without knowing it"*

So, let's have a look at this piece of codes below.

```dart
abstract class Vehicle{
   void refuel();
   void move();
}
```
```dart
class ElectricCar extends Vehicle{

   @override
   void refuel(){
      print('Charging the battery...');
   }
      
   @override
   void move(){
      print('Moving...');
   }
}
 ```
```dart

class PetrolCar extends Vehicle{

  @override
  void refuel(){
     print('Refilling the petrol...');
  }
      
  @override
  void move(){
      print('Moving...');
  }
}
 ```
```dart
void serviceVehicle(Vehicle vehicle){
   vehicle.refuel();
      
   // some more servicing activities

}
 ```
   These set of codes violates the **Liskov Subsititution Priciple**.

   Let's look at some of hints to help you with figuring this out.

   **Hints:**

   1. Identify methods that aren't applicable to **all subclasses**.
   2. Consider splitting the superclass into more specific subclasses or interfaces.
   3. Ensure that each subclass can be used interchangeably with the superclass without causing any issues.

   Take some time and try to figure out.

   Did you succeeded? Ok fine let's look at the solution.

   ```dart
   abstract class Vehicle{
     void move();
   }

   abstract class FuelVehicle extends Vehicle {
     void refuel();
   }

   abstract class ElectricVehicle extends Vehicle {
     void recharge();
   }
   ```
   ```dart
   class ElectricCar extends ElectricVehicle {

     @override
     void recharge() {
        print('Recharging the car.....');
     }
   
     @override
     void move(){
        print('Electric car is moving...');
     }

   }

   class PetrolCar extends FuelVehicle{
     @override
     void refuel() {
       print('Refueling the car....');
     }
   
     @override
     void move() {
        print('Moving the petrol car...');
     }
   }
   ```
   ```dart
   void serviceFuelVehicle(FuelVehicle fuelVehicle){
      fuelVehicle.refuel();
      // some more servicing activities
   }

   void serviceElectricVehicle(ElectricVehicle electricVehicle){
      electricVehicle.recharge();
      // some more servicing activities
  }
   ```
  So, now let's have a look at what exactly have we done?

   1. In the refactored solution, we separated `FuelVehicle` and `ElectricVehicle` as two different abstractions, both extending `Vehicle`

      ```dart
      abstract class FuelVehicle extends Vehicle {
      void refuel();
      }

      abstract class ElectricVehicle extends Vehicle {
         void recharge();
      }
         ```
  2. This allows us to create **separate service methods** for each type of vehicle, ensuring that we don't attempt to perform an action that doesn't make sense for a particular type of vehicle.
   
   This is where the **Liskov Substitution Principle** is very important.
   
   You cannot really charge a car that needs fuel and you cannot fuel a car that needs charge.

   This was semantic problem.

   #### So, what was really wrong with the original code?

   - The original code violated the **Liskov Substitution Principle** because `ElectricCar`, as a subclass of `Vehicle`, wasn't truly substitutable for `Vehicle` in all situations.
   - Specifically, the `refuel()` method didn't make sense for `ElectricCar`.

   An electric car cannot be fueled because it needs to be charged.

   This is a semantic issue as in fact electric and petrol vehicles will need to be serviced differently.

   You even see this in real life where you have special charging stations for electric cars, which are different from gas station.

### 4. Interface Segregation Principle (ISP)

*"Clients should not be forced to depend upon interfaces that they do not use"*

So let's look at the bad code first

```dart
abstract class SmartDevice {
  void makeCall();
  void sendEmail();
  void browseInternet();
  void takePicture();
}
```
```dart
class SmartPhone implements SmartDevice {
  @override
  void makeCall() {
    print('Making a  call...');
  }

  @override
  void sendEmail() {
    print('Sending email...');
  }

  @override
  void browseInternet() {
    print('Browsing the internet');
  }

  @override
  void takePicture() {
    print('Taking a picture');
  }
}
```
Now let's have a look at another smart device.

```dart
class SmartWatch implements SmartDevice {
  @override
  void makeCall() {
    print('Making a call...');
  }

  @override
  void sendEmail() {
    throw UnimplementedError('This device cannot send emails');
  }

  @override
  void browseInternet() {
    throw UnimplementedError('This device cannot browse the internet');
  }

  @override
  void takePicture() {
    throw UnimplementedError('This device cannot take picture');
  }
}
```
So thechnically, we could say it does implement all the contract functions, but in reality it does not provide the functionality.

What you see here is that the `SmartWatch` only truly implements the `makeCall()` function.

#### So what is wrong with this code and how do we fix it?

**Hints:**

1. Identify methods in the interface that are not relevant to all classes implementing the inferface.
2. Split the interface into smaller, more specific interfaces.
3. Have each class implements only the interfaces it needs.

So let's look at the solution.

```dart
abstract class Phone {
  void makeCall();
}

abstract class EmailDevice {
  void sendEmail();
}

abstract class WebBrowser {
  void browseInternet();
}

abstract class Camera {
  void takePicture();
}
```
```dart
class SmartWatch implements Phone {
  @override
  void makeCall() {
    print('Making a call...');
  }
}
```
```dart
class SmartPhone implements Phone, EmailDevice, WebBrowser, Camera {
  @override
  void makeCall() {
    print('Making a  call...');
  }

  @override
  void sendEmail() {
    print('Sending email...');
  }

  @override
  void browseInternet() {
    print('Browsing the internet');
  }

  @override
  void takePicture() {
    print('Taking a picture');
  }
}
```
When you look at this, it seems to make a lot of sense.