---
title: "SOLID principles in swift"
date: 2024-03-31 17:36:06
categories: ['solid principles', 'solid principles swift', 'Swift', 'swift best practice']
layout: post
---

<!-- wp:paragraph -->
<p id="44b0">SOLID represents 5 five design principles intended to make <a href="https://en.wikipedia.org/wiki/Object-oriented">object-oriented</a> designs more understandable, flexible, and <a href="https://en.wikipedia.org/wiki/Software_maintenance">maintainable</a>. 


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item {"style":{"typography":{"fontStyle":"normal","fontWeight":"700"}},"fontSize":"medium"} -->
<li style="font-style:normal;font-weight:700" class="has-medium-font-size"><strong>S</strong>ingle Responsibility Principle</li>
<!-- /wp:list-item -->

<!-- wp:list-item {"style":{"typography":{"fontStyle":"normal","fontWeight":"700"}},"fontSize":"medium"} -->
<li style="font-style:normal;font-weight:700" class="has-medium-font-size"><strong>O</strong>pen/Closed Principle</li>
<!-- /wp:list-item -->

<!-- wp:list-item {"style":{"typography":{"fontStyle":"normal","fontWeight":"700"}},"fontSize":"medium"} -->
<li style="font-style:normal;font-weight:700" class="has-medium-font-size"><strong>L</strong>iskov Substitution Principle</li>
<!-- /wp:list-item -->

<!-- wp:list-item {"style":{"typography":{"fontStyle":"normal","fontWeight":"700"}},"fontSize":"medium"} -->
<li style="font-style:normal;font-weight:700" class="has-medium-font-size"><strong>I</strong>nterface Segregation</li>
<!-- /wp:list-item -->

<!-- wp:list-item {"style":{"typography":{"fontStyle":"normal","fontWeight":"700"}},"fontSize":"medium"} -->
<li style="font-style:normal;font-weight:700" class="has-medium-font-size"><strong>D</strong>ependency Inversion</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
Let's discuss one by one


