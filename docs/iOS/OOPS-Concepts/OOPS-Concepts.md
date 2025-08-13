## 1. Classes and Objects
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
Here’s a clear and blog-friendly explanation of **Encapsulation** in Swift, along with an example:

---

## 2. 🔐 Encapsulation in Swift

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
Here’s a clean and informative table you can include in your blog to explain **Swift’s access control levels**:

---

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
