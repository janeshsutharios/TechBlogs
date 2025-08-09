# 🔌 Adapter (Structural)

The **Adapter** pattern allows incompatible interfaces to work together by converting the interface of one class into an interface expected by the client. It's like a power plug adapter that lets a U.S. charger work in a European socket.

---

### ✅ When to Use

- You want to use an existing class but its interface doesn't match your needs.
- You want to create a reusable class that works with unrelated or legacy classes.
- You want to bridge **incompatible systems** without changing their code.

---

### 💡 Real-World Example

#### 🎧 Audio Player Adapter

```swift
protocol MediaPlayer {
    func play(filename: String)
}

class MP3Player: MediaPlayer {
    func play(filename: String) {
        print("🎵 Playing MP3 file: \(filename)")
    }
}

// Existing incompatible class
class VLCPlayer {
    func playVLC(file: String) {
        print("🎬 Playing VLC file: \(file)")
    }
}

// Adapter that makes VLCPlayer compatible
class VLCAdapter: MediaPlayer {
    private let vlcPlayer = VLCPlayer()
    
    func play(filename: String) {
        vlcPlayer.playVLC(file: filename)
    }
}
````

#### 🧪 Usage

```swift
let mp3 = MP3Player()
mp3.play(filename: "song.mp3")

let vlcAdapter = VLCAdapter()
vlcAdapter.play(filename: "movie.vlc")
```

---

### 🍎 iOS Built-in Usage

iOS uses the Adapter pattern in many places:

* **URLSession vs. Third-party Networking (like Alamofire)**
  You may create an adapter that converts `URLSession` calls to match a common protocol.

* **Bridging Swift with Objective-C classes**
  Swift automatically creates adapters (known as **bridging headers**) to allow compatibility.

* **UICollectionViewDiffableDataSource** adapts legacy data source logic into modern diffable models.

---

### 🧩 Summary

| Component | Role                                               |
| --------- | -------------------------------------------------- |
| `Target`  | The interface the client expects                   |
| `Adaptee` | The existing, incompatible interface               |
| `Adapter` | Translates `Adaptee` methods to `Target` interface |

> 🔌 The Adapter pattern promotes **code reusability** by allowing legacy or third-party code to be reused in modern systems without modification.

---
Here’s the **markdown version** of the 🌉 **Bridge Pattern** using the **Payment Gateway Integrations** example — perfect for your `README.md`:

---

# 🌉 Bridge (Structural)

### 🧠 Intent

The **Bridge Pattern** decouples an abstraction from its implementation so that the two can vary independently. It's especially useful when you have multiple dimensions of variation in your system.

---

### 💡 Real-World Example: **Payment Gateway Integrations**

Suppose you're building an e-commerce app that needs to support:

* Multiple **payment types** (One-time, Subscription, Refunds, etc.)
* Multiple **payment gateways** (Stripe, PayPal, Razorpay)

Hard-coding all combinations leads to a mess.
With the Bridge pattern, we **separate the payment logic (abstraction)** from **gateway implementations**, keeping your system extensible and maintainable.

---

### 🧱 Structure

```swift
// MARK: - Implementation Interface
protocol PaymentGateway {
    func processPayment(amount: Double)
}

// MARK: - Concrete Implementations
class StripeGateway: PaymentGateway {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via Stripe.")
    }
}

class PayPalGateway: PaymentGateway {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via PayPal.")
    }
}

// MARK: - Abstraction
class Payment {
    let gateway: PaymentGateway

    init(gateway: PaymentGateway) {
        self.gateway = gateway
    }

    func makePayment(amount: Double) {
        gateway.processPayment(amount: amount)
    }
}

// MARK: - Refined Abstractions
class SubscriptionPayment: Payment {
    override func makePayment(amount: Double) {
        print("Handling subscription logic...")
        super.makePayment(amount: amount)
    }
}

class OneTimePayment: Payment {
    override func makePayment(amount: Double) {
        print("Handling one-time payment logic...")
        super.makePayment(amount: amount)
    }
}
```

---

### ✅ Usage

```swift
let stripe = StripeGateway()
let paypal = PayPalGateway()

let monthlySub = SubscriptionPayment(gateway: stripe)
monthlySub.makePayment(amount: 999.0)

// Output:
// Handling subscription logic...
// Processing ₹999.0 via Stripe.

let oneTime = OneTimePayment(gateway: paypal)
oneTime.makePayment(amount: 499.0)

// Output:
// Handling one-time payment logic...
// Processing ₹499.0 via PayPal.
```

---

### 🍎 iOS Usage Analogy

* `UIView` uses a `CALayer` underneath → a form of **bridge** between visual abstraction and rendering engine.
* `NSURLSession` is an abstraction that can delegate network behavior to different `URLProtocol` implementations.
* In SwiftUI, `View` is protocol-based but rendering is handled separately by the system — another subtle bridge.

Got it — here’s your **🌿 Composite Pattern** explanation in clean, GitHub-ready markdown.

---

# 🌿 Composite (Structural)

### 🧠 Definition:

The **Composite Pattern** lets you treat individual objects and compositions of objects uniformly. It’s perfect for representing **hierarchical, tree-like structures** where you want to work with both single items and groups in the same way.

---

### 🧾 Real-World Example:

**File System**

* A **File** is a single item.
* A **Folder** can contain files and other folders.
* Both `File` and `Folder` can be treated using the same operations like `getSize()`, `displayName()`, or `delete()`.

---

### 📱 iOS Real Example:

* **UIView hierarchy** in UIKit or **View** hierarchy in SwiftUI.
* `UIView` can be:

  * A leaf (e.g., `UILabel`, `UIImageView`)
  * A composite (e.g., `UIStackView` containing other views)
* Both respond to methods like `.addSubview()` and `.removeFromSuperview()`.

---

### 🧑‍💻 Swift Example:

```swift
// Component Protocol
protocol FileSystemItem {
    var name: String { get }
    func display(indentation: String)
}

// Leaf
struct File: FileSystemItem {
    let name: String
    func display(indentation: String) {
        print("\(indentation)📄 \(name)")
    }
}

// Composite
class Folder: FileSystemItem {
    let name: String
    private var items: [FileSystemItem] = []

    init(name: String) {
        self.name = name
    }

    func add(_ item: FileSystemItem) {
        items.append(item)
    }

    func display(indentation: String = "") {
        print("\(indentation)📂 \(name)")
        items.forEach { $0.display(indentation: indentation + "  ") }
    }
}

// Usage
let file1 = File(name: "Resume.pdf")
let file2 = File(name: "CoverLetter.pdf")
let docsFolder = Folder(name: "Documents")
docsFolder.add(file1)
docsFolder.add(file2)

let rootFolder = Folder(name: "Home")
rootFolder.add(docsFolder)
rootFolder.display()
```

**Output:**

```
📂 Home
  📂 Documents
    📄 Resume.pdf
    📄 CoverLetter.pdf
```

---

### 🧰 When to Use:

* Represent part-whole hierarchies.
* You want to treat individual objects and groups of objects uniformly.
* Common in **UI trees, graphics engines, DOM structures, file explorers**.

---

If you want, I can also make a **SwiftUI composite example** where views are dynamically built in a recursive manner — perfect for scalable UI systems. That example would make the iOS connection even stronger.
  