<!-- /wp:paragraph -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="wp-block-heading has-ast-global-color-1-color has-text-color">1. <strong>Single Responsibility Principle </strong></h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Every class should have only one responsibility<br>Example: In below example <code>class UserProfileManager</code> is single responsibility class which has <code>getUserProfile</code> <code>function</code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class UserProfileManager {
    func getUserProfile(userId: String) -> UserProfile {
        // Retrieve user profile from database
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="wp-block-heading has-ast-global-color-1-color has-text-color">2.<strong>O</strong>pen/Closed Principle</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Software entities such as classes, modules, and functions should be open for extension but closed for modification<br>Or in other term the behavior of a "module" should be extendable without modifying its source code.<br>Example: -


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Processes different types of orders. Let's consider a simplified version of an order processing system:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Base class representing an order
class Order {
    var totalAmount: Double
    
    init(totalAmount: Double) {
        self.totalAmount = totalAmount
    }
    
    func calculateDiscount() -> Double {
        return 0
    }
}
// Now below example which shows open for extentions which uses calculateDiscount
// Subclass representing a standard order
class StandardOrder: Order {
    override func calculateDiscount() -> Double {
        // Standard orders have no discount
        return 0
    }
}

// Subclass representing a bulk order
class BulkOrder: Order {
    override func calculateDiscount() -> Double {
        // Bulk orders receive a 10% discount
        return totalAmount * 0.1
    }
}

/// Example usage
let bulkOrder = BulkOrder(totalAmount: 100)
print("bulkOrder-Discount", bulkOrder.calculateDiscount())// prints 10</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Explanation of closed for modification: -- <br>Now, imagine that we need to introduce a new type of order, a "Promotional Order," which applies a fixed discount amount. Instead of modifying the existing code, we can adhere to the Open/Closed Principle by extending the system's functionality:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Subclass representing a promotional order
class PromotionalOrder: Order {
    let promotionalDiscount: Double
    
    init(totalAmount: Double, promotionalDiscount: Double) {
        self.promotionalDiscount = promotionalDiscount
        super.init(totalAmount: totalAmount)
    }
    
    override func calculateDiscount() -> Double {
        // Promotional orders apply a fixed discount amount
        return totalAmount - promotionalDiscount
    }
}

// Usage 
let userWithPromotion = PromotionalOrder(totalAmount: 100, promotionalDiscount: 10)
print("promotion-Discount", userWithPromotion.calculateDiscount())// prints 90</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="wp-block-heading has-ast-global-color-1-color has-text-color"><strong>3.Liskov Substitution Principle</strong></h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Functions that use references to base classes must be able to use objects of derived classes without knowing it.<br>Let's understand with banking example: - 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//---------Example of Liskov Substitution------------------/
// Base class representing a bank account
class AccountParentClass {
    var balance: Double
    
    init(balance: Double) {
        self.balance = balance
    }
    
    // Method to calculate interest
    func calculateInterest() -> Double {
        fatalError("Method must be overridden by subclasses")
    }
}

// Subclass representing a Current Account
class CurrentAccount: AccountParentClass {
    
    // Subclass able to use parent class function here
    override func calculateInterest() -> Double {
        // current account has no interest
        return 0
    }
}

// Subclass representing a Savings Account
class SavingsAccount: AccountParentClass {
    let interestRate: Double
    
    init(balance: Double, interestRate: Double) {
        self.interestRate = interestRate
        super.init(balance: balance)
    }
    // Subclass able to use parent class function here
    override func calculateInterest() -> Double {
        // Calculate interest based on balance and interest rate
        return balance * interestRate
    }
}

func printInterest(account: AccountParentClass) {
    let interest = account.calculateInterest()
    print("Interest:", interest)
}

let checking = CurrentAccount(balance: 1000)
let savings = SavingsAccount(balance: 2000, interestRate: 0.05)

printInterest(account: checking) // Output: Interest: 0
printInterest(account: savings) // Output: Interest: 100
//---------------------------/</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="wp-block-heading has-ast-global-color-1-color has-text-color">4. Interface Segregation Principle (ISP)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Clients should not be forced to depend upon methods that they do not use. Essentially, rather than having one large interface, you should have several smaller functions, so that clients only need to know about the methods that are of interest to them.<br>Let's understand with an example : - <br>Imagine you are developing a software system for a Smart Home environment. In this system, you have different devices like lights & security cameras. Instead of having a single, monolithic interface for all devices, you segregate the interfaces according to their functionalities.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Interface for any device that can be turned on and off
protocol Switchable {
    func turnOn()
    func turnOff()
}

// Interface for devices that can capture video
protocol VideoCapable {
    func startRecording()
    func stopRecording()
}

// A class for a smart light, which only needs to be switched on or off
class SmartLight: Switchable {
    func turnOn() {
        print("Light turned on")
    }
    
    func turnOff() {
        print("Light turned off")
    }
}

// A class for a thermostat, which can be turned on/off and temperature adjusted
class Thermostat: Switchable {
    func turnOn() {
        print("Thermostat turned on")
    }
    
    func turnOff() {
        print("Thermostat turned off")
    }
}

// A class for a security camera, which can be turned on/off and start/stop recording
class SecurityCamera: Switchable, VideoCapable {
    func turnOn() {
        print("Camera turned on")
    }
    
    func turnOff() {
        print("Camera turned off")
    }
    
    func startRecording() {
        print("Recording started")
    }
    
    func stopRecording() {
        print("Recording stopped")
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="wp-block-heading has-ast-global-color-1-color has-text-color">5. Dependency Inversion principle</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
The dependency inversion principle is a specific methodology for loosely coupled software modules.<br>A) High-level modules should not import anything from low-level modules. Both should depend on abstractions (e.g., interfaces). <br>B)Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.<br>Let's understand with an example - 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<em><strong>Notification System</strong> :</em> Imagine you're building a system where you need to notify users about certain events, like completing a registration process or receiving a message. Initially, you decide to notify users via email.<br>By following the Dependency Inversion Principle, our code is now more flexible and easier to maintain. We can add new notification methods without changing the high-level modules that use them.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// First, let's define an abstraction for sending notifications:
// Abstraction
protocol NotificationService {
    func sendNotification(message: String, toUser: String)
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Next, we implement this protocol with a class that sends notifications via email:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Concrete implementation for email notification
class EmailNotificationService: NotificationService {
    func sendNotification(message: String, toUser: String) {
        print("Sending email to \(toUser) with message: \(message)")
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Now, let’s say our application evolves, and we also want to send SMS notifications. Instead of modifying our high-level module (which sends notifications), we can simply create a new class that implements <code>NotificationService</code>:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Another concrete implementation for SMS notification
class SMSNotificationService: NotificationService {
    func sendNotification(message: String, toUser: String) {
        print("Sending SMS to \(toUser) with message: \(message)")
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
The high-level module that uses the <code>NotificationService</code> doesn’t need to know about the concrete implementation:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class UserNotificationManager {
    let notificationService: NotificationService
    
    init(notificationService: NotificationService) {
        self.notificationService = notificationService
    }
    
    func notifyUser(message: String, user: String) {
        notificationService.sendNotification(message: message, toUser: user)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
You can see that <code>UserNotificationManager</code> is not directly dependent on <code>EmailNotificationService</code> or <code>SMSNotificationService</code>. It depends on the <code>NotificationService</code> abstraction. This way, if we want to change the notification method (from email to SMS), we can do so easily without needing to alter the <code>UserNotificationManager</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
To switch the notification method, we just instantiate <code>UserNotificationManager</code> with a different implementation of <code>NotificationService</code>:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">let emailService = EmailNotificationService()
let userManagerWithEmail = UserNotificationManager(notificationService: emailService)
userManagerWithEmail.notifyUser(message: "Welcome to our service!", user: "user@example.com")

let smsService = SMSNotificationService()
let userManagerWithSMS = UserNotificationManager(notificationService: smsService)
userManagerWithSMS.notifyUser(message: "Your code is 1234", user: "+123456789")</code></pre>
<!-- /wp:code -->