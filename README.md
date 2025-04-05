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
