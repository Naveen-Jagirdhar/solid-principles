# solid-principles

The **SOLID Principles** are set of 5 design principles that make software system easier to understand, maintain & extend.

---
## What is SOLID?

The acronym **SOLID** stand for

- **S** - Singe Responsibility Principle (SRP)
- **O** - Open/Closed Principle(OCP)
- **L** - Liskov Substitution Principle(LSP)
- **I** - Interface Segregation Principle (ISP)
- **D** - Dependency Inversion Principle (DIP)
---

## 1. Single Responsibility Principle (SRP)

> A class should have only **one reason to change**.

This means that a class should have **one Job** or **One responsibility**

### Example

//Violates SRP

```bash
class UserService {

    public void registerUser(String username, String password) {
        // registration logic
    }

    public void sendEmail(String message) {
        // email logic
    }
}
```

// Follows SRP

```bash
class UserService {

    public void registerUser(String username, String password) {
        // registration logic
    }
}

class EmailService {

 public void sendEmail(String message) {
        // email logic
    }
}
```

## 2. Open/Closed Principle (OCP)

> Software entities should be **open for extension** but **closed for modification**

You should be able to add new functionality without changing existing code.This is commonly achieved using interface, inheritance & polymorphism.

### Example

//Follows OCP

```bash

interface Shape {
    double area();
}

class Circle implements Shape {
    double radius;
    public double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle implements Shape {
    double width, height;
    public double area() {
        return width * height;
    }
}

class AreaCalculator {
    public double calculateTotalArea(List<Shape> shapes) {
        return shapes.stream().mapToDouble(Shape::area).sum();
    }
}

```

## 3. Liskov Substituion Principle (LSP)

> if a child class replaces a parent class, everything should still work fine.

Think of it like this:
> if your code work with a **Parent** , it should also work the same way with any of its **children - without breaking or chaning the behaviour**

LSP says:
> "Dont break expectations when replacing a parent class with a child class"

## Example

//Violates LSP

```bash
class Bird {
    void fly() {
        System.out.println("Flying");
    }
}
```
Now you create a subclass
```bash
class Sparrow extends Bird {
    // All good, sparrows can fly
}
```
But what if you do this
```bash
class Ostrich extends Bird {
    void fly() {
        throw new UnsupportedOperationException("Ostrich can't fly!");
    }
}
```
Now, if your program assumes every bird can fly & suddenly you pass an **Ostrich** - your code **crashes**
That's a violation of **LSP**.

//Follows LSP

```bash
interface Bird {}

interface FlyingBird extends Bird {
    void fly();
}

class Sparrow implements FlyingBird {
    public void fly() {
        System.out.println("Sparrow flying");
    }
}

class Ostrich implements Bird {
    // No fly() method. No surprises!
}

```
Now, you will never accidentally ask an Ostrich to fly!Your code is safer, cleaner & easier to understand.

## 4. Interface Segregation Principle (ISP)

> Clients should not be forced to depend on interfaces they do not use

Rather than one big interface , Split into smaller more specific interfaces.

## Example

//Violates ISP

```bash
interface invoiceAction {
    void create();
    void approve();
    void reject();
}

class InvoiceCreator implements invoiceAction {
    public void create() {}
    public void approve() {} // not supported
    public void reject() {}  // not supported
}

```
// Follows ISP
``` bash
interface CreateInvoice {
    void create();
}

interface ApproveInvoice {
    void approve();
}

class ApproverInvoice implements ApproveInvoice {
    public void approve() {
      //approval logic for invoice
    }
}
```

## 5. Dependency Inversion Principle (DIP)

> High-Level things (like business logic) should not depend on low-level things(like database),Both should depend on an abstract idea(interface).

## Example

//Violates DIP

```bash
class MySQLDatabase {
    void save(String data) {
        System.out.println("Saved to MySQL");
    }
}

class ReportService {
    MySQLDatabase db = new MySQLDatabase();

    void generateReport(String data) {
        db.save(data); // tightly coupled to MySQL
    }
}
```
Problem? if you want to switch to mongoDB or File Storage you must edit ReportService.

//Follows or with DIP

```bash
interface Database {
    void save(String data);
}

class MySQLDatabase implements Database {
    public void save(String data) {
        System.out.println("Saved to MySQL");
    }
}

class ReportService {
    private Database db;

    public ReportService(Database db) {
        this.db = db; // inject dependency
    }

    public void generateReport(String data) {
        db.save(data); // works with any Database implementation
    }
}
```
Now ReportService does not care how the data is saved.It just knows it will be saved.You can plug in MYSQL, MongoDB,FileSystem or even a fake database for testing - no changes needed in the service.


## Why Use SOLID?

The SOLID principles make your code:

- Easier to maintain
- More flexible for future changes
- Less prone to bugs
- Cleaner and more understandable

Here’s a quick summary of each principle and its core benefit:

| Principle | Key Benefit                          |
|-----------|--------------------------------------|
| **SRP**   | Better separation of concerns        |
| **OCP**   | Easier to add new features           |
| **LSP**   | Prevents runtime surprises           |
| **ISP**   | Interface clarity and granularity    |
| **DIP**   | Promotes loose coupling & testability |

