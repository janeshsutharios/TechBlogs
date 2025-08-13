## 1. 🧱 Classes and Objects
A class is a blueprint for creating objects that encapsulate data and behavior. An object is an instance of a class, representing a specific entity with its own values and functionality. This approach helps organize code in a modular, reusable, and scalable way.

```swift
class Student {
    var name: String
    var age: Int
    var grade: String

    init(name: String, age: Int, grade: String) {
        self.name = name
        self.age = age
        self.grade = grade
    }

    func displayInfo() {
        print("Name: \(name), Age: \(age), Grade: \(grade)")
    }
}

// Usage -
let student1 = Student(name: "Aarav", age: 14, grade: "8th")
student1.displayInfo()
````
---

## 2. 🔐 Encapsulation

> **Encapsulation** is the OOP principle of hiding internal object details and exposing only what’s necessary. In Swift, this is achieved using access control keywords like `private`, `internal`, and `public`, which help protect data and maintain clean interfaces.

### 🧪 Example: Bank Account

```swift
class BankAccount {
    private var balance: Double = 0.0

    func deposit(amount: Double) {
        balance += amount
    }

    func getBalance() -> Double {
        return balance
    }
}

let account = BankAccount()
account.deposit(amount: 1000)
print("Current Balance: ₹\(account.getBalance())")
```

### ✅ Output:
```
Current Balance: ₹1000.0
```

### 💡 Explanation:
- The `balance` property is marked `private`, so it can't be accessed directly from outside the class.
- Only controlled access is provided through `deposit()` and `getBalance()` methods.

### 🔐 Swift Access Specifiers Table

| Access Level   | Scope of Access                                                                 | Use Case Example                                                                 |
|----------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| `open`         | Accessible and **overridable** outside the module (framework or app)            | Used in frameworks where classes/methods need to be subclassed externally       |
| `public`       | Accessible outside the module, but **not overridable**                          | Expose APIs without allowing subclassing or overriding                          |
| `internal`     | Default level. Accessible **within the same module**                            | Most common for app-level code                                                  |
| `fileprivate`  | Accessible **only within the same file**                                        | Hide implementation details within a file                                       |
| `private`      | Accessible **only within the enclosing scope** (class, struct, or extension)    | Strict encapsulation of properties or methods                                   |

---

### 💡 Tip:
- Use `private` or `fileprivate` to enforce **encapsulation**.
- Use `internal` for most app code.
- Use `public` or `open` when building **reusable frameworks**.
---

## 🧬 3. Inheritance

> **Inheritance** is an OOP concept where one class (called a *subclass*) inherits properties and methods from another class (called a *superclass*). Swift supports **single inheritance**, allowing you to reuse and extend existing functionality.

### 🐾 Example: Animal → Dog

```swift
class Animal {
    var name: String

    init(name: String) {
        self.name = name
    }

    func speak() {
        print("\(name) makes a sound")
    }
}

class Dog: Animal {
    func fetch() {
        print("\(name) is fetching the ball")
    }

    override func speak() {
        print("\(name) barks")
    }
}

let myDog = Dog(name: "Buddy")
myDog.speak()   // Buddy barks
myDog.fetch()   // Buddy is fetching the ball
```

### 💡 Explanation:
- `Dog` inherits from `Animal`, gaining access to its `name` property and `speak()` method.
- `Dog` overrides `speak()` to provide its own behavior.
- It also adds a new method `fetch()`.

---

### 🧭 Real-World Example: ViewController Inheritance

> In iOS development, every custom screen or view is typically a subclass of `UIViewController`. This is a classic example of inheritance, where your custom controller inherits built-in functionality like view lifecycle methods (`viewDidLoad`, `viewWillAppear`, etc.) from `UIViewController`.

### 📱 Example: Custom ViewController

```swift
import UIKit

class WelcomeViewController: UIViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        print("Welcome screen loaded")
    }
}
```

### 💡 Explanation:
- `WelcomeViewController` inherits from `UIViewController`.
- It overrides `viewDidLoad()` to customize behavior when the view loads.
- You get access to all the built-in methods and properties of `UIViewController` without writing them from scratch.

---

Perfect choice, Janesh! Here's a blog-ready explanation of **Polymorphism** using a **Payment Gateway** example — something readers can easily relate to in real-world app development.

---
## 🔄 4. Polymorphism
> Polymorphism allows objects of different classes to be treated as objects of a common superclass or protocol. It enables a single interface to represent different underlying forms (types), making code more flexible and extensible.

### 💳 Polymorphism in a Payment Gateway System

> In a payment gateway, different payment methods (like UPI, Credit Card, Net Banking) can be handled using a common interface. This is a classic use of **polymorphism**, where each payment type behaves differently but is accessed through the same protocol or superclass.

### 🧪 Example: Payment Protocol

```swift
protocol PaymentMethod {
    func processPayment(amount: Double)
}

class CreditCardPayment: PaymentMethod {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via Credit Card")
    }
}

class UPIPayment: PaymentMethod {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via UPI")
    }
}

class NetBankingPayment: PaymentMethod {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via Net Banking")
    }
}
```

### 🧾 Usage

```swift
let payments: [PaymentMethod] = [
    CreditCardPayment(),
    UPIPayment(),
    NetBankingPayment()
]

