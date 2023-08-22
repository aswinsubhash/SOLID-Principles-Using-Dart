# SOLID Principles Using Dart 

## Introduction

In the realm of software development, creating applications that are robust, maintainable, and scalable is an art. The **SOLID** principles are guiding lights on this path, illuminating the way to crafting effective software solutions.

In this article, we explore the core concepts of the SOLID principles. From the Single Responsibility Principle to the Dependency Inversion Principle, we unravel how these principles contribute to adaptable and functional code.
Discover how each SOLID principle becomes a cornerstone for software that thrives amidst changing requirements.

Whether you're a developer or an architect, this article provides actionable insights and a fresh perspective on integrating SOLID principles into your coding practices. Let's journey into the world of SOLID principles and unlock the secrets to crafting exceptional software.
 
 ## SOLID principles in object oriented programming

  ### 1. Single Responsibility Principle (SRP)

  *"There should never be more than one reason for a class to change"*. Each class should have only one central responsibility.

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
      
  Did you succeed? 
      
  Ok fine let's look at the solution.

  
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

   Did you succeeded? 
   
   Ok fine let's look at the solution.

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
So technically, we could say it does implement all the contract functions, but in reality it does not provide the functionality.

What you see here is that the `SmartWatch` only truly implements the `makeCall()` function.

#### How do we fix it?

**Hints:**

1. Identify methods in the interface that are not relevant to all classes implementing the interface.
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

Yes, we have more interfaces, but we are not forcing classes to implement interfaces that they do not need.

Let's recap the refactores solution.

1. In the refactored solution, the `SmartDevice` interface is segregated into four interfaces: `Phone`, `EmailDevice`, `WebBrowser` and `Camera`.
2. The `SmartPhone` class implements all four interfaces while the `SmartWatch` class implements only the `Phone` interface.
3. This way, the `SmartWatch` class is not forced to implement the `sendMail()`, `browseInternet()` and `takePicture()` methods, which it doesn't need.

#### What's wrong in the original code?

1. The original (bad) code violated to  **Interface Segregation Principle** because it forced the `SmartWatch` class to depend on methods that it didn't use.
2. This made the `SmartWatch` class implement methods throwing an `UnimplementedError`, which could lead to runtime errors.

Let's move to the final topic of **S.O.L.I.D**

### 5. Dependency Inversion Principle (DIP)

*"Depend upon abstractions, [not] concretions"*

Let's look at the bad code first

```dart
class User {
  String name;

  // Other propertise

  User(this.name);
}
```
```dart
class MySQLDatabase {

  void saveUser(User user) {
    print('Saving ${user.name} to MySQL database...');

    // Actual implementation...
  }
}
```
```dart
class UserService {
  MySQLDatabase database;

  UserService(this.database);
}
```
Seemingly, this is good design since we've abstracting the database access behind the `UserService` class but we can definitely make this little architecture much better.

The current code violates the **Dependency Inversion Principle**, so by eliminating that issue, we will make this code better.

**Hints:**

1. Identify direct dependencies between high level and low level modules in your code.
2. Introduce an interface or abstract class to decouple these modules. 
3. Modify the high level module to depend on the abstraction, not on the low level module.
4. Implement the abstraction in each low level module.
5. Use dependency injection to provide the low level module to the high level module.

So here the question for you would be which one is the high level module and which one is the low level module in this code?

So let's look at with a refactored solution.

```dart
class User {
  String name;
  // Other propertise
  User(this.name);
}
```

```dart
abstract class Database {
  void saveUser(User user);
}
```

```dart
class MySQLDatabase implements Database {
  void saveUser(User user) {
    print('Saving ${user.name} to MySQL database...');
    // Actual implementation...
  }
}
```

```dart
class PostgreSQLDatabase implements Database {
  void saveUser(User user) {
    print('Saving ${user.name} to PostgreSQL database...');
    // Actual implementation...
  }
}
```

```dart
class UserService {
  Database database; // dependency injection
  UserService(this.database);

  void saveUser(User user){
    database.saveUser(user);
  }
}
```
Let's recap what we did here.

1. In the refactored solution, we create an abstract class `Database` that declares the `saveUser()` method.
2. Both `MySQLDatabase` and `PostgreSQLDatabase` implements this interface.
3. The `UserService` class depends on the `Database` abstraction, not on a specific database specific class.
4. This way, we can easily switch between different database systems without changing `UserService`.

That's very powerful.

#### What exactly was wrong with the original code?

- The original code violates the **Dependency Inversion Principle**, because `UserService` directly depends on a specific database class which is the `MySQLDatabase`.
- This makes UserService less flexible and harder to adapt to changes (like switching to another database system).

So I hope that this has shed a little bit more light on what it is exactly about the **SOLID Principles**

## Conclusion