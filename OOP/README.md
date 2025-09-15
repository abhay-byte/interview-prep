### **OOP Questions**

**1. Q: What is Object-Oriented Programming (OOP)?**
*   **A:** OOP is a programming paradigm based on the concept of "objects," which can contain data (in the form of fields or attributes) and code (in the form of procedures or methods). The primary goal of OOP is to structure a program by bundling related properties and behaviors into individual objects, promoting modularity and reusability.

**2. Q: What are the four main pillars of OOP?**
*   **A:** The four pillars are **Encapsulation**, **Abstraction**, **Inheritance**, and **Polymorphism**. These principles help in creating scalable, manageable, and robust software.

**3. Q: What is Encapsulation?**
*   **A:** Encapsulation is the practice of bundling an object's data (attributes) and the methods that operate on that data into a single unit (a class). It also involves restricting direct access to an object's internal state, typically by using private access modifiers. This is often called "data hiding."

**4. Q: What is Abstraction?**
*   **A:** Abstraction is the concept of hiding complex implementation details from the user and only exposing essential features. It simplifies complex systems by modeling classes appropriate to the problem. For example, when you drive a car, you use a simple interface (steering wheel, pedals) without needing to know the engine's mechanics.

**5. Q: What is Inheritance?**
*   **A:** Inheritance is a mechanism where a new class (subclass or child) derives attributes and methods from an existing class (superclass or parent). This promotes code reuse and establishes an "IS-A" relationship (e.g., a `Dog` IS-A `Animal`).

**6. Q: What is Polymorphism?**
*   **A:** Polymorphism, meaning "many forms," allows objects of different classes to be treated as objects of a common superclass. It is the ability to present the same interface for differing underlying forms. This is typically achieved through **Method Overriding** (runtime polymorphism) and **Method Overloading** (compile-time polymorphism).

**7. Q: What is the difference between a Class and an Object?**
*   **A:** A **Class** is a blueprint or template for creating objects. It defines a set of properties and methods that are common to all objects of that type. An **Object** is a specific instance of a class, with its own state (values for its attributes).

**8. Q: What is a Constructor?**
*   **A:** A constructor is a special method within a class that is automatically called when a new object is created (instantiated). Its primary purpose is to initialize the object's attributes with initial values.

**9. Q: What is Method Overloading?**
*   **A:** Method Overloading is defining multiple methods with the same name within the same class, but with different parameters (either a different number of arguments or different types of arguments). This is an example of compile-time polymorphism.

**10. Q: What is Method Overriding?**
*   **A:** Method Overriding occurs when a subclass provides a specific implementation for a method that is already defined in its superclass. The method signature (name and parameters) must be the same. This is an example of runtime polymorphism.

**11. Q: What is an Abstract Class?**
*   **A:** An abstract class is a class that cannot be instantiated on its own and is meant to be subclassed. It can contain both abstract methods (methods without a body) and concrete methods (methods with a body). A subclass must implement all abstract methods of its parent.

**12. Q: What is an Interface?**
*   **A:** An interface is a completely abstract type that defines a contract of methods. Any class that implements an interface must provide an implementation for all the methods declared in it. A class can implement multiple interfaces, allowing for a form of multiple inheritance.

**13. Q: Compare an Abstract Class and an Interface.**
*   **A:**
    *   **Implementation:** Abstract classes can have both abstract and concrete methods. Interfaces can only have abstract method declarations (in most classic OOP languages).
    *   **Inheritance:** A class can inherit from only one abstract class but can implement multiple interfaces.
    *   **State:** Abstract classes can have instance variables (state). Interfaces cannot.

**14. Q: What is the difference between Composition and Inheritance?**
*   **A:**
    *   **Inheritance** defines an "IS-A" relationship (a `Car` is a `Vehicle`). It provides strong coupling.
    *   **Composition** defines a "HAS-A" relationship (a `Car` has an `Engine`). It is more flexible than inheritance and involves creating objects of other classes within a class.

**15. Q: Why is Composition often preferred over Inheritance?**
*   **A:** Composition is generally preferred because it offers more flexibility. It allows behavior to be changed at runtime by swapping out composed objects, and it avoids the rigid, hierarchical classifications of inheritance, leading to a more loosely coupled and maintainable design.

**16. Q: What are SOLID principles?**
*   **A:** SOLID is an acronym for five design principles intended to make software designs more understandable, flexible, and maintainable:
    *   **S** - Single Responsibility Principle
    *   **O** - Open/Closed Principle
    *   **L** - Liskov Substitution Principle
    *   **I** - Interface Segregation Principle
    *   **D** - Dependency Inversion Principle

**17. Q: Briefly explain the Single Responsibility Principle (SRP).**
*   **A:** The SRP states that a class should have only one reason to change, meaning it should have only one job or responsibility. This makes the class more robust and easier to understand.

