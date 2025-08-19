**SOLID principles with Swift**

SOLID represents 5 five design principles intended to make [object-oriented](https://en.wikipedia.org/wiki/Object-oriented) designs more understandable, flexible, and [maintainable](https://en.wikipedia.org/wiki/Software_maintenance).  

1. **S**ingle Responsibility Principle  
2. **O**pen/Closed Principle  
3. **L**iskov Substitution Principle  
4. **I**nterface Segregation  
5. **D**ependency Inversion  

Let's discuss one by one.

---

#### 1. **Single Responsibility Principle**

Every class should have only one responsibility.  

Example: `UserProfileManager` is a single responsibility class which has `getUserProfile` function.

```swift
class UserProfileManager {
    func getUserProfile(userId: String) -> UserProfile {
        // Retrieve user profile from database
    }
}
````

---

#### 2. **Open/Closed Principle**

Software entities such as classes, modules, and functions should be open for extension but closed for modification.
Or in other words, the behavior of a "module" should be extendable without modifying its source code.

Example: Processing different types of orders.

```swift
// Base class representing an order
class Order {
    var totalAmount: Double
    
    init(totalAmount: Double) {
        self.totalAmount = totalAmount
    }
    
    func calculateDiscount() -> Double {
        return 0
    }
}

// Subclass representing a standard order
class StandardOrder: Order {
    override func calculateDiscount() -> Double {
        return 0
    }
}

// Subclass representing a bulk order
class BulkOrder: Order {
    override func calculateDiscount() -> Double {
        return totalAmount * 0.1
    }
}

/// Example usage
let bulkOrder = BulkOrder(totalAmount: 100)
print("bulkOrder-Discount", bulkOrder.calculateDiscount()) // prints 10
```

Closed for modification: instead of editing existing code, extend functionality.

```swift
// Subclass representing a promotional order
class PromotionalOrder: Order {
    let promotionalDiscount: Double
    
    init(totalAmount: Double, promotionalDiscount: Double) {
        self.promotionalDiscount = promotionalDiscount
        super.init(totalAmount: totalAmount)
    }
    
    override func calculateDiscount() -> Double {
        return totalAmount - promotionalDiscount
    }
}

// Usage 
let userWithPromotion = PromotionalOrder(totalAmount: 100, promotionalDiscount: 10)
print("promotion-Discount", userWithPromotion.calculateDiscount()) // prints 90
```

---

#### 3. **Liskov Substitution Principle**

Functions that use references to base classes must be able to use objects of derived classes without knowing it.

Banking example:

```swift
// Base class representing a bank account
class AccountParentClass {
    var balance: Double
    
    init(balance: Double) {
        self.balance = balance
    }
    
    func calculateInterest() -> Double {
        fatalError("Method must be overridden by subclasses")
    }
}

class CurrentAccount: AccountParentClass {
    override func calculateInterest() -> Double {
        return 0
    }
}

class SavingsAccount: AccountParentClass {
    let interestRate: Double
    
    init(balance: Double, interestRate: Double) {
        self.interestRate = interestRate
        super.init(balance: balance)
    }
    
    override func calculateInterest() -> Double {
        return balance * interestRate
    }
}

func printInterest(account: AccountParentClass) {
    let interest = account.calculateInterest()
    print("Interest:", interest)
}

let checking = CurrentAccount(balance: 1000)
let savings = SavingsAccount(balance: 2000, interestRate: 0.05)

printInterest(account: checking) // Interest: 0
printInterest(account: savings)  // Interest: 100
```

---

#### 4. **Interface Segregation Principle (ISP)**

Clients should not be forced to depend upon methods they do not use.
Instead of one large interface, have smaller, specific ones.

Example: Smart Home environment with lights & cameras.

```swift
protocol Switchable {
    func turnOn()
    func turnOff()
}

protocol VideoCapable {
    func startRecording()
    func stopRecording()
}

class SmartLight: Switchable {
    func turnOn() { print("Light turned on") }
    func turnOff() { print("Light turned off") }
}

class Thermostat: Switchable {
    func turnOn() { print("Thermostat turned on") }
    func turnOff() { print("Thermostat turned off") }
}

class SecurityCamera: Switchable, VideoCapable {
    func turnOn() { print("Camera turned on") }
    func turnOff() { print("Camera turned off") }
    func startRecording() { print("Recording started") }
    func stopRecording() { print("Recording stopped") }
}
```

---

#### 5. **Dependency Inversion Principle**

High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details. Details should depend on abstractions.

Example: **Notification System**

```swift
// Abstraction
protocol NotificationService {
    func sendNotification(message: String, toUser: String)
}
```

Concrete email implementation:

```swift
class EmailNotificationService: NotificationService {
    func sendNotification(message: String, toUser: String) {
        print("Sending email to \(toUser) with message: \(message)")
    }
}
```

Adding SMS without modifying existing code:

```swift
class SMSNotificationService: NotificationService {
    func sendNotification(message: String, toUser: String) {
        print("Sending SMS to \(toUser) with message: \(message)")
    }
}
```

High-level module depends only on abstraction:

```swift
class UserNotificationManager {
    let notificationService: NotificationService
    
    init(notificationService: NotificationService) {
        self.notificationService = notificationService
    }
    
    func notifyUser(message: String, user: String) {
        notificationService.sendNotification(message: message, toUser: user)
    }
}
```

Usage:

```swift
let emailService = EmailNotificationService()
let userManagerWithEmail = UserNotificationManager(notificationService: emailService)
userManagerWithEmail.notifyUser(message: "Welcome!", user: "user@example.com")

let smsService = SMSNotificationService()
let userManagerWithSMS = UserNotificationManager(notificationService: smsService)
userManagerWithSMS.notifyUser(message: "Your code is 1234", user: "+123456789")
```

---