for payment in payments {
    payment.processPayment(amount: 500.0)
}
```

### ✅ Output:
```
Processing ₹500.0 via Credit Card  
Processing ₹500.0 via UPI  
Processing ₹500.0 via Net Banking
```

---

### 💡 Explanation:
- All payment classes conform to the `PaymentMethod` protocol.
- The `processPayment()` method is called polymorphically — the correct implementation is chosen at runtime based on the object type.
- This makes the system **extensible** — you can add new payment types without changing existing code.

---

## 🧠 5. Abstraction

> **Abstraction** is the OOP principle of hiding complex implementation details and exposing only the essential features through a simplified interface. In Swift, abstraction is commonly achieved using **protocols**, which define a blueprint of methods and properties without specifying how they’re implemented.

---

### 🧪 Example: Payment Abstraction

```swift
protocol PaymentMethod {
    func processPayment(amount: Double)
}

class UPIPayment: PaymentMethod {
    func processPayment(amount: Double) {
        // UPI-specific logic
        print("Paid ₹\(amount) using UPI")
    }
}

class CreditCardPayment: PaymentMethod {
    func processPayment(amount: Double) {
        // Credit card-specific logic
        print("Paid ₹\(amount) using Credit Card")
    }
}
```

### 🧾 Usage

```swift
func makePayment(using method: PaymentMethod, amount: Double) {
    method.processPayment(amount: amount)
}

let payment = UPIPayment()
makePayment(using: payment, amount: 750.0)
```

### ✅ Output:
```
Paid ₹750.0 using UPI
```
 **Abstraction** VS **Encapsulation**
 **Abstraction** and **Encapsulation** are closely related but serve different purposes in object-oriented programming. Here's a clear comparison to help your blog readers understand the difference:

---

## 🧠 Abstraction vs 🔐 Encapsulation

| Feature         | **Abstraction**                                           | **Encapsulation**                                       |
|----------------|-----------------------------------------------------------|----------------------------------------------------------|
| **Purpose**     | Hides *implementation complexity*                        | Hides *internal data* from outside access                |
| **Focus**       | Focuses on *what* an object does                         | Focuses on *how* an object protects its data             |
| **Achieved Using** | `protocols`, abstract interfaces                        | Access modifiers like `private`, `fileprivate`, etc.     |
| **Example**     | `PaymentMethod` protocol with `processPayment()` method | `BankAccount` class with private `balance` property      |
| **Benefit**     | Simplifies usage and promotes flexibility                | Secures data and maintains integrity                     |

---

### 🔍 Quick Analogy:
- **Abstraction** is like using a **remote control** — you press buttons without knowing the internal electronics.
- **Encapsulation** is like the **plastic casing** around the remote — it protects the internal parts from being tampered with.


Great choice, Janesh! Here's a blog-ready section on **Method Overloading in Swift**, using a **Calculator App** as a real-world example:

---

## 🧮 6. Method Overloading in Swift: 

> **Method Overloading** allows you to define multiple methods with the same name but different parameters. In a calculator app, this is especially useful for handling different types of inputs like integers, doubles, or multiple operands.

---

### 🧪 Calculator App Example

```swift
class Calculator {
    
    // Overload for two integers
    func add(a: Int, b: Int) -> Int {
        return a + b
    }

    // Overload for two doubles
    func add(a: Double, b: Double) -> Double {
        return a + b
    }

    // Overload for three integers
    func add(a: Int, b: Int, c: Int) -> Int {
        return a + b + c
    }

    // Overload with argument labels
    func add(first a: Int, second b: Int) -> Int {
        return a + b
    }
}
```

### 🧾 Usage

```swift
let calc = Calculator()

print(calc.add(a: 2, b: 3))             // 5
print(calc.add(a: 2.5, b: 3.5))         // 6.0
print(calc.add(a: 1, b: 2, c: 3))       // 6
print(calc.add(first: 10, second: 20))  // 30
```

---

### 💡 Why It Matters

- **Flexibility**: You can handle different types and numbers of inputs without changing method names.
- **Readability**: Keeps your code clean and intuitive.
- **Scalability**: Easily extend functionality as your app grows.








## 🧩 Summary of OOP Concepts

## 🧩 Summary of OOP Concepts

| Concept 🧩         | Description                                                                 | Swift Feature Used         | Real-World Example                          |
|-------------------|-----------------------------------------------------------------------------|----------------------------|---------------------------------------------|
| **🧱📦 Classes & Objects** | Blueprint and instance representing data and behavior                     | `class`, `init`, properties, methods | `Student`, `Car`, `UIViewController`         |
| **🔐📦 Encapsulation**     | Hiding internal details and exposing only necessary parts                | `private`, `fileprivate`, `public`   | `BankAccount` with hidden balance            |
| **🧬📱 Inheritance**       | Reusing and extending functionality from a parent class                  | `class`, `super`, `override`         | `Dog` inherits from `Animal`, `UIViewController` |
| **🔄💳 Polymorphism**      | One interface, many implementations                                      | `override`, `protocol`, dynamic dispatch | `Shape` drawing, `PaymentMethod` handling    |
| **🧠💡 Abstraction**       | Hiding complexity behind a simplified interface                          | `protocol`                             | `PaymentMethod` protocol with multiple types |

---


### 💡 Explanation:
- The `PaymentMethod` protocol defines the **abstract behavior**.
- Concrete classes (`UPIPayment`, `CreditCardPayment`) implement the behavior in their own way.
- The caller (`makePayment`) doesn’t need to know how the payment is processed — it just uses the abstract interface.

---

While Swift is OOP-friendly, there are a few limitations:

### ❌ Multiple Inheritance
Swift does **not** support multiple inheritance with classes. You can only inherit from one class. However, you can use **protocols** to simulate multiple inheritance.

### ❌ Abstract Classes
Swift does **not** have a direct concept of abstract classes. You can use protocols to define abstract behavior.

### ❌ Method Overloading Based on Return Type
Swift does **not** allow method overloading based solely on return type.

---