**18. Q: Briefly explain the Open/Closed Principle (OCP).**
*   **A:** The OCP states that software entities (classes, modules, functions) should be **open for extension** but **closed for modification**. This means you should be able to add new functionality without changing existing code.

**19. Q: What is the difference between Association, Aggregation, and Composition?**
*   **A:** All three describe relationships between objects.
    *   **Association:** A general relationship where objects are aware of each other (`Student` and `Teacher`).
    *   **Aggregation:** A "has-a" relationship where the child can exist independently of the parent (`Department` has `Teachers`, but teachers exist if the department is closed).
    *   **Composition:** A strong "part-of" relationship where the child cannot exist without the parent (`House` has `Rooms`; if the house is destroyed, the rooms are too).

**20. Q: What is Coupling and Cohesion?**
*   **A:**
    *   **Coupling:** The degree of dependency between two or more modules. **Low coupling** is desirable, as it means a change in one module is less likely to affect others.
    *   **Cohesion:** The degree to which elements inside a single module belong together. **High cohesion** is desirable, as it means the module has a well-defined and focused purpose.

---

### **Part 2: Practical OOP Design Questions**

**1. Q: How would you design a system for a parking lot?**
*   **A: High-Level Design:**
    *   **Classes:**
        *   `ParkingLot`: Manages the entire lot. Attributes: `levels`, `gates`. Methods: `findSpot()`, `parkVehicle()`, `exitVehicle()`.
        *   `Level`: Represents a floor. Attributes: `spots`. Methods: `findAvailableSpot()`.
        *   `ParkingSpot`: Represents a single spot. Attributes: `spotNumber`, `spotType` (Compact, Large), `isAvailable`.
        *   `Vehicle`: An abstract base class. Subclasses: `Car`, `Truck`, `Motorcycle`. Attributes: `licensePlate`, `vehicleType`.
        *   `Ticket`: Issued upon entry. Attributes: `vehicle`, `spot`, `entryTime`. Methods: `calculateFee()`.

    *   **Relationships:** `ParkingLot` HAS `Level`s. A `Level` HAS `ParkingSpot`s. A `Ticket` IS-ASSOCIATED-WITH a `Vehicle` and a `ParkingSpot`.

**2. Q: Design the classes for a standard deck of cards.**
*   **A: High-Level Design:**
    *   **Enums (for fixed values):**
        *   `Suit`: CLUBS, DIAMONDS, HEARTS, SPADES.
        *   `Rank`: TWO, THREE, ..., KING, ACE.
    *   **Classes:**
        *   `Card`: Represents a single card. Attributes: `suit` (Suit), `rank` (Rank). Methods: `getValue()`.
        *   `Deck`: Represents 52 cards. Attributes: `cards` (a list of `Card` objects). Methods: `shuffle()`, `dealOneCard()`, `reset()`.
        *   `Player`: Represents a participant. Attributes: `hand` (a list of `Card`s). Methods: `addCardToHand()`, `playCard()`.

    *   **Logic:** The `Deck` class would be initialized by creating one `Card` object for each combination of `Suit` and `Rank`.

**3. Q: Design a simple vending machine.**
*   **A: High-Level Design:**
    *   **Classes:**
        *   `VendingMachine`: The main class. Attributes: `inventory`, `balance`. Methods: `insertCoin()`, `selectItem()`, `dispenseItem()`, `returnCoins()`.
        *   `Item`: Represents a product. Attributes: `name`, `price`.
        *   `Inventory`: Manages the stock. Attributes: `items` (a map of `Item` to its quantity). Methods: `getQuantity()`, `reduceStock()`, `isAvailable()`.
    *   **State Management:** The `VendingMachine` would manage its state (e.g., `NoCoinState`, `HasCoinState`, `SoldOutState`). The methods would behave differently based on the current state.
    *   **Relationships:** `VendingMachine` HAS an `Inventory`. `Inventory` HAS `Item`s.

**4. Q: How would you design a basic library management system?**
*   **A: High-Level Design:**
    *   **Classes:**
        *   `Library`: Manages the system. Attributes: `books` (list), `members` (list). Methods: `addBook()`, `registerMember()`, `issueBook()`, `returnBook()`.
        *   `Book`: An abstract class. Subclasses: `FictionBook`, `ReferenceBook`. Attributes: `bookID`, `title`, `author`, `isIssued`.
        *   `Member`: Represents a library user. Attributes: `memberID`, `name`, `booksIssued` (list).
        *   `Librarian`: A user who manages the library. Extends a base `User` class.
        *   `BookLending`: A record of a transaction. Attributes: `book`, `member`, `issueDate`, `returnDate`.

    *   **Relationships:** `Library` HAS `Book`s and `Member`s. `Member`s can BORROW `Book`s. `Librarian` MANAGES the `Library`.