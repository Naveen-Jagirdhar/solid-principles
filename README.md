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
